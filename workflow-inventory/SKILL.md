---
name: "workflow-inventory"
description: "Build one inventory of an organization's automated workflows from the exports a person supplies: every workflow with its environment, whether it is enabled, its owner, when it last ran, how that run ended and how many runs are queued. The inventory flags owner gaps, workflows that failed at their last run, queued runs and workflows that have been quiet, and it writes every flag as a question for the platform owner. A quiet workflow is a question, never a candidate for removal. The assistant prepares; it connects to nothing, and it never assigns an owner, pauses, enables, retires, reruns or edits a workflow."
license: "MIT"
metadata:
  version: "0.1.0"
  publisher: "Fully Powered AI"
  template: "Workflow inventory"
---

# Workflow inventory

This is the technical file for a Fully Powered workflow template. It carries the instructions an AI product follows. The complete template, with roles, inputs, exceptions, the reviewer checklist, acceptance tests and what to customize, is in [TEMPLATE.md](TEMPLATE.md). A worked example with invented data is in [EXAMPLE.md](EXAMPLE.md).

## Instructions

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

## Before relying on it

Decide every item under "What to customize" in TEMPLATE.md and set the limits the instructions in this file leave open, written in square brackets such as [N], to your own. Then run the acceptance tests in TEMPLATE.md on past work. A person starts this work, supplies the inputs and decides what happens with the result.
