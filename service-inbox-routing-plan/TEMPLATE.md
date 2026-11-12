# Service inbox routing plan

Workflow template, version 0.1.0.

## Purpose

Turn an approved list of service addresses and the company's current mail settings into one routing plan for a new service inbox: where each address leads today, the queue it should reach, who owns that queue, the change the administrator would need to consider, the checks to run before activation, and a numbered register of wrong-address risks, loop risks, unconfirmed queue owners and other gaps. The assistant prepares; it creates or changes no address, mailbox, rule or setting, sends no test message, and never fills a gap with a guess.

## When to use it and when not to

Use it when a new service inbox needs a routing plan, after a named person has approved the addresses. Run it again whenever the approved list, a queue owner or the current settings change.

Do not use it:

- to decide which addresses the company should have, or to approve them; a person does that first;
- to sort or answer the mail that arrives; that is inbox triage;
- to set reply or resolution targets; that is the support service level definition;
- to sort tickets that already exist; that is support ticket triage;
- to change a platform, switch anything on, or run a test; the administrator and the service owner do those.

## Roles

- **Runs it:** the service owner, or the person helping them.
- **Approves any configuration, supplies the current settings and makes every change:** the systems administrator.
- **Accepts the routing behaviour before activation, and approves addresses:** the service owner.
- **Confirms ownership of a queue:** the owner named for that queue.

## Inputs

1. **Plan settings,** as `name: value` lines. Required: `Business`, `Service`, `Service owner`, `Administrator`, `As-of date` (YYYY-MM-DD) and `Company domains` (separated by semicolons). Optional: `Prepared for`, `Planned activation date` and `Automated mail handling`, one line saying what the system does with out-of-office replies and bounces. If a required setting is missing, stop and ask.
2. **Approved addresses** (addresses.csv), with these headers: `address`, `purpose`, `approved_by`, `approved_date`, `intended_queue`, `auto_reply`. `auto_reply` is `yes` or `no`. A row with `approved_by` or `approved_date` blank is not approved. If the file is missing or has no rows, stop. If a header does not match, stop and ask which column is which; never guess.
3. **Current settings** (current_settings.csv), with these headers: `name`, `kind`, `delivers_to`, `status`. `kind` is as the company's system names it, such as `shared mailbox`, `alias`, `forward` or `personal mailbox`. `delivers_to` holds a queue name or addresses separated by semicolons, and is blank for a mailbox where mail stays. If the file is missing, say that today's paths are not known, plan the intended routes only and raise a gap. If a header does not match, stop and ask.
4. **Queues** (queues.csv), with these headers: `queue`, `owner`, `owner_confirmed`, `hours`, `backup_owner`. `owner_confirmed` is `yes` only when the owner has said so; any other value, or blank, means not confirmed. If the file is missing, every queue is a gap. If a header does not match, stop and ask.
5. **Test scenarios** (scenarios.csv), optional, with these headers: `scenario_id`, `sent_to`, `sender_kind`, `description`, `expected_queue`. If a header does not match, stop and ask.

The assistant works from the settings, files and notes the person supplies. It needs no connection to a mail system or help desk, and never asks for a password, a login code or a key; if one is pasted in, it does not copy it into the plan and tells the person to remove it.

## The procedure

1. **Check the inputs.** Compare addresses by their text after trimming spaces and ignoring case. Stop if an address repeats in the approved list or in the current settings. A row whose approval is blank is listed under `Not approved, left out`, gets no block and no checks, and is otherwise ignored.
2. **Read the queues.** For each approved address, find its `intended_queue` in the queues file by name, ignoring case. A blank `intended_queue` or a queue not in the file is an other gap, and the proposed routing then names the queue as written, or says `no queue named`.
3. **Follow today's path.** Start at the address and find it in the current settings.
   - Not found: `not set up`.
   - Found with a blank `delivers_to`: if the kind is `personal mailbox`, the path ends at a personal mailbox; otherwise it ends with no destination.
   - Found with a `delivers_to`: take each item in turn. If it is a queue name, the path reaches that queue and stops. If it is a name already on the path, the path loops back and stops. If it is on a company domain and in the settings, follow it. If it is on a company domain and not in the settings, say it points to a name that is not in the current settings. If it is outside the company domains, say the path leaves the company there and that what happens beyond is not visible.
   - Stop after eight steps and say the path does not end within eight steps.
   Print the path with each name joined by `->`. An address matches the plan today only when every branch reaches its intended queue, passes through no address that is missing from the approved list, and the plan has no other reason to expect a different result.
4. **Propose the routing.** Print `[address] -> [intended queue]`. Then print one line headed `Change from today`: create the address and deliver it to the queue if it is not set up; replace the delivery that goes elsewhere; remove the step that loops; or `none: today already matches`. Where an address both loops and delivers elsewhere, one line may combine the replacement and the removal. This is a proposal for the administrator. The assistant never carries it out.
5. **Show the queue.** Give the queue's owner and whether the owner is confirmed, its hours and its backup (`none named` if blank), and the auto-reply value of the address. A blank `auto_reply` is shown as `not stated` and is an other gap.
6. **Raise the risks.** Raise one risk per rule per address (rule e once for the plan), and number them in this order: wrong-address risks (rules a to c) in the order of the approved list, then loop risks (rules d to f), then unconfirmed queue owners, then other gaps.
   - **a. Look-alike address.** Reduce the part before the @ of each address on a company domain to lower case with hyphens, dots and underscores removed and one final `s` removed. Another approved address or an address in the current settings, other than the address itself, is a look-alike when its reduced form is the same, or differs by one letter added, removed or changed, or by two neighbouring letters swapped. Only compare forms of five letters or more. Name the look-alike, where it delivers today and which queue it reaches.
   - **b. Ends elsewhere.** Today's path ends at a personal mailbox, a queue other than the intended one, no destination, a name not in the settings, or a point outside the company. Not raised when the address is not set up or the path loops (rule d).
   - **c. Passes through an unapproved address.** An address in the middle of today's path, not at its end, is not on the approved list. Name it.
   - **d. Loop.** Today's path returns to a name it has already passed through. Give the chain. If the address's `auto_reply` is `yes`, say so.
   - **e. Automatic replies with no stated handling.** `Automated mail handling` is blank and at least one planned address has `auto_reply` `yes` or `not stated`. Raise one risk for the plan, naming those addresses.
   - **f. Path leaves the company.** Today's path leaves the company domains. A forward back cannot be ruled out because what happens beyond is not visible.
   - **Unconfirmed queue owner.** A queue that a planned address is meant to reach has a blank owner, or `owner_confirmed` is not `yes`. Raise one risk per queue and note a missing backup.
   - **Other gaps.** The blank or unlisted queues, the blank `auto_reply` values and a missing current-settings or queues file, each once.
   Each risk gives where it is, what is wrong, what would resolve it and who can supply that. In each address block, `Risks` lists the numbers of every risk that concerns that address, including the unconfirmed-owner risk for the queue it reaches (so one queue risk can appear in several blocks) and rule e where it names the address; the register itself holds each risk once. Who can supply is the service owner for wrong-address rules a and c, loop rule e, unconfirmed queue owners and other gaps, and the administrator for wrong-address rule b and loop rules d and f. The role is named from the inputs.
7. **Prepare the checks.** For each planned address prepare, in this order: a plain message from an outside sender; an automatic out-of-office message from an outside sender; and, only where the address has a wrong-address or loop risk, one risk check naming those risks. The expected result of the plain message is the intended queue and, by `auto_reply`, whether one auto-reply goes to the sender (`not stated` stays `not stated`). The expected result of the automatic message is the `Automated mail handling` line word for word, or `not stated` if blank. A risk check sends a plain message from an outside sender, to the look-alike address for rule a and to the planned address for any other risk. A risk check for a look-alike expects whatever the service owner accepts, and says where it reaches today. A risk check for any other risk expects the intended queue once, with no delivery to the place the risk names (the unapproved address, the personal mailbox or the destination outside the company). Where a loop is present the check says: run only after the loop is removed. Number the checks V1 onward in the order of the blocks.
8. **Compare the supplied scenarios.** For each, if `sent_to` is not a planned address, print `Outside the approved list: no routing is planned for it` and say to add the address or drop the scenario. Otherwise print the expected queue, the planned queue and `agrees` or `differs`, and what happens today in a few words.
9. **Close.** Count the addresses, those matching today, the risks by kind and the checks. List every queue in the queues file, in file order, with the planned addresses that reach it or `no address in this plan`, then every other name in the current settings with why it is listed: on the path of a planned address, a look-alike, or not part of this plan. State the two decisions that belong to people. State that nothing has been created, changed or sent, end with the trace line and return the plan to the service owner only. In the checks line and the next step, where the administrator or the service owner is given as a role, write "the" before it ("after the Systems administrator has made the change"); before a person's name, do not.

## Exceptions and stop conditions

- **A required setting is missing, or a file is missing as described:** stop and ask.
- **A header does not match the default:** stop and ask which column is which.
- **An address repeats:** stop and report which.
- **A row is not approved:** leave it out and list it; do not plan around it.
- **A queue or address named in one file is not in another:** raise a gap; do not stop.
- **A path cannot be followed past an outside address:** say so and raise the loop risk (rule f), with the wrong-address risk for rule b; do not guess.
- **A password, login code or key is pasted in:** do not copy it; ask the person to remove it.
- **Asked to create, change, delete or test an address, forward, alias, rule or setting, switch the inbox on, send a test message, fill a gap with a plausible value, judge a mail-filter or security decision, or approve the plan:** decline; the administrator approves configuration and the service owner accepts the behaviour.

## Output format

```
SERVICE INBOX ROUTING PLAN: [service], [business]

For: [prepared for, or service owner] (service owner). Administrator: [administrator]. As of [date]. Planned activation: [date, or not stated].

SUMMARY
Addresses planned: [n] ([n] not set up, [n] set up differently, [n] matching today).
Not approved, left out: [addresses, or none].
Open items: [n] ([n] wrong-address risks, [n] loop risks, [n] unconfirmed queue owners, [n] other gaps).
Checks: [n] prepared; [n] supplied ([n] compared with the plan, [n] outside the approved list, or none supplied).

ADDRESSES

[address]
Purpose: [purpose]. Approved by [approver], [date].
Queue: [queue]. Owner: [owner] ([confirmed or not confirmed]). Hours: [hours]. Backup: [backup or none named].
Auto-reply: [yes, no or not stated]
Today: [path, or not set up, or current settings not supplied].
Proposed routing: [address] -> [queue]
Change from today: [one line, or none: today already matches].
Risks: [numbers, or none]
Checks: [V numbers, or none]

[repeat for every planned address in the order of the approved list]

QUEUES
[queue]: owner [owner] ([confirmed or not confirmed]); hours [hours]; backup [backup or none named]. Reached by: [addresses, or no address in this plan].

OTHER ADDRESSES IN THE CURRENT SETTINGS
[name] ([kind]) -> [where it delivers, or ends there]. [Why listed.]
[or: None.]

CHECKS TO RUN BEFORE ACTIVATION
Run each check only after [administrator] has made the change shown for its address and [service owner] has accepted the behaviour. The plan sends nothing.

Supplied by the service owner:
[scenario_id]: [sent_to], [sender_kind]. Expected [queue]. Plan: [queue] ([agrees or differs]). Today: [short result].
[or: Outside the approved list: no routing is planned for it. Add the address to the approved list or drop the scenario.]
[or: None supplied.]

Prepared by the plan:
V[n]: [address]. [What is sent]. Expected: [result].

RISKS AND GAPS

Wrong-address risks
[n]. [Address]: [what is wrong]. To resolve: [what is needed]. Who can supply: [role].
[or: None.]

Loop risks
[n]. [Address]: [what is wrong]. To resolve: [what is needed]. Who can supply: [role].
[or: None.]

Unconfirmed queue owners
[n]. [Queue]: [what is wrong]. To resolve: [what is needed]. Who can supply: [role].
[or: None.]

Other gaps
[n]. [Where]: [what is missing]. To resolve: [what is needed]. Who can supply: [role or not stated].
[or: None.]

Next step: [administrator] approves any configuration. [Service owner] accepts the routing behaviour before activation on [date, or the planned date once set]. No address, mailbox, rule or setting has been created, changed or connected, and no test message has been sent.

Every path and value traces to the plan settings for [service] and the approved addresses, current settings, queues and scenarios supplied. The plan changes nothing and sends nothing.
```

## Reviewer checklist

1. Every path follows the current settings exactly, with no step added or skipped. (Administrator)
2. Every address in the plan is on the approved list with an approver and a date. (Service owner)
3. Every queue name, owner, confirmation and backup is as supplied. (Service owner)
4. Every risk is raised once per rule per address, numbered in the order given, with who can supply. (Administrator)
5. Every look-alike named really matches the rule, and no real address has been mistaken for one. (Administrator)
6. Every check has an expected result that follows from the inputs, and no check is marked as run. (Service owner)
7. The counts in the summary agree with the blocks and the register. (Service owner)
8. The plan states that nothing was created, changed or sent, and recommends no mail-filter or security setting. (Administrator)

## Acceptance tests

Proposed tests. None has been run.

1. **Normal run.** The invented example in the public folder. Expected: three address blocks, one not set up, two set up differently, none matching; five open items (three wrong-address, one loop, one unconfirmed owner); nine prepared checks; four supplied, three agreeing with the plan and one outside the approved list.
2. **Header mismatch.** The queues file names a column `lead` in place of `owner`. Expected: stops and asks which column is which.
3. **Repeated address.** The approved list holds the same address twice, once in capitals. Expected: stops and reports which.
4. **Not approved.** One approved-list row has a blank `approved_date`. Expected: listed under `Not approved, left out`; no block, no checks.
5. **Forward leaving the company.** An address forwards to a name on another domain. Expected: the path stops there with the note that what follows is not visible, a loop risk for rule f and a wrong-address risk for rule b.
6. **No stated handling of automatic messages.** `Automated mail handling` is blank and one address has `auto_reply` `yes`. Expected: one loop risk naming the address, and the automatic-message check shows `not stated`.
7. **Queue not in the file.** An address names a queue absent from the queues file. Expected: an other gap; the routing line still names the queue as written; the block shows no owner.
8. **Asked to configure or test.** "Set up the forward" or "send a test message to each address." Expected: declines both; the administrator and the service owner decide.

## Instructions for the AI assistant

```
You prepare a service inbox routing plan for the service owner from an
approved list of addresses and the company's current settings. You never
create, change, delete or test an address, mailbox, forward, alias, rule or
setting, you never send a message, and you never fill a gap with a guess.
The systems administrator approves any configuration; the service owner
accepts the routing behaviour before activation. Never ask for a password,
a login code or a key.

The user will supply: plan settings (name: value lines); approved
addresses; current settings; queues; optionally test scenarios. Required
settings: Business, Service, Service owner, Administrator, As-of date and
Company domains. If one is missing, stop and ask. If a file header does not
match the headers below, stop and ask which column is which. Stop if an
address repeats in the approved list or in the current settings
(compared after trimming spaces and ignoring case). Headers: addresses: address, purpose, approved_by,
approved_date, intended_queue, auto_reply. Current settings: name, kind,
delivers_to, status. Queues: queue, owner, owner_confirmed, hours,
backup_owner. Scenarios: scenario_id, sent_to, sender_kind, description,
expected_queue.

1. Approval: a row with approved_by or approved_date blank is listed as not
   approved and left out of everything else.
2. Path: start at each approved address and follow the current settings.
   A found name with a blank delivers_to ends at a personal mailbox if
   its kind is personal mailbox, otherwise with no destination.
   A name that is a queue ends the path there. A name already on the path
   is a loop. A name outside the company domains ends what you can see.
   A name on a company domain that is not in the settings is reported as
   such. Stop after eight steps. Print the path with "->".
3. Proposal: print the address -> intended queue, and one line headed
   "Change from today" saying what the administrator would need to change
   (create the address, replace a delivery that goes elsewhere, remove a
   step that loops; two of these may share one line), or "none: today
   already matches". Show the queue's owner, whether confirmed, hours and
   backup ("none named" if blank), and the address's auto-reply value.
   In each address block, "Risks" lists every risk that concerns the
   address, including the unconfirmed-owner risk for its queue and the
   automatic-replies risk where it names the address.
4. Risks, one per rule per address (automatic replies with no stated
   handling once for the plan), numbered in this order: look-alike
   address, ends elsewhere, passes through an unapproved address (one in
   the middle of the path, not at its end, and not on the approved list); then
   loop, automatic replies with no stated handling, path leaves the
   company; then unconfirmed queue owners (owner_confirmed other than
   "yes"); then other gaps. Look-alike test: take the part before the @ of
   each address on a company domain, lower case it, remove hyphens, dots,
   underscores and one final "s"; another approved address or a name in the
   current settings, other than the address itself, is a look-alike if the
   reduced form is the same or differs by one letter added, removed or
   changed or by two neighbouring letters swapped; compare only forms of
   five letters or more. Ends elsewhere (personal mailbox, other queue, no
   destination, name not in the settings, outside the company) is not
   raised when the address is not set up or loops. A path that leaves the
   company is both a loop risk and an ends-elsewhere risk, because what
   follows is not visible. Give where, what is wrong, what resolves it and
   who can supply it, using only roles named in the inputs: the service
   owner for look-alike, passes through an unapproved address, automatic
   replies, unconfirmed queue owners and other gaps; the administrator
   for ends elsewhere, loop and path leaves the company.
5. Checks: for each planned address a plain message from an outside
   sender, an automatic out-of-office message from an outside sender and,
   if it has a wrong-address or loop risk, one risk check. Expected results
   follow from the inputs only: the plain message expects the intended
   queue and the auto-reply value, the automatic message expects the
   "Automated mail handling" line word for word or "not stated", a risk
   check sends a plain message (to the look-alike for a look-alike, which
   expects whatever the service owner accepts; otherwise to the planned
   address, expecting the intended queue once and no delivery to the place
   the risk names). Number them V1 onward. Never say a check has been run.
   For a loop, say to run it only after the loop is removed.
6. Compare each supplied scenario with the plan; one whose address is not
   planned is outside the approved list. List every queue in the queues
   file, in file order, with the addresses that reach it or "no address in
   this plan", and every other name in the current settings with why it is
   listed.
7. Use the output format exactly. Print "None." for an empty section. End
   with the next step and the trace line. Where the administrator or
   service owner is given as a role, write "the" before it in the checks
   line and the next step.

Do not judge a mail filter, a security setting or a targeting choice, and
do not recommend which address the company should have. If asked to
create, change or test anything, send a message, switch the inbox on or
approve the plan, decline; a person decides.
```

## What to customize

- Your company domains and the words your system uses for each kind of address.
- The names of your queues, their owners, hours and backups.
- The one line saying what your system does with out-of-office replies and bounces.
- Who is the systems administrator and who is the service owner for each inbox.
- The scenarios you always run before activation.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried once on its invented example in Claude on 10 November 2026, on the wording before the review changes of the same day; the run was not blind and the record is published beside it (`public/trial.md`). Not yet tested in a client environment.
