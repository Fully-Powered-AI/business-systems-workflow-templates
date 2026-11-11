# Service inbox routing plan: tried once on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example in `public/example.md` (Client N, an invented online kitchenware retailer, with addresses on the reserved example domain). No client data was used. The five inputs are the plan settings, addresses.csv, current_settings.csv, queues.csv and scenarios.csv, exactly as printed in that example. The assistant followed the fenced instruction block and the output format in `member/template.md`, with the full procedure in the template as its reference.

One thing to know about how this run was done: the run was set up so that the example's output would be read only after the plan was written. In practice the whole example file, output included, was printed on screen in the same step as the inputs, so the output was seen before the plan below was produced. The plan below was still built rule by rule from the template, and the differences listed afterwards are real ones, but this run is a weaker witness than a run that never saw the answer. A later trial should be given the inputs alone.

## What came out

```
SERVICE INBOX ROUTING PLAN: Returns inbox, Client N

For: Customer care manager (service owner). Administrator: Systems administrator. As of 2026-11-10. Planned activation: 2026-11-23.

SUMMARY
Addresses planned: 3 (1 not set up, 2 set up differently, 0 matching today).
Not approved, left out: none.
Open items: 5 (3 wrong-address risks, 1 loop risk, 1 unconfirmed queue owner, 0 other gaps).
Checks: 9 prepared; 4 supplied (3 compared with the plan, 1 outside the approved list).

ADDRESSES

returns@clientn.example
Purpose: Customers asking to return an order. Approved by Customer care manager, 2026-11-04.
Queue: Returns. Owner: Returns coordinator (confirmed). Hours: Mon-Fri 09:00-17:00. Backup: Customer care manager.
Auto-reply: yes
Today: not set up.
Proposed routing: returns@clientn.example -> Returns
Change from today: create the address and deliver it to Returns.
Risks: 1
Checks: V1 to V3

exchanges@clientn.example
Purpose: Customers asking to swap an item. Approved by Customer care manager, 2026-11-04.
Queue: Returns. Owner: Returns coordinator (confirmed). Hours: Mon-Fri 09:00-17:00. Backup: Customer care manager.
Auto-reply: no
Today: exchanges@clientn.example -> priya@clientn.example (personal mailbox, ends there).
Proposed routing: exchanges@clientn.example -> Returns
Change from today: replace the delivery to priya@clientn.example with delivery to Returns.
Risks: 2
Checks: V4 to V6

refunds@clientn.example
Purpose: Customers asking when a refund will arrive. Approved by Customer care manager, 2026-11-04.
Queue: Billing queries. Owner: Accounts receivable clerk (not confirmed). Hours: Mon-Fri 09:00-17:00. Backup: none named.
Auto-reply: yes
Today: refunds@clientn.example -> finance-queue@clientn.example -> refunds@clientn.example (loops back).
Proposed routing: refunds@clientn.example -> Billing queries
Change from today: replace the delivery to finance-queue@clientn.example with delivery to Billing queries, which also removes the step that loops (finance-queue@clientn.example back to refunds@clientn.example).
Risks: 3, 4
Checks: V7 to V9

QUEUES
Returns: owner Returns coordinator (confirmed); hours Mon-Fri 09:00-17:00; backup Customer care manager. Reached by: returns@clientn.example, exchanges@clientn.example.
Billing queries: owner Accounts receivable clerk (not confirmed); hours Mon-Fri 09:00-17:00; backup none named. Reached by: refunds@clientn.example.
General: owner Customer care manager (confirmed); hours Mon-Fri 09:00-17:00; backup Returns coordinator. Reached by: no address in this plan.

OTHER ADDRESSES IN THE CURRENT SETTINGS
care@clientn.example (shared mailbox) -> General. Not part of this plan.
return@clientn.example (alias) -> care@clientn.example -> General. Look-alike of returns@clientn.example (risk 1).
priya@clientn.example (personal mailbox), ends there. On the path of exchanges@clientn.example (risk 2).
finance-queue@clientn.example (forward) -> refunds@clientn.example. On the path of refunds@clientn.example (risks 3 and 4).

CHECKS TO RUN BEFORE ACTIVATION
Run each check only after Systems administrator has made the change shown for its address and Customer care manager has accepted the behaviour. The plan sends nothing.

Supplied by the service owner:
T1: returns@clientn.example, outside customer. Expected Returns. Plan: Returns (agrees). Today: not set up.
T2: exchanges@clientn.example, outside customer. Expected Returns. Plan: Returns (agrees). Today: ends at the personal mailbox priya@clientn.example.
T3: refunds@clientn.example, outside customer. Expected Billing queries. Plan: Billing queries (agrees). Today: loops back to refunds@clientn.example.
T4: support@clientn.example, outside customer. Outside the approved list: no routing is planned for it. Add the address to the approved list or drop the scenario.

Prepared by the plan:
V1: returns@clientn.example. A plain message from an outside sender. Expected: lands in Returns; one auto-reply goes to the sender.
V2: returns@clientn.example. An automatic out-of-office message from an outside sender. Expected: Out-of-office replies are discarded; bounces go to the Returns queue.
V3: returns@clientn.example. Risk check for risk 1: a plain message to return@clientn.example from an outside sender. Expected: whatever the service owner accepts for that address; today it reaches General.
V4: exchanges@clientn.example. A plain message from an outside sender. Expected: lands in Returns; no auto-reply.
V5: exchanges@clientn.example. An automatic out-of-office message from an outside sender. Expected: Out-of-office replies are discarded; bounces go to the Returns queue.
V6: exchanges@clientn.example. Risk check for risk 2: a plain message from an outside sender. Expected: lands once in Returns; no delivery to priya@clientn.example.
V7: refunds@clientn.example. A plain message from an outside sender. Expected: lands in Billing queries; one auto-reply goes to the sender.
V8: refunds@clientn.example. An automatic out-of-office message from an outside sender. Expected: Out-of-office replies are discarded; bounces go to the Returns queue.
V9: refunds@clientn.example. Risk check for risks 3 and 4: a plain message from an outside sender. Run only after the loop is removed. Expected: lands once in Billing queries; no delivery to finance-queue@clientn.example.

RISKS AND GAPS

Wrong-address risks
1. returns@clientn.example: return@clientn.example is in the current settings and reads almost the same (the final "s" differs). Today it delivers to General through care@clientn.example. To resolve: a decision on whether return@clientn.example stays, is redirected or is retired. Who can supply: Customer care manager.
2. exchanges@clientn.example: today it ends at the personal mailbox priya@clientn.example, not at the intended queue Returns. To resolve: the delivery is changed once approved. Who can supply: Systems administrator.
3. refunds@clientn.example: the path passes through finance-queue@clientn.example, which is not on the approved list. To resolve: approve that address, or remove it from the path. Who can supply: Customer care manager.

Loop risks
4. refunds@clientn.example: the path returns to refunds@clientn.example (refunds@clientn.example -> finance-queue@clientn.example -> refunds@clientn.example), and auto-reply is yes for this address. To resolve: one of the two forwards is removed. Who can supply: Systems administrator.

Unconfirmed queue owners
5. Billing queries: owner Accounts receivable clerk has not confirmed, and no backup is named. To resolve: the owner confirms and a backup is named. Who can supply: Customer care manager.

Other gaps
None.

Next step: Systems administrator approves any configuration. Customer care manager accepts the routing behaviour before activation on 2026-11-23. No address, mailbox, rule or setting has been created, changed or connected, and no test message has been sent.

Every path and value traces to the plan settings for Returns inbox and the approved addresses, current settings, queues and scenarios supplied. The plan changes nothing and sends nothing.
```

## What was observed

Every required part was produced, in the order of the output format. Nothing in the run called for a stop: all required settings were present, every header matched, no address repeated and every row was approved. The counts (three addresses, five open items, nine prepared checks, four supplied scenarios) match the template's first acceptance test.

Where the instructions were ambiguous and a choice had to be made:

1. **Look-alike against itself.** exchanges@clientn.example is both on the approved list and in the current settings, so its reduced form matches itself. The rule says "another approved address or an address in the current settings" and does not say that an address is not its own look-alike. It was treated as not one.
2. **Wording of the checks line.** The format says "[administrator] has made the change" and "[service owner] has accepted". Filled with the values as supplied, this reads "Systems administrator has made ... Customer care manager has accepted", without "the". The template does not say whether to add the article.
3. **What a risk check sends.** The procedure says what a risk check expects, but not what it sends. A plain message from an outside sender was used for all three, and for the look-alike one, sent to the look-alike address.
4. **Risk check for a personal mailbox.** The rule expects "no delivery to the unapproved address". Priya's mailbox is not an approved address, so it was read as the unapproved address. The wording was written for a pass-through address and fits this case loosely.
5. **Change from today when two kinds apply.** For refunds@ both "replace the delivery that goes elsewhere" and "remove the step that loops" apply. The template lists them as separate options; one line saying both was written.
6. **The queues list.** Step 9 says to list the queues that planned addresses reach, but the format allows "no address in this plan", which only makes sense if a queue nobody reaches is listed. General was listed with that phrase.
7. **Out-of-list scenario.** The format has no place to say what happens today for a scenario outside the approved list, so none was given.
8. **A period in the example format.** The auto-reply, risk and check wording for the automatic message follows the "word for word" rule, which produces a capital letter mid-sentence ("Expected: Out-of-office replies are discarded; ..."). This is as instructed.

Differences from the published example, after reading it:

- **Checks V7 and V9.** The example adds "(owner not confirmed)" to V7 and "one auto-reply; no repeated deliveries" to V9. The procedure asks for neither, so this run left them out. V9 here expects "no delivery to finance-queue@clientn.example" instead, which is what the rule says.
- **Checks V3 and V6.** Wording differs. V6 in the example says "a plain message after the change" and expects "nothing arrives in priya@"; this run adds "once".
- **Rule 3 risk for refunds@.** Same risk, but the example's "Change from today" and risk text word the fix as the administrator doing it; this run kept to the template's roles.
- **Other addresses.** The example says care@ is "left as it is". The template asks only for why the name is listed, and "left as it is" is a recommendation that is not in the inputs, so this run said "Not part of this plan."
- **Scenario T3.** The example says "Today: loops"; this run says where it loops back to.
- **Forms of words.** The example writes "the administrator" and "the service owner" in the checks line; this run used the supplied names (point 2 above).
- **Risk 3 resolve text and risk 4 path.** Minor wording; same content.
- **The "Risks:" line for refunds@.** The example lists "3, 4, 5"; this run lists "3, 4". The Billing queries owner (risk 5) is a risk of the queue, not of the address block as the template defines it ("Risks: [numbers]"), and the template does not say whether a queue-level risk is listed against each address that reaches it. The example lists it; this run did not. This changes the block, not the register or the counts.

Facts in either output that are not in the inputs:

- In the example: "left as it is" for care@clientn.example (see above); "Customer care manager ran the capability once the three addresses had been approved" and "opening a returns inbox" in its introduction (the settings give the service as Returns inbox, but not who ran it).
- In this run: none found. Every name, date and path traces to the five inputs.

Not shown by this run: any behaviour of the template with a missing file, a mismatched header, a repeated address, an unapproved row, a path that leaves the company, or a blank "Automated mail handling" line. Acceptance tests 2 to 8 were not run here.

After this run, the template and the example were revised (review of the same day), so the example in `public/example.md` no longer matches the example described in the two sections above: its checks V7 and V9, the care@ line and the introduction were changed, and its wording of the automatic out-of-office checks, V3 and the checks line was aligned with the template. The "Risks:" line for refunds@ ("3, 4" in this run, "3, 4, 5" in the earlier example) is now settled by procedure step 6, which lists the unconfirmed-owner risk in every block that reaches the queue. The run above was not repeated on the revised wording.
