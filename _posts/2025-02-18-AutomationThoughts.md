---
title: Automation Thoughts - A Three-Axis Model
date: 2025-02-18 02:00:00 +0800
categories: [Technology, Artificial Intelligence]
tags: [automation, ai, workforce]
---

This blog post suggests a three-axis model for categorizing automation initiatives. It is meant to help the reader understand the impact of different types of automation on organizations, the space of possible job-altering automation strategies, and the differences between historical trends and modern automation initiatives. It may also aid speculation about future patterns of automation.

The concepts discussed in this post are discussed in a very linear style: each section builds on the previous one. This may not constitute a good reading experience.

I'll try to update this post as I continue to think about these concepts, and demonstrate a less linear style in future posts.

## What is Automation?

Let's briefly discuss what distinguishes automation from other forms of technological improvement.

The term **automation** must refer to a technology that independently handles some of the discrete decisions or micro‐steps required to complete a task: rather than performing the full series of mental or physical sub-tasks, these steps are organized into whole actions which can be delegated to a machine. If this weren't the case, we'd just be talking about tools. 

This becomes clearer when we consider the case in which a worker uses a hammer to drive nails. Although the use of a hammer aids the process of completing the task, it does not automate the task. This is explained by the fact that the worker must still swing for each nail, controlling direction and force. Therefore, an automation can not merely make a task easier or faster to complete: we must consider the degree to which the technology *abstracts over the necessary steps towards task completion* before concluding that it is an automation.

Automation implies that, instead of manually executing each step (like calculating each digit in arithmetic), humans shift to a higher-level role: determining how to operate an interface (like deciding which series of buttons to press on a calculator), checking if outputs make sense (like verifying the calculator's sum), and making judgment calls the system can't handle (like deciding when calculation is needed). 

I'll use these observations to suggest an interim definition for automation, which we will refine as we continue: an **automation** is an interface to a system capable of performing useful actions on behalf of a human, that abstracts much of the mental or physical requirements of task completion away from the human operator.

The **Three‐Axis Model**, introduced in this post, primarily applies when a system automates **the primary tasks that define a paid job role**. It only concerns systems of automation which significantly alter the nature of the job, resulting in **workforce impacts** (discussed later) such as retooling, transforming, or removing entire jobs. It is less applicable to systems that automate the **secondary tasks** associated with a job, which are only part of the role when they are necessary for the completion of the primary tasks associated with the job.

### What's The Difference Between Secondary And Primary Tasks?

Consider the impact of typewriters on secretarial work. Although writing out text on paper may have consumed a significant portion of a secretary's time, it would never have been part of their role if it were not necessary for their their primary tasks to be completed: composing, organizing, and managing business communications. Therefore, the task of writing out letters was secondary to the role of a secretary. The role remained (mostly) unchanged: the same personnel continued doing largely the same work with the same workflow, now using the interface of a typewriter.

### Why Is "Extent of Automation" Not A Helpful Concept?

If only **minor or peripheral tasks** are automated, the result might merely **adapt** the role: the same employees remain, adjusting their workflows or learning to use the system. Conversely, if **primary tasks** (the main reason the job exists) are automated, the entire role may be **transformed** into something quite different or be **removed** altogether. Yet, if the automation of primary tasks is considered "partial", it's unclear how much of the role will be transformed or removed as a result.

Even when automation requires skilled human operators, it can eliminate roles entirely if it covers core responsibilities. For example, if AI automates 80% of an accountant's primary tasks, the remaining 20% may or may not be absorbed by higher-level management positions - effectively removing the original role. This illustrates why the concept of "extent of automation" is unhelpful: we must discuss how much an automation reduces the time and cost of completing primary tasks separately from its actual workforce impact.

These nuances tie directly into **Axis 3 (Workforce Impact):** Adapt / Transform / Remove.

## How Does Automation Relate To Changes In Working Strategy?

An interface provides the operator with the ability to select predefined sequences of steps, trigger the automation to execute those sequences, and generate measurable progress on the task. Through this interface, the operator's role shifts from performing individual steps to choosing which automated sequences to invoke. These options are **sometimes not isomorphic** to the operator's manual process, and thus the operator may be forced to choose a **different strategy** towards completing the task than they would have chosen without the automation.

Here's an example: a brute-force search tool that presents false positives replacing an operator's manual screening process. The machine performing the screening may present a list of potential matches, but the operator must choose which ones to investigate further, which involves manually checking each potential match. We know that this is different from the operator's manual process, since if the actions taken by the machine were isomorphic to the operator's manual process, the operator would not need to choose which matches to investigate further.

It's not merely that introducing an automation reduces the number of steps required by humans for the task. When a new strategy for task completion is required, it transforms the practical aspects of completing the task from the operator's perspective, which further complicates our previous discussion about determining the extent of an automation.

These nuances tie directly into **Axis 2 (Oversight):** Manual / Supervised / Autonomous. 

---

## The Three‐Axis Model and Its Rationale

This model is organized around three questions. By concatenating the answers, we can create a “label” for any automation initiative:

1. **Ownership:** Who builds and controls the system?  
   - **In‐House:** Internal teams develop it and run it.  
   - **Contracted:** An external vendor develops it, then hands it off for the organization to run.  
   - **Outsourced:** A third‐party handles both creation and ongoing operations.

2. **Oversight:** How much human oversight is involved in day‐to‐day operation?  
   - **Manual (Human in the Loop):** A human must explicitly guide or approve major actions.  
   - **Supervised (Human on the Loop):** The system runs on its own most of the time; humans monitor and may intervene.  
   - **Autonomous (Human out of the Loop):** The system requires minimal or no routine human involvement.

3. **Workforce Impact:** What is the impact on employees who used to do these tasks?  
   - **Adapt:** The same employees remain but adapt (learn new skills, adjust workflows).  
   - **Transform:** The role changes drastically; many current staff are not a good fit, so partial displacement or redeployment occurs.  
   - **Remove:** The job is eliminated altogether (the system’s automation of core tasks makes the role obsolete).

Example: "In-House, Supervised, Adapt" refers to a system that is built and operated by an internal team, with human oversight required for major actions. The workforce remains, but employees learn new skills and adjust their workflows.

### Independence of Axes

For this model to be useful, it is important for the axes to be (mostly) distinct. 

As we saw earlier, an automation's interface design directly influences task completion strategies, which in turn determines both the **Workforce Impact** (by dictating skill requirements) and the **Oversight** needed (through the need for human judgment at decision points and the complexity of interventions). 

However, these axes remain worth discussing separately. I'll demonstrate that this is the case:

1. **Ownership** doesn't tightly correlate with **Workforce** changes. One might imagine an “Outsourced” system to which employees "Adapt", if the external SaaS product only automates minor tasks. Conversely, an “In‐House” system could completely Remove roles if it fully automates the core function. 
2. **Oversight** doesn't tightly correlate with **Workforce** changes: a non-autonomous automation might be used to adapt, transform, or remove roles, as we illustrated with the example of accountant roles possibly being absorbed into higher-level management positions. 
3. Any degree of **Oversight** can co-occur with any **Ownership** model.

Therefore, there are twenty-seven possible automation profiles in this model.

### Why This Model Is Useful.

Firstly, there is a clear relationship between the essential aspects of how the automation works - specifically how actions are presented to the operator via the abstraction mechanism - and the two main axes of the system: Oversight and Workforce Impact. The abstraction style directly determines oversight requirements, with more complex abstractions requiring frequent operator decisions leading to Manual or Supervised models, while simplified abstractions that eliminate decision points enable Autonomous operation. This same abstraction mechanism, combined with job market and organizational context, shapes workforce impact by influencing whether roles can be retained with retraining, must transform significantly, or will be eliminated entirely, as well as determining how remaining tasks might be redistributed.

Secondly, the Oversight and Workforce Impact axes represent two logically distinct aspects that people often conflate when trying to quantify the "extent" of an automation. When someone claims an automation is "more automated" than another, they might be referring to either its degree of autonomy (Oversight) or its displacement of human roles (Workforce Impact), which are separate considerations. By establishing this framework, we can trace a direct line of reasoning from an automation's interface design through to these two components of its "extent": the interface's abstraction mechanism determines both oversight requirements and, in conjunction with organizational context, workforce changes. This makes tractable what was previously an ambiguous discussion about how "automated" a system is.

Thirdly, the Ownership axis provides a practical framework for analyzing concrete choices organizations face when pursuing automation. Since the necessary extent of oversight is determined by the limitations of the automation technology, and the workforce impact is mostly outside of the organization's control, their possible choices are determined mostly around the Ownership axis. 

Consider a future organization that has the means to automate the work of some junior developers using an "AI Agent" product. Let's assume that they're certain that the "supervised" model of oversight is the only way to ensure tasks get done correctly. They must now determine whether they they should transform the role of junior developers, employing them to assist the agent, or scrap the role entirely, delegating the oversight workload to senior developers. If they scrap the junior developer role in favour of a commercial (outsourced) agent product, they run the risk of becoming more dependent on the external vendor than is ideal. If they own and maintain their own "AI Agent", their risk of regret is lower, but they must also consider the cost of building the product. This leaves them with six possible choices, determined by prepending "In-House", "Contracted", or "Outsourced" to "Supervised-Transform" and "Supervised-Remove". Their choice of automation strategy is now a matter of weighing the tradeoffs between these six scenarios, some of which are easily eliminated as undesirable.

---

## Historical Overview of Automation (1985–2025)

This is a work in progress.