# Database table quality check

A findings sheet for the owner of a shared table: duplicate keys, blanks, bad values and broken links, each with its rows. Nothing is changed.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See Database table quality check on our website](https://fullypowered.ai/workflows/database-table-quality-check/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check). Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the sample ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Business systems and integrations · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/database-table-quality-check/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check)*

## The outcome

The owner of a table knows exactly what is wrong with it, row by row, before anyone builds on it. Every finding names the field, the problem, how many rows it touches and which ones, with each row's key beside its line number, so each one is quick to find. The sheet opens by counting every row in the export against the count the database tool shows, so nobody has to wonder whether part of the table was skipped.

Duplicates come in two kinds: the same key used twice, and records that look like the same thing under different keys, such as one serial number typed two ways. The sheet lists both and the fields where the rows differ, and never says which row is the real one.

Where the owner's rules are silent, the sheet asks instead of guessing. The owner decides every fix, and a person makes it in the database tool. The workflow template changes no record, merges nothing and deletes nothing.

## Who starts the work, and when

The operations or systems owner of the table starts it once a month, and always before the table is moved to another tool, before a report is built on it, or before an automation starts reading or writing it. It suits any table the team keeps its records in: customers, assets, projects, stock, suppliers or members.

## What they supply

- **The table export from the database tool your team keeps its records in**, as a CSV file with the column names on the first line: every record and every field of one table, unfiltered.
- **The table's rules, written once by the owner** and kept for every later run: which fields are required, which field is the key, the allowed values for each field, the format of each date and number, and which field links to which other table.
- **The linked table's export,** if you want the links checked; without it, the sheet says that link was not checked.
- **A few settings:** the table's name, the date, the reason for the check, the record count the database tool shows, and the fields that point to the same real thing when they match.

## What comes out

One numbered findings sheet in a fixed order: the rows read, duplicate keys, likely duplicates, blanks in required fields, values outside the allowed list, dates and numbers in the wrong form, and links that point to no record. Each section says how many values it read and prints a plain line when it finds nothing. Then a summary of findings and rows touched, numbered questions where a rule is missing, what the owner decides, and what was not checked.

If a column name in the export does not match the rules, or the export holds a different number of rows from the one the tool shows, the work stops and says why before any finding is written.

See the worked example in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Business systems and integrations](https://fullypowered.ai/functions/business-systems-and-integrations/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check), where the person who owns a system answers for the records in it.
- [Operations and process improvement](https://fullypowered.ai/functions/operations-and-process-improvement/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check), where a shared table runs a daily process and a bad record turns into a missed visit or a wrong order.
- [Professional services](https://fullypowered.ai/industries/professional-services/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check), where client and project tables feed billing, staffing and the reports partners read.
- [Construction](https://fullypowered.ai/industries/construction/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check), where asset, site and subcontractor tables are kept by several people across several sites.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check), where stock and location tables have to agree before an automation moves anything.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check), when a table started by one person is now trusted by the whole team.
- [Acquisitions & integration](https://fullypowered.ai/situations/acquisitions-and-integration/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check), when two companies' tables are about to become one.

It checks a table against rules the owner has written. To decide what fields an app needs in the first place, use [app data requirements](https://fullypowered.ai/workflows/app-data-requirements/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check). For an analyst's first look at an unfamiliar extract, use [dataset profile](https://fullypowered.ai/workflows/dataset-profile/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check); this one is the owner's recurring check. To explain why two reports give different numbers, use [metric definition reconciliation](https://fullypowered.ai/workflows/metric-definition-reconciliation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check).

## What has to change for your company

Write the rules file once per table and keep it beside the table; it is the part that makes later runs quick. Export the whole table, not a filtered view, and use the column names exactly as the tool writes them, since a mismatch stops the work on purpose. Decide which fields point to the same real thing for each table, such as a serial number for assets or a supplier code for stock, and list the words your team types instead of leaving a field blank. Name who receives the sheet, who decides each fix and who has edit rights to make it. It runs in ChatGPT, Claude, Copilot or Gemini from files you supply, needs no connection to your database tool, and never asks for a login.

## What has been checked

FullyPowered AI wrote this workflow template. It was editorially reviewed on 19 November 2026. It was tried once on its example on 19 November 2026 in Claude; the record is published with it, and lists the small edits made afterward that have not been run again. Only the first of its eleven acceptance tests has been run. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a copy of a table your owner already knows well, with faults planted and written down in advance: a key used twice, the same thing entered under two keys, a required field left blank, a value off the list, a date in a second format, a link to a record that does not exist, and a renamed column that should stop the work. The owner confirms each finding against the table before anyone relies on the sheet. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check) describes the record we keep.

- Written by FullyPowered AI.
- Sources and rights reviewed.
- Editorially reviewed on 19 November 2026.
- Package format checked by script on every release.
- Tried once on its example in Claude on 19 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete workflow template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example.
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

- [App data requirements](../app-data-requirements/)
- [Dataset profile](https://fullypowered.ai/workflows/dataset-profile/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check)
- [Metric definition reconciliation](https://fullypowered.ai/workflows/metric-definition-reconciliation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-database-table-quality-check&from=gh-database-table-quality-check).
