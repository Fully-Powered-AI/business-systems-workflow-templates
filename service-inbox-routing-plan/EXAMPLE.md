# Service inbox routing plan: an invented example

*Illustrative example with invented data.* The business, its addresses (on the reserved example domain), the roles, the help desk and every date below are invented. Client N is an invented online kitchenware retailer opening a returns inbox. In this example the service owner is the customer care manager. First come the inputs supplied, in full, then the plan the capability returned.

## The inputs

### 1. Plan settings

```
Business: Client N (an invented online kitchenware retailer)
Service: Returns inbox
Service owner: Customer care manager
Administrator: Systems administrator
Prepared for: Customer care manager
As-of date: 2026-11-10
Planned activation date: 2026-11-23
Company domains: clientn.example
Automated mail handling: Out-of-office replies are discarded; bounces go to the Returns queue
```

### 2. Approved addresses (addresses.csv)

```
address,purpose,approved_by,approved_date,intended_queue,auto_reply
returns@clientn.example,Customers asking to return an order,Customer care manager,2026-11-04,Returns,yes
exchanges@clientn.example,Customers asking to swap an item,Customer care manager,2026-11-04,Returns,no
refunds@clientn.example,Customers asking when a refund will arrive,Customer care manager,2026-11-04,Billing queries,yes
```

### 3. Current settings (current_settings.csv)

```
name,kind,delivers_to,status
care@clientn.example,shared mailbox,General,in use
return@clientn.example,alias,care@clientn.example,in use
exchanges@clientn.example,forward,priya@clientn.example,in use
priya@clientn.example,personal mailbox,,in use
refunds@clientn.example,forward,finance-queue@clientn.example,in use
finance-queue@clientn.example,forward,refunds@clientn.example,in use
```

### 4. Queues (queues.csv)

```
queue,owner,owner_confirmed,hours,backup_owner
Returns,Returns coordinator,yes,Mon-Fri 09:00-17:00,Customer care manager
Billing queries,Accounts receivable clerk,no,Mon-Fri 09:00-17:00,
General,Customer care manager,yes,Mon-Fri 09:00-17:00,Returns coordinator
```

### 5. Test scenarios (scenarios.csv)

```
scenario_id,sent_to,sender_kind,description,expected_queue
T1,returns@clientn.example,outside customer,Customer asks to return a mug,Returns
T2,exchanges@clientn.example,outside customer,Customer asks to swap a size,Returns
T3,refunds@clientn.example,outside customer,Customer asks where a refund is,Billing queries
T4,support@clientn.example,outside customer,Customer writes to an old address,General
```

## The plan

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
Today: exchanges@clientn.example -> priya@clientn.example (personal mailbox). Ends there.
Proposed routing: exchanges@clientn.example -> Returns
Change from today: deliver the address to Returns in place of the forward to priya@clientn.example.
Risks: 2
Checks: V4 to V6

refunds@clientn.example
Purpose: Customers asking when a refund will arrive. Approved by Customer care manager, 2026-11-04.
Queue: Billing queries. Owner: Accounts receivable clerk (not confirmed). Hours: Mon-Fri 09:00-17:00. Backup: none named.
Auto-reply: yes
Today: refunds@clientn.example -> finance-queue@clientn.example -> refunds@clientn.example (loops back).
Proposed routing: refunds@clientn.example -> Billing queries
Change from today: deliver the address to Billing queries in place of the forward to finance-queue@clientn.example; the forward from finance-queue@clientn.example back to this address is the loop.
Risks: 3, 4, 5
Checks: V7 to V9

QUEUES
Returns: owner Returns coordinator (confirmed); hours Mon-Fri 09:00-17:00; backup Customer care manager. Reached by: returns@clientn.example, exchanges@clientn.example.
Billing queries: owner Accounts receivable clerk (not confirmed); hours Mon-Fri 09:00-17:00; backup none named. Reached by: refunds@clientn.example.
General: owner Customer care manager (confirmed); hours Mon-Fri 09:00-17:00; backup Returns coordinator. Reached by: no address in this plan.

OTHER ADDRESSES IN THE CURRENT SETTINGS
care@clientn.example (shared mailbox) -> General. Not part of this plan.
return@clientn.example (alias) -> care@clientn.example -> General. Looks like returns@clientn.example (risk 1).
priya@clientn.example (personal mailbox), ends there. On the path of exchanges@clientn.example (risk 2).
finance-queue@clientn.example (forward) -> refunds@clientn.example. On the path of refunds@clientn.example (risks 3 and 4).

CHECKS TO RUN BEFORE ACTIVATION
Run each check only after the Systems administrator has made the change shown for its address and the Customer care manager has accepted the behaviour. The plan sends nothing.

Supplied by the service owner:
T1: returns@clientn.example, outside customer. Expected Returns. Plan: Returns (agrees). Today: not set up.
T2: exchanges@clientn.example, outside customer. Expected Returns. Plan: Returns (agrees). Today: ends at the personal mailbox priya@clientn.example.
T3: refunds@clientn.example, outside customer. Expected Billing queries. Plan: Billing queries (agrees). Today: loops.
T4: support@clientn.example, outside customer. Outside the approved list: no routing is planned for it. Add the address to the approved list or drop the scenario.

Prepared by the plan:
V1: returns@clientn.example. A plain message from an outside sender. Expected: lands in Returns; one auto-reply goes to the sender.
V2: returns@clientn.example. An automatic out-of-office message from an outside sender. Expected: Out-of-office replies are discarded; bounces go to the Returns queue.
V3: returns@clientn.example. Risk check for risk 1: a plain message to return@clientn.example from an outside sender. Expected: whatever the service owner accepts for that address; today it reaches General.
V4: exchanges@clientn.example. A plain message from an outside sender. Expected: lands in Returns; no auto-reply.
V5: exchanges@clientn.example. An automatic out-of-office message from an outside sender. Expected: Out-of-office replies are discarded; bounces go to the Returns queue.
V6: exchanges@clientn.example. Risk check for risk 2: a plain message after the change. Expected: lands in Returns; nothing arrives in priya@clientn.example.
V7: refunds@clientn.example. A plain message from an outside sender. Expected: lands in Billing queries; one auto-reply goes to the sender.
V8: refunds@clientn.example. An automatic out-of-office message from an outside sender. Expected: Out-of-office replies are discarded; bounces go to the Returns queue.
V9: refunds@clientn.example. Risk check for risks 3 and 4: a plain message. Run only after the loop is removed. Expected: lands once in Billing queries; no delivery to finance-queue@clientn.example.

RISKS AND GAPS

Wrong-address risks
1. returns@clientn.example: return@clientn.example is in use and looks almost the same (the final "s" differs). It delivers to General through care@clientn.example. To resolve: the service owner and administrator decide whether return@clientn.example stays, is redirected or is retired. Who can supply: Customer care manager.
2. exchanges@clientn.example: today it ends at the personal mailbox priya@clientn.example, not at Returns. To resolve: the administrator changes the delivery once approved. Who can supply: Systems administrator.
3. refunds@clientn.example: the path passes through finance-queue@clientn.example, which is not on the approved list. To resolve: the service owner approves it or the administrator removes it from the path. Who can supply: Customer care manager.

Loop risks
4. refunds@clientn.example: the path returns to refunds@clientn.example (refunds@ -> finance-queue@ -> refunds@) and auto-reply is on. To resolve: the administrator removes one forward. Who can supply: Systems administrator.

Unconfirmed queue owners
5. Billing queries: owner Accounts receivable clerk has not confirmed, and no backup is named. To resolve: the owner confirms and a backup is named. Who can supply: Customer care manager.

Other gaps
None.

Next step: The Systems administrator approves any configuration. The Customer care manager accepts the routing behaviour before activation on 2026-11-23. No address, mailbox, rule or setting has been created, changed or connected, and no test message has been sent.

Every path and value traces to the plan settings for Returns inbox and the approved addresses, current settings, queues and scenarios supplied. The plan changes nothing and sends nothing.
```
