# Workflow inventory: an invented example

*Illustrative example with invented data.* The company, the people, the platform, the workflows and the dates below are all invented. The company is an invented 80-person online retailer whose platform owner reviews its automated workflows once a quarter. Nothing here describes a real organization or a measured result.

## The inputs

### 1. Settings

```
Platform: an invented workflow platform
Review date: 2026-11-10
Quiet threshold: 90 days (quiet means the last run is more than 90 days before the review date)
Platform owner: the person who receives the inventory
```

### 2. Workflow export

```
workflow_id,name,environment,enabled,owner,last_run,last_run_status,queued_runs
W01,New order to warehouse,Production,yes,Mara,2026-11-10,succeeded,0
W02,Refund approval request,Production,yes,Dev,2026-11-09,succeeded,0
W03,Low stock alert,Production,yes,Mara,2026-11-10,failed,3
W04,Supplier price file import,Production,yes,,2026-11-03,succeeded,0
W05,Year-end stock count reminder,Production,yes,Tomas,2025-12-19,succeeded,0
W06,Customer survey send,Production,yes,Priya,2026-02-14,succeeded,0
W07,Old returns form to email,Production,no,Dev,2026-04-30,succeeded,0
W08,Carrier tracking update,Production,yes,integrations team,2026-11-10,succeeded,12
W09,Wholesale account setup,Production,yes,Tomas,2026-07-02,succeeded,0
W10,New order to warehouse (copy),Test,yes,Mara,2026-10-21,failed,0
W11,Refund approval request,Test,no,Dev,2026-09-15,succeeded,0
W12,Holiday promo banner switch,Test,yes,Priya,2026-09-30,succeeded,0
W13,Gift card balance sync,Demo,yes,,,,0
W14,Low stock alert,Demo,no,Mara,2026-05-06,failed,0
W15,Supplier price file import,Production,yes,Dev,2026-11-04,succeeded,0
```

### 3. Environment list

```
environment,purpose,environment_owner
Production,live store and warehouse,Dev
Test,building and checking changes,Mara
Demo,demonstrations for wholesale buyers,
```

### 4. People list

```
name,status
Mara,current
Dev,current
Tomas,current
Priya,left
integrations team,group
```

### 5. Notes

```
- The year-end stock count reminder runs once a year, in December.
```

## The output

**WORKFLOW INVENTORY: an invented workflow platform, reviewed 2026-11-10**

- **For:** Platform owner. Quiet means a last run more than 90 days before 2026-11-10, that is, before 2026-08-12.
- **Prepared:** From the workflow export (15 rows), the environment list (3), the people list (5), the settings and 1 note.
- **Counts:** 15 workflows: 12 enabled, 3 disabled. Workflows flagged: 9. Environments checked: 3 of 3 in the export are on the environment list.

**Environments**

- **Production** (live store and warehouse; owner Dev): 10 workflows, 9 enabled, 1 disabled. Owner gaps 3. Failed at last run 1. Queued runs 2 workflows, 15 runs. Quiet 3.
- **Test** (building and checking changes; owner Mara): 3 workflows, 2 enabled, 1 disabled. Owner gaps 1. Failed at last run 1. Queued runs 0 workflows, 0 runs. Quiet 0.
- **Demo** (demonstrations for wholesale buyers; owner not stated): 2 workflows, 1 enabled, 1 disabled. Owner gaps 1. Failed at last run 0. Queued runs 0 workflows, 0 runs. Quiet 0.

**Inventory**

Production

- **W01** New order to warehouse. Enabled: yes. Owner: Mara. Last run: 2026-11-10 (0 days ago), succeeded. Queued: 0. Flags: none.
- **W02** Refund approval request. Enabled: yes. Owner: Dev. Last run: 2026-11-09 (1 day ago), succeeded. Queued: 0. Flags: none.
- **W03** Low stock alert. Enabled: yes. Owner: Mara. Last run: 2026-11-10 (0 days ago), failed. Queued: 3. Flags: failed at last run, queued runs. See question 1.
- **W04** Supplier price file import. Enabled: yes. Owner: no owner. Last run: 2026-11-03 (7 days ago), succeeded. Queued: 0. Flags: no owner, name repeated in this environment (W15). See question 2.
- **W05** Year-end stock count reminder. Enabled: yes. Owner: Tomas. Last run: 2025-12-19 (326 days ago), succeeded. Queued: 0. Flags: none. Quiet, explained by a note: "The year-end stock count reminder runs once a year, in December."
- **W06** Customer survey send. Enabled: yes. Owner: Priya (left). Last run: 2026-02-14 (269 days ago), succeeded. Queued: 0. Flags: owner has left, quiet. See question 3.
- **W07** Old returns form to email. Enabled: no. Owner: Dev. Last run: 2026-04-30 (194 days ago), succeeded. Queued: 0. Flags: none.
- **W08** Carrier tracking update. Enabled: yes. Owner: integrations team (group). Last run: 2026-11-10 (0 days ago), succeeded. Queued: 12. Flags: group owner, queued runs. See question 4.
- **W09** Wholesale account setup. Enabled: yes. Owner: Tomas. Last run: 2026-07-02 (131 days ago), succeeded. Queued: 0. Flags: quiet. See question 5.
- **W15** Supplier price file import. Enabled: yes. Owner: Dev. Last run: 2026-11-04 (6 days ago), succeeded. Queued: 0. Flags: name repeated in this environment (W04). See question 9.

Test

- **W10** New order to warehouse (copy). Enabled: yes. Owner: Mara. Last run: 2026-10-21 (20 days ago), failed. Queued: 0. Flags: failed at last run. See question 6.
- **W11** Refund approval request. Enabled: no. Owner: Dev. Last run: 2026-09-15 (56 days ago), succeeded. Queued: 0. Flags: none.
- **W12** Holiday promo banner switch. Enabled: yes. Owner: Priya (left). Last run: 2026-09-30 (41 days ago), succeeded. Queued: 0. Flags: owner has left. See question 7.

Demo

- **W13** Gift card balance sync. Enabled: yes. Owner: no owner. Last run: no run recorded. Queued: 0. Flags: no owner, no run recorded. See question 8.
- **W14** Low stock alert. Enabled: no. Owner: Mara. Last run: 2026-05-06 (188 days ago), failed. Queued: 0. Flags: none.

**Owner gaps**

- No owner: W04, W13.
- Owner has left: W06 and W12 (Priya).
- Group named as owner: W08 (integrations team).
- Owner not on the people list: none.
- Environments with no owner stated: Demo.

**Failed at last run (enabled workflows)**

- W03 Low stock alert, Production, 2026-11-10.
- W10 New order to warehouse (copy), Test, 2026-10-21.

**Queued runs**

- W03 Low stock alert: 3 queued.
- W08 Carrier tracking update: 12 queued.

**Quiet workflows (enabled, last run more than 90 days ago)**

- W05 Year-end stock count reminder: 326 days. Explained by the note: "The year-end stock count reminder runs once a year, in December."
- W06 Customer survey send: 269 days. No note.
- W09 Wholesale account setup: 131 days. No note.

**Data gaps**

- W04: owner not stated (shown as no owner).
- W13: owner not stated (shown as no owner); no last run and no run status in the export.
- Demo: no environment owner stated.

**Owners**

- Mara: 4 (W01, W03, W10, W14). Dev: 4 (W02, W07, W11, W15). Tomas: 2 (W05, W09). Priya, left: 2 (W06, W12). integrations team, group: 1 (W08). No owner: 2 (W04, W13). Total 15.

**Questions for the platform owner: 9**

1. **W03 Low stock alert, failed at last run, queued runs.** In Production, owned by Mara. It failed at its last run on 2026-11-10 and 3 runs are queued. Who is looking at the failure and the queue, and who decides whether to investigate or pause it?
2. **W04 Supplier price file import, no owner, name repeated in this environment.** It last ran on 2026-11-03 and succeeded. W15 has the same name in Production, owned by Dev, and last ran on 2026-11-04. Who owns W04?
3. **W06 Customer survey send, owner has left, quiet.** Its owner, Priya, is marked as left. It last ran on 2026-02-14, 269 days ago, and succeeded. Who owns it now? What process does it serve, and who can say?
4. **W08 Carrier tracking update, group owner, queued runs.** The owner is the integrations team, a group. 12 runs are queued although it ran on 2026-11-10. Which person owns it? Who is looking at it, and who decides whether to investigate or pause it?
5. **W09 Wholesale account setup, quiet.** Owned by Tomas. It last ran on 2026-07-02, 131 days ago, and succeeded. What process does it serve, and who can say?
6. **W10 New order to warehouse (copy), failed at last run.** In Test, owned by Mara. It failed at its last run on 2026-10-21. Who is looking at the failure, and who decides whether to investigate or pause it?
7. **W12 Holiday promo banner switch, owner has left.** In Test and enabled. Its owner, Priya, is marked as left. It last ran on 2026-09-30. Who owns it now?
8. **W13 Gift card balance sync, no owner, no run recorded.** In Demo and enabled. The export shows no last run and no run status. Who owns it, and has it ever run?
9. **W15 Supplier price file import, name repeated in this environment.** Owned by Dev. W04 in Production has the same name and no owner. See question 2.

Draft for the platform owner. Nothing has been paused, retired, changed or sent, and no owner has been assigned.
