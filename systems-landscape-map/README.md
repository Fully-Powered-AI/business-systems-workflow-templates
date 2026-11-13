# Systems landscape and data flow map

Before a major system decision, or at the annual review, the operations or systems lead gets one map of the company's systems from the lists and interviews supplied: what each is the record for, who owns it, which data moves between them, and every gap and duplicate record of truth as a question.

*Workflow template · Business systems and integrations · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/systems-landscape-map/)*

## The outcome

The company sees all of its systems on one page, the way an architect would draw them, without having to hire one. A table shows every system with what it is used for, the kinds of record it is the record of truth for, what else it holds, its business owner and the person who runs it. A list of flows shows what data moves between systems, how it moves (automatically, by file, or retyped by hand), how often and who keeps it running. A plain-text diagram draws the same flows so anyone in the meeting can follow them.

The map marks what usually only surfaces halfway through a system project: two systems that are each treated as the truth for customers, a spreadsheet that holds the prices and belongs to nobody, orders that live in three places with no agreed home, a weekly file nobody owns. It never settles these itself. Each one becomes a plain question for the person who can answer it, and the map reviewer gets a short list of decisions, with the ones that bear on the system under decision marked.

The workflow template works only from the lists and notes you give it. It connects to no system, asks for no login and changes nothing. People decide which system is the record for what, who owns each system and flow, and what happens next.

## Who starts the work, and when

The operations lead or systems lead starts it in a company without an architect, before a major system decision: replacing the accounting system, adding an online shop, bringing two companies' tools together. It runs again at each annual review, with last year's map, so the changes show. The person collects a systems list and a list of known connections, talks to the owner of each system, writes up the notes, reads the map and takes the questions to the people they are addressed to.

## What they supply

- **A systems list,** one row per system: what it is used for, the kinds of record it holds, the kinds it is the record of truth for, its business owner and its administrator. Spreadsheets and shared folders that are the only home of something belong on it.
- **A connections list,** one row per known flow: from which system to which, the records it carries, how it moves, how often and who owns it.
- **Interview notes** from short conversations with each system's owner and the people who move data by hand, each headed with the person's role and the date.
- **Settings:** the company or unit, the reason for the map, the system under decision if there is one, who reviews the map, the kinds of record to map (or the standard list), and last year's map if there is one.

## What comes out

One map in a fixed order: the files and their header check, the systems table, the record of truth for each kind of record, the data flows, the diagram, the gaps, the duplicate records of truth, the changes since last year, questions grouped by who answers them, and decisions for the map reviewer. A section with nothing to report says what was checked and that it found nothing.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Business systems and integrations](https://fullypowered.ai/functions/business-systems-and-integrations/), where someone has to know how the company's systems fit together before choosing what to keep, add or retire.
- [IT and systems](https://fullypowered.ai/functions/it-and-systems/), where the person who runs the tools is asked which one holds the real customer list.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where client records sit in a CRM, a billing tool and a project tool at once.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/), where products, stock and orders pass between sales, the warehouse and accounts, often by hand.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where an online shop, a warehouse system and the books each hold their own copy of orders and products.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/), where shipments, stock and invoices move between several systems every day.
- [Acquisitions and integration](https://fullypowered.ai/situations/acquisitions-and-integration/), when two companies' systems have to be laid side by side before anything is merged.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/), when tools added one at a time have become a landscape nobody has drawn.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/), where how data moves lives in a few long-serving people's heads and should live on a page.

For the fields two systems share before a sync is switched on, use the [CRM field ownership map](https://fullypowered.ai/workflows/crm-field-ownership-map/). For what each subscription costs and who owns it, use the [software subscription and vendor spend review](https://fullypowered.ai/workflows/software-subscription-and-vendor-spend-review/). For the automations running on one platform, use the [workflow inventory](https://fullypowered.ai/workflows/workflow-inventory/). This workflow template is for the whole landscape.

## What has to change for your company

Settle the kinds of record your company runs on: the standard list covers customers, suppliers, products, prices, sales orders, invoices, payments received, stock levels and employees, and you can add projects, contracts or service tickets. Keep the systems list in the shape the workflow template reads and ask each owner to fill in their own row. Decide who reviews the map and who stands in for an owner who is away. Keep the approved map where next year's review can find it. It runs in ChatGPT, Claude, Copilot or Gemini from files and notes you supply, and needs no connection to any of your systems.

## What has been checked

Fully Powered AI wrote this workflow template. It was editorially reviewed on 11 November 2026. It was tried once on its invented example, in Claude on 11 November 2026, and the record of that run is published with it, listing where the instructions were ambiguous. Clarifications made afterward, to settle those places and to put a privacy rule into the instruction text, have not been run again; the record lists them. One run on an invented example is not a test. It has not yet been tested in a client environment.

Testing in your environment means running it on a part of your landscape your operations lead already knows well, plus hard cases written in advance, each with its expected result: two systems both named as the record for customers, a spreadsheet with no owner, a flow someone mentions that is on no list, a renamed column in the systems list, a password pasted into a note. The operations lead checks every row and flow against the lists and notes before anyone relies on the map. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/) builds that test set, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 11 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 11 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete workflow template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the workflow template drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related workflow templates

- [CRM field ownership map](../crm-field-ownership-map/)
- [Software subscription and vendor spend review](https://fullypowered.ai/workflows/software-subscription-and-vendor-spend-review/)
- [Workflow inventory](../workflow-inventory/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
