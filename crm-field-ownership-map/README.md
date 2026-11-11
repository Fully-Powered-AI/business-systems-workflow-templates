# CRM field ownership map

Before a CRM sync or field mapping changes, the systems owner gets a field map from the supplied exports and sample records: each field's source, match keys and conflict rule, with unclear keys, consent fields and duplicates left as questions for each field's owner.

*Capability template · Business systems and integrations · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/crm-field-ownership-map/)*

## The outcome

Two systems that both hold the same customer stop overwriting each other by accident. Before the change goes live, the systems owner has one page that lists every field the two systems share, says which system the definitions name as the source for each, shows how the records would be matched, and states the rule that would settle a disagreement. Each statement says what it rests on: a definition someone supplied, the fact that only one system holds the field, or nothing yet.

Where the definitions are silent or disagree, the page does not pick. It writes a question for the person who owns that field in the business, with the rows beside it. Identity keys that conflict, consent fields and duplicates that match more than one record always become questions. The page also proposes holding any open field out of the sync until its owner answers.

The capability connects to no system, changes no mapping and moves no data. The integration owner approves the mapping together with the field owners.

## Who starts the work, and when

The systems owner or CRM administrator starts it when a sync between the CRM and another system is about to be switched on, widened or rewired, or when a field is about to be added to a mapping. It is also useful after a merger or a tool change, when two customer lists must be reconciled field by field. The person supplies the exports, definitions and sample records, reads the map, and takes the questions to the field owners.

## What they supply

- **Schema exports** for both systems, one line per field, with the object, type, whether it is required and any allowed values.
- **Approved definitions,** one line per field: what it means, who owns it in the business and, where it has been decided, which system is the source.
- **The planned mapping,** the pairs of fields the change would connect, and which way it would write.
- **Sample records** from each system, as CSV rows, chosen by the person. If they are a sample, say so.
- **Settings:** the match keys to test, the fields that hold consent, any columns to report as counts only, and who approves the mapping.

## What comes out

One field map in a fixed order: the files and their header check, the field map with a source, role and conflict rule for each pair, fields held by only one system, match keys, duplicates and ambiguous matches, consent fields, questions for the field owners grouped by owner, and decisions for the integration owner. A section with nothing to report says what was checked and found nothing.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Business systems and integrations](https://fullypowered.ai/functions/business-systems-and-integrations/), where a mapping change is the moment shared fields need an owner.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where product, billing and CRM records are joined by sync tools.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where client records live in a CRM, a billing tool and a project tool at once.
- [Ecommerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where customer records flow between a shop, a CRM and a mailing tool.
- [Acquisitions and integration](https://fullypowered.ai/situations/acquisitions-and-integration/), when two companies' customer systems must be connected.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/), when a sync built for a small team is stretched to a larger one.

To understand a single export before relying on it, use [dataset profile](https://fullypowered.ai/capabilities/dataset-profile/). For two reports that give different numbers for one measure, use [metric definition reconciliation](https://fullypowered.ai/capabilities/metric-definition-reconciliation/). To plan a dashboard, use [dashboard brief](https://fullypowered.ai/capabilities/dashboard-brief/). This capability is for the fields two systems share.

## What has to change for your company

Keep your approved definitions in the form the capability reads, with an owner for every field, and add the source system to each line as decisions are made. Name your consent fields, and name the columns that must appear as counts only. Decide which match keys to test and which system writes in which direction. Say who approves a mapping. It runs in ChatGPT, Claude, Copilot or Gemini from files you supply. It needs no connection to your CRM, and it never asks for a login.

## What has been checked

Fully Powered AI wrote this capability template. It was editorially reviewed on 10 November 2026. It was tried on its invented example in Claude on 10 November 2026; the record is published with it. The run showed that the example's map left out some counts and questions the instructions call for; the example was corrected afterwards and the instructions were clarified. A later review added missing fallbacks to the instructions, settled five points the run found open and corrected small details of the example; the edited version has not been run again. It has not yet been tested in a client environment, and not yet as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a past mapping change your team already understands, with cases written in advance: a contact with no email, two records that share one, a stored cross-reference that points to a different record, a consent field that disagrees. The systems owner checks every count against the exports before anyone relies on the map. [Pilot acceptance-test preparation](https://fullypowered.ai/capabilities/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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

- [Dataset profile](https://fullypowered.ai/capabilities/dataset-profile/)
- [Metric definition reconciliation](https://fullypowered.ai/capabilities/metric-definition-reconciliation/)
- [Dashboard brief](https://fullypowered.ai/capabilities/dashboard-brief/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
