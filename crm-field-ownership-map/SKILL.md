---
name: "crm-field-ownership-map"
description: "Prepare, before a CRM sync or field mapping changes, one field map for two systems from the exports and sample records the systems owner supplies. For each pair of fields the map gives the authoritative source, the role the field plays in matching records, and the conflict rule, and it says what each of these rests on. Conflicting identity keys, consent fields, duplicates that match more than one record and every field the definitions leave open become numbered questions for the field's business owner. The assistant prepares and proposes; it connects to no system, never changes a mapping, never merges or edits a record, never moves data and never decides a source the definitions do not name."
license: "MIT"
metadata:
  version: "0.1.0"
  publisher: "Fully Powered AI"
  capability: "CRM field ownership map"
---

# CRM field ownership map

This is the technical file for a Fully Powered capability template. It carries the instructions an AI product follows. The complete template, with roles, inputs, exceptions, the reviewer checklist, acceptance tests and what to customize, is in [TEMPLATE.md](TEMPLATE.md). A worked example with invented data is in [EXAMPLE.md](EXAMPLE.md).

## Instructions

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

## Before relying on it

Decide every item under "What to customize" in TEMPLATE.md and set the limits the instructions in this file leave open, written in square brackets such as [N], to your own. Then run the acceptance tests in TEMPLATE.md on past work. A person starts this work, supplies the inputs and decides what happens with the result.
