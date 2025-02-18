---
title: Automation Thoughts - A Three-Axis Model
date: 2025-02-18 02:00:00 +0800
categories: [Technology, Artificial Intelligence]
tags: [automation, ai, workforce]
---

**THIS DOCUMENT IS A WORK IN PROGRESS.**

This blog post suggests a three-axis model for categorizing automation initiatives, particularly those that change the nature of jobs. It is meant to help the reader understand the impact of different types of automation on organizations, the space of possible automation initiatives, and the differences between historical trends and modern automation initiatives. It may also aid speculation about future patterns of automation.

## Defining Automation in Terms of Tasks

A key starting point is: **What exactly counts as “automation”?**  
- A **job** can be viewed as a collection of tasks, some of which are primary (they define the job's purpose) and some of which are secondary (they are merely necessary for the primary tasks to be completed).  
- An **automation** is a interface that abstracts away the mental and physical work of job tasks. Instead of manually executing each step (like calculating each digit in arithmetic), humans shift to a higher-level role: determining how to operate the interface (like deciding which series of buttons to press on a calculator), checking if outputs make sense (like verifying the calculator's sum), and making judgment calls the system can't handle (like deciding when calculation is needed).

### Automation vs. General Technological Improvement

- **Not all new technology is automation.** A more powerful computer or a better hammer still leaves every discrete action in the hands of a human. The use of a hammer does not automate the task of driving nails: the user must still swing for each nail, controlling direction and force.  
- **Automation** implies that the technology itself handles some of the discrete decisions or micro‐steps: rather than performing deliberate mental or manual labor for every step, the sub-tasks required to complete the job are organized into whole processes that are easily delegated to the system of automation.
- **Automation Example – The Calculator**:  
  - **Without a calculator**: a person must track digits, carry over numbers, and check each step when adding 333 + 287.  
  - **With a calculator**: the system encapsulates the step‐by‐step arithmetic. The human only needs to input the numbers and read the output.  
  - This device demonstrates how automation substitutes transaction‐level labor (digit‐by‐digit calculation) for a process‐level abstraction.
- The **Three‐Axis Model** primarily applies when a system automates **the primary tasks** that define a role, resulting in potential **workforce impact** (discussed later) such as retooling, transforming, or removing entire jobs. It does not apply to tools like calculators that only automate secondary tasks: while calculators automated arithmetic previously done by accountants, performing arithmetic does not define the accountant's role and did not significantly retool, transform, or remove any jobs.

### Why the Degree of Task Replacement Matters

- If only **minor or peripheral tasks** are automated, the result might merely **retool** the role: the same employees remain, adjusting their workflows or learning to use the system.  
- If **primary tasks** (the main reason the job exists) are automated, the entire role may be **transformed** into something quite different or be **removed** altogether.  
- Partial automation can still eliminate roles if the tasks it covers are central. For instance, if an AI handles 80% of a staff accountant’s core responsibilities, the remaining 20% might be absorbed by a manager or consolidated into another position, effectively removing the accountant role.  

These nuances tie directly into **Axis 3 (Workforce Impact):** Retool / Transform / Remove.

---

## The Three‐Axis Model and Its Rationale

This model is organized around three questions that create a concise “label” for any automation initiative:

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

### Interactions Among the Axes

- **Implementation** may or may not correlate tightly with **Workforce** changes. One might imagine an “Outsourced” system that’s used to Retool employees (if the external SaaS product only automates minor tasks). Conversely, an “In‐House” system could completely Remove roles if it fully automates the core function.  
- **Supervision** and **Workforce** can overlap, but partial or even manual supervision does not always protect a job if the tasks that matter have been subsumed by the system. For instance, a fully autonomous AI that takes over 70% of crucial tasks might still require a single manager for oversight, but that manager could be entirely different from the original employees doing the tasks. The original role is effectively Removed.

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