# App data requirements

Turn unclear internal app requirements into one data specification of entities, fields and questions for the process owner. Nothing is built.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See App data requirements on our website](https://fullypowered.ai/workflows/app-data-requirements/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements) Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the invented ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Business systems and integrations · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/app-data-requirements/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements)*

## The outcome

The people who will build the app and the people who will use it work from the same list of what the app must know and who may read or change it. Every field in the list says which line of the request or which approved rule asks for it. Where the request is vague, the specification does not fill the gap; it writes a question the process owner can answer in a sentence.

A request such as "managers handle the long loans" stops being a surprise in the middle of the build. The verb is flagged as unclear, the object it acts on is named, and the question waits for the process owner before any configuration starts.

The analyst confirms the specification with the process owner. Nothing in it counts as agreed until both have said so.

## Who starts the work, and when

The business systems analyst starts it when the notes for an internal app have been gathered and the fields or actions are still unclear, before anyone configures or builds. It runs again when the notes change, a rule is approved or the process owner has answered the questions.

## What they supply

- **The request notes,** as plain text, one statement to a line.
- **The approved process rules,** one numbered rule to a line.
- **The object definitions** of the systems the app will use: each object, its fields, their types and whether they are required, as an export with the default column headers.
- **Sample records,** invented ones, in a file with the default column headers. They are never copied from live data.
- **A few settings:** the app's name, the date, who the specification is for and which verbs your company uses to mean reading, writing or sending.

## What comes out

One specification in a fixed order: the files and the header check, the names matched, the entities, the fields with who reads and writes each, the actions, the approved rules checked against the fields, the sample records checked against the definitions, numbered questions for the process owner, the decisions that remain and what was not checked. A section with nothing to report says what was checked and found nothing.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Business systems and integrations](https://fullypowered.ai/functions/business-systems-and-integrations/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements), where an internal app has to agree with the systems around it before anyone configures it.
- [Operations and process improvement](https://fullypowered.ai/functions/operations-and-process-improvement/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements), where the process owner's rules become data the app has to hold.
- [Professional services](https://fullypowered.ai/industries/professional-services/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements), where internal tools for requests, approvals and tracking are often built from a few lines of notes.
- [Software and technology](https://fullypowered.ai/industries/software-technology/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements), where the analyst turns a product or support request into the data a build team can read.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements), where small internal apps for stock, returns and requests grow beside the store.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements), when a shared spreadsheet has become an app and nobody has written down what it holds.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements), when a long-running process moves into a new internal tool.

It settles the data an app needs. To write the testable behaviours of a story, use [acceptance criteria sheet](https://fullypowered.ai/workflows/acceptance-criteria-sheet/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements). To settle what a report shows, use [dashboard brief](https://fullypowered.ai/workflows/dashboard-brief/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements). To understand one unfamiliar export, use [dataset profile](https://fullypowered.ai/workflows/dataset-profile/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements).

## What has to change for your company

Check that your object definitions use the default column headers, or rename the headers before you run it; a mismatch stops the work on purpose. List the verbs your company uses for reading, writing and sending, since "handle", "process" and "track" mean different things in different places. Decide who plays the process owner and who confirms. Prepare sample records by hand and make sure none comes from live data; the work stops if one looks real. It runs in ChatGPT, Claude, Copilot or Gemini from files you supply, needs no connection to your systems, and never asks for a login.

## What has been checked

FullyPowered AI wrote this workflow template. It was editorially reviewed on 10 November 2026. It was tried on its invented example in Claude on 10 November 2026; the record is published with it. The first run found that the example stated things the notes do not (who sets a due date, which fields a history reads, two fields counted as needed that no line asks for), that it left out two headings the format requires, and that the procedure could not produce the counts the template expected. The template and the example were then changed, and the edited version was run once more on the example by the assistant that made the edits, not independently. That run covered unclear verbs, names with no match, a word that fits an object and one of its fields, a rule that needs a field nobody mentioned and a sample date that is not a date; it did not reach a mismatched header, a sample value that looks real, a missing rules file or a request to build the app. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on the notes for a small app your analyst already knows, with gaps planted in copies and written down in advance: a verb with no clear meaning, a name that matches no object, a rule that needs a field nobody mentioned, a sample value of the wrong type. The analyst checks every line of the specification against the notes before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements) describes the record we keep.

- Written by FullyPowered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
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

- [Acceptance criteria sheet](https://fullypowered.ai/workflows/acceptance-criteria-sheet/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements)
- [Dashboard brief](https://fullypowered.ai/workflows/dashboard-brief/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements)
- [Dataset profile](https://fullypowered.ai/workflows/dataset-profile/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-app-data-requirements&from=gh-app-data-requirements).
