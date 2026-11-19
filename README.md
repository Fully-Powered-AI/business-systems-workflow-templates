# AI workflow templates for business systems owners

FullyPowered Workflow Templates for operations and systems teams turn the AI your company already pays for into a team that knows how the work is done: a systems lead with the company's systems and data flows mapped, a service owner with the new inbox routing plan prepared, a systems owner with the CRM field ownership map drafted. 7 workflow templates, made to be customized and deployed. All plain Markdown, all free, MIT license.

We are FullyPowered AI. We build AI workflows for companies, and these are the templates we start from. We publish them because a good starting point should be open to everyone. Copy one. Change it. Make it yours.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** These are templates, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See more examples for operations and systems teams](https://fullypowered.ai/functions/business-systems-and-integrations/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-readme&from=gh-business-systems-readme) · [Have one built for your team](https://fullypowered.ai/pricing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-readme&from=gh-business-systems-readme) Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Who this is for**

- Owners and CEOs who want the business systems they already run to work together cleanly.
- Operations and systems leads who want a clear map and plan their team can use this week.
- The systems owner or analyst who gets a precise first draft and still makes every call.

**What these are for**

- **Your best way of doing it, for the whole team.** One piece of work, written down precisely enough that an assistant prepares it the same way every time.
- **Work you can check.** Every template says what it needs, what it produces, what it checked and what it could not.
- **A person decides.** Anything that sends, posts, pays or changes a record waits for someone to approve it.
- **Tied into your business systems.** A workflow can be designed to pull from the systems your company already runs, and even push data back into them, with guardrails and a person approving. [Browse the Connectors Directory](https://fullypowered.ai/connectors/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-readme&from=gh-business-systems-readme).
- **Free, open and portable.** MIT-licensed plain instructions that run in the assistant or agent your team already uses: ChatGPT, Claude, Claude Code, Claude Cowork, Codex, Copilot, Gemini, Grok, Perplexity.

**Quick start**

1. **Map your systems with an assistant you already use.** Open ChatGPT, Claude, Copilot or Gemini. Copy the text below into a new chat. Replace the square brackets with a plain list of your systems and how data moves between them. Typed notes are enough. You do not need a file, and you give no passwords.

   ```text
   You are helping an operations lead build a map of the company's business systems. I will paste a list of systems, a list of how data moves between them, and notes from conversations. Do not ask for any password or login. Do not decide anything for me. For each system, show what it is used for, which kinds of record it is the record of truth for, who owns it and who runs it. List every flow of data with its method, how often it runs and who owns it. Draw the flows in plain text. Mark gaps and duplicate records of truth. Turn every unknown into a question for the person who can answer it. I decide which system is the record, who owns what and what happens next. Nothing is connected or changed. My systems: [list]. My flows: [list]. My notes: [notes].
   ```

2. Read what comes back. It marks what it checked and what is left for you. What comes out, with invented data:

   ```text
   SYSTEMS LANDSCAPE MAP: Company R

   For: Operations lead. Prepared 11 November 2026 from the systems list (6 rows), the connections list (7 rows), 4 interview notes, and the settings. Reason: the owners decide in the spring whether to replace the accounting system. System under decision: S2 Accounting system.
   Summary: 6 systems. 9 record types: 5 stated, 2 disputed, 0 named in an interview only, 2 none named, 0 not held. 8 flows: 7 from the connections list, 1 from interviews; 4 re-keyed by hand; 1 with no owner. 11 questions. 6 decisions.

   1. THE FILES
   Header check: both lists have the headers expected.
   Systems list: 6 rows (lines 2 to 7). Connections list: 7 rows (lines 2 to 8). Interview notes: Finance manager, 3 November 2026; E-commerce manager, 4 November 2026; Sales director, 5 November 2026; Warehouse manager, 5 November 2026.
   Record types: the default list (9): customers; suppliers; products; prices; sales orders; invoices; payments received; stock levels; employees. Values not on the list: none.
   ```

3. Stop there. You will know if this is for you. When you want it fitted to your company, or built into your agents, [that is what we do](https://fullypowered.ai/pricing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-readme&from=gh-business-systems-readme).

A person starts each workflow, supplies the inputs and decides; the template prepares and checks, and every question it raises goes to the person who can answer it.

These are examples and a starting point, made to be changed to fit how your company works. A workflow can be one step or many, and work that is not here can be built for your company, one step or many.

## The workflow templates here today

- **[App data requirements](app-data-requirements/)**: When the requirements for an internal app leave fields or actions unclear, the business systems analyst gets one data specification: entities, fields, who reads and writes each, and every unresolved name as a question. Nothing is built or changed.
- **[CRM field ownership map](crm-field-ownership-map/)**: Before a CRM sync or field mapping changes, the systems owner gets a field map from the supplied exports and sample records: each field's source, match keys and conflict rule, with unclear keys, consent fields and duplicates left as questions for each field's owner.
- **[Notification channel plan](notification-channel-plan/)**: When a business event needs to notify people, the integration owner gets one channel plan from the event definitions: trigger, urgency, who is told by which channel, what needs confirmation, fallbacks and reply handling. Consent and message rules stay as questions. Nothing is sent.
- **[Record sharing access matrix](record-sharing-access-matrix/)**: When an approved access policy has to reach the CRM, the system owner lays the current sharing setup beside the proposed one, by record type and by role, internal and external. Every change is a question for its owner; inherited and platform-fixed settings are marked unknown.
- **[Service inbox routing plan](service-inbox-routing-plan/)**: When a new service inbox is being set up, the service owner gets a routing plan: each approved address, the queue it should reach and who owns it, checks to run before it goes live, and the wrong-address risks, loop risks and unconfirmed queue owners still open. Nothing is configured.
- **[Systems landscape and data flow map](systems-landscape-map/)**: Before a major system decision, or at the annual review, the operations or systems lead gets one map of the company's systems from the lists and interviews supplied: what each is the record for, who owns it, which data moves between them, and every gap and duplicate record of truth as a question.
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

The [FullyPowered Workflows Directory](https://fullypowered.ai/workflows/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-readme&from=gh-business-systems-readme) lists every workflow template across functions and industries, with search. A machine-readable list of this repository is in [index.json](index.json).

For the work these templates come from, by team and by task, see [AI workflow examples for business systems and integrations teams](https://fullypowered.ai/functions/business-systems-and-integrations/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-readme&from=gh-business-systems-readme).

## Licence and credits

MIT, in [LICENSE](LICENSE) and in every folder. Each folder's SOURCES.md names what the workflow template drew on. Published by [FullyPowered AI](https://fullypowered.ai/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-readme&from=gh-business-systems-readme).
