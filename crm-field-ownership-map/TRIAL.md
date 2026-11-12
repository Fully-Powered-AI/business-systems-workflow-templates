# CRM field ownership map: tried on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example in [example.md](example.md): Company K, a CRM and a billing system, 7 and 6 sample rows. No client data was used. The assistant read the workflow template and the example's inputs only, produced the map, and only then compared it with the example's map and with the reviewer checklist. This was one run by an assistant that did not write the template.

## Inputs used

The six inputs in example.md, unchanged: the settings, the schema exports, the approved definitions, the planned mapping, the CRM sample and the Billing sample.

## What came out

All nine sections of the output format were produced, in order, with the trace line. The map follows.

```
CRM FIELD OWNERSHIP MAP: CRM (contact) and Billing (customer)

For: Systems owner. Prepared 10 November 2026 from the settings, schema exports, definitions, planned mapping and samples supplied. Planned change: switch on a two-way sync between CRM contacts and billing customers next Monday.

1. THE FILES
Header check: all files have the headers expected, and each sample's headers match its schema export's field names (8 CRM fields, 8 Billing fields). Every row has 8 fields. Definitions: 16 rows, covering 16 of 16 schema fields. Planned mapping: 6 pairs; every field exists in its schema.
Samples: 7 CRM rows (lines 2 to 8) and 6 Billing rows (lines 2 to 7), samples and not full tables, as stated. Every count below describes these rows only. Line numbers count the header as line 1.

2. FIELD MAP
Key, for CRM and Billing: stated = the definitions name the source; open = no source named, or the two definitions disagree. Where a source is open, the proposed rule holds the field out of the sync in both directions until its owner answers.
F1. email <-> email (match key). Owner: Sales operations lead. Source: open, both definitions leave it blank. Proposed rule: held. Schema: text on both sides, required on both, no difference. Matched pairs: 5 compared, 5 agree (the pairs were made on this field), 0 differ, 0 with one side blank. Questions 7, 11, 12.
F2. full_name <-> name (ordinary field). Owner: Sales operations lead. Source: CRM, stated (both definitions name CRM). Proposed rule: CRM wins; Billing does not write this field. Schema: text on both sides, required on both, no difference. Matched pairs: 5 compared, 4 agree, 1 differs (pair 4: CRM line 6 "Devesh Patel", Billing line 5 "Dev Patel"), 0 with one side blank. Question 10.
F3. phone <-> phone (ordinary field). Owner: Sales operations lead. Source: open; the CRM definition names CRM and the Billing definition names Billing. Proposed rule: held. Schema: text on both sides, optional on both, no difference. Matched pairs: 5 compared, 4 agree, 1 differs (pair 2: CRM line 3 "555-0102", Billing line 3 "555-0199"), 0 with one side blank. Question 8.
F4. company_name <-> company (ordinary field). Owner: Finance lead. Source: Billing, stated (both definitions name Billing). Proposed rule: Billing wins; CRM does not write this field. Schema: text on both sides; required in Billing, optional in CRM. No sample row shows the difference (all 7 CRM rows have a company name). Matched pairs: 5 compared, 4 agree, 1 differs (pair 1: CRM line 2 "Exampleco Ltd", Billing line 2 "Exampleco Limited"), 0 with one side blank. Questions 1, 2.
F5. marketing_opt_in <-> marketing_ok (consent field, named). Owner: Head of marketing. Source: open, both definitions leave it blank. Proposed rule: held. Schema: yes/no on both sides, allowed values "yes or no" on both; required in CRM, optional in Billing. No sample row shows the difference (all 6 Billing rows are filled). Matched pairs: 5 compared, 2 agree, 3 differ (pair 2: CRM line 3 "no", Billing line 3 "yes"; pair 4: CRM line 6 "no", Billing line 5 "yes"; pair 5: CRM line 7 "yes", Billing line 6 "no"), 0 with one side blank. Questions 4, 5, 6.
F6. billing_id <-> customer_id (key link). Owner: Sales operations lead for billing_id, Finance lead for customer_id. Source: Billing, stated (the Billing definition names Billing; the CRM definition was blank). Proposed rule: copies from Billing and does not write back. Schema: text on both sides; required in Billing, optional in CRM. The sample shows it: CRM billing_id is blank on lines 4 and 8. Matched pairs: 5 compared, 4 agree, 1 differs (pair 5: CRM line 7 "B-299", Billing line 6 "B-206"), 0 with one side blank. Questions 3, 13, 14.
One-system fields (in no pair of the planned mapping, so the change would not touch them):
CRM contact_id (ordinary, source CRM, owner Sales operations lead): 7 filled, 7 distinct.
CRM lifecycle_stage (ordinary, source CRM, owner Sales operations lead): customer 5 (lines 2, 3, 5, 6, 7), lead 2 (lines 4, 8), former 0.
Billing billing_address (ordinary, source Billing, owner Finance lead): 6 filled, 6 distinct.
Billing status (ordinary, source Billing, owner Finance lead): active 5 (lines 2, 3, 4, 5, 7), closed 1 (line 6).
Fields without a definition: none.

3. MATCH KEYS
email, compared exactly as written:
CRM: 6 filled, 5 distinct, 1 blank (line 8). Repeated: dev@pinecrest.test (lines 5, 6).
Billing: 6 filled, 6 distinct, 0 blank. Repeated: none.
Matched exactly: 5 CRM rows (lines 2, 3, 5, 6, 7) to 4 Billing rows (lines 2, 3, 5, 6), so 5 record pairs: pair 1 CRM 2 / Billing 2; pair 2 CRM 3 / Billing 3; pair 3 CRM 5 / Billing 5; pair 4 CRM 6 / Billing 5; pair 5 CRM 7 / Billing 6.
Match only if capitals and surrounding spaces are ignored: CRM line 4 "Cara@Harbor.test" and Billing line 4 "cara@harbor.test " (trailing space). Left out of the comparisons in section 2.
No exact match: CRM lines 4 (near-match only), 8 (blank email); Billing lines 4 (near-match only), 7.
billing_id (CRM) to customer_id (Billing): CRM 5 filled, 4 distinct, 2 blank (lines 4, 8); repeated B-204 (lines 5, 6). Billing customer_id: 6 filled, 6 distinct. Of the 5 filled CRM values, 4 are found in the Billing sample (B-201 line 2, B-202 line 3, B-204 lines 5 and 6) and 1 is not (B-299, line 7). Billing customer ids not named by any CRM row: B-203, B-206, B-207. Of the 5 record pairs, 4 name the same record by email and by billing_id (pairs 1 to 4); pair 5 does not (email matches Billing line 6, B-206; billing_id says B-299).

4. DUPLICATES AND AMBIGUOUS MATCHES
Same key, different values: CRM lines 5 and 6 (email dev@pinecrest.test). Columns that differ: contact_id (C-104, C-105), full_name ("Dev Patel", "Devesh Patel"), marketing_opt_in (yes, no). Columns that agree: email, phone (555-0104), company_name (Pinecrest LLC), lifecycle_stage (customer), billing_id (B-204). Both match Billing line 5.
Identical rows: none found in either sample.
Ambiguous matches: Billing line 5 matches two CRM records (lines 5, 6). No Billing record matches more than one in the other direction beyond that. No record chosen.

5. KEY CONFLICTS
CRM line 7 (C-106): email matches Billing line 6 (B-206), but billing_id says B-299, which is not in the Billing sample.

6. CONSENT FIELDS
Named: marketing_opt_in (CRM), marketing_ok (Billing). Fields that look like consent but are not named: none found.
Matched pairs: 5 compared, 2 agree, 3 differ (pair 2 lines CRM 3 / Billing 3, "no" and "yes"; pair 4 lines CRM 6 / Billing 5, "no" and "yes"; pair 5 lines CRM 7 / Billing 6, "yes" and "no"), 0 with one side blank.
Proposed rule for marketing_opt_in and marketing_ok: held, with no write in either direction. The map sets no other rule for a consent field; the owner decides.

7. QUESTIONS FOR THE FIELD OWNERS
Finance lead
1. Pair 1 (CRM line 2, Billing line 2) differs on company name: CRM "Exampleco Ltd", Billing "Exampleco Limited". Which wording is the company's name?
2. Company name is required in Billing and optional in CRM; all 7 CRM sample rows have one. What should Billing hold for a CRM contact with no company name?
3. CRM line 7 names Billing customer B-299, which is not among the 6 Billing sample rows (Billing line 6 is B-206, same email). Does customer B-299 exist in Billing, and is it the same person as B-206?
Head of marketing
4. Marketing agreement differs on 3 of 5 matched pairs: pair 2 (CRM line 3 "no", Billing line 3 "yes"), pair 4 (CRM line 6 "no", Billing line 5 "yes"), pair 5 (CRM line 7 "yes", Billing line 6 "no"). Which system's value records the person's current choice?
5. CRM lines 5 and 6 share one email but hold marketing_opt_in "yes" (line 5) and "no" (line 6). Which value stands for this person?
6. marketing_opt_in is required in CRM and marketing_ok is optional in Billing; no Billing sample row is blank. What does a blank marketing_ok mean?
Sales operations lead
7. Neither definition names a source for email, the match key. Which system is the source?
8. The CRM definition of phone names CRM and the Billing definition names Billing; pair 2 differs (CRM line 3 "555-0102", Billing line 3 "555-0199"). Which system is the source for phone?
9. CRM lines 5 and 6 share email dev@pinecrest.test and billing_id B-204, and differ in contact_id, full_name and marketing_opt_in; both match Billing line 5. Are they one person or two?
10. Pair 4 differs on name: CRM line 6 "Devesh Patel", Billing line 5 "Dev Patel" (CRM line 5 is "Dev Patel"). Which spelling is the person's full name?
11. CRM line 4 "Cara@Harbor.test" and Billing line 4 "cara@harbor.test " match only when capitals and the trailing space are ignored; CRM billing_id is blank and Billing customer_id is B-203. Are they the same person?
12. CRM line 8 (C-107, Fay Wong) has no email although email is required in CRM. What is the email, or is a blank expected?
13. CRM line 7: email points to Billing B-206, billing_id says B-299. Which one identifies this contact?
14. billing_id is optional in CRM and blank on lines 4 and 8 (both lifecycle_stage lead); customer_id is required in Billing. Is a blank expected for a contact with no billing customer?

8. DECISIONS FOR THE INTEGRATION OWNER (Systems owner), with the field owners
1. email (F1), held: waits on questions 7, 11, 12. Options: approve as proposed, change, hold out, wait.
2. phone (F3), held: waits on question 8. Options: approve as proposed, change, hold out, wait.
3. full_name (F2), CRM wins: waits on questions 9, 10. Options: approve as proposed, change, hold out, wait.
4. company_name (F4), Billing wins: waits on questions 1, 2. Options: approve as proposed, change, hold out, wait.
5. marketing_opt_in and marketing_ok (F5), held: waits on questions 4, 5, 6. Options: approve as proposed, change, wait.
6. billing_id (F6), copies from Billing and does not write back: waits on questions 3, 13, 14. Options: approve as proposed, change, hold out, wait.
7. CRM lines 5 and 6 (one ambiguous match) and the near-match at CRM line 4 / Billing line 4: waits on questions 9 and 11. Options: wait, change the plan.
Approval of the mapping belongs to the Systems owner with the field owners; the map itself changes nothing.

9. NOT CHECKED
Whether the values are true; rows outside the samples; other objects or fields; how the sync tool resolves conflicts by default; what happens to Billing line 7 (gus@bay.test) and CRM line 8, which have no match; the effect of any rule on the full tables. No mapping has been changed and no data moved.

Every figure counts the 7 CRM rows and 6 Billing rows supplied on 10 November 2026. This map connects to no system, changes no mapping and moves no data.
```

## What was observed

- **Every required part was produced.** The nine sections, the six field blocks, the numbered questions grouped by owner in alphabetical order, the numbered decisions, the not-checked section and the trace line all came out. Nothing in the instructions called for a stop: every header matched, every field existed and every row had eight fields.
- **Agreement with the published example.** The findings are the same: the same five record pairs, the same counts of agreeing and differing values for every field pair, the same near-match, the same ambiguous match, the same key conflict, and the same sources and proposed rules. Nothing was asked of the person.
- **Differences from the example as it stood at the time of the run.** The example was edited after this run to correct the points below (see the note at the end of this record); the list describes the example as it was when this run was compared with it.
  - The example's field blocks for consent and for the key link leave out some counts (blank-side counts for the consent field; all matched-pair counts for the key link). This run gave all four counts for every pair, as the output format asks.
  - The example lists Billing customer_id among the "one-system fields", although it is in a pair of the planned mapping (the key link). This run left it out of that list.
  - The example has 8 questions where this run has 14. This run asked a separate question for each open point the procedure lists (the open email source, the blank-key requirement difference for marketing, the blank billing_id, and so on), and put the consent requirement difference and the two duplicate points into their own questions. The example folds several points together.
  - The example's decisions are four and are grouped by theme; this run wrote seven, one for each field plus one for the record-level points.
  - The example names a likely outcome in question 1 ("the CRM value would become Exampleco Limited"). This run stated the rule in the map and asked only which wording is the company name.
  - Wording, ordering inside a section, and the way the pair numbers are cited differ.
- **Facts not in the inputs.** None found in either output. Every value, line number and count recomputes from the rows supplied.
- **Where the instructions were ambiguous, and a guess was needed.**
  - The planned mapping is described as "written in both directions" in the example, but the file lists each pair once. The template does not say what direction the sync writes beyond the settings sentence.
  - A pair can have two business owners (billing_id and customer_id). The format has one "Owner" slot and the questions are grouped by one owner. This run named both owners in the field block and put each question under the owner of the field it concerns.
  - Whether a stored cross-reference to a record that is not in the sample (B-299) counts as a "key conflict" ("names a different record than the key does") is not stated. This run reported it as one, with the reason.
  - The role of a field that is both a match key candidate and held (email) is "match key", but the proposed rule is "held". The template allows it, and it reads oddly: the key is used to match records and also held out of the sync.
  - Records that exist in only one system (Billing line 7, CRM line 8) get no question, no rule and no decision. The template says to list them and nothing more. This run listed them and named them in "not checked".
  - The decisions step does not say whether a record-level choice (the duplicate, the near-match) belongs in the decisions. This run added one decision for them.
  - Whether to count "contact_id" among the columns that differ in a duplicate group is not stated; this run counted it because the values differ.
  - The cap of ten line numbers per finding was never reached, so it was not exercised.
- **Defects in the template.** None that stopped the run. The acceptance tests are marked proposed and have not been run; this trial did not run them either.
- **Not shown by this run.** It does not show how the template behaves with sensitive columns marked counts-only, a header mismatch, a missing planned mapping, or a request to merge or to say the sync is safe. It does not show how the template behaves in ChatGPT, Copilot or Gemini, or with any real client data.

## After this record was written

The example's map was edited to settle the differences listed above: the consent and key-link blocks now carry all four matched-pair counts, Billing customer_id is no longer listed among the one-system fields, every field block names its role, the key link is written with the template's rule (copies from Billing and does not write back) and no record-level hold, the questions now include the open source for email and the billing_id requirement difference (ten questions, renumbered, with the decisions updated), question 1 was made neutral, the consent-like name list includes gdpr, the no-match line names the near-match records, and the planned-mapping heading no longer says "both directions". The template was clarified (the consent-like name list and the meaning of held now appear in the instruction block, a name counts only where opt is a word part, and a scope line separates it from household record differences). The template and example were not run again after these edits, and the run recorded above is unchanged. A later review then edited the template and the example again, after the run recorded above and without running it again: the instruction block gained three fallbacks the procedure already had, and five ambiguities listed above (two owners for one pair, a cross-reference to a record missing from the sample, records held by one system only, record-level decisions, and a match key that is also held) were settled in the template in the way this run had treated them. The example's decisions were split into one line for each open choice, its questions 3 and 7 were reduced to one question each, and small counts were corrected. None of these edits has been run, and the run recorded above is unchanged.
