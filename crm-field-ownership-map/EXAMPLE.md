# CRM field ownership map: an invented example

*Illustrative example with invented data.* The company, the systems, the people and every row below are invented. The company is called Company K here. Its systems owner is about to turn on a two-way sync between the contacts in the CRM and the customers in the billing system. First come the inputs the systems owner supplied, in full, then the map the capability returned.

## The inputs

### 1. Settings (typed by the systems owner)

```
Today: 10 November 2026
Planned change: switch on a two-way sync between CRM contacts and billing customers next Monday
Systems: CRM (object contact) and Billing (object customer)
Samples: a sample of 7 CRM contacts and a sample of 6 billing customers, chosen by the sales operations lead; neither is the full table
Match key candidates: email; billing_id (CRM) to customer_id (Billing)
Consent fields: marketing_opt_in (CRM), marketing_ok (Billing)
Counts-only columns: none
Integration owner: Systems owner
```

### 2. Schema exports (system,object,field,type,required,allowed_values)

```
system,object,field,type,required,allowed_values
CRM,contact,contact_id,text,yes,
CRM,contact,email,text,yes,
CRM,contact,full_name,text,yes,
CRM,contact,phone,text,no,
CRM,contact,company_name,text,no,
CRM,contact,marketing_opt_in,yes/no,yes,yes or no
CRM,contact,lifecycle_stage,picklist,yes,lead or customer or former
CRM,contact,billing_id,text,no,
Billing,customer,customer_id,text,yes,
Billing,customer,email,text,yes,
Billing,customer,name,text,yes,
Billing,customer,phone,text,no,
Billing,customer,company,text,yes,
Billing,customer,billing_address,text,yes,
Billing,customer,marketing_ok,yes/no,no,yes or no
Billing,customer,status,picklist,yes,active or closed
```

### 3. Approved definitions (system,field,meaning,business_owner,system_of_record)

```
system,field,meaning,business_owner,system_of_record
CRM,contact_id,The CRM's own number for a contact,Sales operations lead,CRM
CRM,email,Main email address of the person we deal with,Sales operations lead,
CRM,full_name,The person's full name,Sales operations lead,CRM
CRM,phone,Main phone number for the person,Sales operations lead,CRM
CRM,company_name,Name of the customer company the person works for,Finance lead,Billing
CRM,marketing_opt_in,Whether the person has agreed to receive marketing email,Head of marketing,
CRM,lifecycle_stage,Where the person is in the sales relationship,Sales operations lead,CRM
CRM,billing_id,The person's customer number in the billing system,Sales operations lead,
Billing,customer_id,The billing system's own number for a customer,Finance lead,Billing
Billing,email,Main email address of the person we deal with,Sales operations lead,
Billing,name,The person's full name,Sales operations lead,CRM
Billing,phone,Main phone number for the person,Sales operations lead,Billing
Billing,company,Name of the customer company the person works for,Finance lead,Billing
Billing,billing_address,Address invoices are sent to,Finance lead,Billing
Billing,marketing_ok,Whether the person has agreed to receive marketing email,Head of marketing,
Billing,status,Whether the customer account is open or closed,Finance lead,Billing
```

### 4. Planned mapping (crm_field,other_field), one line for each pair

```
crm_field,other_field
email,email
full_name,name
phone,phone
company_name,company
marketing_opt_in,marketing_ok
billing_id,customer_id
```

### 5. Sample records, CRM contacts (header is line 1)

```
contact_id,email,full_name,phone,company_name,marketing_opt_in,lifecycle_stage,billing_id
C-101,ana@exampleco.test,Ana Ruiz,555-0101,Exampleco Ltd,yes,customer,B-201
C-102,ben@northwind.test,Ben Okafor,555-0102,Northwind Traders,no,customer,B-202
C-103,Cara@Harbor.test,Cara Lin,,Harbor Studio,yes,lead,
C-104,dev@pinecrest.test,Dev Patel,555-0104,Pinecrest LLC,yes,customer,B-204
C-105,dev@pinecrest.test,Devesh Patel,555-0104,Pinecrest LLC,no,customer,B-204
C-106,eli@lakeside.test,Eli Moss,555-0106,Lakeside Foods,yes,customer,B-299
C-107,,Fay Wong,555-0107,Wong Supply,yes,lead,
```

### 6. Sample records, Billing customers (header is line 1)

```
customer_id,email,name,phone,company,billing_address,marketing_ok,status
B-201,ana@exampleco.test,Ana Ruiz,555-0101,Exampleco Limited,12 Mill Rd,yes,active
B-202,ben@northwind.test,Ben Okafor,555-0199,Northwind Traders,4 Quay St,yes,active
B-203,cara@harbor.test ,Cara Lin,555-0103,Harbor Studio,9 Elm Ct,yes,active
B-204,dev@pinecrest.test,Dev Patel,555-0104,Pinecrest LLC,77 Hill Ave,yes,active
B-206,eli@lakeside.test,Eli Moss,555-0106,Lakeside Foods,3 Dock Ln,no,closed
B-207,gus@bay.test,Gus Hall,555-0108,Bay Cafe,8 Bay Rd,yes,active
```

## The map

```
CRM FIELD OWNERSHIP MAP: CRM contact and Billing customer

For: the Systems owner. Prepared 10 November 2026 from the settings, schema exports, definitions, planned mapping and samples supplied. Planned change: switch on a two-way sync between CRM contacts and billing customers next Monday.

1. THE FILES
Header check: all five files have the headers expected. The CRM sample's 8 headers match the 8 CRM fields in the schema export, and the Billing sample's 8 headers match the 8 Billing fields, in the same order. Definitions: 16 rows, one for each of the 16 schema fields. Planned mapping: 6 pairs, every field named in it exists in its schema.
Samples: 7 CRM rows (lines 2 to 8) and 6 Billing rows (lines 2 to 7), both samples, as stated. Every count below describes these rows only. Line numbers count the header as line 1.

2. FIELD MAP
Key, for CRM and Billing: stated = the definitions name the source; open = no source named, or the two definitions disagree. Where a source is open, the proposed rule holds the field out of the sync in both directions until its owner answers.
F1. email <-> email (match key). Owner: Sales operations lead. Source: open, both definitions leave it blank. Proposed rule: held. Schema: text in both, required in both. Matched pairs: 5 compared, 5 agree (the pairs were made on this field), 0 differ, 0 with one side blank. CRM line 8 is blank although the field is required. Questions 4, 5, 6.
F2. full_name <-> name (ordinary field). Owner: Sales operations lead. Source: CRM (stated in both definitions). Proposed rule: CRM wins; Billing does not write this field. Schema: text in both, required in both. Matched pairs: 5 compared, 4 agree, 1 differs (pair 4: "Devesh Patel" in CRM line 6, "Dev Patel" in Billing line 5, see question 7), 0 with one side blank.
F3. phone <-> phone (ordinary field). Owner: Sales operations lead. Source: open, the CRM definition says CRM and the Billing definition says Billing. Proposed rule: held. Schema: text in both, not required in either. Matched pairs: 5 compared, 4 agree, 1 differs (pair 2: "555-0102" in CRM line 3, "555-0199" in Billing line 3), 0 with one side blank (question 9).
F4. company_name <-> company (ordinary field). Owner: Finance lead. Source: Billing (stated in both definitions). Proposed rule: Billing wins; CRM does not write this field. Schema: text in both; not required in CRM, required in Billing; no sample row shows the difference. Matched pairs: 5 compared, 4 agree, 1 differs (pair 1: "Exampleco Ltd" in CRM line 2, "Exampleco Limited" in Billing line 2), 0 with one side blank (questions 1 and 2).
F5. marketing_opt_in <-> marketing_ok (consent field). Owner: Head of marketing. Source: open, both definitions leave it blank. Proposed rule: held. Schema: yes or no in both; required in CRM, not required in Billing; all 6 Billing rows have marketing_ok filled, so no sample row shows the difference. Matched pairs: 5 compared, 2 agree, 3 differ (see section 6), 0 with one side blank (question 3).
F6. billing_id <-> customer_id (key link). Owner: Sales operations lead for billing_id, Finance lead for customer_id. Source: Billing for customer_id (stated); the billing_id definition is blank, so the CRM value is read as a copy. Proposed rule: copies from Billing and does not write back. Schema: text in both; not required in CRM, required in Billing. The sample shows the difference: CRM billing_id is blank on lines 4 and 8. Matched pairs: 5 compared, 4 agree, 1 differs (pair 5: CRM line 7 "B-299", Billing line 6 "B-206"), 0 with one side blank (questions 8, 10).

One-system fields (CRM and Billing; in no pair of the planned mapping, so the change would not touch them):
CRM contact_id (ordinary field, source CRM stated, owner Sales operations lead): 7 filled, 7 distinct.
CRM lifecycle_stage (ordinary field, source CRM stated, owner Sales operations lead): 7 filled; customer 5, lead 2; all within the allowed list.
Billing billing_address (ordinary field, source Billing stated, owner Finance lead): 6 filled, 6 distinct.
Billing status (ordinary field, source Billing stated, owner Finance lead): 6 filled; active 5, closed 1; all within the allowed list.
Fields without a definition: none.

3. MATCH KEYS
email, compared exactly as written:
CRM: 6 filled, 5 distinct, 1 blank (line 8). Repeated: dev@pinecrest.test (lines 5, 6).
Billing: 6 filled, 6 distinct, 0 blank. Repeated: none.
Matched exactly: 5 CRM rows (lines 2, 3, 5, 6, 7) to 4 Billing rows (lines 2, 3, 5, 6), so 5 record pairs: pair 1 CRM line 2 and Billing line 2; pair 2 CRM line 3 and Billing line 3; pair 3 CRM line 5 and Billing line 5; pair 4 CRM line 6 and Billing line 5; pair 5 CRM line 7 and Billing line 6.
Match only if capitals and surrounding spaces are ignored: CRM line 4 ("Cara@Harbor.test") and Billing line 4 ("cara@harbor.test "). Left out of the comparisons in section 2 (question 6).
No exact match: CRM line 4 (near-match only) and line 8 (blank email); Billing line 4 (near-match only) and line 7 (gus@bay.test).
billing_id (CRM) to customer_id (Billing):
CRM billing_id: 5 filled, 4 distinct, 2 blank (lines 4, 8). Repeated: B-204 (lines 5, 6). Billing customer_id: 6 filled, 6 distinct.
Found in Billing: 4 of the 5 filled rows (lines 2, 3, 5, 6), holding 3 distinct values (B-201, B-202, B-204). Not found: B-299 (line 7).
Agreement with the email match: 5 CRM rows have both an exact email match and a billing_id. For 4 of them (lines 2, 3, 5, 6) the billing_id names the same Billing row as the email. For 1 (line 7) it does not: the email matches Billing line 6 (B-206), the billing_id is B-299.

4. DUPLICATES AND AMBIGUOUS MATCHES
Same key, different values: CRM lines 5 and 6 share the email dev@pinecrest.test and the billing_id B-204. They differ in contact_id (C-104, C-105), full_name (Dev Patel, Devesh Patel) and marketing_opt_in (yes, no); they agree in phone, company_name and lifecycle_stage. Both match Billing line 5, so the match is ambiguous: one Billing customer, two CRM contacts.
Identical rows: none found in either sample.
Ambiguous matches in the other sample: Billing line 5 is matched by two CRM rows (lines 5, 6), as above. No CRM row matches two Billing rows.

5. KEY CONFLICTS
CRM line 7 (C-106): email matches Billing line 6 (B-206) but billing_id is B-299, which is not in the Billing sample. See section 3 and question 8.

6. CONSENT FIELDS
Named: marketing_opt_in (CRM), marketing_ok (Billing). No other field name in either schema contains consent, opt, unsubscribe, gdpr or marketing.
Matched pairs: 5 compared, 2 agree (pairs 1 and 3, yes and yes), 3 differ: pair 2 (CRM line 3 "no", Billing line 3 "yes"), pair 4 (CRM line 6 "no", Billing line 5 "yes"), pair 5 (CRM line 7 "yes", Billing line 6 "no"), 0 with one side blank.
Proposed rule for marketing_opt_in and marketing_ok: held, with no write in either direction. The map sets no other rule for a consent field; the owner decides.

7. QUESTIONS FOR THE FIELD OWNERS
Finance lead
1. company_name: CRM line 2 reads "Exampleco Ltd" and Billing line 2 reads "Exampleco Limited". Which wording is the company's name?
2. CRM does not require company_name and Billing requires company. All 7 CRM sample rows have a company, so no row shows the case. What should the sync do for a CRM contact with no company?
Head of marketing
3. marketing_opt_in and marketing_ok disagree in 3 of 5 matched pairs (CRM lines 3, 6, 7 against Billing lines 3, 5, 6). Which system's value records the person's current choice?
Sales operations lead
4. Neither definition names a source for email, the match key. Which system is the source for email?
5. CRM line 8 (C-107) has no email, and CRM requires one. The email is the match key. What should the sync do with a contact that has none?
6. CRM line 4 ("Cara@Harbor.test") and Billing line 4 ("cara@harbor.test ") match only when capitals and the trailing space are ignored. Are they the same person, and should the key be compared that way?
7. CRM lines 5 and 6 (C-104 and C-105) share dev@pinecrest.test and both name B-204. They differ in full_name ("Dev Patel", "Devesh Patel") and in marketing_opt_in (yes, no). Are they one person or two?
8. CRM line 7 (C-106) has the email of Billing line 6 (B-206) but names B-299 as its billing customer. Which is right?
9. phone: the CRM definition names CRM as the source and the Billing definition names Billing. Which system is the source? CRM line 3 and Billing line 3 differ ("555-0102", "555-0199").
10. billing_id is optional in CRM and blank on lines 4 and 8, and customer_id is required in Billing. Is a blank billing_id expected for a contact with no billing customer?

8. DECISIONS FOR THE INTEGRATION OWNER (Systems owner), with the field owners
1. Match rule for email (waits on answers 5 and 6): exact as written, or ignoring capitals and spaces; and what happens to a contact with no email. Options: approve as proposed, change, wait.
2. The records at CRM lines 5, 6 and 7 (waits on answers 7 and 8): approve their matches, change them, or hold them out of the sync.
3. F1 email, held (waits on answer 4): approve the hold, set a rule, or wait.
4. F2 full_name, CRM wins (waits on answer 7): approve as proposed, change, hold out, or wait.
5. F3 phone, held (waits on answer 9): approve the hold, set a rule, or wait.
6. F4 company_name, Billing wins (waits on answers 1 and 2): approve as proposed, change, hold out, or wait.
7. F5 marketing_opt_in and marketing_ok, held (waits on answer 3): approve the hold, set a rule, or wait.
8. F6 billing_id, copies from Billing (waits on answers 8 and 10): approve as proposed, change, hold out, or wait.
Approval of the mapping belongs to the Systems owner with the field owners; the map itself changes nothing.

9. NOT CHECKED
Whether the values are true; rows outside the two samples; any other object or field in either system; how the sync tool resolves a conflict by default; the effect of a rule on the full tables. No mapping has been changed and no data moved.

Every figure counts the 7 CRM rows and 6 Billing rows supplied on 10 November 2026. This map connects to no system, changes no mapping and moves no data.
```
