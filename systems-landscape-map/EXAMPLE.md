# Systems landscape and data flow map: an invented example

*Illustrative example with invented data.* The company, its systems, the people and every row and note below are invented. The company is called Company R here: a maker of outdoor furniture with about 80 people, selling to retailers and online. Its owners will decide in the spring whether to replace the accounting system, and the operations lead wants the whole picture first. First come the inputs the operations lead supplied, in full, then the map the workflow template returned.

## The inputs

### 1. Settings (typed by the operations lead)

```
Today: 11 November 2026
Company: Company R
Reason: the owners decide in the spring whether to replace the accounting system
System under decision: Accounting system
Map reviewer: Operations lead
Record types: the default list
Previous map: none
```

### 2. Systems list (header is line 1)

```
system,used_for,records_held,record_for,business_owner,administrator
CRM,Retail accounts and the sales pipeline,customers; prices; sales orders,customers,Sales director,Sales coordinator
Accounting system,Invoices and the books,customers; suppliers; invoices; payments received,customers; invoices; payments received,Finance manager,Finance manager
Online shop,Direct sales to consumers,customers; products; prices; sales orders; payments received; stock levels,,E-commerce manager,E-commerce manager
Warehouse system,Stock and dispatch,products; sales orders; stock levels,products; stock levels,Warehouse manager,Warehouse manager
Price list spreadsheet,Wholesale and retail price list,products; prices,prices,,Sales coordinator
Payroll service,Pay runs and staff records,employees,employees,Finance manager,Finance manager
```

### 3. Connections list (header is line 1)

```
from_system,to_system,records,method,frequency,owner
Online shop,Warehouse system,sales orders,automatic,every 15 minutes,E-commerce manager
Warehouse system,Online shop,stock levels,automatic,hourly,E-commerce manager
CRM,Warehouse system,sales orders,re-keyed by hand,daily,Sales coordinator
Warehouse system,Accounting system,sales orders,manual export and import,daily,Finance manager
Online shop,Accounting system,payments received,scheduled file,weekly,
Price list spreadsheet,CRM,prices,re-keyed by hand,when prices change,Sales coordinator
Price list spreadsheet,Online shop,prices,re-keyed by hand,when prices change,E-commerce manager
```

### 4. Interview notes (written up by the operations lead)

```
Finance manager, 3 November 2026:
We go by the accounting system for customer names and addresses, because
invoices are sent from it. When a salesperson changes a customer's address
in the CRM, they email me the change and I retype it in the accounting
system. Suppliers only live in the accounting system.

E-commerce manager, 4 November 2026:
The online shop is the master for product names, descriptions and photos.
The warehouse system only has product codes, sizes and weights.

Sales director, 5 November 2026:
Nobody has really looked after the price list spreadsheet since the last
sales manager left; whoever needs a change makes it. Trade orders are taken
in the CRM, and the sales coordinator types them into the warehouse system
daily.

Warehouse manager, 5 November 2026:
The warehouse system is the truth for stock levels; counts are only ever
changed there. We also keep a returns log in a spreadsheet on the shared
drive.
```

## The map

```
SYSTEMS LANDSCAPE MAP: Company R

For: Operations lead. Prepared 11 November 2026 from the systems list (6 rows), the connections list (7 rows), 4 interview notes, and the settings. Reason: the owners decide in the spring whether to replace the accounting system. System under decision: S2 Accounting system.
Summary: 6 systems. 9 record types: 5 stated, 2 disputed, 0 named in an interview only, 2 none named, 0 not held. 8 flows: 7 from the connections list, 1 from interviews; 4 re-keyed by hand; 1 with no owner. 11 questions. 6 decisions.

1. THE FILES
Header check: both lists have the headers expected.
Systems list: 6 rows (lines 2 to 7). Connections list: 7 rows (lines 2 to 8). Interview notes: Finance manager, 3 November 2026; E-commerce manager, 4 November 2026; Sales director, 5 November 2026; Warehouse manager, 5 November 2026.
Record types: the default list (9): customers; suppliers; products; prices; sales orders; invoices; payments received; stock levels; employees. Values not on the list: none.
Systems named but not listed: 1 (see section 6). Previous map: none.

2. SYSTEMS
ID | System | Used for | Record of truth for | Also holds | Business owner | Administrator | Flows out | Flows in | Flags
S1 | CRM | Retail accounts and the sales pipeline | customers (disputed) | prices; sales orders | Sales director | Sales coordinator | F3, F8 | F6 | none
S2 | Accounting system | Invoices and the books | customers (disputed); invoices; payments received | suppliers | Finance manager | Finance manager | none | F4, F5, F8 | system under decision
S3 | Online shop | Direct sales to consumers | products (disputed) (from an interview) | customers; prices; sales orders; payments received; stock levels | E-commerce manager | E-commerce manager | F1, F5 | F2, F7 | none
S4 | Warehouse system | Stock and dispatch | products (disputed); stock levels | sales orders | Warehouse manager | Warehouse manager | F2, F4 | F1, F3 | none
S5 | Price list spreadsheet | Wholesale and retail price list | prices | products | not stated | Sales coordinator | F6, F7 | none | no business owner
S6 | Payroll service | Pay runs and staff records | employees | none | Finance manager | Finance manager | none | none | none

3. RECORD OF TRUTH BY RECORD TYPE
R1. customers. Status: disputed. Record: named as the record by: S1 CRM (systems list, line 2); S2 Accounting system (systems list, line 3; the Finance manager, 3 November, agrees). Also held in: S3 Online shop. Flows carrying it: F8.
R2. suppliers. Status: none named. Record: none named. Held in: S2 Accounting system. Flows carrying it: none.
R3. products. Status: disputed. Record: named as the record by: S4 Warehouse system (systems list, line 5); S3 Online shop (E-commerce manager, 4 November, for product names, descriptions and photos). Also held in: S5 Price list spreadsheet. Flows carrying it: none.
R4. prices. Status: stated. Record: S5 Price list spreadsheet (systems list, line 6). Also held in: S1 CRM, S3 Online shop. Flows carrying it: F6, F7. Flag: the record's system has no business owner.
R5. sales orders. Status: none named. Record: none named. Held in: S1 CRM, S3 Online shop, S4 Warehouse system. Flows carrying it: F1, F3, F4.
R6. invoices. Status: stated. Record: S2 Accounting system (systems list, line 3). Also held in: none. Flows carrying it: none.
R7. payments received. Status: stated. Record: S2 Accounting system (systems list, line 3). Also held in: S3 Online shop. Flows carrying it: F5.
R8. stock levels. Status: stated. Record: S4 Warehouse system (systems list, line 5; the Warehouse manager, 5 November, agrees). Also held in: S3 Online shop. Flows carrying it: F2.
R9. employees. Status: stated. Record: S6 Payroll service (systems list, line 7). Also held in: none. Flows carrying it: none.

4. DATA FLOWS
F1. S3 Online shop -> S4 Warehouse system. Records: sales orders. Method: automatic. Frequency: every 15 minutes. Owner: E-commerce manager. Source: connections list, line 2. Flags: none.
F2. S4 Warehouse system -> S3 Online shop. Records: stock levels. Method: automatic. Frequency: hourly. Owner: E-commerce manager. Source: connections list, line 3. Flags: none.
F3. S1 CRM -> S4 Warehouse system. Records: sales orders. Method: re-keyed by hand. Frequency: daily. Owner: Sales coordinator. Source: connections list, line 4; also described by the Sales director, 5 November. Flags: re-keyed by hand.
F4. S4 Warehouse system -> S2 Accounting system. Records: sales orders. Method: manual export and import. Frequency: daily. Owner: Finance manager. Source: connections list, line 5. Flags: S2 Accounting system does not list sales orders as held.
F5. S3 Online shop -> S2 Accounting system. Records: payments received. Method: scheduled file. Frequency: weekly. Owner: not stated. Source: connections list, line 6. Flags: no owner.
F6. S5 Price list spreadsheet -> S1 CRM. Records: prices. Method: re-keyed by hand. Frequency: when prices change. Owner: Sales coordinator. Source: connections list, line 7. Flags: re-keyed by hand.
F7. S5 Price list spreadsheet -> S3 Online shop. Records: prices. Method: re-keyed by hand. Frequency: when prices change. Owner: E-commerce manager. Source: connections list, line 8. Flags: re-keyed by hand.
F8. S1 CRM -> S2 Accounting system. Records: customers. Method: re-keyed by hand. Frequency: when an address changes. Owner: Finance manager. Source: interview, Finance manager, 3 November; not confirmed. Flags: re-keyed by hand, from an interview, not confirmed.
Methods: 2 automatic, 1 scheduled file, 1 manual export and import, 4 re-keyed by hand, 0 unknown or unclear.

5. DIAGRAM
Legend: ==> automatic or scheduled file   --> manual export and import
        ..> re-keyed by hand   ??> unknown or unclear   i = from an interview, not confirmed
[S1 CRM]
  ..> S4 Warehouse system  sales orders, daily (F3)
  ..> S2 Accounting system  customers, when an address changes (F8, i)
[S3 Online shop]
  ==> S4 Warehouse system  sales orders, every 15 minutes (F1)
  ==> S2 Accounting system  payments received, weekly (F5)
[S4 Warehouse system]
  ==> S3 Online shop  stock levels, hourly (F2)
  --> S2 Accounting system  sales orders, daily (F4)
[S5 Price list spreadsheet]
  ..> S1 CRM  prices, when prices change (F6)
  ..> S3 Online shop  prices, when prices change (F7)
Receives only: S2 Accounting system
No flows recorded: S6 Payroll service
Not on the systems list: returns log

6. GAPS
Systems missing an owner, administrator or records held, or claiming a type they do not list: S5 Price list spreadsheet: no business owner; Sales director, 5 November: "Nobody has really looked after the price list spreadsheet since the last sales manager left; whoever needs a change makes it."
Systems named but not on the list: returns log (Warehouse manager, 5 November).
Record types with no record named: suppliers (held in S2 Accounting system); sales orders (held in S1 CRM, S3 Online shop, S4 Warehouse system).
Record types held in no listed system: none.
Record types named as the record in an interview only: none.
Record type values not on the list: none.
Flows with no owner: F5.
Flows re-keyed by hand: F3, F6, F7, F8.
Flows with a method or frequency unknown or not stated: none.
Flows carrying a type a system does not list as held: F4 (S2 Accounting system, sales orders).
Copies no flow reaches: customers in S3 Online shop; no flow carries products between S3 Online shop, S4 Warehouse system and S5 Price list spreadsheet.
Flows from interviews, not confirmed: F8.

7. DUPLICATE RECORDS OF TRUTH
D1. customers. Named as the record by: S1 CRM (systems list, line 2); S2 Accounting system (systems list, line 3; Finance manager, 3 November: "We go by the accounting system for customer names and addresses"). Also held in: S3 Online shop. Flows carrying it: F8.
D2. products. Named as the record by: S4 Warehouse system (systems list, line 5); S3 Online shop (E-commerce manager, 4 November: "The online shop is the master for product names, descriptions and photos"). Also held in: S5 Price list spreadsheet. Flows carrying it: none.

8. CHANGES SINCE THE LAST MAP
No previous map supplied; nothing compared.

9. QUESTIONS
E-commerce manager
1. F5 sends payments received from the online shop to the accounting system as a weekly scheduled file (connections list, line 6), and no owner is named. Who runs it?
2. The online shop holds customers (systems list, line 4), but no flow on the map carries customers into or out of it. Do online customers reach the CRM or the accounting system, and if so, how?
E-commerce manager and Warehouse manager
3. Products: the systems list names the warehouse system as the record (line 5), and the E-commerce manager (4 November) says the online shop is the master for product names, descriptions and photos. Which system is the record for products?
4. Products are held in the online shop, the warehouse system and the price list spreadsheet (lines 4, 5 and 6), and no flow on the map carries them between any of the three. How does a new or changed product reach each one? The price list spreadsheet has no business owner, so this question goes to the two owners named.
E-commerce manager, Sales director and Warehouse manager
5. Sales orders are held in the CRM, the online shop and the warehouse system (lines 2, 4 and 5), and none of the three is named as the record for them. Which system is the record for sales orders?
Finance manager
6. Suppliers are held only in the accounting system (line 3), which is not named as the record for them; your note of 3 November says suppliers "only live in the accounting system". Which system, if any, is the record for suppliers?
7. F4 brings sales orders from the warehouse system into the accounting system daily (connections list, line 5), but the systems list does not show the accounting system holding sales orders (line 3). What does it do with them?
Finance manager and Sales director
8. Customers: the systems list names both the CRM (line 2) and the accounting system (line 3) as the record, and the Finance manager (3 November) goes by the accounting system for customer names and addresses. Which system is the record for customers?
Operations lead
9. The price list spreadsheet is the record for prices (line 6) and has no business owner; the Sales director (5 November) says whoever needs a change makes it. Who owns it?
Sales director
10. The Finance manager (3 November) says that when a salesperson changes a customer's address in the CRM, the change is emailed and retyped in the accounting system (F8). Is that how every customer change reaches the accounting system?
Warehouse manager
11. Your note of 5 November mentions a returns log in a spreadsheet on the shared drive. What is it used for, who owns and runs it, and which records does it hold?

10. DECISIONS FOR THE MAP REVIEWER (Operations lead)
1. customers: named as the record by both S1 CRM and S2 Accounting system. Before the decision. Waits on questions 2, 8 and 10. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
2. suppliers: no record named; held only in S2 Accounting system. Before the decision. Waits on question 6. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
3. products: named as the record by both S4 Warehouse system and S3 Online shop. Waits on questions 3 and 4. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
4. sales orders: no record named; held in S1 CRM, S3 Online shop and S4 Warehouse system, and F4 carries them into S2 Accounting system. Before the decision. Waits on questions 5 and 7. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
5. S5 Price list spreadsheet: no business owner, and it is the record for prices. Waits on question 9. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
6. returns log: named by the Warehouse manager but not on the systems list. Waits on question 11. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
People decide every record of truth, owner and next step; this map decides none.

11. NOT CHECKED
Whether the lists are complete or the notes accurate; the fields inside any flow; how data is changed on the way; volumes, errors and timings; access and security; costs and contracts; the returns log, which is not on the systems list. No system was connected to and nothing was changed.

Every entry traces to the systems list, the connections list, the interview notes or the settings supplied on 11 November 2026. This map connects to no system and changes nothing.
```
