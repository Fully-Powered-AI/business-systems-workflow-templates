# App data requirements: a second run on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (`claude-sonnet-5-5`)
- **Date:** 2026-11-10

The inputs were the invented example's own: the settings, `request_notes.txt`, `process_rules.txt`, `object_definitions.csv` and `sample_records.csv` in [the example](example.md). No client data was used. This is the second run on those inputs. The first run, made earlier the same day on the first version of the template, found the faults listed below; the template and the example were then edited, and this run is of the edited template.

Two limits. This run was not blind: the assistant that made the edits ran it, and the example's specification was written in the same session just before it. And the run was a check of the edited instruction block against the example, made by deriving the specification from the inputs one step at a time, not an independent trial. It was run once.

After the independent review, three details of the specification above were changed to match the notes and rules more closely: R2b was added to the exact match for "item" and to the Item entity line, R4 was added to the Loan entity line, and the two reads by "the reminder" were reworded as "not stated; needed to work out overdue". I re-derived those lines from the inputs myself, in the same session as the edits; the rest of the output is as first recorded. The re-derivation was not blind and not independent either, and an independent re-run on a fresh session is still worth having.

## What came out

```
DATA SPECIFICATION: Equipment loans

For: the business systems analyst, to confirm with the process owner (the office manager). Prepared Tuesday 10 November 2026 from request_notes.txt, process_rules.txt, object_definitions.csv and sample_records.csv (all supplied 2026-11-10). Nothing was built, configured or changed, and no live data was used.

1. THE FILES
Header check: object_definitions.csv and sample_records.csv match the defaults in name and order. request_notes.txt: 7 lines (8 statements once split). process_rules.txt: 4 rules (5 statements once split). object_definitions.csv: 13 field rows in 3 objects. sample_records.csv: 13 rows in 3 sample records. Sample records confirmed invented by the analyst. Verb lists: defaults.

2. NAMES
Matched exactly:
- "item" (N2a, N7, R1, R2b, R3, R4) is Item.
- "loan" (N3, N4, N6, N7, R1, R2a, R2b) is Loan.
- "person" (R1) is Person.
- "team" (N7) is Person.team.
Matched by meaning, to confirm (Question 1):
- "free" (N1) is Item.status: the note says "which shared equipment is free"; the definition says "Current state of the item".
- "takes" (N2a) is Loan.date_out: the note says "when someone takes an item"; the definition says "Date item left".
- "comes back" (N2b) and "returned" (R4) are Loan.date_returned: the note says "when it comes back"; the definition says "Date item came back".
- "due back date" (N3) is Loan.date_due: the note says "a due back date"; the definition says "Date due back".
- "borrower" (N7) is Loan.person_id: the note says "the borrower's team"; the definition says "Borrower".
- "staff" (N1), "someone" (N2a) and "people" (N6) are Person: the note says "Staff should be able to see"; Person.person_id says "Staff number".
No match:
- "repair" (N5; "in repair", R3): no existing name shares a word. Question 6.
- "approval" (R2b): no existing name shares a word. Question 5.
- "condition" (R4): no existing name shares a word. Question 7.
- "reminder" (N6): no existing name shares a word. Question 8.
Ambiguous:
- "equipment" (N1) could be Item or Item.category (described as "Type of equipment"). Question 2.
Roles named: "staff" (N1), "the office manager" (N2a, N2b, N7, R4), "managers" (N4), "a manager" (R2b). The definitions hold no role or permission field. Question 3.

3. ENTITIES
- Item (object_definitions.csv lines 2 to 5, 4 fields): used by N1, N2a, N7, R1, R2b, R3, R4.
- Person (lines 6 to 8, 3 fields): used by N1, N2a, N6, N7, R1.
- Loan (lines 9 to 14, 6 fields): used by N2a, N2b, N3, N4, N6, N7, R1, R2a, R2b, R4.
Named but not defined: 4. Repair (N5, R3), approval (R2b), condition (R4) and reminder (N6). Whether each is an object, fields on an existing object, a status value or only a view of existing records is open: Questions 5 to 8.

4. FIELDS
Needed (10 of 13 defined fields):
- Item.item_id (text, required, line 2): implied by N2a (to log which item is taken, the item must be identified; Loan.item_id points to it, R1). Read by: not stated. Written by: not stated. Sample: EQ-014 (sample line 2). Question 12.
- Item.item_name (text, required, line 3): Read by staff (N1, implied: to see which items are free, staff must be shown which item each is). Written by: not stated. Sample: Projector A (sample line 3). Question 12.
- Item.status (choice, required, line 5): Read by staff (N1); by the office manager before a loan is logged (R3, implied). Written by: not stated. Rule: R3. Sample: Available (sample line 5). Question 10.
- Person.person_id (text, required, line 6): implied by N2a and R1 (a loan is for one person, so the person must be identified). Read by: not stated. Written by: not stated. Sample: P-0007 (sample line 6). Question 12.
- Person.team (text, not required, line 8): Read by the office manager (N7). Written by: not stated. Sample: Sales (sample line 8). Question 12.
- Loan.item_id (text, required, line 10): Written by the office manager when a loan is logged (N2a, R1). Read by the office manager, to find the loans of an item (N7, implied by "any item"). Sample: EQ-014 (sample line 10). Question 9.
- Loan.person_id (text, required, line 11): Written by the office manager when a loan is logged (N2a, R1). Read by the office manager, to reach the borrower's team (N7, implied). Sample: P-0007 (sample line 11). Question 9.
- Loan.date_out (date, required, line 12): Written by the office manager (N2a). Read by: not stated; N7 does not say which loan fields the history shows. Rule: R2. Sample: 2026-11-02 (sample line 12). Question 9.
- Loan.date_due (date, required, line 13): Written by: not stated (N3 says a loan has a due back date, normally a week after it goes out, and R2a that the standard loan is 7 days; none names who sets it). Read by: not stated; needed to work out overdue (N6, implied). Rule: R2. Sample: "next Monday" (sample line 13), not a date. Question 11.
- Loan.date_returned (date, not required, line 14): Written by the office manager (N2b). Read by: not stated; needed to work out overdue (N6, implied). Sample: blank (sample line 14), allowed. Question 8.
Defined, not mentioned in the notes or rules: 3.
- Item.category (choice, required, line 4); sample Presentation (sample line 4). N1's "equipment" may mean it (Question 2). Question 13.
- Person.full_name (text, required, line 7); sample Person One (sample line 7). Question 13.
- Loan.loan_id (text, required, line 9); sample L-0101 (sample line 9). Question 13.
Needed but not defined: 5.
- A person's role (N1, N2a, N4, R2b): which people are staff, the office manager or a manager. Question 3.
- Approval of a loan over 14 days (R2b): written by a manager (R2b); who reads it is not stated. Question 5.
- Repair (N5, R3): who records it and what is kept are not stated. Question 6.
- Condition at return (R4): written by the office manager; values Good, Worn, Damaged. Question 7.
- Reminder (N6): where it goes and whether a sent reminder is kept; Person holds no contact field. Question 8.
Worked out, not stored: loan length in days (date_due minus date_out, for the 14-day line in R2b and "long loans" in N4); whether a loan is overdue (date_due and date_returned, for N6). Whether either is stored is the process owner's choice.

5. ACTIONS
- A1 staff: Read. See which equipment is free: Item.item_name, Item.status (N1). Question 2.
- A2 office manager: Write, creates a Loan. Log that an item is taken: Loan.item_id, Loan.person_id, Loan.date_out (N2a, R1); reads Item.status first (R3, implied).
- A3 office manager: Write, updates a Loan. Log that an item comes back: Loan.date_returned (N2b).
- A4 managers: Unclear. "handle" the long loans (N4). Acts on Loan. Question 4.
- A5 not stated: Unclear. "track" repairs (N5). Repair has no definition. Question 6.
- A6 people (the borrower, if the match is confirmed): Message. "get a reminder" when a loan is overdue (N6). Question 8.
- A7 office manager: Read. See the loan history of any item, with the borrower's team: Loan.item_id, Loan.person_id, Person.team (N7). Which other loan fields it shows: Question 9.
- A8 a manager: Write. Approve a loan of more than 14 days before the item leaves (R2b). No field holds it. Question 5.
- A9 office manager: Write. Record the condition of a returned item (R4). No field holds it. Question 7.
Totals: 9 actions; 2 read, 4 write, 3 unclear or message.

6. RULES
- R1: covered. Loan.item_id and Loan.person_id each hold one value.
- R2: partly covered. R2a is covered by Loan.date_out and Loan.date_due (who sets date_due: Question 11); for R2b nothing holds the approval. Question 5.
- R3: partly covered. Item.status can show an item's state; no value is defined, so "in repair" is not held. Questions 6 and 10.
- R4: partly covered. Loan.date_returned records the return; nothing holds the condition. Question 7.
Totals: 4 rules; 1 covered, 3 partly covered, 0 not covered.
No note and rule disagree: N3 and R2a both give a week (7 days); N4 says "long loans" without a length.

7. SAMPLE RECORDS
Checked 13 values in 3 records (S1 Item, S2 Person, S3 Loan): 12 filled, 1 blank (Loan.date_returned, line 14; not required).
- Text: 8 values, all filled.
- Number: none.
- Date: 3 values. 1 fits (date_out 2026-11-02, line 12). 1 does not (date_due "next Monday", line 13). 1 is blank (date_returned, line 14). Question 11.
- Yes-no: none.
- Choice: 2 values (category Presentation, line 4; status Available, line 5). Allowed values are not in the definitions. Questions 10 and 13.
- Links: Loan.item_id EQ-014 (line 10) matches Item.item_id (line 2). Loan.person_id P-0007 (line 11) matches Person.person_id (line 6).
- Required fields blank: none. Sample fields with no definition: none. Defined fields missing from the samples: none.
- One reading: S1 shows status Available (line 5), while S3 shows a loan of EQ-014 out on 2026-11-02 with no return date (lines 12 and 14). Question 10.

8. QUESTIONS FOR THE PROCESS OWNER
1. Are the matches by meaning in section 2 right: free is Item.status, takes is Loan.date_out, comes back and returned are Loan.date_returned, due back date is Loan.date_due, borrower is Loan.person_id, and staff, someone and people are Person?
2. N1 says "shared equipment". The Item object holds items, and Item.category is described as "Type of equipment" (line 4). Does "equipment" in N1 mean the item, its category, or both?
3. N1, N2a, N2b, N4, N7, R2b and R4 name three roles: staff, the office manager and managers. The definitions hold no role. How will the app know who holds which role?
4. N4 says managers "handle" the long loans. What do they do with them: see them, approve them, extend them, or something else? Is a long loan the same as a loan of more than 14 days (R2b)?
5. R2b requires a manager's approval for a loan of more than 14 days before the item leaves the office. Nothing holds it. What must be kept: who approved, when, or nothing? Who may read it? Must the loan wait for it? Which manager: any, the borrower's own, or a named one?
6. N5 says repairs need to be tracked and R3 says an item "in repair" cannot be loaned. Is a repair a record of its own, with what to enter and see, or only a status on the item? Who records it?
7. R4 records the condition (Good, Worn or Damaged) when an item is returned. Nothing holds it. Is it kept on each loan, on the item, or both?
8. N6 says people get a reminder when a loan is overdue. Is a loan overdue when date_due has passed and date_returned is blank? Person holds no contact field: where does the reminder go? Who sends it, and is a sent reminder recorded?
9. N7 says the office manager sees the loan history of any item, with the borrower's team. Does the history show date_out, date_due and date_returned? Is it only the Loan records of that item, or is something else kept? Who else may see it?
10. Who sets Item.status when a loan starts and when it ends? What are its allowed values, and is "in repair" one of them? S1 shows Available (line 5) while S3 shows EQ-014 out with no return date (lines 12 and 14).
11. N3 says a loan has a due back date, normally a week after it goes out (R2a: 7 days). Who sets date_due, and how is it entered? The sample has "next Monday" (line 13), not a date. May it change after the loan is logged?
12. Nothing says who creates or changes Item and Person records, or who may read Item.item_id, Item.item_name and Person.person_id beyond what N1 and N7 show. Who does, and how? Person.team is not required: what should N7 show when it is blank?
13. Item.category (line 4), Person.full_name (line 7) and Loan.loan_id (line 9) are required but no note or rule uses them by name. Are they needed in this app? What are the allowed values of category (the sample has Presentation)? How is a loan number made?

9. DECISIONS FOR THE PROCESS OWNER AND THE ANALYST
1. Names and scope (Questions 1, 2 and 13): accept each match, say what "equipment" means, rename, or leave the unused fields out of this app.
2. Roles and approval (Questions 3, 4 and 5): how a role is held, what managers do with long loans, and whether approval is kept as fields on the loan, as a record of its own or not at all.
3. Repairs and condition (Questions 6 and 7): fields on existing objects, a new object, or status values only.
4. Reminders (Question 8): the meaning of overdue, a contact field, a record of reminders, and whether a person or the app sends them.
5. The loan history (Question 9): which fields it shows and who sees it.
6. Who writes what (Questions 10, 11 and 12): who creates records, who sets status and due dates, and how dates are entered.
Confirming this specification with the process owner is the analyst's decision.

10. NOT CHECKED
Whether the object definitions match the live system; who is permitted to do what beyond the roles named; screens, layout and wording; volumes and speed; how records reach other systems; whether the notes are complete; whether the sample records show the variety of real use. No file was changed and no system was touched.

Every line number counts from line 1 of its file as supplied on Tuesday 10 November 2026; a sample line is a line of sample_records.csv. N is a line of request_notes.txt and R a rule in process_rules.txt (a letter after the number marks a part, as N2a), and S is a sample record in sample_records.csv. This specification builds nothing, configures nothing and uses no live data.
```

## What was observed

The specification has all ten sections and every heading in order, including Ambiguous, Number and Yes-no. The header check, counts and sample checks recompute from the files: 7 note lines (8 statements), 4 rules (5 statements), 13 field rows in 3 objects, 13 sample values (12 filled, 1 blank), 10 of 13 fields needed and 3 defined but not mentioned, 9 actions (2 read, 4 write, 3 unclear or message), 4 rules (1 covered, 3 partly covered). No input triggered a stop condition, and no meaning was chosen where the notes were unclear.

Compared with the example, the output agreed line for line, which is expected given the limits above. One gap turned up during the run: the verb lists put "get" in the unclear class and "get a reminder" in the message class, and the instruction block did not say which wins for N6. The block and the procedure now say a longer listed phrase beats a shorter word; the output did not change. Nothing else in the output differed from the example.

Where the edited template still needs a judgment:

- Splitting is by one stated rule (a sentence end, or an "and" that joins a second verb or event). Whether "who" or "normally" clauses should also split is decided against: N3 and R4 stay whole. A line the rule does not foresee would need a person's reading.
- "Implied" remains a judgment. This run marked Item.item_id and Person.person_id implied by N2a and R1, Item.item_name implied by N1, and Loan.item_id and Loan.person_id read by N7 as implied by "any item" and "the borrower's team". A different reader might list item_id and item_name as defined, not mentioned.
- "Equipment" is listed as ambiguous between Item and Item.category, so Item.category is listed as defined, not mentioned, with a note that N1 may mean it.
- A requirement that a role give an approval (R2b) counts as that role approving; that is a convention of the template, not something the notes say.
- The words "history", "long" and "overdue" are deliberately not listed as names; the history is read as Loan records of an item, and "overdue" is worked out from two fields.

## What the first run found

The first run, on the first version of the template and example, was recorded earlier the same day. In summary, and with nothing softened:

- Statements were split (N2 and N3) although the procedure did not say how; this run produced 9 actions, not the 7 the example and the second acceptance test expected.
- Following "never mark a field implied on a hunch", Loan.loan_id and Person.full_name had no line that needs them, so the run listed 10 fields as needed and 3 as defined, not mentioned; the example and the test said 12 and 1.
- "Equipment" was listed as ambiguous between Item and Item.category; the example matched it to Item by meaning.
- No note names who sets the due date; the example had the office manager write Loan.date_due, which the inputs do not support. The example also had the office manager read Person.full_name, which N7 does not mention.
- The run printed the Ambiguous heading and the Number and Yes-no lines; the example left them out.
- The template left undefined which words count as names, how to class verbs such as "takes" and "comes back", how a by-meaning match to an object can cite a description, how to split a rule of two sentences, and why the format cited "sample line" while the trace line explained S ids.

Those findings led to the edits described in the version notes of the template. Everything above them is now defined in the procedure, except for the judgments listed under "Where the edited template still needs a judgment".
