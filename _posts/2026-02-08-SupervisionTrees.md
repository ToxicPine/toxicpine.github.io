---
title: "DRAFT: Supervision Trees Are All You Need"
date: 2026-02-08 02:00:00 +0100
categories: [Technology, Papers]
tags: [papers, supervision trees, kubernetes, orchestration, capabilities, cybersecurity]
---

We discuss the possibility of a simpler, more robust alternative to kubernetes-style orchestration based on hierarchical supervision trees. In this model, CPU time and I/O access are treated as delegable capabilities rather than global abstractions. Instead of a centralized controller, an active Supervisor process grants a slice of its own resources to its children. This approach also aligns lifecycle management directly with application logic. We conclude by outlining the necessity of a standardized library for the implementation of this capability-based architecture.

### 1\. Introduction

Workload management is the transition from "I have binaries" to "I have correct behavior": getting a set of processes to run on hardware and operate in tandem.

Assuming the hardware works, the behavior of a deployed subsystem is determined by two things:

1. The capacity for processes to exert computational side-effects (I/O): writing to disk, sending packets, communicating with each other through IPC or networking.  
2. Which CPU time-slices are occupied by which processes, where criticality defines which process gets the slice when contention occurs.

If a deployment consists of an API and a database, the definition of "working" is: *the API and DB share a communication channel, the DB has CPU time to query, the API has CPU time to serve, and the API can transmit on the network with a routable identity.*

### 2\. Centralized Orchestration

If this were the whole problem, we could run these processes with a local supervisor like SystemD on a suitably configured device. Many deployments, however, need to be reproducible across machines and scalable through replication, which requires describing systems without knowing which computer they run on. Also, once a deployment spans multiple machines, we typically need to enforce security policy uniformly across them and ensure availability through lifecycle management (restart policies, etc).

Orchestrators like Kubernetes assume ownership of the environment to create a uniform abstraction layer. Typically, they:

1. Define a topologically flat virtual network where the API can find the DB anywhere (Service Discovery).  
2. Enforce network policy (NetworkPolicy, RBAC) to regain security boundaries within the flat network.  
3. Perform process supervision: monitor liveness and restart processes, without access to the application's internal state.  
4. Schedule processes, deciding how much CPU time each container receives.

Regarding §1, A and B relate to 1, C and D relate to 2\.

This means of orchestration concentrates networking, lifecycle, and scheduling authority in a single control plane. The model works well for stateless services at datacenter scale; its limitations appear in mixed-criticality, high-performance, high-security, and latency-sensitive deployments. The following sections examine the I/O abstractions (A, B) first, then lifecycle and scheduling (C, D).

### 3\. Flat Network Topologies

In Kubernetes, the approach to I/O is to "flatten then restrict": abstract away the physical network, presenting a uniform topology where every service is reachable. Cardelli \[1\] identified two physical realities that make this kind of abstraction unreliable.

#### Latency and Locality

Cardelli argued that you cannot hide the difference between local and remote interaction. A procedure call to the antipodes is bounded by the speed of light; a local call is bounded by the speed of the bus.

In a flat cluster, `service-a.local` is a stable identifier regardless of whether `service-a` is on the same rack or in a different region, erasing the distinction between a \<1ms dependency and a \>50ms dependency.

Consider a high-frequency trading bot or real-time data pipeline. If a scheduler reschedules a dependency to a different Availability Zone to balance load, the deployment breaks. The logic is correct, but the physics have changed: timeouts calibrated for local traffic fire, treating physical distance as system failure, and retries amplify the load into cascading failure.

The latency between two processes constrains what they can do together, but a flat network topology encodes no distinction between nodes on the same rack and nodes across the world. Engineers recover latency information out-of-band with node affinity rules, topology spread constraints, and manual pinning of workloads to zones. In more complex deployments, engineers rely on scripting to manage resources, effectively replacing the declarative model with an imperative one.

#### Security and Mobility

Cardelli's second observation is that barriers are the fundamental structuring concept for wide-area systems. Barriers define locality (being in the same or different places), mobility (crossing from one place to another), and security (the ability or inability to cross). In the Ambient Calculus, a process cannot interact with a context unless it possesses the capability to enter that context. Security is therefore coupled to mobility: what you can reach determines what you can affect.

A flat network erases barriers, so mobility and security decouple. A "PII Scraper" and a "Public Webhook" share the same network overlay; preventing them from communicating is a matter of policy configuration, not network structure. Thus, Kubernetes engineers must maintain NetworkPolicy objects that describe the topology that should exist but was flattened away. As such, the security of the deployment depends on the correctness of this shadow topology, defined in Kubernetes.

### 4\. I/O Boundaries as Capabilities

Both features in §3 stem from the same design choice: a flat network provides a uniform I/O surface and then layers restrictions on top. If instead each component declares which I/O boundaries it requires, computation migrates at deploy time to any environment that can satisfy those requirements, subject to RBAC. 

These declarations could be polymorphic over locality, as capabilities may be described using dependent types at deploy-time: a deployment manifest might require "a RESTful API z, defined over any network," or more specifically, "the LAN-variant of z." The first is portable; the second encodes a latency constraint. If the constraint cannot be met, the deployment fails at admission rather than silently at runtime.

The same structure enforces security policy. Imagine a script that needs to process sensitive records:

* The script requests admission to an Ambient that offers the `UserRecords` capability.  
* The Platform ensures that any Ambient offering `UserRecords` is constructed *without* an `InternetGateway` capability.  
* Once the script moves to the data, exfiltration is not possible. The context with both PII access and Internet access does not exist.

Security here is absence of access, not restriction. I/O boundaries are mediated by capability handles, and since handles can be dropped, restricting an administrative domain means granting a process access to an environment that lacks the capabilities you wish to deny.

This model has an immediate further implication. If I/O boundaries are capability-gated, it becomes possible to delegate the ability to deploy into an administrative domain with least privilege: you hand someone a restricted set of capabilities and they can spawn processes within that domain. Those processes, however, consume CPU time and compete for resources with everything else in the domain, and the I/O capability model on its own says nothing about how that contention is managed. This brings us to the concerns we deferred in §2: process supervision and scheduling.

### 5\. Lifecycle and Scheduling

Examining scheduling behaviour and lifecycle management independently of the I/O abstraction, there are limitations worth noting. In Kubernetes, process lifecycle and scheduling are managed by the same control plane that manages networking. The control plane receives health and lifecycle signals from processes for auto-scaling, and sends kill, restart, and reschedule signals to processes for crash recovery and adaptation. Each direction is an attack surface: a compromised process can feed false health signals upward to manipulate scaling decisions, while a compromised control plane can send arbitrary lifecycle signals downward to every workload it manages.

There is also a separation-of-concerns problem. Returning to the API-and-DB example: the API will crash if the DB has not been booted ahead of time, and will hang if the DB crashes during operation. This ordering must be managed by the control plane, but the ordering logic is application-specific. Since the control plane manages the lifecycle for every process in the cluster, it ends up carrying per-application knowledge in generic configuration (Readiness Probes, init containers), separating the logic that understands the application from the authority to manage its execution.

Seemingly, the capability model from §4, intended for the I/O abstraction, applies here too. Accessing the CPU is an effect mediated by the kernel: changing interrupt behavior and allocating memory via the MMU go through the syscall interface, like any other I/O operation. Treating Time as a Capability (an SeL4-style Scheduling Context) allows it to be delegated, so that a process holds a budget of CPU time and passes slices of that budget to its children, aligning the authority to execute with the logic of the application. The same model that addresses I/O also addresses scheduling, and the resource contention that I/O delegation introduces is resolved by the same mechanism.

### 6\. The Supervisor Model

If we treat I/O and Time as capabilities, we no longer need a centralized orchestrator.

We propose a model where the unit of deployment is an active supervisor process.

1. At deploy time, the Supervisor declares which capabilities it needs (e.g., a private network handle and 20% of a CPU). This is a polymorphic request: it can run in any environment that satisfies it. Once admitted, the Supervisor's authority is exactly what it requested, and it subdivides the granted CPU budget and I/O surface among the processes it spawns.  
2. The Supervisor is responsible for pulling the binaries of its children, spawning them, and delegating capability handles to each. Since it is application code, it implements the precise lifecycle logic required: "Start DB, wait for consistency, then spawn API." If the DB hangs, the Supervisor, which owns the DB's CPU budget, can revoke it, kill the process, and restart it.

The lifecycle management logic of the deployment (restarts, scaling, backoff, dependency management) is internal behavior of the Supervisor, not an orchestrator.

We may implement access control over program binaries over the same structure: the Supervisor fetches its children's executables through the capabilities available in its environment, so if the environment cannot reach a particular registry or storage backend, those binaries are inaccessible.

So far the model has been described as purely restrictive: as if authority flows downward and each level has at most what its parent granted. However, a supervisor could also create new interfaces: it could spawn a process that consumes primitive I/O and exposes structured access to it. For example, a database supervisor could take disk access and CPU time and expose a query interface. How these interfaces are exposed (over a Unix socket, a TCP listener, shared memory) is a runtime question we defer to §8.

### 7\. Supervision Trees

A Supervisor can delegate timeslices and capabilities to child Supervisors, so the model nests into a tree: each node holds a subset of its parent's budget and capabilities and can subdivide further. A node cannot grant what it does not have, so authority strictly decreases down the tree.

The admission system is itself a Supervisor. It holds a CPU budget, some I/O capabilities, and the ability to receive deployment requests over the network. When a request arrives, it carves off a slice of its budget and a subset of its capabilities and spawns a child Supervisor with those resources. That child can subdivide internally however it likes without exceeding what it was given.

Deploying is finding a node in the tree that exposes an admission endpoint you can reach, submitting your Supervisor binary and capability requirements, and either being accommodated or rejected. The topology of the tree is the placement and security policy: if a subtree lacks Internet access, nothing deployed within it can reach the Internet. A platform team provisions deployment targets by constructing subtrees with the appropriate capabilities.

#### Development Shells

Development shells are a useful case to consider because they are created and destroyed frequently, often by many engineers concurrently, and the primary difficulty in provisioning them is access control: a shell needs access to internal services, database replicas, and build tooling, but should not have access to production secrets, customer data, or external networks it doesn't need.

In the supervision tree model, a platform team constructs a subtree for development shells with the appropriate capabilities: access to a sandboxed network, a local database replica, build toolchains, and a scoped CPU budget. The subtree lacks production credentials and unrestricted Internet access, so any shell spawned within it inherits those constraints without per-shell configuration. When an engineer requests a shell, the admission Supervisor at that node carves off a slice of its budget, spawns a child, and the shell is ready. When the engineer is done, the child's resources are reclaimed. The access control is not per-session policy that must be applied and audited; it is a property of the subtree itself, and it holds regardless of how many shells are created or how quickly they turn over.

### 8\. Toward a Supervisor Library

Supervisors need a shared API for declaring capabilities, negotiating with parents, and mapping granted capabilities onto kernel resources.

**Contract.** A supervisor consumes capabilities and may expose new ones. The contract language needs to express both: what a supervisor requires from its parent, and what it makes available once running. It also needs to express how produced capabilities compose across the tree: whether a child's outputs propagate upward, remain confined to siblings, or something else. Admission is a check against these contracts, and the polymorphism from §4 carries over. The precise semantics of these contracts are an open question.

**Protocol.** The contract describes what is expressible; the protocol governs what happens over time. Admission is the initial exchange, but a child under load may need to negotiate more CPU from its parent, and a parent whose budget is oversubscribed may need to reclaim from idle children. The protocol must support renegotiation, and the parent needs a fairness policy for arbitrating competing requests.

**Runtime.** A granted capability must become something real on the machine. A CPU budget maps to a cgroup, a network handle to a namespace or socket. These mappings are OS-specific. Open questions remain at this layer: the mechanism for delegating handles between local processes, whether a child can pass a handle to a sibling directly, and how a parent manages the budget of a child on a different physical host.

---

### References

\[1\] L. Cardelli, "Mobility and Security," Lecture Notes for the Marktoberdorf Summer School, 1999\. From works by L. Cardelli and A. D. Gordon.  