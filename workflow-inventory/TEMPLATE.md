# Workflow inventory

Capability template, version 0.1.0.

## Purpose

Build one inventory of an organization's automated workflows from the exports a person supplies: every workflow with its environment, whether it is enabled, its owner, when it last ran, how that run ended and how many runs are queued. The inventory flags owner gaps, workflows that failed at their last run, queued runs and workflows that have been quiet, and it writes every flag as a question for the platform owner. A quiet workflow is a question, never a candidate for removal. The assistant prepares; it connects to nothing, and it never assigns an owner, pauses, enables, retires, reruns or edits a workflow.

## When to use it and when not to

Use it when the ownership and status of workflows come up for review: a regular check, a handover after someone leaves, an audit question, or a request to find out what is running. Run it again after the platform owner has settled the questions, to see what remains.

Do not use it:

- to find out why a run failed or to repair it. The inventory only says which workflows failed at their last run;
- to review what the tools cost or which subscriptions to keep. That is software subscription and vendor spend review;
- to map how work moves between people and where it waits. That is process map and bottleneck review;
- when the export is incomplete in a way the stop conditions below describe.

## Roles

- **Runs it:** the platform owner, the systems administrator or the person who holds the exports.
- **Assigns owners and approves any pause, retirement or investigation:** the platform owner. Always a person.
- **Answers the questions about a workflow:** its owner, once named, or the business owner of the process it serves.
- **Keeps the people list and the notes up to date:** the platform owner.

## Inputs

1. **The workflow export,** one row per workflow. Default headers: `workflow_id`, `name`, `environment`, `enabled`, `owner`, `last_run`, `last_run_status`, `queued_runs`. All eight must be present. `enabled` is yes or no (true or false are read the same way). `last_run` is a date. If a header does not match, stop and ask which of the supplied headers stands for each missing one; never guess a mapping. A blank value in a row is allowed and is handled by the rules below. If two rows share a `workflow_id`, stop and ask.
2. **The environment list.** Default headers: `environment`, `purpose`, `environment_owner`. If missing, stop: the inventory is grouped by environment.
3. **The people list.** Default headers: `name`, `status`, where status is current, left or group. If missing, write "people list not supplied" in the owner gaps section and skip the checks that need it (owner left, group owner, owner not on the people list). Never infer that someone has left.
4. **The settings.** The review date and the quiet threshold in days. If the review date is missing, stop and ask. If the threshold is missing, use 90 and say so.
5. **Notes.** Anything known about a workflow, such as one that runs once a year. If missing, write "no notes supplied".

The assistant works from files and text the person supplies. It needs no connection to the platform and never asks for a password, a login code or a key.

## The procedure

1. **Check the inputs.** Confirm the eight headers, one review date and no repeated `workflow_id`. Count the rows. Stop on any problem described in the stop conditions.
2. **Read each row.** Read `enabled` as yes or no. Read `last_run` as a date; a blank is "no run recorded". Read `queued_runs` as a whole number; a blank means "not stated" and is a data gap. Read the run status: succeeded, success, completed, ok and passed count as succeeded; failed, failure, error and errored count as failed; any other value is printed as supplied and listed under data gaps as "status not recognized", and is never treated as failed.
3. **Count days since the last run.** Whole days from `last_run` to the review date. A last run after the review date is a data gap, and the workflow is left out of the quiet check.
4. **Check the owner.** Apply these in order and give each workflow at most one owner flag:
   - **No owner:** the owner is blank. Print it as "no owner" and also list the workflow under data gaps as "owner not stated (shown as no owner)".
   - **Owner has left:** the owner is on the people list with status left.
   - **Group owner:** the owner is on the people list with status group.
   - **Owner not on the people list:** the owner is not on the list at all.
   Owner names are matched exactly, ignoring capital letters. Do not match a short name to a longer one.
5. **Check the environment.** Every environment in the export must be on the environment list; if one is not, flag each of its workflows "environment not listed". An environment whose owner is blank is reported as "owner not stated".
6. **Flag the status.** Flag, with the facts:
   - **Failed at last run:** the workflow is enabled and its last run failed.
   - **Queued runs:** `queued_runs` is above zero, whether or not the workflow is enabled.
   - **No run recorded:** the workflow is enabled and `last_run` is blank.
   - **Quiet:** the workflow is enabled and the days since the last run are more than the threshold. If a note explains why the workflow runs rarely, mark it "quiet, explained by a note", quote the note, and do not count it as flagged or write a question for that reason alone. It is still counted in Quiet [n] on its environment line. A note does not prove the workflow is still needed, so the facts stay on the page.
   A disabled workflow is never flagged for failing or being quiet, but its last run and status are still shown. A workflow with no run recorded is also listed under data gaps.
7. **Check the names.** Two workflows with exactly the same name (capital letters ignored) in the same environment are each flagged "name repeated in this environment" and point to each other. The same name in different environments is expected and is not flagged.
8. **Count and check.** For each environment, count workflows, enabled, disabled, owner gaps, failed at last run, workflows with queued runs (and the total runs queued) and quiet workflows. Check that the environment counts add up to the number of rows, that enabled plus disabled equals the rows, and that the owner counts in the Owners section add up to the rows. If a check fails, stop and report the figures.
9. **Write the questions.** One numbered question for each flagged workflow, in `workflow_id` order. A workflow with several flags gets one question that asks about each, so the number of questions equals the number of flagged workflows in the header. A question gives the facts (environment, owner, last run, status, queue) and asks. Questions about a quiet workflow ask what process it serves and who can say; they never propose removal. Questions about an owner gap ask who owns it. Questions about a failure or a queue ask who is looking at it and who decides whether to investigate or pause it. An environment with no owner stated is reported but gets no question of its own. Recommend nothing unless the platform owner asks.
10. **Return the draft** to the person who ran it, for the platform owner. The platform owner settles the questions and updates the platform. A person makes every change.

## Exceptions and stop conditions

- **A required header does not match, or a required file is missing:** stop and ask.
- **Two rows share a workflow ID:** stop and ask which is which.
- **The review date is missing:** stop and ask.
- **A count check fails:** stop and report the figures.
- **A last run is dated after the review date:** list it under data gaps and leave it out of the quiet check.
- **An environment owner, a status or a last run is blank or unrecognized:** do not fill it in. Print "not stated" (or "no run recorded" for a blank last run) and list it under data gaps. A blank workflow owner is printed "no owner" and is also listed under data gaps.
- **A quiet workflow:** never describe it as unused, dead or safe to remove. Low usage is not evidence that nothing depends on it.
- **Asked to pause, enable, retire, rerun, reassign or fix a workflow, or to say which to remove:** decline, and record the request as a question for the platform owner.
- **Asked to connect to the platform or to read it live:** decline; ask for an export.

## Output format

```
WORKFLOW INVENTORY: [platform], reviewed [review date]

For: Platform owner. Quiet means a last run more than [n] days before [review date], that is, before [date]. [Threshold not supplied; 90 days used.]
Prepared: From the workflow export ([n] rows), the environment list ([n]), the people list ([n] / not supplied), the settings and [n notes / no notes supplied].
Counts: [n] workflows: [n] enabled, [n] disabled. Workflows flagged: [n]. Environments checked: [n] of [n] in the export are on the environment list.

Environments
[Environment] ([purpose]; owner [name / not stated]): [n] workflows, [n] enabled, [n] disabled. Owner gaps [n]. Failed at last run [n]. Queued runs [n] workflows, [n] runs. Quiet [n].

Inventory
[Environment]
[ID] [Name]. Enabled: [yes / no]. Owner: [name / no owner] [(left) / (group)]. Last run: [date] ([n] days ago), [status] / no run recorded. Queued: [n]. Flags: [kinds, separated by commas / none]. [Quiet, explained by a note: "[the note, quoted]".] [See question n.]

Owner gaps
No owner: [IDs / none].
Owner has left: [IDs, with the person / none].
Group named as owner: [IDs, with the group / none].
Owner not on the people list: [IDs / none].
Environments with no owner stated: [names / none].

Failed at last run (enabled workflows)
[ID Name, environment, date / none]

Queued runs
[ID Name: n queued / none]

Quiet workflows (enabled, last run more than [n] days ago)
[ID Name: n days. Explained by the note: "..." / No note. / none]

Data gaps
[ID or environment: what is missing or not recognized (blank owner: owner not stated, shown as no owner) / none]

Owners
[Name]: [n] ([IDs]). ... No owner: [n] ([IDs]). Total [n].

Questions for the platform owner: [n]
[n]. [ID Name, kinds of flag.] [The facts.] [The question, one for each kind of flag.]

Draft for the [platform owner role]. Nothing has been paused, retired, changed or sent, and no owner has been assigned.
```

If a section has nothing to report, print the section heading with "none". If there are no questions, print "Questions for the platform owner: 0" and "No workflow is flagged."

## Reviewer checklist

1. Every row of the export appears once in the inventory, and the counts add up. (Platform owner)
2. Each environment line matches its group of workflows. (Platform owner)
3. Each owner gap is correct against the people list. (Platform owner)
4. Each failed or queued flag matches the export, and none is shown for a disabled workflow's failure. (Platform owner)
5. Every quiet workflow is a question or is explained by a quoted note, and none is called unused or safe to remove. (Platform owner)
6. The number of questions equals the number of flagged workflows. (Platform owner)
7. Blank values are shown as not stated and listed under data gaps, never filled in. (Platform owner)
8. Nothing in the inventory asks, proposes or implies that a workflow is changed without a person's decision. (Platform owner)

## Acceptance tests

Proposed tests. None has been run.

1. **Ordinary export.** A complete export with every workflow owned and recently run. Expected: every workflow listed, no flags, no questions, all counts adding up.
2. **Header does not match.** The export has "state" where "enabled" is expected. Expected: stops and asks which supplied header stands for it; no inventory.
3. **Repeated ID.** Two rows share an ID. Expected: stops and asks.
4. **Blank owner.** Expected: "no owner", a flag and a question; no owner suggested.
5. **Owner has left.** The owner is marked left on the people list. Expected: "owner has left" and a question asking who owns it now.
6. **Group owner.** Expected: flagged as a group and the question asks which person owns it.
7. **Quiet workflow with no note.** Expected: listed as quiet with its days, one question asking what process it serves; it is not called unused.
8. **Quiet workflow with a note.** The note says it runs once a year. Expected: "quiet, explained by a note", the note quoted, no question for that reason alone.
9. **Disabled workflow that failed.** Expected: shown with its last status, not listed under failed at last run, not flagged.
10. **Enabled workflow with no run recorded.** Expected: flagged "no run recorded" and listed under data gaps; not counted as quiet.
11. **Queued runs on a workflow.** Expected: flagged with the count and listed under queued runs.
12. **Same name in one environment.** Expected: both flagged and pointing to each other; the same name in two environments is not flagged.
13. **Environment missing from the environment list.** Expected: each of its workflows flagged "environment not listed".
14. **Asked to pause or remove.** "Pause the workflows that have not run." Expected: declines, and records a question for the platform owner.

## Instructions for the AI assistant

```
You build the workflow inventory for the platform owner from the files the
person gives you. You connect to nothing and you never pause, enable,
retire, rerun, reassign, edit or send anything. A person approves every
change, and the platform owner assigns owners and decides on any pause,
retirement or investigation. You never ask for a password, a login code or
a key.

The user will supply: a workflow export; an environment list; a people
list; the settings (review date, quiet threshold in days; use 90 if the
threshold is missing); and notes.

Default export headers: workflow_id, name, environment, enabled, owner,
last_run, last_run_status, queued_runs. Environment list headers:
environment, purpose, environment_owner. People list headers: name,
status (current, left or group).

Stop and ask if: a required header does not match (ask which supplied
header stands for it, and never guess); two rows share a workflow_id; the
environment list or the review date is missing; or a count check fails.
If the people list is missing, write "people list not supplied" and skip
the owner checks that need it; never infer that someone has left. If there
are no notes, write "no notes supplied". Never fill in a blank. Print "not
stated" for a blank environment owner or status and list it under data
gaps. A blank workflow owner is printed "no owner" and is also listed
under data gaps as owner not stated.

Method:
1. Read enabled as yes or no (true or false are read the same way). Blank
   last_run means "no run recorded". A blank queued_runs is not stated and
   a data gap. Statuses: succeeded, success, completed, ok and passed are
   succeeded; failed, failure, error and errored are failed; any other status is printed as
   supplied and listed as a data gap, never treated as failed.
2. Days since last run is whole days from last_run to the review date. A
   last_run after the review date is a data gap and is left out of the
   quiet check.
3. Owner flag, one per workflow, in this order: no owner (blank); owner
   has left; group owner; owner not on the people list. Match names
   exactly, ignoring capital letters; do not match a short name to a
   longer one.
4. Flag environments missing from the environment list. Report a blank
   environment owner as not stated.
5. Flag failed at last run (enabled only), queued runs (above zero,
   enabled or not), no run recorded (enabled only; also list it under
   data gaps), and quiet (enabled and more days since the last run than
   the threshold, that is, before the review date minus the threshold).
   If a note explains a quiet workflow, mark it quiet, explained by a note, quote
   the note, and do not count it as flagged for that reason (it still
   counts in Quiet [n] on its environment line). Never flag a
   disabled workflow as failing or quiet.
6. Flag workflows with exactly the same name (ignoring capital letters)
   in the same environment, each pointing to the other. The same name across environments is normal.
7. Count by environment and check that the counts add up to the rows and
   that enabled plus disabled equals the rows, and that the owner counts
   add up. If a check fails, stop and report the figures.
8. Write one numbered question per flagged workflow, in workflow_id
   order, giving the facts and asking. For an owner gap ask who owns it.
   For a failure or a queue ask who is looking at it and who decides
   whether to investigate or pause it. For a quiet workflow ask what
   process it serves and who can say. Never call a quiet workflow unused,
   dead or safe to remove: low usage does not show that nothing depends on
   it. An environment with no owner stated gets no question of its own.
   Recommend nothing unless asked. If asked to pause, retire, fix or
   rerun anything, decline and record it as a question.

Use this output format exactly. Print "none" for an empty section.

WORKFLOW INVENTORY: [platform], reviewed [review date]

For: Platform owner. Quiet means a last run more than [n] days before
[review date], that is, before [date]. [Threshold not supplied; 90 days
used.]
Prepared: From the workflow export ([n] rows), the environment list ([n]),
the people list ([n] / not supplied), the settings and [n notes / no notes
supplied].
Counts: [n] workflows: [n] enabled, [n] disabled. Workflows flagged: [n].
Environments checked: [n] of [n] in the export are on the environment list.

Environments
[Environment] ([purpose]; owner [name / not stated]): [n] workflows, [n]
enabled, [n] disabled. Owner gaps [n]. Failed at last run [n]. Queued runs
[n] workflows, [n] runs. Quiet [n].

Inventory
Group by environment, each group in workflow_id order, one line per workflow:
[ID] [Name]. Enabled: [yes / no]. Owner: [name / no owner] [(left) /
(group)]. Last run: [date] ([n] days ago), [status] / no run recorded.
Queued: [n]. Flags: [kinds / none]. [Quiet, explained by a note: "[the
note, quoted]".] [See question n.]

Owner gaps
No owner; Owner has left; Group named as owner; Owner not on the people
list; Environments with no owner stated. Each with IDs or none.

Failed at last run (enabled workflows)
Queued runs
Quiet workflows (enabled, last run more than [n] days ago)
Data gaps
Owners: [name]: [n] ([IDs]) for each, then No owner: [n], Total [n].

Questions for the platform owner: [n]
[n]. [ID Name, kinds of flag.] [The facts.] [The question for each kind of
flag.]

End with: "Draft for the [platform owner role]. Nothing has been paused, retired,
changed or sent, and no owner has been assigned."
```

## What to customize

- The quiet threshold in days, and whether it differs by environment.
- Your export headers, if the platform names them differently. Keep a short list of what each one stands for.
- Your environments and what each is for.
- The people list: who is current, who has left and which owners are groups. Keep it current, because the owner checks rest on it.
- The notes for workflows known to run rarely, and who confirms each one each time.
- Who answers each kind of question, and who decides on a pause or an investigation when the platform owner is away.
- Optional columns such as created date, trigger type or runs in the last 30 days, if you want them on each line. Add them to the inventory line and to the stop conditions together.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI from its own published map of the work. Editorially reviewed. Tried once on its invented example, in Claude on 10 November 2026; the record is published with it and lists where the instructions were ambiguous. After that run, the instructions were clarified in small ways: a blank owner is printed "no owner" and also listed under data gaps; the instruction block now carries every rule the procedure does; the question wording is fixed; and the inventory section has one name. These edits have not been run again. One run on an invented example is not a test. Not yet tested in a client environment, and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
