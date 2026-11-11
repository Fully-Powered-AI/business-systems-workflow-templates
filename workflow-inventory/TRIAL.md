# Workflow inventory: a trial on the invented example

- **Product:** Claude, run in Claude Code

Model: Claude Sonnet 5.5 (model ID claude-sonnet-5-5). Date: 2026-11-10.

The inputs are the invented example in [example.md](example.md): the settings, the workflow export (15 rows), the environment list (3), the people list (5) and one note. They are invented, and no client data was used. The run used the instruction block and the output format in the member template, on those inputs only. The model had not written the template and did not read the example's output until after its own output was complete. The days-since-last-run figures were worked out by hand and then checked with a short date calculation.

## What came out

```
WORKFLOW INVENTORY: an invented workflow platform, reviewed 2026-11-10

For: Platform owner. Quiet means a last run more than 90 days before 2026-11-10, that is, before 2026-08-12.
Prepared: From the workflow export (15 rows), the environment list (3), the people list (5), the settings and 1 note.
Counts: 15 workflows: 12 enabled, 3 disabled. Workflows flagged: 9. Environments checked: 3 of 3 in the export are on the environment list.

Environments
Production (live store and warehouse; owner Dev): 10 workflows, 9 enabled, 1 disabled. Owner gaps 3. Failed at last run 1. Queued runs 2 workflows, 15 runs. Quiet 3.
Test (building and checking changes; owner Mara): 3 workflows, 2 enabled, 1 disabled. Owner gaps 1. Failed at last run 1. Queued runs 0 workflows, 0 runs. Quiet 0.
Demo (demonstrations for wholesale buyers; owner not stated): 2 workflows, 1 enabled, 1 disabled. Owner gaps 1. Failed at last run 0. Queued runs 0 workflows, 0 runs. Quiet 0.

Inventory
Production
W01 New order to warehouse. Enabled: yes. Owner: Mara. Last run: 2026-11-10 (0 days ago), succeeded. Queued: 0. Flags: none.
W02 Refund approval request. Enabled: yes. Owner: Dev. Last run: 2026-11-09 (1 day ago), succeeded. Queued: 0. Flags: none.
W03 Low stock alert. Enabled: yes. Owner: Mara. Last run: 2026-11-10 (0 days ago), failed. Queued: 3. Flags: failed at last run, queued runs. See question 1.
W04 Supplier price file import. Enabled: yes. Owner: no owner. Last run: 2026-11-03 (7 days ago), succeeded. Queued: 0. Flags: no owner, name repeated in this environment (W15). See question 2.
W05 Year-end stock count reminder. Enabled: yes. Owner: Tomas. Last run: 2025-12-19 (326 days ago), succeeded. Queued: 0. Flags: none. Quiet, explained by a note: "The year-end stock count reminder runs once a year, in December."
W06 Customer survey send. Enabled: yes. Owner: Priya (left). Last run: 2026-02-14 (269 days ago), succeeded. Queued: 0. Flags: owner has left, quiet. See question 3.
W07 Old returns form to email. Enabled: no. Owner: Dev. Last run: 2026-04-30 (194 days ago), succeeded. Queued: 0. Flags: none.
W08 Carrier tracking update. Enabled: yes. Owner: integrations team (group). Last run: 2026-11-10 (0 days ago), succeeded. Queued: 12. Flags: group owner, queued runs. See question 4.
W09 Wholesale account setup. Enabled: yes. Owner: Tomas. Last run: 2026-07-02 (131 days ago), succeeded. Queued: 0. Flags: quiet. See question 5.
W15 Supplier price file import. Enabled: yes. Owner: Dev. Last run: 2026-11-04 (6 days ago), succeeded. Queued: 0. Flags: name repeated in this environment (W04). See question 9.
Test
W10 New order to warehouse (copy). Enabled: yes. Owner: Mara. Last run: 2026-10-21 (20 days ago), failed. Queued: 0. Flags: failed at last run. See question 6.
W11 Refund approval request. Enabled: no. Owner: Dev. Last run: 2026-09-15 (56 days ago), succeeded. Queued: 0. Flags: none.
W12 Holiday promo banner switch. Enabled: yes. Owner: Priya (left). Last run: 2026-09-30 (41 days ago), succeeded. Queued: 0. Flags: owner has left. See question 7.
Demo
W13 Gift card balance sync. Enabled: yes. Owner: no owner. Last run: no run recorded (status not stated). Queued: 0. Flags: no owner, no run recorded. See question 8.
W14 Low stock alert. Enabled: no. Owner: Mara. Last run: 2026-05-06 (188 days ago), failed. Queued: 0. Flags: none.

Owner gaps
No owner: W04, W13.
Owner has left: W06, W12 (Priya).
Group named as owner: W08 (integrations team).
Owner not on the people list: none.
Environments with no owner stated: Demo.

Failed at last run (enabled workflows)
W03 Low stock alert, Production, 2026-11-10.
W10 New order to warehouse (copy), Test, 2026-10-21.

Queued runs
W03 Low stock alert: 3 queued.
W08 Carrier tracking update: 12 queued.

Quiet workflows (enabled, last run more than 90 days ago)
W05 Year-end stock count reminder: 326 days. Explained by the note that it runs once a year, in December.
W06 Customer survey send: 269 days. No note.
W09 Wholesale account setup: 131 days. No note.

Data gaps
W13: last run and last run status not stated; owner not stated (shown as no owner above).
W04: owner not stated (shown as no owner above).
Demo: environment owner not stated.

Owners
Mara: 4 (W01, W03, W10, W14). Dev: 4 (W02, W07, W11, W15). Tomas: 2 (W05, W09). Priya (left): 2 (W06, W12). integrations team (group): 1 (W08). No owner: 2 (W04, W13). Total 15.

Questions for the platform owner: 9
1. W03 Low stock alert, failed at last run, queued runs. Production, owned by Mara, enabled. Its last run, on 2026-11-10, failed, and 3 runs are queued. Who is looking at the failure, and who decides whether to investigate or pause it? Is the queue expected?
2. W04 Supplier price file import, no owner, name repeated in this environment. Production, enabled, last ran 2026-11-03 and succeeded. W15 has the same name in Production (owner Dev). Who owns W04? Is it a second copy of W15 or a separate workflow?
3. W06 Customer survey send, owner has left, quiet. Production, enabled. The owner, Priya, is marked as left. It last ran on 2026-02-14, 269 days ago, and succeeded. Who owns it now? What process does it serve, and who can say?
4. W08 Carrier tracking update, group owner, queued runs. Production, enabled. The owner is the integrations team, a group. It last ran on 2026-11-10 and succeeded, and 12 runs are queued. Which person owns it? Who is looking at the queue, and who decides whether to investigate or pause it?
5. W09 Wholesale account setup, quiet. Production, owned by Tomas, enabled. It last ran on 2026-07-02, 131 days ago, and succeeded. What process does it serve, and who can say?
6. W10 New order to warehouse (copy), failed at last run. Test, owned by Mara, enabled. Its last run, on 2026-10-21, failed. Who is looking at the failure, and who decides whether to investigate or pause it?
7. W12 Holiday promo banner switch, owner has left. Test, enabled. The owner, Priya, is marked as left. It last ran on 2026-09-30 and succeeded. Who owns it now?
8. W13 Gift card balance sync, no owner, no run recorded. Demo, enabled. The export has no last run and no run status. Who owns it, and has it run?
9. W15 Supplier price file import, name repeated in this environment. Production, owned by Dev, enabled, last ran 2026-11-04 and succeeded. W04 has the same name and no owner. Is W15 the workflow in use, or is W04? (See question 2.)

Draft for the platform owner. Nothing has been paused, retired, changed or sent, and no owner has been assigned.
```

## What was observed

- **Every required part was produced.** The inventory has all 15 rows once, the three environment lines, every section of the format and 9 questions for 9 flagged workflows. The counts add up: 10, 3 and 2 workflows make 15; 12 enabled and 3 disabled make 15; the owner counts also make 15. Nothing in the run asked the model to stop, and no stop condition applied.
- **The disabled workflows behaved as the rules say.** W07, W11 and W14 are shown with their last status (W14 failed) and carry no flag. The same name in two environments (W02 and W11, W03 and W14) was not flagged. W10, "New order to warehouse (copy)", is not flagged against W01, because the names are not the same.
- **Difference from the published example, content.** After the run the output was compared with the example's output. The flags, counts, days, questions and their order are the same. The wording of the questions differs. The one real difference is the data gaps section: this run also listed the blank owners (W04, W13) there, because the stop conditions say a blank owner is not filled in and is listed under data gaps; the example lists only W13's missing run and status and the Demo owner. Minor differences: this run printed "Queued runs 0 workflows, 0 runs" where the example prints "Queued runs 0"; it put the quoted note on W05's line; and it added a question about the queue to W03 and about who looks at the queue to W08.
- **Facts not in the inputs.** None found in this run's output. In the published example, the questions only restate facts from the inputs. Some of the questions' wording suggests possibilities, such as "a second copy", which the inputs do not say, but each is put as a question.

### Where the instructions were ambiguous, or the template and its instruction block disagree

1. **Blank owner and the data gaps section.** Step 4 makes a blank owner the flag "no owner". The stop conditions say a blank owner is "not stated" and listed under data gaps. The run did both; the published example did only the first.
2. **Quiet count for a workflow explained by a note.** The environment line asks for "Quiet [n]". The template says an explained quiet workflow is not "counted as flagged", but does not say whether it is counted in this figure. The run counted it (Production: 3), as did the example. The line does not show that one of the three is explained.
3. **Where the no-run-recorded workflow goes.** Acceptance test 10 says it is listed under data gaps. Step 6 and the instruction block do not say so. The run listed it.
4. **The instruction block is shorter than the procedure.** It leaves out: reading true or false as yes or no; a blank queued_runs as a data gap; a last run after the review date as a data gap; and the instruction to write "people list not supplied" and "no notes supplied". It also names the section "Inventory, grouped by environment, in workflow_id order" where the format has "Inventory", and it does not show where "(left)" and "(group)" go in the Owners section. An assistant that follows only the block could miss these.
5. **Exact name match.** "Two workflows with the same name" is not defined as an exact match. A name like "(copy)" is treated as different, which a platform owner may not want. The run read it as exact.
6. **The date after "that is, before".** It is the review date minus the threshold (2026-08-12). The template does not say so, and a last run exactly 90 days back is not quiet. The run worked it out from the words "more than".
7. **Questions with several flags.** The template says one question for each kind of flag but gives no pattern for the repeated-name question, which has no natural owner to ask. The run asked who owns W04 and which of the two is in use.
8. **The Demo environment with no owner** is reported in two places (Environments and Owner gaps) and in data gaps, but is not a flagged workflow and has no question. The template does not say whether it should have one.

### Shortcomings of this trial

- It is one run, by one model, on one invented example with no ambiguous or messy data beyond the blanks above. Most acceptance tests did not arise: no header mismatch, no repeated ID, no environment missing from the list, no request to pause or remove, and no people list missing were tried.
- It does not show how the template behaves in ChatGPT, Copilot or Gemini, or on a real export. It is not a test in a client environment.

### Clarifications made after this run

The recorded output and observations above are unchanged. After the run, the template was clarified in small ways, and these edits have not been run again:

- A blank workflow owner is printed "no owner" and is also listed under data gaps as owner not stated (ambiguity 1). The published example now matches the run on this point.
- The instruction block now carries the rules the procedure has: true or false as yes or no, a blank queued_runs as a data gap, a last run after the review date as a data gap left out of the quiet check, "people list not supplied", "no notes supplied", no matching of a short name to a longer one, a workflow with no run recorded listed under data gaps, and the review date minus the threshold as the quiet date (ambiguity 4, and in part 6). The section is named "Inventory" in both places (ambiguity 4).
- A quiet workflow explained by a note has the note quoted, and the example's questions follow the wording of the procedure.
- Ambiguity 2 is settled in the template: a workflow quiet but explained by a note is still counted in Quiet [n] on its environment line. Ambiguity 5 is settled in part: the same name means exactly the same name, capital letters ignored. Ambiguity 8 is settled: an environment with no owner stated is reported but gets no question. Ambiguity 3 is covered. Ambiguity 7, the question pattern for a repeated name, is left open.
- The example's questions were also trimmed so that none asks more than the procedure's patterns. These edits have not been run again.
