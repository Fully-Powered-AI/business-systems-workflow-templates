# Workflow inventory

When the ownership and status of your automated workflows come up for review, the platform owner gets one inventory built from the exports supplied: environments, enabled states, last run, queued runs and owner gaps. Quiet workflows become questions, not removal lists.

*Capability template · Business systems and integrations · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/workflow-inventory/)*

## The outcome

The platform owner sees every automated workflow in one list, grouped by environment, in the same shape every time. Each line says whether it is switched on, who owns it, when it last ran, how that run ended and whether runs are waiting. The gaps are on the page: workflows with no owner, owners who have left, groups named where a person is needed, and workflows that have never been seen running.

A workflow that has been quiet for a long time is not treated as dead weight. It appears as a question with its facts, because some of the most useful workflows run once a quarter or once a year. The platform owner assigns owners and decides whether anything is paused, retired or looked into. The capability decides nothing and touches nothing.

## Who starts the work, and when

The platform owner, the CRM or systems administrator, or whoever runs the business systems starts it when ownership and status of workflows come up for review: a quarterly check, a handover when someone leaves, an audit question, or the day somebody asks who owns that automation. The platform owner reviews the result and takes the questions to the people who can answer them.

## What they supply

- **The workflow export.** One row per workflow: its ID, name, environment, whether it is enabled, its owner, when it last ran, how that run ended and how many runs are queued.
- **The environment list.** Each environment, what it is for and who owns it.
- **The people list.** Each named owner, marked as current, left or a group.
- **The review date and the quiet threshold,** the number of days without a run after which a workflow is raised as a question.
- **Notes,** such as a workflow that is known to run only once a year.

The capability works from files the person supplies. It connects to nothing, and it never asks for a password, a login code or a key.

## What comes out

One inventory in a fixed order: counts and a line for each environment, every workflow with its facts and flags, the owner gaps, the workflows that failed at their last run, the queued runs, the quiet workflows, the data gaps, how many workflows each owner holds, and a numbered list of questions for the platform owner. The counts are checked against each other so a missing row shows up before anyone relies on the page.

Every flag is a statement of what the export shows. Nothing in the inventory pauses, retires or changes a workflow, and nothing is sent.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Business systems and integrations](https://fullypowered.ai/functions/business-systems-and-integrations/), where the owner of the platform needs to know what is running before changing anything around it.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where client-facing automations pile up around matters, billing and onboarding.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where internal automations multiply faster than anyone records them.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where order, stock and refund workflows run all day and a failed one costs real orders.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/), where automations outlive the people who built them.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/), when a handful of automations becomes a hundred.

It is a different piece of work from [software subscription and vendor spend review](https://fullypowered.ai/capabilities/software-subscription-and-vendor-spend-review/), which looks at what tools cost, and from [process map and bottleneck review](https://fullypowered.ai/capabilities/process-map-and-bottleneck-review/), which looks at how work moves between people. This one looks at the automations themselves.

## What has to change for your company

Decide how many days without a run is worth a question; the default is 90. Name your environments and what each is for. Keep a people list that marks who has left and which owners are groups. Decide which workflows are known to be occasional and write them as notes. Settle who answers each kind of question. Adjust the export columns to the names your platform uses. The method does not change with the platform, and the capability works from the exports you give it, not from a particular product.

## What has been checked

Fully Powered AI wrote this capability template. It was editorially reviewed on 10 November 2026. It was tried once on its invented example, in Claude on 10 November 2026, and the record of that run is published with it, listing where the instructions were ambiguous. Small clarifications made afterward, to settle those places, have not been run again; the record lists them. One run on an invented example is not a test. It has not yet been tested in a client environment, and it has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on an export your platform owner already knows well, with cases written in advance: a workflow with no owner, an owner who has left, a workflow that is quiet for a good reason, a run that failed, a column header that does not match. The platform owner checks every line against the platform itself before anyone relies on the inventory. [Process map and bottleneck review](https://fullypowered.ai/capabilities/process-map-and-bottleneck-review/) can help sort out what a given workflow is for once its owner is found.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete capability template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the capability drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related capabilities

- [Software subscription and vendor spend review](https://fullypowered.ai/capabilities/software-subscription-and-vendor-spend-review/)
- [Process map and bottleneck review](https://fullypowered.ai/capabilities/process-map-and-bottleneck-review/)
- [Learning system access review](https://fullypowered.ai/capabilities/learning-system-access-review/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
