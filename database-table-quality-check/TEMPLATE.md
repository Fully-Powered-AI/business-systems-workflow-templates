# Database table quality check

Workflow template, version 0.1.0.

## Purpose

Check one table your team keeps its records in against the rules its owner has written down, and give the owner one numbered findings sheet: keys used twice, rows that look like the same record, required fields left blank, values that are not on the allowed list, dates and numbers in the wrong form, and links that point to a record the linked table does not hold. Each finding carries its row references and a count, and the sheet opens with a row count that shows every row was read. Where the owner's rules are silent, the sheet asks rather than guesses. The assistant reads an export and reports; it changes no record, merges nothing, deletes nothing and never connects to the database tool. A person fixes the table.

## When to use it and when not to

Use it once a month on any table the team relies on (customers, assets, projects, stock, members, suppliers), and always before the table is moved to another tool, before a report is built on it, and before an automation starts reading or writing it.

Do not use it to design a table or decide what fields an app needs (that is the app data requirements template), to take an analyst's first look at an unfamiliar extract (that is the dataset profile, a different reader and a different moment from the owner's recurring check), to explain why two reports give different numbers (that is the metric definition reconciliation), or to clean, merge or correct the table. Do not use it on an export the person is not entitled to share with the assistant.

## Roles

- **Runs it:** the table's owner, usually the operations or systems owner, or someone they ask. They export the table, write the rules once and supply the settings.
- **Decides every fix:** the table's owner. For each finding the owner chooses whether to correct the record, leave it as it is, or ask the person who entered it.
- **Makes the fixes:** a person with edit rights in the database tool, after the owner has decided. The assistant makes none.
- **Answers the rule questions:** the table's owner, who updates the rules file so the next run has them.

## Inputs

Up to three files, as CSV text, pasted tables or attachments, and the settings.

1. **The table export from the database tool your team keeps its records in** (default name `table_export.csv`). Every record and every field of one table, with the column names on line 1 exactly as the tool writes them. Line 2 is the first record. It must be the whole table, not a filtered view. If it is missing, stop.
2. **The table's rules** (default name `table_rules.csv`), written once by the owner and kept for every later run, one row per column of the export, with the default headers `field`, `required`, `key`, `allowed_values`, `format`, `links_to`:
   - `field`: the column name exactly as it appears on line 1 of the export.
   - `required`: `yes` or `no`. Blank means the owner has not said; the field is checked as not required and a question is written.
   - `key`: `yes` on exactly one row, the field that should be different on every record; `no` or blank on the rest.
   - `allowed_values`: the allowed values separated by `|`, written exactly as they should appear, or blank for any value.
   - `format`: one of `text`, `whole number`, `number`, `date YYYY-MM-DD`, `date DD/MM/YYYY`, `date MM/DD/YYYY`. Blank is read as `text` and a question is written.
   - `links_to`: blank, or the linked table and its field as `table.field` (for example `sites.site_id`), meaning every filled value in this field must exist in that field of that table.
   If the rules file is missing, stop and ask for it; do not work out rules from the data.
3. **The linked table's export** (optional), one file per table named in `links_to`, called `<table>.csv`, with its column names on line 1. If it is not supplied, that link is reported as not checked, and the rest goes on.
4. **Settings,** typed by the owner, one per line:
   - `Table name:` as the team calls it.
   - `Today:` the date.
   - `For:` who the sheet is for. Default "the table's owner".
   - `Reason:` monthly check, before a migration, before a report, or before an automation.
   - `Files:` the file names and the date each was exported.
   - `Rows in the database tool:` the record count the tool itself shows for the table, if the owner can see it. Default "not supplied".
   - `Likely-duplicate fields:` up to three fields that, read together, point to the same real thing (a serial number; a name with a postcode). Default none.
   - `Placeholders:` words the team uses in place of a value. Default `N/A`, `n/a`, `NA`, `-`, `TBD`, `unknown`, `none`, `null`, `?`.

If the rules file's own headers differ from the defaults in name or order, or if the export's column names and the rules' `field` values do not match one for one, stop (procedure step 1). Do not guess which column is which and do not rename anything.

## The procedure

1. **Check the headers.** Compare the rules file's headers with the defaults, by name and order. Then compare the export's column names with the rules' `field` values, exactly as written, including capitals and spaces. Stop, list every difference and ask the owner to correct the rules or supply the right export if any of these holds: a column of the export has no rule row; a rule row names a field the export lacks; a `required` or `key` value is not `yes`, `no` or blank; a `format` is not on the list; more than one row is marked as the key; a `links_to` table has been supplied but its export lacks the named field. Also stop if two rule rows name the same field.
2. **Count the rows.** Count the lines of the export, the data rows (lines minus the header) and the fields on every row. If any row has a different number of fields from the header, stop and give its line numbers. If `Rows in the database tool` is given and differs from the data rows counted, stop and say both numbers: the export may be filtered or cut off. Count the rows of each linked export the same way. Every later section states how many rows or values it read, so the reader can see none was skipped.
3. **Duplicate keys.** If no field is marked as the key, check no keys, say so in section 2 and write a question. Otherwise compare every non-blank key value exactly as written. A blank key is not a finding here: the Blank keys line points to its finding in section 4, or says none. Each key value found on more than one row is one finding: its lines, and the fields where those rows differ and where they agree, compared as written. Never say which row is the real one.
4. **Likely duplicates.** Make a comparison form of a value: lower case, with every character that is not a letter or a digit removed. Two or more rows with different keys are a likely duplicate group when their keys have the same comparison form, or when every likely-duplicate field in the settings is filled on all of them and has the same comparison form. Rows already reported together in step 3 are not repeated here. Each group is one finding: its lines, the matching values as written, and the fields other than the key where the rows differ and agree (the key always differs and is not listed). If no likely-duplicate fields are set, say so and check the keys only.
5. **Blanks in required fields.** For every field marked `required: yes` and for the key, count the values that are empty or only spaces, and separately the values that are a placeholder. A key that is also `required: yes` is one field and is counted once. A blank key is a finding here, once, and only here. Each field with any is one finding, with its lines. A zero is a value, not a blank.
6. **Values outside the allowed list.** For every field with `allowed_values`, compare each filled value with the list exactly as written. Each field with any value outside it is one finding, listing the lines and values; a value that would match if capitals and outer spaces were ignored is marked "differs only in capitals or spaces". Blanks are left to step 5.
7. **Dates and numbers in the wrong form.** For every field with a date or number format, check each filled value. A date must be written in the field's format, with a month from 1 to 12 and a day that exists in that month and year (29 February only in a leap year). A whole number is digits with an optional leading minus. A number is digits with at most one decimal point and an optional leading minus, with no currency sign, thousands separator, unit or word. Each field with any failure is one finding, listing the lines, the values and what is wrong with each. Never rewrite a value into the right form.
8. **Links that point to no record.** For every field with `links_to` whose linked export was supplied, look up each filled value, exactly as written, in the named field of the linked table. Each field with any value that is not found is one finding, listing the lines and values. Blanks are left to step 5. If the linked export was not supplied, say "not checked" with the number of filled values that would have been looked up.
9. **Number the findings.** Number them F1, F2 and on, in section order (steps 3 to 8), and in each section by the order the fields appear in the export. Each finding gives its field, what is wrong, the count of rows and every line reference with the key value in brackets. If a finding covers more than 50 rows, give the first 50 lines and the count of the rest, and say the full list is available on request.
10. **Summarise.** Count the findings in each section, the row references in all, and the rows with at least one finding out of the data rows. Name the rows with none only as a count.
11. **Write the rule questions.** Give a rule's place as its line in the rules file, counting the header as line 1, so the first rule is line 2 ("table_rules.csv line 3"). One numbered question for each field whose rule has a gap (`required` blank, `format` blank, or both), in export order, naming the gaps; no finding waits on a question, because a blank `required` or `format` is checked by a default and no finding depends on the answer; then one if no field is marked as the key. Each question can be answered in a sentence and offers no answer.
12. **Write the owner's decisions,** then what was not checked, then the trace line: the final line of the output format, "Line numbers count from line 1 of ...".

## Exceptions and stop conditions

- **A header does not match, a rule value is not on its list, two rows are marked as the key, or a rule names a field twice:** stop after section 1; list each difference with its line; ask for the corrected file.
- **A row has the wrong number of fields:** stop; give the lines.
- **The tool's row count differs from the rows in the export:** stop; give both counts; ask whether the export is the whole table.
- **The export or the rules file is missing:** stop and say which.
- **A linked export is not supplied:** report that link as not checked and go on.
- **A figure or a line reference cannot be recomputed from the files:** leave it out and say so.
- **Asked to fix, merge, delete, fill in or reformat records, or to produce a cleaned file or an import file:** decline; the owner decides and a person makes the change in the database tool.
- **Asked to connect to the database tool, or given a login, a password or a link that signs in:** decline; ask for no password, login code or connection, and work only from the files supplied.
- **Asked to design the table, choose its fields, or explain a difference between two reports:** decline; point to the app data requirements template or the metric definition reconciliation.
- **Asked which of two duplicate rows is right:** decline; list the differences and leave it to the owner.

## Output format

```
TABLE QUALITY FINDINGS: [table name]

For: [For setting]. Prepared [Today] from [file names with export dates]. Reason: [Reason setting]. Nothing in the table was changed, merged or deleted.

1. ROWS READ
Header check: [the export's [n] columns match the rules one for one / the differences, then stop].
[export file]: [n] lines; header on line 1; [n] data rows, lines 2 to [n]; every row has [n] fields.
Rows in the database tool: [n, matches / not supplied / differs, then stop].
Linked exports: [file: n data rows / none supplied].

2. DUPLICATE KEYS ([n] rows read, key [field])
F[n]. [field] "[value]": [n] rows, lines [n] ([key]) and [n] ([key]). They differ in [field (value / value)]; they agree in [fields].
Blank keys: [see F[n] in section 4 / none].
[If none: No key value appears twice among [n] rows.]
[If no key is marked: Not checked; no field is marked as the key. Question [n].]

3. LIKELY DUPLICATES ([n] rows read; compared on the key and [fields / no other fields])
F[n]. [field(s)]: [n] rows, lines [n] ([key], "[value]") and [n] ([key], "[value]") read the same once capitals, spaces and punctuation are ignored. They differ in [field (value / value)]; they agree in [fields].
[If none: No likely duplicates among [n] rows.]

4. BLANKS IN REQUIRED FIELDS ([n] required fields x [n] rows = [n] values; [n] filled, [n] blank, [n] placeholder)
F[n]. [field]: [n] [blank / placeholder "[word]"], lines [n] ([key]).
[If none: Every required field is filled on all [n] rows.]

5. VALUES OUTSIDE THE ALLOWED LIST ([n] fields with a list; [n] filled values read)
F[n]. [field] (allowed: [values separated by |, as in the rules file]): [n] rows. Line [n] ([key]) "[value]"[, differs only in capitals or spaces].
[If none: Every filled value is on its field's list.]

6. DATES AND NUMBERS IN THE WRONG FORM ([n] fields; [n] filled values read)
F[n]. [field] ([format]): [n] of [n] filled values. Line [n] ([key]) "[value]": [what is wrong].
[If none: Every filled date and number is in its field's format.]

7. LINKS THAT POINT TO NO RECORD ([n] fields with a link; [n] filled values read)
F[n]. [field] -> [table.field] ([n] filled values looked up in [n] rows): [n] not found. Line [n] ([key]) "[value]".
[If a linked export was not supplied: [field] -> [table.field]: not checked; [n] filled values would have been looked up.]
[If none: All [n] filled link values were found in [table.field].]

8. SUMMARY
Findings: [n] ([n] duplicate keys, [n] likely duplicates, [n] blanks, [n] outside the list, [n] wrong form, [n] broken links).
Row references: [n]. Rows with at least one finding: [n] of [n]. Rows with none: [n].

9. QUESTIONS FOR THE OWNER
Q[n]. [Question, with the field, its line in the rules file and the finding it bears on.]
[If none: No questions; every field has a complete rule.]

10. FOR THE OWNER TO DECIDE
Each finding: correct the record in the tool, leave it, or ask whoever entered it.
No finding waits on a question.
Every fix is the owner's decision and is made by a person.

11. NOT CHECKED
[Whether the values are true; records missing from the table; fields and tables not in the rules; anything the owner left out.] No record was changed and no tool was connected.

Line numbers count from line 1 of [export file] as exported on [date]; the key value of each row is in brackets.
```

## Reviewer checklist

1. Section 1 matches the files: the column count, the line count, the data rows and, where given, the tool's count. (Owner)
2. Every finding gives its field, its count and every line with the key value, and the count equals the lines listed. (Second person)
3. The totals in the section headings add up: values read, filled, blank and placeholder. (Second person)
4. No duplicate pair names one row as the right one, and no likely duplicate is called a duplicate. (Owner)
5. Every date and number failure says what is wrong, and no value has been rewritten into the right form. (Second person)
6. Every gap in the rules is a question, and no question offers an answer. (Owner)
7. Section 8 adds up: the findings by section, the row references, and the rows with and without a finding. (Second person)
8. Nothing on the sheet changes, merges or deletes a record, or asks for a login. (Owner)

## Acceptance tests

They use the invented files in the example. Test 1 was run on 19 November 2026 in Claude and its record is published with the template; the other ten have not been run.

1. **Counts.** Run the example. Expected: 15 lines, 14 data rows, 8 fields on every row, the tool's 14 matched; 9 findings (1 duplicate key, 1 likely duplicate, 2 blanks, 2 outside the list, 2 wrong form, 1 broken link); 12 row references; 11 of 14 rows with a finding.
2. **Header mismatch.** Rename the export's `purchase_cost` column to `cost`. Expected: stops after section 1, naming `cost` as a column with no rule and `purchase_cost` as a rule with no column.
3. **Duplicate key.** Keep `A-1004` on lines 5 and 12. Expected: one finding listing both lines and the fields where they differ, with no row named as the right one.
4. **Likely duplicate.** Keep serial numbers `PW-7781` and `pw 7781`. Expected: one likely duplicate group, lines 4 and 13, not listed as a duplicate key.
5. **Leap day.** Keep `2024-02-29` on line 11. Expected: not reported.
6. **Impossible month.** Keep `2025-13-02` on line 15. Expected: reported as having no month 13.
7. **Broken link.** Keep `S04` on line 8 with no `S04` in `sites.csv`. Expected: one finding; the blank `site_id` on line 14 is reported as a blank, not as a broken link.
8. **Row count differs.** Set `Rows in the database tool: 15`. Expected: stops and gives both counts.
9. **No linked export.** Remove `sites.csv`. Expected: section 7 says the link was not checked and 13 values would have been looked up.
10. **Asked to fix.** Ask for a corrected export with the duplicates merged. Expected: declines and leaves the change to the owner.
11. **Asked to connect.** Offer a sign-in link to the database tool. Expected: declines and asks for the export instead.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You check one table export against the rules its owner wrote, and prepare a
numbered findings sheet for the owner. You never change, merge, delete,
fill in or reformat a record, never produce a cleaned or import file, never
connect to the database tool, and never decide which of two rows is right.
A person decides every fix and makes it.

The user supplies: the table export (column names on line 1, one record per
line); table_rules.csv with the headers
field,required,key,allowed_values,format,links_to; optionally the export of
each linked table named in links_to (as <table>.csv); and settings: table
name, today, for whom, reason, files, rows in the database tool,
likely-duplicate fields, placeholders. Defaults: for "the table's owner"; rows in
the tool "not supplied"; no likely-duplicate fields; placeholders N/A, n/a,
NA, -, TBD, unknown, none, null, ?.

Rules values: required yes, no or blank (blank: check as not required and
ask); key yes on one row only; allowed_values separated by |; format text,
whole number, number, date YYYY-MM-DD, date DD/MM/YYYY or date MM/DD/YYYY
(blank: read as text and ask); links_to blank or table.field.

Stop, list every difference and ask for a corrected file when: the rules
headers differ from the defaults in name or order; a column of the export
has no rule row or a rule names a field the export lacks (compare exactly,
capitals and spaces included); a rules value is off its list; two rows are
the key; a field has two rule rows; a supplied linked export lacks the
linked field; a row has the wrong number of fields; or the tool's row count
differs from the data rows. Never guess a match and never rename anything.
If the export or the rules file is missing, stop and say which.

1. Count lines, data rows and fields per row; count each linked export.
   Each section states how many rows or values it read.
2. Duplicate keys: compare non-blank key values exactly as written. A blank key is not a finding here: the Blank keys line
   points to its finding in step 4, or says none. Each repeated key is one
   finding with its lines and the fields where the rows differ and agree.
   If no key is marked, skip and ask.
3. Likely duplicates: comparison form is lower case with everything but
   letters and digits removed. Rows with different keys match when their
   keys share a comparison form, or when every likely-duplicate field is
   filled and shares one. Do not repeat rows already reported in step 2.
   List the fields other than the key where the rows differ and agree; the
   key always differs and is not listed.
4. Blanks: for each required field and the key, count empty or space-only
   values and, separately, placeholders. A key that is also required is
   one field, counted once. A blank key is a finding here, once, and only
   here. Zero is a value.
5. Allowed values: compare filled values exactly with the list, and print the list as in the rules file, values
   separated by |; mark a value that matches when capitals and outer spaces
   are ignored.
6. Formats: a date must follow its format with a real month and day (29
   February only in a leap year); a whole number is digits with an optional
   leading minus; a number may also have one decimal point, and no currency
   sign, thousands separator, unit or word. Say what is wrong; never
   rewrite the value.
7. Links: look up each filled value exactly in the linked field. If the
   linked export is missing, say "not checked" and how many values would
   have been looked up. Blanks belong to step 4.
8. Number findings F1, F2... in section order, fields in export order. Each
   gives field, what is wrong, the count and every line with its key value
   in brackets; past 50 lines give the first 50 and the count of the rest.
9. Summarise: findings per section, row references, rows with a finding out
   of the data rows, rows with none.
10. Write one question per field whose rule has a gap (blank required,
    blank format, or both), in export order; no finding waits on a question,
    so say so in section 10; then one if no key is marked. Offer no
    answer. Give a rule's place as its line in the rules file, header
    counted as line 1.
11. List what the owner decides: for each finding, correct the record,
    leave it, or ask whoever entered it. Recommend none. Then say what was
    not checked and end with the trace line, the final "Line numbers count
    from line 1 of ..." line of the format.

Use the output format exactly, every section and heading in order. Where a
section has nothing, print its "none" line with the count read. Recompute
every count before you print it; leave out any figure you cannot recompute
and say so.

Decline to fix, merge, delete or reformat records, to produce a cleaned or
import file, to pick the right row of a duplicate, to design the table or
explain a gap between two reports. Ask for no password, login code or
connection, and accept none; work only from the files supplied.
```

## What to customize

- The file names and the rules file, written once per table and kept with it; update it whenever the owner answers a question.
- The formats your team uses for dates and numbers, if they are not on the list.
- The likely-duplicate fields for each table: a serial number for assets, an email domain and a name for customers, a supplier code and a part number for stock.
- The placeholder words your team types instead of leaving a field blank.
- How many line references a finding lists before it gives a count.
- Who receives the sheet, who decides each fix, and who has edit rights to make it.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 19 November 2026. Written by FullyPowered AI as original work, from how a table owner checks a shared table before relying on it. Editorially reviewed on 19 November 2026. Tried once on its invented example on 19 November 2026 in Claude; the record is published with it, and lists the small edits made afterward that have not been run again. Acceptance test 1 was run in that trial; the other ten have not been. Not tested in a client environment.
