# Systems landscape and data flow map: trial on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-11

The inputs are the invented example for this workflow template (Company R, a made-up maker of outdoor furniture). No client data was used. The inputs used are the four in [the example](example.md): the settings, the systems list, the connections list and the four interview notes. The run followed the instruction block and the output format in the template exactly. The example's own output was not read until the run was finished.

## What came out

The run produced all eleven sections, the summary and the closing line. It was not stopped by any header problem, missing file or secret. The full output follows.

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
R1. customers. Status: disputed. Record: named as the record by: S1 CRM (systems list); S2 Accounting system (systems list; Finance manager, 3 November 2026, agrees). Also held in: S3 Online shop. Flows carrying it: F8.
R2. suppliers. Status: none named. Record: none named. Also held in: S2 Accounting system. Flows carrying it: none.
R3. products. Status: disputed. Record: named as the record by: S4 Warehouse system (systems list); S3 Online shop (E-commerce manager, 4 November 2026). Also held in: S5 Price list spreadsheet. Flows carrying it: none.
R4. prices. Status: stated. Record: S5 Price list spreadsheet (systems list). Also held in: S1 CRM, S3 Online shop. Flows carrying it: F6, F7. Flag: the record's system has no business owner.
R5. sales orders. Status: none named. Record: none named. Also held in: S1 CRM, S3 Online shop, S4 Warehouse system. Flows carrying it: F1, F3, F4.
R6. invoices. Status: stated. Record: S2 Accounting system (systems list). Also held in: none. Flows carrying it: none.
R7. payments received. Status: stated. Record: S2 Accounting system (systems list). Also held in: S3 Online shop. Flows carrying it: F5.
R8. stock levels. Status: stated. Record: S4 Warehouse system (systems list; Warehouse manager, 5 November 2026, agrees). Also held in: S3 Online shop. Flows carrying it: F2.
R9. employees. Status: stated. Record: S6 Payroll service (systems list). Also held in: none. Flows carrying it: none.

4. DATA FLOWS
F1. S3 Online shop -> S4 Warehouse system. Records: sales orders. Method: automatic. Frequency: every 15 minutes. Owner: E-commerce manager. Source: connections list, line 2. Flags: none.
F2. S4 Warehouse system -> S3 Online shop. Records: stock levels. Method: automatic. Frequency: hourly. Owner: E-commerce manager. Source: connections list, line 3. Flags: none.
F3. S1 CRM -> S4 Warehouse system. Records: sales orders. Method: re-keyed by hand. Frequency: daily. Owner: Sales coordinator. Source: connections list, line 4; also described by Sales director, 5 November 2026. Flags: re-keyed by hand.
F4. S4 Warehouse system -> S2 Accounting system. Records: sales orders. Method: manual export and import. Frequency: daily. Owner: Finance manager. Source: connections list, line 5. Flags: S2 Accounting system does not list sales orders as held.
F5. S3 Online shop -> S2 Accounting system. Records: payments received. Method: scheduled file. Frequency: weekly. Owner: not stated. Source: connections list, line 6. Flags: no owner.
F6. S5 Price list spreadsheet -> S1 CRM. Records: prices. Method: re-keyed by hand. Frequency: when prices change. Owner: Sales coordinator. Source: connections list, line 7. Flags: re-keyed by hand.
F7. S5 Price list spreadsheet -> S3 Online shop. Records: prices. Method: re-keyed by hand. Frequency: when prices change. Owner: E-commerce manager. Source: connections list, line 8. Flags: re-keyed by hand.
F8. S1 CRM -> S2 Accounting system. Records: customers. Method: re-keyed by hand. Frequency: when a customer's address is changed in the CRM. Owner: Finance manager. Source: interview, Finance manager, 3 November 2026; not confirmed. Flags: re-keyed by hand, from an interview, not confirmed.
Methods: 2 automatic, 1 scheduled file, 1 manual export and import, 4 re-keyed by hand, 0 unknown or unclear.

5. DIAGRAM
Legend: ==> automatic or scheduled file   --> manual export and import
        ..> re-keyed by hand   ??> unknown or unclear   i = from an interview, not confirmed
[S1 CRM]
  ..> S4 Warehouse system  sales orders, daily (F3)
  ..> S2 Accounting system  customers, when a customer's address is changed (F8, i)
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
Not on the systems list: returns log (a spreadsheet on the shared drive)

6. GAPS
Systems missing an owner, administrator or records held, or claiming a type they do not list: S5 Price list spreadsheet: no business owner; Sales director, 5 November 2026: "Nobody has really looked after the price list spreadsheet since the last sales manager left; whoever needs a change makes it."
Systems named but not on the list: returns log (Warehouse manager, 5 November 2026).
Record types with no record named: suppliers (held in S2 Accounting system); sales orders (held in S1 CRM, S3 Online shop, S4 Warehouse system).
Record types held in no listed system: none.
Record types named as the record in an interview only: none.
Record type values not on the list: none.
Flows with no owner: F5.
Flows re-keyed by hand: F3, F6, F7, F8.
Flows with a method or frequency unknown or not stated: none.
Flows carrying a type a system does not list as held: F4 (S2 Accounting system, sales orders).
Copies no flow reaches: customers in S3 Online shop; no flow carries products between S3 Online shop, S4 Warehouse system, S5 Price list spreadsheet.
Flows from interviews, not confirmed: F8.

7. DUPLICATE RECORDS OF TRUTH
D1. customers. Named as the record by: S1 CRM (systems list); S2 Accounting system (systems list; Finance manager, 3 November 2026: "We go by the accounting system for customer names and addresses"). Also held in: S3 Online shop. Flows carrying it: F8.
D2. products. Named as the record by: S4 Warehouse system (systems list); S3 Online shop (E-commerce manager, 4 November 2026: "The online shop is the master for product names, descriptions and photos"). Also held in: S5 Price list spreadsheet. Flows carrying it: none.

8. CHANGES SINCE THE LAST MAP
No previous map supplied; nothing compared.

9. QUESTIONS
E-commerce manager
1. F5 carries payments received from the online shop to the accounting system as a weekly scheduled file (connections list, line 6) and has no owner. Who runs it?
2. The online shop holds customers (systems list, line 4) and no flow carries customers into or out of it. How do customers held there relate to the CRM and the accounting system?
E-commerce manager and Warehouse manager
3. Products: the systems list names the warehouse system (line 5) and the E-commerce manager's note of 4 November 2026 names the online shop for product names, descriptions and photos. Which system is the record for products?
4. Products are held in the online shop, the warehouse system and the price list spreadsheet (lines 4, 5, 6) and no flow carries them between any of the three. How does a new or changed product reach each? The price list spreadsheet has no business owner, so this goes to the two owners named.
E-commerce manager, Sales director and Warehouse manager
5. Sales orders are held in the CRM, the online shop and the warehouse system (lines 2, 4, 5) and none is named as the record. Which system is the record for sales orders?
Finance manager
6. Suppliers are held only in the accounting system (line 3), which is not named as the record for them; the note of 3 November 2026 says they "only live in the accounting system". Is it the record for suppliers?
7. F4 carries sales orders from the warehouse system into the accounting system daily (connections list, line 5), and the accounting system does not list sales orders as held (line 3). What does it do with them?
Finance manager and Sales director
8. Customers: the systems list names both the CRM (line 2) and the accounting system (line 3), and the Finance manager's note of 3 November 2026 goes by the accounting system. Which system is the record for customers?
Operations lead
9. The price list spreadsheet is the record for prices (line 6) and has no business owner. Who owns it?
Sales director
10. F8 is described only in the Finance manager's note of 3 November 2026: address changes in the CRM are emailed and retyped in the accounting system. Is that how customer changes reach the accounting system?
Warehouse manager
11. Your note of 5 November 2026 mentions a returns log in a spreadsheet on the shared drive. Is it a system to be listed, with its owner, administrator and the records it holds?

10. DECISIONS FOR THE MAP REVIEWER (Operations lead)
1. customers: named as the record by both S1 CRM and S2 Accounting system. Before the decision. Waits on questions 2, 8, 10. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
2. suppliers: no record named. Before the decision. Waits on question 6. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
3. products: named as the record by both S4 Warehouse system and S3 Online shop. Waits on questions 3, 4. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
4. sales orders: no record named. Before the decision. Waits on questions 5, 7. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
5. S5 Price list spreadsheet: no business owner. Waits on question 9. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
6. returns log: named but not on the systems list. Waits on question 11. Options: settle now; settle before the decision on S2 Accounting system; leave open until the next annual review.
People decide every record of truth, owner and next step; this map decides none.

11. NOT CHECKED
Whether the lists are complete or the notes accurate; the fields inside any flow; how data is changed on the way; volumes, errors and timings; access and security; costs and contracts; the returns log, which is not on the systems list. No system was connected to and nothing was changed.

Every entry traces to the systems list, the connections list, the interview notes or the settings supplied on 11 November 2026. This map connects to no system and changes nothing.
```

## What was observed

Every required part was produced, in the order and form of the output format. Nothing stopped the run: the headers matched, every row had six fields, no system name repeated, and no note held a password or a pay or conduct matter.

Compared with the published example afterwards: the counts, statuses, flow numbers, diagram, gaps, the eleven questions with their groups and order, and the six decisions with the "before the decision" marks all agree. The differences are in wording only: the example adds line numbers to the basis of each claim, words several questions differently, and writes the frequency of F8 as "when an address changes". No fact appears in either output that is not in the inputs. The example gives the returns log the name "Returns log spreadsheet", which the note only implies.

Where the template left room to guess:

1. **Frequency of an interview flow.** The Finance manager's note says the retyping happens "when a salesperson changes a customer's address". The template does not say whether that counts as a stated frequency. This run treated it as stated, as it treats "when prices change", and did not flag it. A stricter reading would flag "frequency not stated" and add a question.
2. **Whether "only live in" is a claim.** The note says suppliers "only live in the accounting system". The claim phrases are a closed list and where data is kept is never a claim, so suppliers came out as "none named". That reading follows the rules but a reader might expect otherwise.
3. **A claim for part of a type.** The online shop is "the master for product names, descriptions and photos", not all product data. The rules count a plain-words claim for the type, so products came out disputed. The template has no way to record a claim for part of a type, and the questions may not offer the answer "split by kind of detail".
4. **"Trade orders" and "address".** The Sales director's "trade orders" was read as sales orders, and the Finance manager's "address" as customers. The template does not say how loosely a note's words may be matched to the record types.
5. **Heading for a group of roles.** The template says to alphabetise group headings but not how to order the roles inside a heading. This run put them in alphabetical order.
6. **"Also held in" for a type with no record named.** For suppliers and sales orders there is no record, so the line lists the holders; the format does not say so.
7. **Questions with no decision.** Question 1 (F5 has no owner) is not waited on by any decision, because decisions cover only types and systems. It is not wrong, but the reader may wonder.
8. **"The system concerned" in decision marks.** For a decision about a system (the price list spreadsheet), "involves the system under decision" is unclear; this run did not mark it.
9. **The instruction block is shorter than the template.** The fenced block leaves out the rule about a note that names a person in a pay, performance or conduct matter, and it does not mention the flag for the system under decision. This run followed the whole template, not only the block. Nothing in the example tested the pay or conduct rule.
10. **The "offers no answer" rule is hard to keep.** Writing a question that can be answered in a sentence while offering no answer needed care. The example's questions 3, 7 and 8 lean towards suggesting an answer ("is it split by kind of detail?", "or only the invoices made from them?").

The template's own version notes and its acceptance tests still say it has not been tried or run. They were not changed. Only the run above is recorded here. No acceptance test beyond this one example was run, and nothing was tested for a client.

## Changes made after the run

Added on 11 November 2026, after an independent review. The run above is unchanged and was not repeated. These clarifications were made to the template afterward and have not been run again:

- Item 9: the rule about a note that names a person in a pay, performance or conduct matter is now in the instruction block as well as in the template, and the block's owner step now flags the system under decision.
- Items 1, 3, 4, 5 and 8: the procedure and the block now say that an event such as "when prices change" is a stated frequency; that a claim for part of a record type counts for the whole type, with the note's words printed; that a note's words match a record type only when they name it or use an everyday word for it, otherwise the author is asked; that roles inside one group heading go in alphabetical order; and that "the system concerned" counts only when it is the system under decision.
- Item 10: five questions in the published example (3, 6, 7, 8 and 11) were reworded so that they no longer suggest an answer; questions 6 and 11 were reworded later than the other three. The example now calls the returns log by the name the note uses.
- Item 6: the format now prints "Held in:" in place of "Also held in:" for a type with none named, in the template and the example. The run above printed "Also held in:" and is unchanged.
- Items 2 and 7: left as designed. The rules give one answer to each. Where data is kept is never a claim, so "only live in" does not make the accounting system the record for suppliers; the note is quoted in question 6 instead. Decisions cover record types and systems, so a question about one flow (question 1, F5 has no owner) waits on no decision.
- Marks and diagram: the example prints a flow's mark as "products (disputed) (from an interview)", the form the run printed, and the template now says the diagram prints square brackets on each block heading only, as the run did. The example had printed brackets round the receiving system too. The run above is unchanged.
- The instruction block now also carries the rule that a figure or flow that cannot be traced to a file or note is left out and named under "Not checked". It was in the template but not in the block. None of these later wording changes has been run again.
- The template's version notes and the profile now say it was tried once, in this run. The last paragraph above describes the version notes as they stood at the time of the run.

Nothing else was run, and nothing was tested for a client.
