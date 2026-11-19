# Database table quality check: an invented example

*Illustrative example with invented data.* The company, the people, the assets, the sites and every value below are invented. The company is an invented facilities-services business, called Company R here. Its operations manager owns the Assets table the team keeps its equipment records in, and wants the table checked before it is moved to a new database tool. First come the inputs the operations manager supplied, in full, then the findings sheet the workflow template returned.

## The inputs

### 1. Settings (typed by the operations manager)

```
Table name: Assets
Today: Thursday 19 November 2026
For: the operations manager, owner of the Assets table
Reason: before the table is moved to a new database tool
Files: assets.csv, table_rules.csv, sites.csv (all exported 2026-11-18)
Rows in the database tool: 14
Likely-duplicate fields: serial_number
Placeholders: defaults
```

### 2. assets.csv: the table export from the database tool your team keeps its records in (header is line 1)

Every record of the Assets table, with all eight fields, exported unfiltered.

```
asset_id,asset_name,category,site_id,purchase_date,purchase_cost,status,serial_number
A-1001,Van 1,Vehicle,S01,2023-03-14,28500,In use,VN-20931
A-1002,Van 2,Vehicle,S01,2023-03-14,28500,In repair,VN-20932
A-1003,Pressure washer,Tool,S02,2024-06-02,640,In use,PW-7781
A-1004,Laptop 14,IT,S03,2025-01-20,1150.00,In use,LT-55012
A-1005,Laptop 15,IT,S03,20/01/2025,1150,In use,LT-55013
A-1006,Desk set,Furniture,S03,2022-09-30,,In store,
A-1007,Generator,Tool,S04,2024-11-11,3200 est,In use,GN-1180
A-1008,Ladder,tool,S02,2021-05-17,180,In use,LD-0042
A-1009,,Tool,S02,2021-05-17,95,In use,LD-0043
A-1010,Van 3,Vehicle,S01,2024-02-29,31200,Sold,VN-20940
A-1004,Laptop 16,IT,S03,2025-01-20,1150,In use,LT-55014
A-1011,Pressure washer,Tool,S02,2025-07-15,640,In use,pw 7781
A-1012,Floor scrubber,Tool,,2025-08-01,2100,In store,FS-310
A-1013,Monitor,IT,S03,2025-13-02,210,In use,MN-8820
```

### 3. table_rules.csv (written once by the operations manager; header is line 1)

```
field,required,key,allowed_values,format,links_to
asset_id,yes,yes,,text,
asset_name,yes,no,,,
category,yes,no,Vehicle|Tool|IT|Furniture,text,
site_id,yes,no,,text,sites.site_id
purchase_date,no,no,,date YYYY-MM-DD,
purchase_cost,no,no,,number,
status,yes,no,In use|In store|In repair|Retired,text,
serial_number,,no,,,
```

### 4. sites.csv: the linked table's export (header is line 1)

```
site_id,site_name
S01,Depot North
S02,Depot South
S03,Head office
```

## The findings sheet

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
F2. serial_number: 2 rows, lines 4 (A-1003, "PW-7781") and 13 (A-1011, "pw 7781") read the same once capitals, spaces and punctuation are ignored. They differ in purchase_date (2024-06-02 / 2025-07-15); they agree in asset_name, category, site_id, purchase_cost and status.

4. BLANKS IN REQUIRED FIELDS (5 required fields x 14 rows = 70 values; 68 filled, 2 blank, 0 placeholder)
F3. asset_name: 1 blank, line 10 (A-1009).
F4. site_id: 1 blank, line 14 (A-1012).

5. VALUES OUTSIDE THE ALLOWED LIST (2 fields with a list; 28 filled values read)
F5. category (allowed: Vehicle|Tool|IT|Furniture): 1 row. Line 9 (A-1008) "tool", differs only in capitals or spaces.
F6. status (allowed: In use|In store|In repair|Retired): 1 row. Line 11 (A-1010) "Sold".

6. DATES AND NUMBERS IN THE WRONG FORM (2 fields; 27 filled values read)
F7. purchase_date (date YYYY-MM-DD): 2 of 14 filled values. Line 6 (A-1005) "20/01/2025": written day/month/year, not year-month-day. Line 15 (A-1013) "2025-13-02": there is no month 13.
F8. purchase_cost (number): 1 of 13 filled values. Line 8 (A-1007) "3200 est": holds a word after the number.

7. LINKS THAT POINT TO NO RECORD (1 field with a link; 13 filled values read)
F9. site_id -> sites.site_id (13 filled values looked up in 3 rows): 1 not found. Line 8 (A-1007) "S04".

8. SUMMARY
Findings: 9 (1 duplicate keys, 1 likely duplicates, 2 blanks, 2 outside the list, 2 wrong form, 1 broken links).
Row references: 12. Rows with at least one finding: 11 of 14. Rows with none: 3.

9. QUESTIONS FOR THE OWNER
Q1. asset_name (table_rules.csv line 3): the format is blank, so the field was read as text. Is text the right format?
Q2. serial_number (table_rules.csv line 9): required and format are both blank, so it was checked as not required and read as text. Is it required, and in what format?

10. FOR THE OWNER TO DECIDE
Each finding: correct the record in the tool, leave it, or ask whoever entered it.
No finding waits on a question.
Every fix is the owner's decision and is made by a person.

11. NOT CHECKED
Whether the values are true (that each asset exists, sits at its site and cost what is recorded); assets missing from the table; the site_name field of sites.csv and the quality of sites.csv itself, which have no rules here; the line 7 blank purchase_cost and serial_number, which the rules allow. No record was changed and no tool was connected.

Line numbers count from line 1 of assets.csv as exported on 18 November 2026; the key value of each row is in brackets.
```

## How the figures were reached

- **Rows:** 15 lines in assets.csv, less the header, is 14 data rows, the same as the 14 the database tool shows.
- **Required values:** asset_id, asset_name, category, site_id and status are required, so 5 fields across 14 rows is 70 values; the blanks are line 10's asset_name and line 14's site_id, leaving 68 filled.
- **Allowed lists:** category and status are filled on all 14 rows each, 28 values. Category reads Vehicle 3, Tool 5, tool 1, IT 4, Furniture 1; status reads In use 10, In repair 1, In store 2, Sold 1.
- **Formats:** purchase_date is filled on all 14 rows; purchase_cost on 13, because line 7 is blank; 27 in all. Line 11's 2024-02-29 is a real date, since 2024 is a leap year, and line 5's 1150.00 is a number.
- **Links:** site_id is filled on 13 rows (S01 3, S02 4, S03 5, S04 1); only S04 is missing from the 3 sites.
- **Rows with a finding:** lines 4, 5, 6, 8, 9, 10, 11, 12, 13, 14 and 15, which is 11; line 8 carries two findings (F8 and F9), so the row references come to 12. Lines 2, 3 and 7 have none.
