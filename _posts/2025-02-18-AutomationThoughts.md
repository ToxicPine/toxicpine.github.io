---
title: Automation Thoughts - A Three-Axis Model
date: 2025-02-18 02:00:00 +0800
categories: [Technology, Artificial Intelligence]
tags: [automation, ai, workforce]
---

**THIS DOCUMENT IS A WORK IN PROGRESS.**

This blog post suggests a three-axis model for categorizing automation initiatives. It is meant to help the reader understand the impact of different types of automation on organizations, the space of possible job-altering automation strategies, and the differences between historical trends and modern automation initiatives. It may also aid speculation about future patterns of automation.

The concepts discussed in this post are discussed in a very linear style: each section builds on the previous one. This may not constitute a good reading experience.

I'll try to update this post as I continue to think about these concepts, and demonstrate a less linear style in future posts.

## What is Automation?

Let's briefly discuss what distinguishes automation from other forms of technological improvement.

The term **automation** must refer to a technology that independently handles some of the discrete decisions or micro‐steps required to complete a task: rather than performing the full series of mental or physical sub-tasks, these steps are organized into whole actions which can be delegated to a machine. If this weren't the case, we'd just be talking about tools. 

This becomes clearer when we consider the case in which a worker uses a hammer to drive nails. Although the use of a hammer aids the process of completing the task, it does not automate the task. This is explained by the fact that the worker must still swing for each nail, controlling direction and force. Therefore, an automation can not merely make a task easier or faster to complete: we must consider the degree to which the technology *abstracts over the necessary steps towards task completion* before concluding that it is an automation.

Automation implies that, instead of manually executing each step (like calculating each digit in arithmetic), humans shift to a higher-level role: determining how to operate an interface (like deciding which series of buttons to press on a calculator), checking if outputs make sense (like verifying the calculator's sum), and making judgment calls the system can't handle (like deciding when calculation is needed). 

I'll use these observations to suggest an interim definition for automation, which we will refine as we continue: an **automation** is an interface to a system capable of performing useful actions on behalf of a human, that abstracts the mental or physical requirements of task completion away from the human operator.

The **Three‐Axis Model**, introduced in this post, primarily applies when a system automates **the primary tasks that define a paid job role**. It only concerns systems of automation which significantly alter the nature of the job, resulting in **workforce impacts** (discussed later) such as retooling, transforming, or removing entire jobs. It is less applicable to systems that automate the **secondary tasks** associated with a job, which are only part of the role when they are necessary for the completion of the primary tasks associated with the job.

### What's The Difference Between Secondary And Primary Tasks?

Consider the impact of typewriters on secretarial work. Although writing out text on paper may have consumed a significant portion of a secretary's time, it would never have been part of their role if it were not necessary for their their primary tasks to be completed: composing, organizing, and managing business communications. Therefore, the task of writing out letters was secondary to the role of a secretary. The role remained (mostly) unchanged: the same personnel continued doing largely the same work with the same workflow, now using the interface of a typewriter.

### Why Is "Extent of Automation" Not A Helpful Concept?

If only **minor or peripheral tasks** are automated, the result might merely **retool** the role: the same employees remain, adjusting their workflows or learning to use the system. Conversely, if **primary tasks** (the main reason the job exists) are automated, the entire role may be **transformed** into something quite different or be **removed** altogether. Yet, if the automation of primary tasks is considered "partial", it's unclear how much of the role will be transformed or removed as a result.

Even when automation requires skilled human operators, it can eliminate roles entirely if it covers core responsibilities. For example, if AI automates 80% of an accountant's primary tasks, the remaining 20% may or may not be absorbed by higher-level management positions - effectively removing the original role. This illustrates why the concept of "extent of automation" is unhelpful: we must discuss how much an automation reduces the time and cost of completing primary tasks separately from its actual workforce impact.

These nuances tie directly into **Axis 3 (Workforce Impact):** Retool / Transform / Remove.

## How Does Automation Relate To Changes In Working Strategy?

An interface provides the operator with the ability to select predefined sequences of steps, trigger the automation to execute those sequences, and generate measurable progress on the task. Through this interface, the operator's role shifts from performing individual steps to choosing which automated sequences to invoke. These options are **sometimes not isomorphic** to the operator's manual process, and thus the operator may be forced to choose a **different strategy** towards completing the task than they would have chosen without the automation.

Here's an example: a brute-force search tool that presents false positives substituting for the operator's manual screening process. The machine performing the screening may present a list of potential matches, but the operator must choose which ones to investigate further, which involves manually checking each potential match. We know that this is different from the operator's manual process, since if the actions taken by the machine were isomorphic to the operator's manual process, the operator would not need to choose which matches to investigate further. It also introduces the need for result-checking steps.

When it is the case that the automation introduces a new strategy, it must be an abstraction over the steps required to complete the task, as well as the sub-tasks that comprise the new strategy, but not the sub-tasks that comprise the old strategy.

These nuances tie directly into **Axis 2 (Supervision):** Manual / Supervised / Autonomous.

---

## The Three‐Axis Model and Its Rationale

This model is organized around three questions. By concatenating the answers, we can create a “label” for any automation initiative:

1. **Implementation:** Who builds and controls the system?  
   - **In‐House:** Internal teams develop it and run it.  
   - **Contracted:** An external vendor develops it, then hands it off for the organization to run.  
   - **Outsourced:** A third‐party handles both creation and ongoing operations.

2. **Supervision:** How much human oversight is involved in day‐to‐day operation?  
   - **Manual (Human in the Loop):** A human must explicitly guide or approve major actions.  
   - **Supervised (Human on the Loop):** The system runs on its own most of the time; humans monitor and may intervene.  
   - **Autonomous (Human out of the Loop):** The system requires minimal or no routine human involvement.

3. **Workforce Impact:** What is the impact on employees who used to do these tasks?  
   - **Retool:** The same employees remain but adapt (learn new skills, adjust workflows).  
   - **Transform:** The role changes drastically; many current staff are not a good fit, so partial displacement or redeployment occurs.  
   - **Remove:** The job is eliminated altogether (the system’s automation of core tasks makes the role obsolete).

Example: "In-House, Supervised, Retool" refers to a system that is built and operated by an internal team, with human oversight required for major actions. The workforce remains, but employees learn new skills and adjust their workflows.

### Independence of Axes

For this model to be useful, it is important for the axes to be (mostly) distinct. I'll demonstrate that this is the case:

1. **Implementation** doesn't tightly correlate with **Workforce** changes. One might imagine an “Outsourced” system that’s used to Retool employees, if the external SaaS product only automates minor tasks. Conversely, an “In‐House” system could completely Remove roles if it fully automates the core function. 
2. **Supervision** doesn't tightly correlate with **Workforce** changes: a non-autonomous automation might be used to retool, transform, or remove roles, as we illustrated with the example of accountant roles possibly being absorbed into higher-level management positions. 
3. Any degree of **Supervision** can co-occur with any **Implementation** model.

Therefore, there are twenty-seven possible automation profiles in this model.

---

## Historical Overview of Automation (1985–2025)

Below is a broad chronological‐cum‐geographical sweep of major automation trends. We will use illustrative examples to clarify how they can be framed via the three axes. We will also connect those examples back to the **task‐based definition** of automation—particularly focusing on when automation tackled **primary job tasks** and hence triggered retool/transform/remove outcomes.

### Late 1980s: Rise of Industrial Robotics and Office IT

- **Context:** Industrial robots in automotive manufacturing were growing especially in Japan, leading to partially automated welding, painting, etc. Meanwhile, in offices worldwide, personal computers and spreadsheets were automating *some* clerical tasks.  
- **Typical Axes Profile:**
  - **Implementation:** Often **In‐House** for major Japanese automakers (they developed proprietary robotic systems in collaboration with local robotics firms, but effectively “owned” the process). In office settings, organizations often brought in outside software (partial “Contracted” approach) but ran it internally.  
  - **Supervision:** Predominantly **Manual or Supervised**. Factory robots needed continuous monitoring and programming from human engineers. Office systems still needed human input to run each spreadsheet or process.  
  - **Workforce:** The immediate effect varied. Many clerical roles began to **Retool** (typing pool staff learned to use word processors). Some jobs were **Transformed** in factories (fewer welders, more robot technicians). Relatively few roles were **Removed** outright in this early phase because the automation was not yet fully autonomous or wide‐ranging enough to make entire jobs vanish.  
- **Task‐Based Rationale:** Robots took over discrete tasks like spot‐welding, but broad lines of assembly still involved humans. Office computers automated tasks (like rewriting letters) but often left humans responsible for organizing, printing, distribution, etc.

### 1990s: Globalization and the IT Boom

- **Context:** Trade liberalization made outsourcing an attractive alternative to local automation for labor‐intensive tasks. Meanwhile, IT systems (ERP, CRMs) automated many back‐office processes.  
- **Axes in Action:**
  - **Implementation:** Large enterprises often pursued a **Contracted** approach (commissioning IT vendors to develop or customize software, then hosting it in‐house). Some SMEs began adopting **Outsourced** models for payroll or data processing, letting service bureaus handle everything.  
  - **Supervision:** A lot of IT systems were **Supervised**—they ran many operations automatically but still had staff overseeing data flows and verifying outputs.  
  - **Workforce:** For tasks that got fully taken over by software (e.g., automatic invoice matching), some clerical roles were **Removed**. However, more common was **Transform**—the nature of accounting or HR staff changed as they became system specialists.  
- **Task‐Based Rationale:** If the software or outsourced service automated a minor subset of tasks, staff usually **Retooled**. If it automated the major tasks on which the role was based (e.g., data entry clerks replaced by scanning + optical character recognition software), the job was either drastically **Transformed** or **Removed**.

### Early 2000s: Offshoring vs. Automation

- **Context:** Companies worldwide ramped up offshoring (particularly to China, India, and Eastern Europe). In manufacturing, the question often became “should we deploy expensive robots locally or just offshore production where labor is cheaper?” Meanwhile, advanced robotics and AI capabilities were improving but still not widespread in every domain.  
- **Axes Examples:**
  - **Implementation:** Widespread **Outsourced** setups emerged—**entire factories** and processes were managed by third‐party suppliers in Asia. This meant organizations effectively outsourced both the building and operation of the process.  
  - **Supervision:** Depending on the deal, the offshoring company might keep some **Manual** or **Supervised** oversight of quality, but in many cases, day‐to‐day operation was effectively run by the local partner (close to “Autonomous” from the original firm’s perspective).  
  - **Workforce:** In high‐wage countries, this strategy often led to **Remove** for local assembly or back‐office staff, because tasks were “removed” from local operations altogether. In the host country, newly employed workers did the tasks *manually*, so the net effect was a shift of roles across borders rather than a retool or transform.  
- **Task‐Based Rationale:** Offshoring is not always “automation”; often it’s simply a lower‐labor‐cost alternative. Nonetheless, from the perspective of the original local workforce, the tasks were effectively removed.

### 2010s: Industry 4.0 and AI‐Driven Service Automation

- **Context:** Post‐2008, pressure to cut costs and the emergence of new digital technologies led to the so‐called “Fourth Industrial Revolution,” featuring advanced robotics, IoT, and AI. Additionally, machine learning (ML) and big data enabled new forms of service automation: chatbots, algorithmic management (Uber, Amazon logistics), etc.  
- **Axes Illustrations:**
  - **Implementation:**  
    - Many factories started adopting advanced **In‐House** solutions to stay competitive (e.g., in Germany’s “Industry 4.0”). These might be partly “Contracted” in development but run on‐site.  
    - Numerous service companies embraced **Outsourced** models for AI (cloud‐based automation platforms).  
  - **Supervision:**  
    - Automated warehouses (e.g., Amazon) typically operate under a **Supervised** model—robots do the heavy lifting, but staff and managers oversee performance.  
    - Some algorithmic systems in finance run with minimal real‐time human oversight (close to **Autonomous**).  
  - **Workforce:**  
    - **Retool:** In many manufacturing settings, line workers learned to operate collaborative robots (cobots).  
    - **Transform:** Some tasks for drivers or warehouse pickers changed significantly as algorithms took over scheduling or routing.  
    - **Remove:** Fully automated processes, like certain “dark” warehouse or fulfillment center cells, made entire picking/packing roles obsolete.  
- **Task‐Based Rationale:** Where the automation system took over *primary tasks* (e.g., product routing, picking), roles were removed. Where it only covered a subset of tasks, roles were retooled or transformed.

### Early 2020s and the COVID‐19 Catalyst

- **Context:** The pandemic accelerated interest in “contactless” operations. Labor disruptions led companies to invest more aggressively in service automation (robots for cleaning, telemedicine) and advanced digital platforms.  
- **Axes Lens:**
  - **Implementation:** Many rushed to adopt **Outsourced** cloud solutions for remote collaboration, process automation, and even robotic services.  
  - **Supervision:** Some of these solutions ended up **Manual** or **Supervised** (e.g., telepresence robots guided by remote staff). Others, like automated cleaning robots, were **Autonomous** once deployed.  
  - **Workforce:** Depending on how central these tasks were, healthcare or logistics workers might be **Retooled** to work alongside telehealth or teleoperation systems, or certain roles were **Removed** if the new system supplanted them.  
- **Task‐Based Rationale:** If the system automated the core tasks of a role (e.g., cleaning staff replaced by autonomous units), the outcome was “Remove.” If it merely offloaded some peripheral tasks, roles shifted to “Retool” or “Transform.”

---

## Cross‐Territorial Dynamics and the Three Axes

The three axes also help frame the **global** dimension of automation:

- **Implementation (In‐House / Contracted / Outsourced)**:  
  - In the 1990s–2000s, many Western companies **outsourced** entire production lines to external suppliers in Asia, removing local jobs.  
  - Since the 2010s, we see partial “reshoring” with high automation: factories in the U.S. or Europe, run “In‐House” with heavy robotics. This can lead to “Remove” of low‐skilled local roles but create or transform new tech roles.

- **Supervision (Manual / Supervised / Autonomous)**:  
  - Many East Asian manufacturers progressed from “Manual” to “Supervised” to near‐“Autonomous” factories over three decades.  
  - By 2025, global leaders in robotics (Japan, Germany, South Korea, China) were edging toward fully autonomous lines in certain sectors, raising important workforce questions.

- **Workforce Impact (Retool / Transform / Remove)**:  
  - In a high‐wage, unionized economy, the arrival of advanced robotics might lead to “Transform” (workers become robot technicians). In a lower‐wage or less regulated environment, the same technology might result in “Remove” for large numbers of assembly staff.  
  - Government policies (e.g., Germany’s apprenticeship model) facilitate “Retool” or “Transform” outcomes. Where no retraining structures exist, job elimination is more likely.

## Future Outlook

This is a work in progress.