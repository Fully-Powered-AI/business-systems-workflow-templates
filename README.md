# Fully Powered Workflow Templates: Business Systems and Integrations

Know what every system holds, who can see it and where it goes next. These workflow templates are written for the person who owns the systems, not the person who codes them. They work from exports you supply, connect to nothing, change nothing and hold no credentials.

This repository holds 6 workflow templates for operations and systems owners. Each one is a single piece of work with its own folder: what it is for and who starts it, the complete template an AI assistant follows, a worked example with invented data, what to change for your company, what has been checked, and its sources.

## The workflow templates

- **[App data requirements](app-data-requirements/)**: When the requirements for an internal app leave fields or actions unclear, the business systems analyst gets one data specification: entities, fields, who reads and writes each, and every unresolved name as a question. Nothing is built or changed.
- **[CRM field ownership map](crm-field-ownership-map/)**: Before a CRM sync or field mapping changes, the systems owner gets a field map from the supplied exports and sample records: each field's source, match keys and conflict rule, with unclear keys, consent fields and duplicates left as questions for each field's owner.
- **[Notification channel plan](notification-channel-plan/)**: When a business event needs to notify people, the integration owner gets one channel plan from the event definitions: trigger, urgency, who is told by which channel, what needs confirmation, fallbacks and reply handling. Consent and message rules stay as questions. Nothing is sent.
- **[Record sharing access matrix](record-sharing-access-matrix/)**: When an approved access policy has to reach the CRM, the system owner lays the current sharing setup beside the proposed one, by record type and by role, internal and external. Every change is a question for its owner; inherited and platform-fixed settings are marked unknown.
- **[Service inbox routing plan](service-inbox-routing-plan/)**: When a new service inbox is being set up, the service owner gets a routing plan: each approved address, the queue it should reach and who owns it, checks to run before it goes live, and the wrong-address risks, loop risks and unconfirmed queue owners still open. Nothing is configured.
- **[Workflow inventory](workflow-inventory/)**: When the ownership and status of your automated workflows come up for review, the platform owner gets one inventory built from the exports supplied: environments, enabled states, last run, queued runs and owner gaps. Quiet workflows become questions, not removal lists.

## How to use one

Open a folder and start with its README. Every folder stands alone, so copy the one you want and leave the rest. The templates are written for ChatGPT, Claude, Copilot and Gemini: paste the instruction block and the output format in as custom instructions, or load the folder in a product that reads `SKILL.md` packages.

To take the whole collection, press **Use this template** at the top of this page: it copies every folder into a repository in your own account, yours to change.

In every template a person starts the work, supplies the inputs and decides. The template prepares and checks. Anything that sends, posts, pays or changes a record waits for a person to approve it.

## What SKILL.md is

Each folder holds a file named `SKILL.md`. It is the technical file: the same instructions and output format as the template, in the packaged form that AI products which load instructions from a folder read. It is generated from `TEMPLATE.md`, so the two always agree. The workflow template is the whole folder; `SKILL.md` is one way of loading it. If your AI product does not read that format, use `TEMPLATE.md`.

## What "checked" means here

Each folder says exactly what was checked and when: who wrote it, that its sources and rights were reviewed, the date of its editorial review, and whether it has been tried on its invented example in a named AI product. Nothing is described as tested for a client unless it was. Test a template on your own past work before your team relies on it; each one comes with acceptance tests for that.

## More workflow templates

The [Fully Powered Workflows Directory](https://fullypowered.ai/workflow templates/) lists every workflow template across functions and industries, with search. A machine-readable list of this repository is in [index.json](index.json).

## Licence and credits

MIT, in [LICENSE](LICENSE) and in every folder. Each folder's SOURCES.md names what the workflow template drew on. Published by [Fully Powered AI](https://fullypowered.ai/).
