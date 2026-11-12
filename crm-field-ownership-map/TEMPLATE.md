# CRM field ownership map

Workflow template, version 0.1.0.

## Purpose

Prepare, before a CRM sync or field mapping changes, one field map for two systems from the exports and sample records the systems owner supplies. For each pair of fields the map gives the authoritative source, the role the field plays in matching records, and the conflict rule, and it says what each of these rests on. Conflicting identity keys, consent fields, duplicates that match more than one record and every field the definitions leave open become numbered questions for the field's business owner. The assistant prepares and proposes; it connects to no system, never changes a mapping, never merges or edits a record, never moves data and never decides a source the definitions do not name.

## When to use it and when not to

Use it when a sync between a CRM and one other system is about to be switched on, widened or rewired, when a field is about to join a mapping, or when the same customers are held in two systems and the shared fields need an owner before the two are connected. It covers one pair of systems and one pair of objects (such as contact and customer) at a time.

Do not use it:

- to understand a single export before relying on it. That is the dataset profile workflow template;
- to explain why two reports give different numbers. That is metric definition reconciliation;
- to plan a dashboard. That is the dashboard brief;
- to compare a wealth-management CRM with a custodian's records household by household. That is household record differences;
- to clean, merge or de-duplicate records, to write a mapping into a tool, or to run or test a sync;
- on records the person is not entitled to share with the assistant. Use invented or masked records where the real ones are sensitive.

## Roles

- **Runs it:** the systems owner or CRM administrator, who supplies the files and settings.
- **Answers the questions:** the business owner named for each field in the definitions, such as a sales operations lead, a finance lead or a head of marketing.
- **Approves the mapping:** the integration owner named in the settings, together with those field owners.
- **Makes every change** in the tools themselves: people with the right access, after approval.

## Inputs

1. **Schema exports,** one for each system or one file holding both. Default headers: `system`, `object`, `field`, `type`, `required`, `allowed_values`. One line per field.
2. **Approved definitions,** one line per field per system. Default headers: `system`, `field`, `meaning`, `business_owner`, `system_of_record`. The last column holds the system that is the source for that field, or is blank where nothing has been decided. A field with no definition is a finding, not a gap to fill.
3. **Planned mapping.** Default headers: `crm_field`, `other_field`. One line per pair the change would connect. If none is supplied, ask once for it; do not pair fields by name alone. If the person cannot supply it, offer fields whose definitions have the same meaning text as "possible pairs, not confirmed" and go on with those.
4. **Sample records,** one file per system, as CSV rows with the header as line 1. The header must hold the field names of the schema export. If they are a sample, the person says so.
5. **Settings,** one per line:
   - `Today:` the date.
   - `Planned change:` one sentence, including which way the sync would write.
   - `Systems:` the name and object of each side.
   - `Samples:` how the samples were chosen and whether they are the full tables.
   - `Match key candidates:` the fields to test as keys, including any stored cross-reference to the other system. If missing, ask once; if unknown, offer the fields that are unique and filled in both samples, labelled "candidate keys, observed, not confirmed".
   - `Consent fields:` the fields that record a person's agreement or refusal. If missing, ask once. Any field whose name contains consent, unsubscribe, gdpr or marketing, or contains opt as a word part (opt_in, optout, but not optional or option), and is not named is listed as "looks like a consent field, not named" and becomes a question.
   - `Counts-only columns:` default none. For these, report counts and line numbers and print no values anywhere.
   - `Integration owner:` who approves. Default "the integration owner".

If a header in any file does not match the default headers above, or a sample's header does not match its schema export's field names, stop and ask (procedure step 1).

## The procedure

1. **Check the files.** Compare each file's headers with the defaults, and each sample's headers with the schema export's field names, by name. If any are missing, extra or different, or a row has a different number of fields, stop: list the differences or line numbers and ask whether to correct the file, rename a column or supply the right file. Do not guess a match. Then check the definitions cover every schema field (list any that do not) and that every field in the planned mapping exists in its schema (list any that do not). State whether each sample is a sample or a full table, as the person says.
2. **Pair the fields.** Pair only what the planned mapping states. A match on name alone is never a pair. Fields in one system that no pair names go in the one-system-only list.
3. **Name the source for each pair.** Take the `system_of_record` from the two definitions. If both name the same system, the source is that system, basis "stated". If one names a system and the other is blank, take the named one and say the other was blank. If both are blank, the source is open. If they name different systems, the source is open and the disagreement is stated. For a field that only one system holds, the source is the system that stores it if its definition says so. Never choose a source from the sample data, from which system fills more rows, or from the field's name.
4. **Set the role and the proposed rule.** The role is match key (named in the settings), key link (a stored cross-reference), consent field (named, or flagged by step 8), or ordinary field. The proposed rule is: "[System] wins; the other system does not write this field" where the source is stated and the field is not a consent field; "copies from [System] and does not write back" for a key link with a stated source; and "held" (no write in either direction until the owner decides) for every open source and every consent field. A rule is a proposal for the owner to approve. The role and the rule are independent: a match key whose source is open keeps the role "match key" and its rule is "held", and the key is still used to test matches in the map.
5. **Compare the schemas.** For each pair, state the types and allowed values on both sides and whether the field is required on each side. State differences in type, allowed values or requirement. Where a difference shows in the samples, give the lines; where no sample row shows it, say so.
6. **Test the match keys.** For each key candidate, in each sample: filled count, distinct count, blank lines, and repeated values with their line numbers. Compare exactly as written. Then list the record pairs that match exactly across the two samples, numbered, with line numbers. List separately any records that would match only if capitals and surrounding spaces were ignored; leave them out of every later comparison and raise a question. List records with no match in each sample. For a stored cross-reference, count the values found and not found in the other sample, and for each record with both an exact key match and a cross-reference, say whether the two name the same record.
7. **Compare the paired fields on the matched pairs.** For each pair of fields, over the numbered record pairs: how many compared, how many agree exactly, how many differ (with line numbers and both values), how many have one side blank. A value is blank only if empty or only spaces. Count each record pair, including pairs that share one record. Do not compare near-match records.
8. **Duplicates, ambiguous matches and consent.** In each sample list records that share a key value: identical rows, or same key with differing values (name the columns that differ and the columns that agree). A record in one sample that matches more than one record in the other, or the reverse, is an ambiguous match. Do not choose a record or suggest a merge. List key conflicts (a cross-reference naming a different record than the key does, including one that names a record not in the other sample, with that reason stated). For consent fields, give the comparison from step 7 and the fields flagged as looking like consent but not named.
9. **Write the questions.** One numbered question for each open point: open or disagreeing sources, key conflicts, near-matches, blank values in a required key, duplicates and ambiguous matches, consent disagreements, and requirement differences. Group them by the business owner in the definitions, in alphabetical order of the owner, numbering continuously. Each question gives the lines and values and can be answered in a sentence. Offer no answer. A point whose owner is not in the definitions goes under "No owner named". Where a pair has two owners, put each question under the owner of the field it concerns. Records with no match in the other sample get no question; they are listed in section 3 and named in "not checked".
10. **Write the decisions** for the integration owner, one numbered line for each open choice (each field block with an open point, and one line for record-level choices such as duplicates, ambiguous matches, near-matches and key conflicts), naming the answers it waits on and the options that fit (approve as proposed, change, hold out, wait). Make no recommendation beyond the proposed rules already in the map. End by saying the integration owner approves the mapping with the field owners and the map changes nothing.
11. **Say what was not checked,** and end with the trace line.

## Exceptions and stop conditions

- **A header does not match, a field named in the mapping or the samples does not exist, or rows have different field counts:** stop, list the differences, ask.
- **No definitions, or no schema export:** stop and ask. The map is only as good as the definitions supplied.
- **No planned mapping:** ask once; do not pair by name alone.
- **A named key candidate is not a field in a sample:** stop and ask.
- **Samples that may be cut off or are not from the objects named:** say so at the top and say the counts describe the rows supplied only.
- **A column is marked counts-only:** print no values for it in any section, question or decision.
- **Asked to choose a source where the definitions do not name one:** decline; write it as a question for the owner.
- **Asked to merge, correct or remove records, to write the mapping into a tool, to run or test the sync, or to connect to a system:** decline; the map is the output, and people make every change after approval.
- **Asked for a login, a password or a connection:** decline; work only from the files supplied.
- **Asked to say whether the sync is safe to switch on:** decline; list the open questions and decisions.
- **More than ten line numbers or keys for one finding:** list ten and give the count of the rest.
- **A figure cannot be recomputed from the rows supplied:** leave it out and say so.

## Output format

```
CRM FIELD OWNERSHIP MAP: [CRM system and object] and [other system and object]

For: [Integration owner]. Prepared [Today] from the settings, schema exports, definitions, planned mapping and samples supplied. Planned change: [sentence].

1. THE FILES
Header check: [all files have the headers expected, and each sample's headers match its schema export / the differences, then stop]. [Definitions: n rows, covering n of n schema fields; any field without a definition.] [Planned mapping: n pairs; any field not in its schema.]
Samples: [n] [system] rows (lines [..]) and [n] [system] rows (lines [..]), [sample / full table], as stated. Every count below describes these rows only. Line numbers count the header as line 1.

2. FIELD MAP
Key, for [system] and [other system]: stated = the definitions name the source; open = no source named, or the two definitions disagree. Where a source is open, the proposed rule holds the field out of the sync in both directions until its owner answers.
F[n]. [field] <-> [field] ([role]). Owner: [business owner; where the two definitions name different owners, both, each with its field]. Source: [system, basis / open, reason]. Proposed rule: [rule]. Schema: [types, required on each side, differences]. Matched pairs: [n] compared, [n] agree, [n] differ ([pair, line, both values]), [n] with one side blank ([lines]). [Question numbers.]
[One block per pair in the planned mapping, in the mapping's order. A pair that is only a possible pair says so.]
One-system fields ([system] and [other system]; in no pair of the planned mapping, so the change would not touch them):
[system field (role, source, owner): filled, distinct, values and counts where it has a list / none]
Fields without a definition: [list / none].

3. MATCH KEYS
[Key candidate], compared exactly as written:
[System]: [n] filled, [n] distinct, [n] blank ([lines]). Repeated: [value (lines) / none].
[Other system]: [same].
Matched exactly: [n] rows ([lines]) to [n] rows ([lines]), so [n] record pairs: [pair 1 lines; pair 2 lines; ...].
Match only if capitals and surrounding spaces are ignored: [lines and values / none]. Left out of the comparisons in section 2.
No match: [system lines]; [other system lines] / none.
[Cross-reference, if any: filled, distinct, blanks, repeated; found and not found in the other sample; agreement with the exact key match.]

4. DUPLICATES AND AMBIGUOUS MATCHES
Same key, different values: [lines; columns that differ with values; columns that agree; which records in the other sample they match / none found].
Identical rows: [lines / none found in either sample].
[Ambiguous matches in the other sample: lines / none.]

5. KEY CONFLICTS
[Lines, the two keys that disagree / none found.]

6. CONSENT FIELDS
Named: [fields]. [Fields that look like consent but are not named: list / none.]
Matched pairs: [n] compared, [n] agree, [n] differ ([pair, lines, values]), [n] with one side blank.
Proposed rule for [consent fields]: held, with no write in either direction. The map sets no other rule for a consent field; the owner decides.

7. QUESTIONS FOR THE FIELD OWNERS
[Business owner]
[n]. [Question with lines and values.]
[Next owner, continuing the numbering.]
[If none: "No questions arise from the findings."]

8. DECISIONS FOR THE INTEGRATION OWNER ([name or role]), with the field owners
[n]. [Open choice, the answers it waits on, the options that fit.]
[If none: "No decisions are open."]
Approval of the mapping belongs to [Integration owner] with the field owners; the map itself changes nothing.

9. NOT CHECKED
[Whether the values are true; rows outside the samples; other objects or fields; how the sync tool resolves conflicts by default; the effect of a rule on the full tables; anything the person left out.] No mapping has been changed and no data moved.

Every figure counts the [n] [system] rows and [n] [system] rows supplied on [Today]. This map connects to no system, changes no mapping and moves no data.
```

When a section has no findings, print its heading, what was checked and "none found", never a blank.

## Reviewer checklist

1. Every header check, row count and filled or distinct count can be reproduced from the files. (Systems owner)
2. Every line number points to the row described, counting each header as line 1. (Systems owner)
3. Every source named in the map is one the definitions name, and the basis is given; none is inferred from the samples. (Systems owner)
4. The record pairs are numbered, and every agree and differ count recomputes from them. (Systems owner)
5. Near-matches are listed and left out of the comparisons. (Systems owner)
6. Every consent field, key conflict, duplicate and open source has a question, addressed to the owner the definitions name. (Field owners)
7. Every question can be answered in a sentence and offers no answer. (Field owners)
8. Every field that is held is held in both directions, and no consent field carries a rule other than held. (Integration owner)
9. Nothing was changed, merged or corrected, and no mapping was written. (Systems owner)
10. Counts-only columns show no values. (Systems owner)

## Acceptance tests

Proposed tests. None has been run.

1. **Header mismatch.** The schema lists `email` and the sample has `email_address`. Expected: stops and lists the difference; no map.
2. **Definition without a source.** Both definitions blank for a field. Expected: source open, rule held, a question for the owner.
3. **Definitions disagree.** One names the CRM, the other the other system. Expected: source open, the disagreement stated, a question.
4. **Name-only look-alike.** Two fields with similar names, not in the planned mapping. Expected: not paired; listed as held by one system only.
5. **Repeated key.** Two records in one sample share the key. Expected: reported as same key, different values, with the differing columns; the ambiguous match listed; no record chosen; a question.
6. **Near-match key.** Same email apart from capitals and a trailing space. Expected: listed separately, left out of the comparisons, a question.
7. **Cross-reference conflict.** A stored id names a different record than the email does. Expected: reported as a key conflict with both keys; a question.
8. **Blank required key.** A required key is blank in one record. Expected: the line is listed; a question; no match is made for it.
9. **Consent disagreement.** A consent field differs on matched pairs. Expected: counts and lines; rule held; a question.
10. **Unnamed consent-like field.** A field called `unsubscribed_at` not named in the settings. Expected: listed as looks like a consent field, not named; a question.
11. **Counts-only column.** A column marked counts-only appears in a difference. Expected: counts and lines, no values.
12. **Asked to merge or write the mapping.** Expected: declines; points to the decisions for the integration owner.
13. **Asked to pick a source where the definitions are silent.** Expected: declines; writes the question.
14. **Asked "is it safe to switch on?"** Expected: declines; lists the open questions and decisions.

## Instructions for the AI assistant

```
You write a CRM field ownership map for a systems owner, from files they
have supplied: schema exports, approved definitions, a planned mapping,
sample records from two systems and some settings. You connect to no
system. You never change a mapping, merge, correct or remove a record, or
move data, and you never name a source the definitions do not name. The
integration owner approves every mapping, with the business owner of each
field, and people make every change in the tools after that approval. You
never ask for a password, a login code or a connection; you work only from
what is supplied.

Default headers. Schema exports: system, object, field, type, required,
allowed_values. Definitions: system, field, meaning, business_owner,
system_of_record. Planned mapping: crm_field, other_field. Samples: CSV
with the header as line 1, whose names match the schema export's fields.
Settings, one per line: Today, Planned change, Systems, Samples, Match key
candidates, Consent fields, Counts-only columns (default none), Integration
owner (default "the integration owner"). A field not named as consent whose
name contains consent, unsubscribe, gdpr or marketing, or opt as a word part
(opt_in, optout, not optional or option), is listed as "looks like a consent
field, not named" and becomes a question. If the schema export, definitions
or samples are missing, stop and say so. If the planned mapping, the match
key candidates or the consent fields are missing, ask once; never pair
fields by name alone; if the person cannot supply a mapping, offer fields
whose definitions have the same meaning text as "possible pairs, not
confirmed" and go on with those; if the person does not know the keys,
offer fields unique and filled in both samples, labelled "candidate keys,
observed, not confirmed". List at most ten line numbers or keys for any
one finding, then give the count of the rest.

1. Check the files. Compare headers with the defaults, and each sample's
   headers with the schema export's field names. If any differ, or a
   named field does not exist, or rows have different field counts, stop,
   list the differences and ask. Check that every field in the planned
   mapping is a listed item in its schema. List schema fields with no
   definition. Say whether each sample is a sample or a full table, as
   stated.
2. Pair only the fields in the planned mapping.
3. Source for each pair, from the two definitions' system_of_record: both
   name the same system, that system (stated); one names a system and the
   other is blank, the named one, noting the blank; both blank, open;
   different systems, open, and state the disagreement. Never choose a
   source from the samples, from fill rates or from names.
4. Role: match key, key link, consent field or ordinary. Proposed rule:
   "[System] wins; the other system does not write this field" where the
   source is stated and the field is not a consent field; "copies from
   [System] and does not write back" for a key link with a stated source;
   "held" (no write in either direction until the owner decides) for every
   open source and every consent field. Role and rule are independent: a
   match key with an open source stays a match key and is held.
5. Compare schemas: types, allowed values and whether required, on each
   side. State differences and the lines where the samples show them, or
   that no row shows them.
6. Match keys: per sample, filled, distinct, blank lines, repeated values
   with lines, compared exactly as written. List numbered record pairs
   that match exactly, then records that would match only ignoring
   capitals and surrounding spaces (leave them out of every later
   comparison), then records with no match. For a stored cross-reference,
   found and not found in the other sample, and whether it names the same
   record as the key.
7. For each pair of fields, over the numbered record pairs: compared,
   agree, differ (lines and both values), one side blank. Count every
   record pair, including pairs that share a record.
8. List identical rows and same-key-different-values groups (columns that
   differ and agree), ambiguous matches, key conflicts (including a
   cross-reference to a record not in the other sample, with that reason),
   and consent comparisons, plus fields that look like consent but are not named. Do
   not choose a record or suggest a merge.
9. Write one numbered question per open point, grouped by the business
   owner in the definitions in alphabetical order, numbering continuously,
   each with lines and values, answerable in a sentence, offering no
   answer. A point with no owner named goes under "No owner named". A pair
   with two owners: each question goes under the owner of the field it
   concerns. Records with no match get no question; list them in section 3
   and name them in "not checked".
10. Write one numbered decision per open choice for the integration owner
   (each field block with an open point, and one for record-level choices
   such as duplicates, near-matches and key conflicts), naming the answers
   it waits on and the options that fit (approve as
   proposed, change, hold out, wait). Recommend nothing beyond the proposed
   rules. Say the integration owner approves with the field owners and the
   map changes nothing.
11. Say what was not checked, then end with the trace line.

Use the output format exactly. If a sample may be cut off or may not be
from the objects named, say so at the top and say the counts describe the
rows supplied only. Where a section has no findings, print its heading,
what was checked and "none found". For counts-only columns print
counts and line numbers and no values. Recompute every figure from the
rows; if one cannot be recomputed, leave it out and say so. If asked to
choose a source the definitions do not name, merge or correct records,
write the mapping into a tool, run the sync, or say whether it is safe to
switch on, decline and point to the questions and decisions.
```

## What to customize

- Your definitions, kept as a standing file with an owner and a source system for every field.
- The columns of your exports, if they differ from the defaults, and the match keys you test.
- Which fields hold consent, and which columns must appear as counts only.
- The rules you allow: for example, whether a source system ever yields to a newer value. As written, only a stated source wins and everything else is held.
- Who approves a mapping, and who answers for each field when its owner is away.
- Where maps are filed, and which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI from its own published map of the work. Editorially reviewed. Tried on its invented example in Claude on 10 November 2026; the record is published with it. After that run the example was corrected (a wrongly listed one-system field, missing counts and missing questions) and the template was clarified (the consent-like name list and the meaning of held are stated in the instruction block, and a name counts only where opt is a word part, not optional or option). A later review added the missing fallbacks to the instruction block and settled five points the trial found open (two owners for one pair, a cross-reference to a record missing from the sample, records held by one system only, record-level decisions, and a match key that is also held). The edited version has not been run again. Not yet tested in a client environment and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
