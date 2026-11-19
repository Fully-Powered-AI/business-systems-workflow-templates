# Database table quality check: a trial on the invented example

- **Product:** Claude, run in Claude Code

Model: Claude Sonnet 5.5 (model ID claude-sonnet-5-5).

Date: 2026-11-19.

The inputs were the invented example's own, and no client data was used. The inputs are the four in `public/example.md`: the settings, `assets.csv`, `table_rules.csv` and `sites.csv`. The model read the template and those inputs first, and only afterwards read the example's findings sheet to compare. It did not install, connect to or run anything; it worked from the files as text.

## What came out

The model followed the instruction block and the output format, and produced all eleven sections plus the closing line. The sheet it produced, in substance:

```
TABLE QUALITY FINDINGS: Assets

For: the operations manager, owner of the Assets table. Prepared Thursday 19 November 2026 from assets.csv, table_rules.csv and sites.csv (all exported 2026-11-18). Reason: before the table is moved to a new database tool. Nothing in the table was changed, merged or deleted.

1. ROWS READ
Header check: the export's 8 columns match the rules one for one.
assets.csv: 15 lines; header on line 1; 14 data rows, lines 2 to 15; every row has 8 fields.
Rows in the database tool: 14, matches.
Linked exports: sites.csv: 3 data rows.

2. DUPLICATE KEYS (14 rows read, key asset_id)
F1. asset_id "A-1004": 2 rows, lines 5 (A-1004) and 12 (A-1004). They differ in asset_name (Laptop 14 / Laptop 16), purchase_cost (1150.00 / 1150) and serial_number (LT-55012 / LT-55014); they agree in category, site_id, purchase_date and status.
Blank keys: none.

3. LIKELY DUPLICATES (14 rows read; compared on the key and serial_number)
F2. serial_number: 2 rows, lines 4 (A-1003, "PW-7781") and 13 (A-1011, "pw 7781") read the same once capitals, spaces and punctuation are ignored. They differ in asset_id (A-1003 / A-1011) and purchase_date (2024-06-02 / 2025-07-15); they agree in asset_name, category, site_id, purchase_cost and status.

4. BLANKS IN REQUIRED FIELDS (5 required fields x 14 rows = 70 values; 68 filled, 2 blank, 0 placeholder)
F3. asset_name: 1 blank, line 10 (A-1009).
F4. site_id: 1 blank, line 14 (A-1012).

5. VALUES OUTSIDE THE ALLOWED LIST (2 fields with a list; 28 filled values read)
F5. category (allowed: Vehicle|Tool|IT|Furniture): 1 row. Line 9 (A-1008) "tool", differs only in capitals or spaces.
F6. status (allowed: In use|In store|In repair|Retired): 1 row. Line 11 (A-1010) "Sold".

6. DATES AND NUMBERS IN THE WRONG FORM (2 fields; 27 filled values read)
F7. purchase_date (date YYYY-MM-DD): 2 of 14 filled values. Line 6 (A-1005) "20/01/2025": written day/month/year, not year-month-day. Line 15 (A-1013) "2025-13-02": there is no month 13.
F8. purchase_cost (number): 1 of 13 filled values. Line 8 (A-1007) "3200 est": a word follows the number.

7. LINKS THAT POINT TO NO RECORD
F9. site_id -> sites.site_id (13 filled values looked up in 3 rows): 1 not found. Line 8 (A-1007) "S04".

8. SUMMARY
Findings: 9 (1 duplicate keys, 1 likely duplicates, 2 blanks, 2 outside the list, 2 wrong form, 1 broken links).
Row references: 12. Rows with at least one finding: 11 of 14. Rows with none: 3.

9. QUESTIONS FOR THE OWNER
Q1. asset_name (rule row 3 of table_rules.csv): format is blank, so it was read as text. Is text the right format?
Q2. serial_number (rule row 8 of table_rules.csv): required and format are both blank, so it was checked as not required and read as text. Is it required, and in what format?

10. FOR THE OWNER TO DECIDE
Each finding: correct the record in the tool, leave it, or ask whoever entered it.
No finding waits on a question.
Every fix is the owner's decision and is made by a person.

11. NOT CHECKED
Whether the values are true; assets missing from the table; the site_name field of sites.csv, which has no rules; the blank purchase_cost and serial_number on line 7, which the rules allow. No record was changed and no tool was connected.

Line numbers count from line 1 of assets.csv as exported on 2026-11-18; the key value of each row is in brackets.
```

## What was observed

Every required part was produced, in the order the format gives. All the counts matched the template's first acceptance test: 15 lines, 14 data rows, 9 findings, 12 row references, 11 of 14 rows with a finding. The model did not meet a stop condition, because the headers matched, every row had 8 fields, and the tool's count of 14 matched.

Differences from the published example's sheet:

- F2 lists the key (asset_id) among the fields where the two rows differ. The example leaves it out. The template says to name "the fields where the rows differ", and two rows with different keys always differ in the key, so either reading is defensible.
- In Q2 the model did not ask whether two assets may share a serial number, and it wrote "No finding waits on a question" in section 10. The example asks that extra question and says F2 waits on Q2. Nothing in the template tells the assistant to decide that F2 depends on the serial number rule, so the model did not.
- The model wrote the rule rows as "rule row 3" and "rule row 8", counting from the first rule after the header. The example writes "table_rules.csv line 3" and "line 9", counting from the header line. The template says "the rule row" without saying how to number it.
- The allowed lists are written with the bare `|` separator as in the rules file; the example puts spaces around it.
- The "not checked" section is shorter. The example adds the assets' existence, their cost and the quality of sites.csv.

No fact appears in either sheet that is not in the inputs, with one qualification: the example's Q2 asks whether two assets may share a serial number, which is a question rather than a fact. Both sheets say the date on line 6 is written day/month/year, which is an inference from the value 20 in the first place, and it is right here.

Where the instructions were ambiguous, and the model had to choose:

- "Trace line" in procedure step 12 and in the instruction block is never defined. The model took it to mean the last line of the output format, about where line numbers count from.
- The key is both a required field and "the key" in step 5. The model counted it once among the five required fields, which gives the 70 values the format's heading expects, but the template does not say so.
- Section numbers on the sheet (1 to 11) differ from the procedure's step numbers (a duplicate-key check is step 3 but section 2), and the instruction block numbers its steps differently again. This is easy to follow but needs care when checking a finding against a step.
- Section 7's heading has no "rows read" count, unlike the others, although the procedure says every section states how many it read. The model put the count in each finding.
- The reviewer checklist asks whether the heading totals add up; the model did this by hand.

The model was not told to stop for anything, and it was not asked to fix, merge, connect or choose a right row, so the decline rules were not exercised. Of the eleven acceptance tests, only the first was run here. The template's own version note said at the run that it had not been tried (since corrected, see below); this trial is one run on the invented example, by one model, and it is not a test in a client environment.

## Changed after the run

Changed on 19 November 2026 after an independent review of the published template, and not run again. The sheet and the observations above are as recorded and describe the template and the example as they stood at the run:

- **The trace line.** The procedure and the pasted instructions now say it is the final "Line numbers count from line 1 of ..." line of the output format.
- **Naming a rule row.** The procedure and the pasted instructions now say a rule's place is its line in the rules file, with the header as line 1, and the output format's question line says "its line in the rules file". The run above wrote "rule row 3" and "rule row 8"; under the new wording those read "table_rules.csv line 3" and "line 9", as the example does.
- **A key that is also required.** The procedure and the pasted instructions now say it is one field, counted once.
- **Section 7's heading.** The output format and the example's sheet now carry a count of fields with a link and filled values read, as the other sections do. The recorded sheet above has no such count.
- **The version notes, the profile and the acceptance-tests note** now state that this trial was run.

Changed again on 19 November 2026 after the independent review's minor points, and not run again. The sheet and observations above still describe the run as recorded:

- **No finding waits on a question.** The run produced no question about whether two assets may share a serial number and wrote "No finding waits on a question". The published example now matches that. The procedure, the pasted instructions and the output format now say that no finding waits on a question, because a blank `required` or `format` is checked by a default.
- **The key in a likely-duplicate finding.** The procedure and the pasted instructions now say the fields listed are those other than the key, which always differs. The run listed asset_id; the example leaves it out, as the wording now does.
- **A blank key** is now a finding in section 4 only; section 2's "Blank keys" line points to it.
- **Allowed lists** are written with the bare `|`, as in the rules file, in the output format and the example, which is how the run wrote them.
- **The paste line.** The template now tells the user to paste the output format after the instruction block.
- **The profile and the template** now say a different number of rows stops the work, and set the dataset profile apart by reader and moment instead of "no rules".
- **Search facts.** A `public/facts.json` was added.
