# App data requirements

Capability template, version 0.1.0.

## Purpose

Turn the request notes for an internal app, the process owner's approved rules, the definitions of the objects the app will use and a few invented sample records into one data specification: the entities, the fields, who reads and who writes each field, the actions people take, and every name or verb that is still unresolved, each written as a question. Every line of the specification names the note, rule or file line that asks for it. The assistant specifies; it builds nothing, configures nothing, connects to nothing and uses no live data. It decides nothing the process owner has not decided, and it never fills a gap by guessing.

## When to use it and when not to

Use it when the requirements for an internal app leave fields or actions unclear and nobody has yet configured or built it, and again when the notes change, a rule is approved or questions have been answered.

Do not use it to write the testable behaviours of a story (that is the acceptance criteria sheet), to settle what a report or dashboard shows (that is the dashboard brief), to understand one unfamiliar export (that is the dataset profile), to build or configure the app, to draw screens, or to design the permissions policy. Do not use it with records taken from a live system: the sample records must be invented.

## Roles

- **Runs it:** the business systems analyst, who supplies the files and the settings.
- **Answers the questions and confirms the specification:** the process owner, the person who owns the process the app supports.
- **Decides what goes into the build:** the analyst and the process owner together. The assistant lists what is open.
- **Reviews the specification against the notes:** a second person, for the first runs.

## Inputs

Four files, as text, pasted tables or attachments, and the settings.

1. **`request_notes.txt`,** plain text with no header: one statement to a line, and line 1 is the first line. A line is cited as N plus its number (N3). A line that holds more than one statement is split in procedure step 2 and its parts are cited as N2a, N2b. If missing, stop.
2. **`process_rules.txt`,** the approved rules, one to a line, each beginning with its number as `R1:`, `R2:` and so on. If a line has no such number, stop and ask for one. If the file is missing, say "no approved rules supplied" in section 6 and continue from the notes alone.
3. **`object_definitions.csv`,** one row per field of the existing objects (tables, lists or record types) the app will use, with the default headers `object_name`, `field_name`, `data_type`, `required`, `description`. `data_type` is one of text, number, date, yes-no, choice. `required` is yes or no. The header is line 1. If the app has no existing objects, the analyst supplies the file with the header line only, and every name is then unmatched. If missing, stop.
4. **`sample_records.csv`,** invented records, with the default headers `sample_id`, `object_name`, `field_name`, `value`: one row per value, and all rows with the same `sample_id` make one sample record of one object. A blank value is a blank field. If missing, say "sample records not supplied" in section 7 and make no type checks.
5. **Settings,** typed by the analyst, one per line:
   - `App name:`
   - `Today:` the date.
   - `For:` who the specification is for. Default "the business systems analyst, to confirm with the process owner".
   - `Files:` the file names and dates.
   - `Sample records invented:` the analyst's confirmation. Without a yes, stop.
   - `Verb lists:` default, or the company's own lists for the four classes below.

Default verb classes:

- **Read:** see, view, show, list, look up, check, find, search, open.
- **Write:** log, record, enter, add, create, update, edit, change, set, mark, approve, delete, remove, cancel.
- **Message:** send, notify, remind, get a reminder, alert, email.
- **Unclear:** every other verb, and especially handle, manage, process, track, maintain, own, review, get, close, sync, submit, support, sort out, deal with, keep.

If a header in `object_definitions.csv` or `sample_records.csv` does not match the defaults in name and order, stop (procedure step 1). Do not guess a match and do not rename headers for the person.

## The procedure

1. **Check the files.** Compare the headers of the two CSV files with the defaults, by name and order. Count rows and fields per row. Stop and list the details if a header differs, if a row has a different number of fields, if a `data_type` or `required` value is outside the lists above, if the same `object_name` and `field_name` appear twice in the definitions (give both lines), if one `sample_id` holds two objects, or if a sample value looks real. A value looks real if it is an email address on a domain other than example.com, example.org or example.net, a phone number, a street address, a government or tax identifier, a card or account number, or a full person's name the analyst has not said is invented. Ask for invented replacements. Then count the lines of the notes, the rules, the field rows and objects, and the sample rows and records.
2. **Split the statements.** Take each line of the notes and each rule as a statement, and split it only at the end of a sentence and at an "and" that joins a second verb or a second event. "The office manager logs when someone takes an item and when it comes back" is N2a and N2b; "The standard loan is 7 days. A loan of more than 14 days needs a manager's approval before the item leaves the office." is R2a and R2b. Do not split at a comma, "who", "with", "normally" or an "and" that joins two nouns ("one item and one person"). A line with one statement keeps its plain reference (N3, R4). A reference without a letter (N2) means all its parts. Count the statements.
3. **Match the names.** Find every name the statements use for a thing: an object, a field, a status, or data a statement needs (repair, approval, condition, reminder). Do not list verbs, except an event verb that a listed verb records (step 4), which is matched as a name; do not list words for a view or list of records (history, list), or words for a value worked out from fields (long, overdue); steps 4 and 6 deal with those. Compare each name with the definitions in three grades.
   - **Exact:** the same text after lowercasing, turning every character that is not a letter or digit into a space, collapsing spaces and dropping a final plural s. Report the sources.
   - **By meaning:** no exact match, but the note's words and one definition's `description` plainly describe the same thing. Quote both, list the match for confirmation and write one question for all of them together. The definitions give an object no description of its own, so a by-meaning match to an object quotes the description of one of its fields.
   - **None:** anything else. Report it as having no match, with the existing names that share a whole word with it, or "no existing name shares a word". Never invent an object or field for it.
   - Several words for one thing (for example "staff", "someone" and "people" for Person) are listed together as a by-meaning match, never merged silently. One word that fits two objects, or an object and one of its fields, is listed as ambiguous and becomes its own question; do not choose between them. For example "equipment" could be Item or, from the description "Type of equipment", Item.category.
   - List the roles the statements name (staff, the office manager, a manager). The definitions rarely hold them; say whether they do.
4. **Sort the actions.** For each statement or part, in the notes or the rules, that says a role does something, make an action with its role, its verb class, the object and the fields it touches. Number the actions in the order of the references, notes first, then rules. Classify by the verb the role performs on the data, using the verb lists; a longer listed phrase beats a shorter word ("get a reminder" is Message, "get" alone is unclear). Where a statement holds a listed verb and an unlisted one, the listed verb decides and the unlisted one is the event it records ("logs when someone takes an item": logs is Write, and takes is matched as a name in step 3). A requirement that a role must give an approval counts as that role approving. A verb in the unclear class, a statement whose only verbs are on no list, or one that does not name what is read or changed, makes the action unclear: say so, name the object it acts on and write a question. If a statement names no actor, write "not stated". A message verb is recorded as a data need only (who receives it, when, what is kept); whether anything is sent is the process owner's and the app owner's decision.
5. **List the entities.** For each defined object: the lines of the definitions it occupies, its field count and the statements that use it. Then the names that are used but not defined.
6. **List the fields.** For each defined field that a statement names or plainly requires: type, required or not, definitions line, who reads it, who writes it, the rules that bear on it and the sample values (with lines).
   - Read and write come only from the statements. A role that sees something reads it; a role that logs, records, sets or approves it writes it. Where a statement does not say, write "not stated" and ask.
   - A field that another statement needs in order to be carried out may be listed as "implied" with the line that needs it (for example, a rule that an item in repair cannot be loaned needs the item's status to be read before a loan is logged). Never mark a field implied on a hunch.
   - Fields that are defined but never used are listed as "defined, not mentioned", with a question.
   - Data a statement needs that no definition holds is listed as "needed but not defined", with its sources.
   - Values that can be worked out from fields (a length in days, an overdue flag) are listed as "worked out, not stored", with the fields they use. Whether to store them is the process owner's choice.
7. **Check the rules.** For each rule, as a whole, naming its parts (R2a, R2b) where they differ, say whether the fields it needs exist: covered, partly covered (say what is missing) or not covered. If a rule and a note disagree, list both with their references and mark "needs a person's confirmation"; never choose.
8. **Check the sample records.** Count the values, filled and blank. For each field check the value against its type: text any non-blank; number digits with at most one decimal point; date written year-month-day with a real month and day; yes-no yes or no; choice any value, listing the distinct values seen, since the definitions give no allowed values. Report a blank in a required field. Check that a value that links two objects (a field of the same name in both) is found in the other. List defined fields missing from the samples and sample fields with no definition. Report any reading that the records raise (for example, two records that cannot both be right), as a reading, not a fault.
9. **Write the questions.** One numbered question for each open point, each with its references and values, answerable in a sentence. Combine the by-meaning matches into one question. The numbers follow the order in which the points are first met, and the sections cite them, so they need not run in section order. Offer no answer and propose nothing as an instruction.
10. **Write the decisions.** One numbered line per open choice, grouping questions that call for the same options, naming only the options that fit. Recommend none. Final line: confirming the specification with the process owner is the analyst's decision.
11. **Say what was not checked,** then end with the trace line.

## Exceptions and stop conditions

- **A header differs, a row has the wrong number of fields, a type is outside the lists, or a definition appears twice:** stop; list the differences with their lines; ask for the corrected file.
- **A sample value looks real, or the analyst has not confirmed the samples are invented:** stop; do not repeat the value; ask for invented replacements.
- **The notes or the definitions are missing:** stop and say which.
- **A verb is unclear, a name has no match, or one name fits two objects:** list it; write the question; never pick a meaning.
- **A note and a rule disagree:** list both; mark "needs a person's confirmation"; choose neither.
- **A figure or line number cannot be recomputed from the files:** leave it out and say so.
- **Asked to build or configure the app, create objects or fields, write an import file or a configuration, or run anything against a system:** decline; the analyst and the application owner do that.
- **Asked to use real records, to connect to a system, or to pick the right meaning for an unclear line:** decline; the process owner decides.
- **Asked for acceptance criteria, a dashboard brief, screens or a permissions policy:** decline; point to the acceptance criteria sheet or the dashboard brief, or leave it with the analyst.
- **Asked for a login, a password or a connection:** decline; work only from the files supplied.

## Output format

```
DATA SPECIFICATION: [app name]

For: [who]. Prepared [Today] from [file names with dates]. Nothing was built, configured or changed, and no live data was used.

1. THE FILES
Header check: [object_definitions.csv and sample_records.csv match the defaults in name and order / the differences, then stop]. request_notes.txt: [n] lines ([n] statements once split). process_rules.txt: [n] rules ([n] statements once split) / not supplied. object_definitions.csv: [n] field rows in [n] objects. sample_records.csv: [n] rows in [n] sample records / not supplied. Sample records confirmed invented by [who]. Verb lists: [defaults / typed lists].

2. NAMES
Matched exactly:
- "[wording]" ([references]) is [Object / Object.field].
Matched by meaning, to confirm (Question [n]):
- "[wording]" ([references]) is [Object / Object.field]: the note says "[quote]"; the definition says "[description]".
No match:
- "[wording]" ([references]): [existing names that share a word / no existing name shares a word]. Question [n].
Ambiguous:
- "[wording]" ([references]) could be [Object.field] or [Object.field]. Question [n].
Roles named: "[role]" ([references]). [Whether the definitions hold a role.] Question [n].
[Where a heading has nothing: None found.]

3. ENTITIES
- [Object] (object_definitions.csv lines [a] to [b], [n] fields): used by [references].
Named but not defined: [n]. [Names]. [What is open about each]: Question [n].

4. FIELDS
Needed ([n] of [n] defined fields):
- [Object.field] ([type], [required / not required], line [n]): Read by [role (reference)] / not stated. Written by [role (reference)] / not stated. Rule: [R-numbers]. Sample: [value] (sample line [n]). Question [n].
Defined, not mentioned in the notes or rules: [n]. [Object.field] ([type], [required], line [n]); sample [value] (sample line [n]). Question [n].
Needed but not defined: [n].
- [What] ([references]): [who reads, who writes, what is known]. Question [n].
Worked out, not stored: [what, from which fields, for which reference] / none.

5. ACTIONS
- A[n] [role / not stated]: [Read / Write, creates or updates / Message / Unclear]. [What is done]: [fields] ([references]). Question [n] where open.
Totals: [n] actions; [n] read, [n] write, [n] unclear or message.

6. RULES
- R[n]: [covered / partly covered / not covered]. [Fields that cover it; what is missing]. Question [n].
Totals: [n] rules; [n] covered, [n] partly covered, [n] not covered.
[If no rules were supplied: No approved rules supplied; this specification rests on the notes alone.]

7. SAMPLE RECORDS
Checked [n] values in [n] records ([sample ids and objects]): [n] filled, [n] blank ([fields and lines]; required or not).
- Text: [n] values, [all filled / the blanks].
- Number: [n] values, [which fit, which do not, with lines] / none.
- Date: [n] values. [n] fit ([field, value, line]). [n] do not ([field, value, line]). [n] blank.
- Yes-no: [as above] / none.
- Choice: [n] values ([field, value, line]). Allowed values are not in the definitions.
- Links: [value, line] matches [field, line] / has no match.
- Required fields blank: [list / none]. Sample fields with no definition: [list / none]. Defined fields missing from the samples: [list / none].
- [Any reading the records raise, with lines, and its question.]
[If not supplied: Sample records not supplied; no type checks were made.]

8. QUESTIONS FOR THE PROCESS OWNER
[n]. [Question with references and values.]
[If there are none: No questions; nothing was found.]

9. DECISIONS FOR THE PROCESS OWNER AND THE ANALYST
[n]. [Open choice (Questions [n]): the options that fit.]
Confirming this specification with the process owner is [the analyst]'s decision.

10. NOT CHECKED
[What the files cannot show.] No file was changed and no system was touched.

Every line number counts from line 1 of its file as supplied on [Today]; a sample line is a line of sample_records.csv. N is a line of request_notes.txt and R a rule in process_rules.txt (a letter after the number marks a part, as N2a), and S is a sample record in sample_records.csv. This specification builds nothing, configures nothing and uses no live data.
```

## Reviewer checklist

1. The header check is right: both CSV files match the defaults, or the work stopped. (Analyst)
2. The counts in section 1 (lines, rules, statements once split, field rows, objects, sample rows and records) match the files, and the field count in section 4 matches the definitions. (Second person)
3. Every field, action and rule cites a line of the notes, a rule or a definitions line, and "implied" is used only where a line needs the data. (Analyst)
4. Every by-meaning match quotes both sides and is listed for confirmation, and none is presented as exact. (Analyst)
5. Every unclear verb and unmatched name is a question, and no meaning has been chosen. (Process owner)
6. Reads and writes come from the statements; "not stated" appears wherever they are silent. (Analyst)
7. Every sample finding quotes the value and the line, and the totals in section 7 add up. (Second person)
8. No question offers an answer, and no decision is recommended. (Process owner)
9. Nothing in the specification builds, configures or sends anything, or asks for a login. (Analyst)

## Acceptance tests

They use the invented files in the example. Tests 2 to 6, 13 and 14 describe cases the example itself contains, and the trial of 10 November 2026 produced them; the others have not been run.

1. **Header mismatch.** Rename `data_type` to `type` in the definitions. Expected: stops after the header check and lists the difference; no later section.
2. **Counts.** Run the example. Expected: 7 note lines (8 statements once N2 is split), 4 rules (5 statements once R2 is split), 13 field rows in 3 objects, 13 sample rows in 3 records; 10 of 13 fields needed and 3 defined but not mentioned; 9 actions (2 read, 4 write, 3 unclear or message); 4 rules (1 covered, 3 partly covered).
3. **Unclear verb.** Keep "Managers handle the long loans." Expected: an unclear action on Loan with a question; no verb class chosen and no field assigned.
4. **Unmatched name.** Keep "condition" in R4 with no matching field. Expected: listed under No match, with "no existing name shares a word", and R4 partly covered.
5. **By meaning, not exact.** Note 3 says "due back date". Expected: listed under matched by meaning with both quotes, not under matched exactly.
6. **Sample type.** Keep the due date "next Monday". Expected: 1 of 3 date values fits, 1 does not (line 13), 1 is blank.
7. **Real-looking value.** Replace a sample name with a personal email address on a company domain. Expected: stops; asks for an invented replacement; does not repeat the value.
8. **Duplicate definition.** Add a second `Loan,date_due` row. Expected: stops and gives both lines.
9. **Rule and note disagree.** Change R2 to a 10-day standard loan while note 3 still says a week. Expected: both listed, marked "needs a person's confirmation", neither chosen.
10. **No rules file.** Remove `process_rules.txt`. Expected: section 6 says no approved rules were supplied, and the rest continues from the notes.
11. **Asked to build.** Ask for the field definitions as an import file. Expected: declines and leaves the build to the analyst.
12. **Asked for acceptance criteria.** Expected: declines and points to the acceptance criteria sheet.
13. **One word, two meanings.** Keep "shared equipment" in note 1 with Item.category described as "Type of equipment". Expected: "equipment" is listed under Ambiguous as Item or Item.category, with its own question, and is not listed as matched.
14. **A due date nobody sets.** Keep note 3 as written. Expected: Loan.date_due is "Written by: not stated", with a question, because the note names no actor.

## Instructions for the AI assistant

```
You prepare a data specification for an internal app request, for the
business systems analyst to confirm with the process owner. You never build
or configure anything, never send or change anything, never connect to a
system, and never decide a meaning the process owner has not given.

The user will supply: request_notes.txt (one statement per line, no header);
process_rules.txt (rules numbered R1, R2...); object_definitions.csv with
the headers object_name,field_name,data_type,required,description;
sample_records.csv with the headers sample_id,object_name,field_name,value;
and settings (app name, date, who it is for, files, a confirmation that the
sample records are invented, verb lists). If the notes or the definitions
are missing, stop. If a header in either CSV file does not match, in name and
order, stop, list the differences and ask for a corrected file; do not guess
and do not rename headers. Also stop on a wrong field count, a type outside
text, number, date, yes-no, choice, a repeated object and field in the
definitions, a required value other than yes or no, one sample_id holding
two objects, or a sample value that looks real (an email on a real domain,
a phone number, an address, an identifier, a card number, an unconfirmed
person's name). Never repeat such a value.

Default verb lists, unless the user types their own:
- Read: see, view, show, list, look up, check, find, search, open.
- Write: log, record, enter, add, create, update, edit, change, set, mark,
  approve, delete, remove, cancel.
- Message: send, notify, remind, get a reminder, alert, email.
- Unclear: every other verb, and especially handle, manage, process, track,
  maintain, own, review, get, close, sync, submit, support, sort out,
  deal with, keep.

1. Count the lines, rules, field rows, objects, sample rows and records.
2. Split each note line and each rule only at the end of a sentence and at
   an "and" that joins a second verb or a second event (N2a, N2b; R2a,
   R2b). Do not split at a comma, "who", "with", "normally" or an "and"
   between two nouns. A line with one statement keeps its plain reference
   (N3, R4); a reference without a letter means all its parts. Count the
   statements.
3. Match every name for a thing (an object, a field, a status, or data a
   statement needs) to the definitions: exact (lowercased, punctuation
   removed, final plural dropped), by meaning (quote the note and the
   description of a field, since objects have none, and list it for one
   confirming question), or no match (name the existing names sharing a
   whole word). A word that fits two objects, or an object and one of its
   fields, is ambiguous: list it with its own question and choose neither.
   Do not list verbs, except an event verb that a listed verb records
   (step 4), which is matched as a name; do not list words for a view of
   records (history, list) or values worked out from fields (long,
   overdue). Never invent an object
   or a field. List the roles named.
4. Sort each action by its verb, using the lists above; a longer listed
   phrase beats a shorter word ("get a reminder" is Message, "get" alone
   is unclear). Where a statement
   holds a listed verb and an unlisted one, the listed verb decides and the
   unlisted one is the event it records. A requirement that a role gives an
   approval counts as that role approving. Unclear verbs, and statements
   whose only verbs are on no list, become questions with the object
   named. Number the actions in the order of the references, notes first,
   then rules. A message is only a data need; whether anything is sent is
   for people to decide.
5. List the entities and the names used but not defined.
6. List each needed field with type, required, definitions line, who reads
   it, who writes it, rules and sample values. Take reads and writes only
   from the statements; write "not stated" where they are silent; mark a
   field "implied" only with the line that needs it. List defined fields
   never mentioned, data needed but not defined, and values worked out
   rather than stored.
7. Check each rule as a whole, naming its parts where they differ: covered,
   partly covered or not covered. If a note and a rule disagree, list both,
   mark "needs a person's confirmation", and choose neither.
8. Check the sample values against the types, the links between objects,
   blanks in required fields, and defined fields missing from the samples.
   Quote value and line.
9. Write one numbered question per open point, answerable in a sentence,
   with references and values, offering no answer. Number them in the order
   the points are first met; the sections cite the numbers.
10. Write the decisions with the options that fit, recommend none, and end:
    confirming the specification with the process owner is the analyst's
    decision.
11. Say what was not checked. Use the output format exactly, with every
    section and every heading in order, printing "None found" with what was
    checked where a heading is empty, and end with the trace line.

Decline to build or configure the app, to create objects or write an
import file or configuration, to use real records, to choose the meaning of
an unclear line, to write acceptance criteria, a dashboard brief, screens or
a permissions policy, or to connect to a system. Ask for no password, login
code or connection; work only from the files supplied.
```

## What to customize

- The verb lists: which verbs your company uses to mean reading, writing and sending, and which it treats as unclear.
- The file names and column headers, if your exports differ; rename the headers before the run, since a mismatch stops it.
- What counts as a sample value that looks real, by your own data rules.
- The roles you expect in the notes, and who plays the process owner and confirms.
- Who may read and change the specification, and where the answers to the questions are recorded.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. It was tried on its invented example in Claude on 10 November 2026; the record is published with it. That first run showed that the example stated things the notes do not (who sets the due date, which fields the loan history reads, and two fields counted as needed that no line asks for), that the example left out two headings the format requires, and that the procedure could not produce the counts in the second acceptance test. The template and the example were then changed: statements are split by one stated rule, the full verb lists are in the instructions, a word that fits an object and one of its fields is ambiguous, and the counts were corrected. The edited version was run once more on the example by the assistant that made the edits, not independently. It has not been tested in a client environment.
