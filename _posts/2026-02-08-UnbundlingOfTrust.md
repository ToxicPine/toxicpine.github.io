---
title: "What Are You Paying Salesforce For?"
date: 2026-02-08 02:00:00 +0100
categories: [Technology, Papers]
tags: [ai, automation, saas, cybersecurity, infrastructure as code]
---

If you pay people to work at computers, you're paying for work they aren't doing.

Nearly half the workforce claims to use AI tools that offer massive leverage, yet per-employee revenue hasn't shifted significantly. These claims can't both be true unless the efficiency gains are leaking out of the firm. I'd wager that at least some of those gains are leaking into your employees' leisure time, because the current employment contract makes it irrational for them to do anything else.

There are two kinds of automation, and only one is actually happening. The first is AI helping a worker do the grunt work: drafting the report, formatting the slides, writing the formulas. The worker still sits there copying the output into your CRM, one field at a time. The second is code that directly reads and writes to company systems with no human in the loop. The first is everywhere. The second is almost entirely blocked.

The productivity leak comes from the first kind being hidden. If an analyst uses AI to draft a report in twenty minutes instead of eight hours, they face a choice: disclose the gain and be rewarded with more work for the same pay, or keep quiet and enjoy the rest of the day. If working faster just gets you more work, you're not going to work faster. So you get [workers holding four jobs simultaneously because ChatGPT handles most of the output](https://www.the-sun.com/tech/7868943/have-four-full-time-jobs-chatgpt/), writing Slack messages to their managers in all lowercase so they look more organic.

If the bot can do half your job, what were you being paid for all this time? Workers hide the automation and pretend the slide deck took all night, because the grind is the proof that the work was hard, and hard work is what justifies the salary. One worker got fired after his manager noticed his emails had become too perfect. Lesson learned: if you're using AI, leave in some mistakes.

You can't hire for a skill that only exists as a gap someone is trying to hide. You can't put "secretly automated my job while pretending to work" on a resume, and there's no other way to credential what you've learned. If a candidate admits they built unauthorized tools at their last job, they're confessing to being a security risk. If they don't admit it, they look like everyone else. The 10x talent is invisible because surfacing it would be career suicide.

## **Mediocrity In Your Ops Departament**

The second kind of automation is blocked for a different reason: it requires access workers shouldn't have. You can use AI to draft a report, but you can't have code directly update the customer database, because that means reading sensitive records and writing to production systems. To go from AI helping with the grunt work to code that acts on your behalf, workers would have to give their tools access to records over the internet. This should give any business heart palpitations. 

Take Samsung, which lifted its ChatGPT ban for the semiconductor division. Within three weeks, proprietary chip-testing source code was sitting on OpenAI's servers. If that's the level of care we should expect from engineers who literally design microprocessors for a living, then handing database credentials to your sales team is suicide.

For twenty years, SaaS was buoyed by standardization. Salesforce held your customer records, HubSpot held your marketing data, Workday held your HR files. This software acted as a trusted straitjacket for data: no matter how careless a user is, they can't accidentally pipe sensitive records to twitter.com. More crucially, the standard choice protects you from blame. If Salesforce gets hacked, it's a global news story and you're a victim. If your custom internal tool gets hacked, it's negligence and you're screwed.

It's not surprising that everyone uses the same tools, however this contributed to the narrowing of operational differentiation: it becomes much harder to out-execute a competitor when you are both contrained by the same products.

The industry accepted this because specialized software came with a bundle:

**Logic.** The code that does the work.

**Stability.** The engineers who fix it at 3 AM.

**Liability.** The lawyers and auditors who answer for a breach.

## **Logic Is Not The Moat**

AI has driven the marginal cost of logic to zero. Claude Code can write in an afternoon what a specialized SaaS team takes six months to ship; you could build a CRM yourself. What are you paying Salesforce for?

You're paying so that when something breaks at 3 AM it's their problem. When the auditors call, their lawyers answer. When the servers crash, their engineers fix it. You used to pay for the software and the safety net bundled together because building software was expensive. Half the value of that bundle just evaporated. The price didn't move.

The reason you still pay the SaaS Tax isn't that their software is better. It's that you don't want to own the Stability and Liability risks of custom code. If your internal script breaks, you have to find the person who wrote it. If Salesforce breaks, they have a fleet of engineers to fix it.

The SaaS bundle persists because owning an asset is a liability.

## **The IT Approval Problem**

The opportunity is to unbundle the creation of software from the assurance of its stability: that's what allows the second kind of automation to finally happen.

Thankfully, software written by AI is getting easier to maintain: for AI to work on a project, the project has to be organized so the AI can follow along, and if one AI can follow along, so can any other, so the code ends up maintainable whether you meant it to or not. Newer AI models will be better than the last at testing and sanity-checking older code, which means quality assurance will become more straightforward also.

As for the servers crashing at 3 AM, the industry has largely solved that too: the process of getting software set-up and running on a server, which has historically been fragile and manual, has become simpler and far easier to audit over the last few years (see "Infrastructure as Code"), so AI models have gotten very good at handling that part too.

Still, we need look at it from IT's perspective. If you approve a tool and something goes wrong, a data breach hits the news and your career is over. If you say no, nothing happens to you. If yes can get you fired and no can't, you're going to say no.

The danger of letting code touch your systems isn't that the code might be buggy, since buggy code without network access or file permissions is just wasted electricity. The danger is that code can reach across the internet: it can authenticate to your servers, pull down customer records, and send them anywhere. That reach is what makes automation dangerous, and right now the only way to control it is to review every tool before it runs. If you're in IT and someone asks you to approve something, you have to read through the code, understand what it does, and stake your job on it being safe. That's hours of work per request, and if you're wrong once, you're the person who approved the breach. Saying no takes ten seconds.

## **Alternative Theories**

You could argue the problem is simpler than all this: people aren't good at using AI coding tools yet, the skills are hard, and we've been underutilizing labor for decades anyway. Yes, I'll grant that this is true, but for workers to get good, they have to be able to try things... and trying things means pointing AI at real work. If an ops manager wants to see whether AI can handle their monthly reconciliation, they need to feed it actual company data. That's exactly what your IT department has been working overtime to prevent.

If the skills gap alone explained the missing productivity shift, we'd still expect to see productivity skyrocket among the more ambitious employees, the kind of people who taught themselves Excel macros before anyone asked them to. We're not, which suggests something is blocking the natural diffusion of skills, and since every path to learning these skills runs through production systems and sensitive data that workers aren't allowed to touch, we have a pretty clear explanation for why the skills aren't diffusing. 

We have the technical know-how for setting up AI models at work without risking the leakage of data, what we haven't solved the liability problem that leaves IT departments no reason to make any of this possible and every reason to prevent it.

## **The Constraint Layer**

Arguably, the solution to our approval problem is to run the code somewhere that can't reach your more sensitive systems in the first place. If the compute environment has no network access to your production servers and no stored credentials, the code physically cannot exfiltrate data or corrupt records, because there's no channel for it to do so. You don't need to trust the code or the person who wrote it. You just need to trust that the environment has no path to the things you're protecting.

What's needed is an environment where workers are given their limits already in place, where the organization decides what each environment can touch before anyone writes a line of code. There are very few solutions for providing this at the organizational level, i.e. Coder.dev, and no such solutions that are geared towards non-technical users. A developer can set up their own constraints, but they start with full access and choose to lock themselves down, which defeats the purpose. We never needed this before because writing code was slow enough that review could keep up. Now Claude Code produces code faster than anyone can review it, and the infrastructure hasn't caught up.

This turns automation from a software purchase into a labor engagement. The contractor who isn't working out is gone by the end of the month. The software that isn't working out is still there next year, and the year after that, and everyone knows it's broken but no one can kill it because too much has already been sunk into it. When you can safely run untrusted, disposable code, you don't buy a reconciliation system. You hire someone to reconcile the accounts.

The code becomes a commodity. The constraint layer that makes it safe to run is what's missing. Whoever builds it captures the productivity that's currently leaking into your employees' afternoons.