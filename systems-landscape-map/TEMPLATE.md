# Systems landscape and data flow map

Workflow template, version 0.1.0.

## Purpose

Build one map of a company's business systems from the lists and interview notes a person supplies: a table of every system with what it is used for, which kinds of record it is the record of truth for, what else it holds, who owns it and who runs it; every flow of data between systems, with its method, frequency and owner; and a plain-text diagram of those flows. Gaps (a system with no owner, a kind of record nobody has named a home for, a flow nobody owns, a copy no flow reaches) and duplicate records of truth (two systems both named as the record for the same thing) are marked, and every unknown becomes a question for the person who can answer it. The assistant prepares the map. It connects to no system, never decides which system is the record of truth, never recommends keeping, buying or retiring a system, and changes nothing.

## When to use it and when not to

Use it before a major system decision (replacing the accounting system, adding an online shop, merging two companies' tools), when the company has no architect and the operations or systems lead needs the whole picture on one page. Use it again at each annual review, with last year's map, to see what has changed. It covers the whole company or one business unit at the level of systems, kinds of record and flows.

Do not use it:

- to map the fields two systems share before a sync is switched on. That is the CRM field ownership map;
- to list subscriptions and what they cost. That is the software subscription and vendor spend review;
- to list the automations running on one platform. That is the workflow inventory;
- to specify the data for one internal app. That is app data requirements;
- to compare a proposed system with the work it must support, or to plan the retirement of a system. The map is an input to those decisions; it does not make them;
- with any password, login code, access key or connection. It works only from the files and notes supplied.

## Roles

- **Runs it and reviews the map:** the operations lead or systems lead named in the settings as the map reviewer.
- **Supply the lists and are interviewed:** the business owner of each system and the people who move data between systems.
- **Answer the questions:** the role or roles each question is addressed to.
- **Decide which system is the record of truth for each kind of record, who owns each system and flow, and what happens next:** the map reviewer with the business owners concerned, and the owners or leadership for any system decision. Always people.

## Inputs

1. **Systems list,** one row per system, CSV with the header as line 1. Default headers: `system`, `used_for`, `records_held`, `record_for`, `business_owner`, `administrator`. `records_held` and `record_for` hold record types from the record-type list, separated by semicolons. `record_for` holds only the types the system's owner says it is the record of truth for; it may be blank. A spreadsheet, shared folder or mailbox that is the only home of a kind of record belongs on this list. If the systems list is missing, stop and ask.
2. **Connections list,** one row per known flow, CSV with the header as line 1. Default headers: `from_system`, `to_system`, `records`, `method`, `frequency`, `owner`. `method` is one of: automatic, scheduled file, manual export and import, re-keyed by hand, unknown. If the connections list is missing, ask once; if there is none, map the flows the interview notes describe and say "no connections list supplied".
3. **Interview notes,** one note per conversation, each opening with a line giving the person's role and the date, such as `Finance manager, 3 November 2026:`. If none are supplied, write "no interview notes supplied" and map from the lists alone.
4. **Settings,** one per line:
   - `Today:` the date.
   - `Company:` the company or business unit being mapped.
   - `Reason:` one sentence: the system decision coming, or "annual review".
   - `System under decision:` the system the decision is about, exactly as named on the systems list, or "none".
   - `Map reviewer:` the role who reviews the map. Default "the operations lead".
   - `Record types:` the kinds of record to map, separated by semicolons, or "the default list": customers; suppliers; products; prices; sales orders; invoices; payments received; stock levels; employees.
   - `Previous map:` last year's map in this template's output format, pasted, or "none".

If a header in either list does not match the default headers above, stop and ask (procedure step 1).

## The procedure

1. **Check the files.** Compare the headers of the systems list and the connections list with the defaults, by name. If any is missing, extra or different, or a row has a different number of fields from its header, stop: list the differences and line numbers and ask whether to correct the file or rename the column. Do not guess. If two rows of the systems list give the same system name, stop and ask which is which. Count the rows of each list (line numbers count the header as line 1) and the interview notes.
2. **Fix the record types.** Use the list in the settings, or the default list. Any value in `records_held`, `record_for` or `records` that is not on the list is a "record type not on the list": name it in section 1, ask the map reviewer whether to add it, and leave it out of the map until answered.
3. **Number the systems** S1, S2 and so on, in the order of the systems list. A system named in the connections list or in an interview note but not on the systems list is "named but not listed": it gets no number and no row in the table; show it as "[name, not listed]" wherever a flow names it.
4. **Find the record of truth for each record type.** A claim is a system that names the type in its `record_for`, or a system an interview note names as the record for it in plain words, such as "is the master for", "is the truth for", "is the record for" or "we go by". Never treat where data is kept, how much a system holds, which way flows run or a system's name as a claim. A claim for part of a type ("the master for product names and photos") counts as a claim for the whole type; print the note's words with it so the reader sees the limit. A note's words match a record type only when they name it or use an everyday word for it ("address" for customers, "trade orders" for sales orders); when unsure, ask the person who wrote the note instead of matching. Then give each type one status:
   - **stated:** exactly one system claims it, and no interview note names another;
   - **disputed:** two or more systems claim it, counting both lists and notes. This is a duplicate record of truth;
   - **named in an interview only:** no `record_for` names it and the notes name one system; not confirmed;
   - **none named:** one or more systems hold it and nobody claims it;
   - **not held:** no listed system holds it.
   An interview note that names the same system as the list is shown as agreeing. A system that claims a type not in its own `records_held` is counted as holding it and flagged "claims a type it does not list as held".
5. **Check the owners.** A blank `business_owner` is "no business owner"; a blank `administrator` is "administrator not stated"; a blank `records_held` is "records held not stated". Each is a flag on the system, and so is "system under decision" on the system named in the settings. Never fill a blank from the notes; where a note speaks to it, quote the note on the system's gap line in section 6.
6. **List the flows.** Number the connections list's rows F1, F2 and so on, in order, then add each flow an interview note describes that the list does not. An interview flow counts only when the note names both systems and the record type; its owner is the role the note names as doing or running it, or "not stated"; it is marked "from an interview, not confirmed". When a note describes a flow already on the list (same from, to and record type), do not add it: write "also described by [role], [date]" on the listed flow, and if the note gives a different method or frequency, write "interview says: [method or frequency]". A frequency written as an event ("when prices change") is a stated frequency; only a missing one is flagged. Flag each flow, kinds separated by commas: no owner; re-keyed by hand; method unknown or not one of the five values (print it as written); frequency not stated; from an interview, not confirmed; a system not listed; "[system] does not list [type] as held" when the sending or receiving system's `records_held` leaves out a type the flow carries.
7. **Find the copies no flow reaches.** For each record type held in two or more listed systems: if no flow carries it, record one finding, "no flow carries [type] between [systems]"; otherwise each holding system that no flow carrying the type starts or ends at is "a copy no flow reaches". Interview flows count.
8. **Draw the diagram.** One block for each system that sends a flow, in S order, headed "[Sn name]", with one line per outgoing flow in F order: the arrow for the method (==> automatic or scheduled file; --> manual export and import; ..> re-keyed by hand; ??> unknown or unclear), the receiving system, the record types, the frequency, the flow number, and "i" for a flow from an interview. Then three lines: systems that only receive flows; systems with no flows; systems named but not listed.
9. **Collect the gaps** in the fixed order of the output format, each line listing what it found or "none".
10. **Write the duplicate records of truth:** one entry per disputed type, with each claiming system and the basis of its claim (systems list, or the note's role and date with its words quoted), where else the type is held, and the flows that carry it.
11. **Compare with the previous map,** when one is supplied: systems added and removed (matched by name), record types whose status or record system changed, and flows added and removed (matched by from, to and record type). If none is supplied, write "No previous map supplied; nothing compared."
12. **Write the questions.** One numbered question for each finding below, addressed as stated:
    - a system with no business owner: the map reviewer;
    - administrator or records held not stated, or a claim the system does not list as held: the system's business owner (the map reviewer if it has none);
    - a disputed type: the business owners of the claiming systems together;
    - a type with none named or named in an interview only: the business owners of the systems that hold it, together;
    - a type not held, or a record type not on the list: the map reviewer;
    - a flow with no owner, a method unknown or frequency not stated, or a type a system does not list as held: the flow's owner, or the business owner of the sending system when the flow has none, or, for the last kind, the business owner of the system that leaves the type out;
    - a flow from an interview: the business owner of the sending system;
    - a copy no flow reaches: the business owner of that system; where no flow carries the type at all, the owners of all its holding systems together;
    - a system named but not listed: the person who named it, or the map reviewer if it came from the connections list.
    Where an addressee is a system with no business owner, put the question to the other owners named, or to the map reviewer if none is left, and say so in the question. Group the questions under the role or roles that answer, in alphabetical order of the group heading ignoring punctuation and capitals; when a heading names several roles, list them in alphabetical order; within a group, order them by where the finding sits (systems, record types in list order, flows in F order, copies no flow reaches, systems named but not listed), and number continuously. Each question gives the facts and the line, flow or note it rests on, can be answered in a sentence, and offers no answer. A flow re-keyed by hand is a gap, not a question, unless it has another flag.
13. **Write the decisions** for the map reviewer: one numbered line for each disputed type, each type with none named, not held or named in an interview only (record types in list order), then each system with no business owner (S order), then each system named but not listed. Each line names the questions it waits on (every question about that type, a copy of it, or a flow carrying it; or about that system) and gives the options: settle now; settle before the decision on [system under decision]; leave open until the next annual review. Mark "before the decision" on each line that involves the system under decision: it holds or claims the type, a flow carrying the type starts or ends there, or it is the system concerned, meaning the system the line is about, which counts only when it is the system under decision. Recommend nothing.
14. **Say what was not checked,** and end with the trace line. Return the map to the map reviewer only.

## Exceptions and stop conditions

- **A header does not match, rows have different field counts, or two systems share a name:** stop, list the differences, ask.
- **No systems list:** stop and ask. Do not build a list from the notes or from a typical company.
- **A list or note holds a password, login code, access key or account detail:** do not repeat it anywhere in the map; tell the person to remove it from the source and keep going without it.
- **A note names a person in connection with a pay, performance or conduct matter:** refer to the point by role and system only.
- **Asked to decide the record of truth, assign an owner, or fill a blank from a guess:** decline; write it as a question.
- **Asked whether to keep, replace, buy or retire a system, or which product to choose:** decline; the map lists the facts and the decisions belong to the people named.
- **Asked to connect to a system, log in, change a setting, move data, or send the map or the questions to anyone:** decline; the map is the only output, and a person shares it after review.
- **More than ten items for one gap line or one flag:** list ten and give the count of the rest.
- **A figure or flow cannot be traced to a file or note supplied:** leave it out and say so under "Not checked".

## Output format

```
SYSTEMS LANDSCAPE MAP: [Company]

For: [Map reviewer]. Prepared [Today] from the systems list ([n] rows), the connections list ([n] rows / not supplied), [n] interview notes / no interview notes supplied, and the settings. Reason: [Reason]. System under decision: [Sn name / none].
Summary: [n] systems. [n] record types: [n] stated, [n] disputed, [n] named in an interview only, [n] none named, [n] not held. [n] flows: [n] from the connections list, [n] from interviews; [n] re-keyed by hand; [n] with no owner. [n] questions. [n] decisions.

1. THE FILES
Header check: [both lists have the headers expected / the differences, then stop].
Systems list: [n] rows (lines [..]). Connections list: [n] rows (lines [..]) / not supplied. Interview notes: [role, date; ...] / none supplied.
Record types: [the default list / the list in the settings] ([n]): [types]. Values not on the list: [value (file, line) / none].
Systems named but not listed: [n] (see section 6). Previous map: [supplied, dated [date] / none].

2. SYSTEMS
ID | System | Used for | Record of truth for | Also holds | Business owner | Administrator | Flows out | Flows in | Flags   [one row per system, in S order]
[Sn] | [name] | [used_for] | [types; "(disputed)" after a disputed type; "(from an interview)" after a claim made only in a note / none] | [types held and not claimed / none] | [role / not stated] | [role / not stated] | [F numbers / none] | [F numbers / none] | [no business owner, administrator not stated, records held not stated, claims a type it does not list as held, system under decision / none]

3. RECORD OF TRUTH BY RECORD TYPE
R[n]. [type]. Status: [stated / disputed / named in an interview only / none named / not held]. Record: [Sn name (basis) / named as the record by: Sn name (basis); Sn name (basis) / none named]. Also held in: [systems / none]. Flows carrying it: [F numbers / none]. [Flag: the record's system has no business owner.]
[One line per record type, in list order. Where the record is "none named", print "Held in:" in place of "Also held in:", since no record is named for it to be held in addition to.]

4. DATA FLOWS
F[n]. [Sn from / name, not listed] -> [Sn to / name, not listed]. Records: [types]. Method: [method]. Frequency: [frequency / not stated]. Owner: [role / not stated]. Source: [connections list, line n / interview, role, date; not confirmed][; also described by role, date][; interview says: ...]. Flags: [kinds / none].
Methods: [n] automatic, [n] scheduled file, [n] manual export and import, [n] re-keyed by hand, [n] unknown or unclear.

5. DIAGRAM
Legend: ==> automatic or scheduled file   --> manual export and import
        ..> re-keyed by hand   ??> unknown or unclear   i = from an interview, not confirmed
[Sn name]
  [arrow] [Sn name]  [types], [frequency] (F[n][, i])
[One block per sending system, in S order. The heading of each block is printed in square brackets, as "[S1 CRM]"; the receiving system on each line is printed without them, as "S4 Warehouse system", except a system not on the list, printed "[name, not listed]". Every other square bracket in this format is a placeholder and is not printed.]
Receives only: [systems / none]
No flows recorded: [systems / none]
Not on the systems list: [names / none]

6. GAPS
Systems missing an owner, administrator or records held, or claiming a type they do not list: [Sn name: what is missing or claimed; any note about it, quoted with role and date / none]
Systems named but not on the list: [name (who named it, date, or connections line) / none]
Record types with no record named: [type (held in systems) / none]
Record types held in no listed system: [types / none]
Record types named as the record in an interview only: [type (system, role, date) / none]
Record type values not on the list: [values / none]
Flows with no owner: [F numbers / none]
Flows re-keyed by hand: [F numbers / none]
Flows with a method or frequency unknown or not stated: [F numbers / none]
Flows carrying a type a system does not list as held: [F number (system, type) / none]
Copies no flow reaches: [type in systems; or "no flow carries [type] between [systems]" / none]
Flows from interviews, not confirmed: [F numbers / none]

7. DUPLICATE RECORDS OF TRUTH
D[n]. [type]. Named as the record by: [Sn name (basis, with the note's words quoted)]; [Sn name (basis)]. Also held in: [systems / none]. Flows carrying it: [F numbers / none].
[If none: "No record type is named as the record by more than one system."]

8. CHANGES SINCE THE LAST MAP
[Systems added; systems removed; record types whose status or record changed; flows added; flows removed / "No previous map supplied; nothing compared."]

9. QUESTIONS
[Role, or roles together]
[n]. [Question with the facts and the line, flow or note it rests on.]
[Next group, numbering continuously.]
[If none: "No questions arise from the findings."]

10. DECISIONS FOR THE MAP REVIEWER ([Map reviewer])
[n]. [Type or system]: [the open point]. [Before the decision.] Waits on questions [numbers]. Options: settle now; settle before the decision on [system under decision]; leave open until the next annual review.
[If none: "No decisions are open."]
People decide every record of truth, owner and next step; this map decides none.

11. NOT CHECKED
Whether the lists are complete or the notes accurate; the fields inside any flow; how data is changed on the way; volumes, errors and timings; access and security; costs and contracts; [anything the person left out]. [A password, login code or access key was found in [file, line] and left out of this map; remove it from the source.] No system was connected to and nothing was changed.

Every entry traces to the systems list, the connections list, the interview notes or the settings supplied on [Today]. This map connects to no system and changes nothing.
```

When a section has no findings, print its heading, what was checked and "none", never a blank.

## Reviewer checklist

1. Every system on the systems list has one row, and no system that is not on the list has a number. (Map reviewer)
2. Every record of truth shown is one a `record_for` cell or an interview note names, with its basis; none is inferred from where data sits or which way it flows. (Map reviewer)
3. Every record type has exactly one status, and the counts in the summary add up to the number of types. (Map reviewer)
4. Every flow traces to a connections list line or a quoted note, and the flow numbers in the systems table, section 4 and the diagram agree. (Map reviewer)
5. Every gap line either lists its findings or says "none", and every flagged item appears under its gap line. (Map reviewer)
6. Every question is addressed to the role the rules name, gives its facts and offers no answer. (Business owners)
7. Every decision names the questions it waits on and recommends nothing; "before the decision" appears exactly where the system under decision is involved. (Map reviewer)
8. The map does not ask for or repeat a password, login code or access key, and does not claim to have connected to a system. (Map reviewer)

## Acceptance tests

Proposed tests. None has been run.

1. **Header mismatch.** The systems list has `owner` instead of `business_owner`. Expected: stops and lists the difference; no map.
2. **Two claims.** Two systems both list customers in `record_for`. Expected: customers disputed; a duplicate entry with both bases; a question to both owners together; a decision.
3. **Interview disagrees.** The list names one system for products and a note says another "is the master". Expected: disputed, the note quoted, no choice made.
4. **Interview only.** No `record_for` names suppliers and a note says "we go by the accounting system for suppliers". Expected: named in an interview only, not confirmed; a question to the holders' owners.
5. **Held, not claimed.** Sales orders are held in three systems and claimed by none. Expected: none named; one question to the three owners together.
6. **Unowned system.** A spreadsheet is the record for prices and has no business owner. Expected: flagged in the table and under gaps; the question goes to the map reviewer; a decision.
7. **Flow from a note.** A note says address changes are emailed and retyped. Expected: a new flow marked from an interview, re-keyed by hand, not confirmed; a question to the sending system's owner.
8. **Copies no flow reaches.** Products are held in three systems and no flow carries them. Expected: one finding naming all three, and one question to their owners together.
9. **System not listed.** A note mentions a returns log on a shared drive. Expected: named but not listed, no number, a question to the person who named it.
10. **A password in a note.** Expected: not repeated anywhere; the person is told to remove it.
11. **Asked which system to keep.** Expected: declines; points to the decisions section.
12. **Annual review.** Last year's map is pasted and one flow has gone. Expected: the flow listed as removed under changes since the last map.

## Instructions for the AI assistant

```
You build a systems landscape and data flow map for a company's operations
or systems lead, from files and notes they supply. You connect to no
system and never ask for a password, login code, access key or
connection. You never decide which system is the record of truth, never
assign an owner, never recommend keeping, buying or retiring a system, and
never send, change or move anything. People make every decision after
the map reviewer has read the map.

Inputs. Systems list (CSV, header line 1): system, used_for, records_held,
record_for, business_owner, administrator; records_held and record_for
hold record types separated by semicolons. Connections list (CSV, header
line 1): from_system, to_system, records, method, frequency, owner;
method is one of automatic, scheduled file, manual export and import,
re-keyed by hand, unknown. Interview notes, each opening with the
person's role and the date. Settings: Today, Company, Reason, System under
decision (or none), Map reviewer (default the operations lead), Record
types (default: customers; suppliers; products; prices; sales orders;
invoices; payments received; stock levels; employees), Previous map (or
none). If the systems list is missing, stop and ask. If the connections
list is missing, ask once, then map the flows the notes describe and say
so. If a header differs from these, a row has the wrong number of fields,
or two systems share a name, stop, list the differences and ask. If a
file or note holds a password, login code or access key, do not repeat it
and tell the person to remove it. If a note names a person in connection
with a pay, performance or conduct matter, refer to the point by role and
system only. List at most ten items per gap line or flag, then give the
count of the rest. A figure or flow you cannot trace to a file or note
supplied, leave out and name under "Not checked".

1. Check the files and count rows; line numbers count the header as 1.
2. Fix the record types. Values not on the list: name them, ask the map
   reviewer, leave them out of the map.
3. Number systems S1.. in list order. A system named elsewhere but not
   listed gets no number; show it as "[name, not listed]".
4. Record of truth per type. A claim is a record_for entry, or a note that
   names a system as the record in plain words ("is the master for", "is
   the truth for", "is the record for", "we go by"). Where data sits,
   volumes, flow direction and names are never claims. Status: stated
   (one claim, no note naming another); disputed (two or more systems
   claim it, lists and notes together); named in an interview only; none
   named (held, unclaimed); not held. A claim for part of a type ("master
   for product names") counts as a claim for the type; quote the words. A
   note's words match a type only if they name it or an everyday word for
   it; if unsure, ask the note's author. A note naming the same system is
   shown as agreeing. A claim on a type a system does not list as held:
   count it as held and flag it.
5. Flag blank business_owner, administrator or records_held, and flag the
   system under decision. Never fill a blank; quote any note about it on
   the gap line.
6. Flows: F1.. in list order, then flows a note describes that the list
   lacks, only when the note names both systems and the type; owner is
   the role the note says runs it, else not stated; marked "from an
   interview, not confirmed". A note matching a listed flow: write "also
   described by [role], [date]" and any different method or frequency.
   A frequency written as an event ("when prices change") is stated.
   Flags: no owner; re-keyed by hand; method unknown or not one of the
   five (print as written); frequency not stated; from an interview, not
   confirmed; a system not listed; "[system] does not list [type] as
   held".
7. For each type held in two or more systems: if no flow carries it,
   "no flow carries [type] between [systems]"; else each holder no flow
   carrying it touches is "a copy no flow reaches".
8. Diagram: a block per sending system in S order; one line per outgoing
   flow in F order with the arrow (==> automatic or scheduled file, -->
   manual export and import, ..> re-keyed by hand, ??> unknown or
   unclear), receiver, types, frequency, F number and i for interview.
   Then: receives only; no flows recorded; not on the systems list.
9. Gaps in the fixed order of the output format, "none" where empty.
10. Duplicate records of truth: each disputed type, every claim with its
   basis (quote the note), where else held, flows carrying it.
11. Previous map: systems, statuses and flows added, removed or changed;
   else "No previous map supplied; nothing compared."
12. Questions, one per finding, addressed as follows. No business owner,
   type not held, value not on the list: map reviewer. Administrator or
   records held not stated, claim not held: system's owner. Disputed:
   owners of the claiming systems together. None named or interview
   only: owners of the holding systems together. Flow with no owner,
   method or frequency missing: the flow's owner, else the sending
   system's owner. Type a system does not list as held: that system's
   owner. Flow from a note: the sending system's owner. Copy no flow
   reaches: that system's owner; where no flow carries the type, all
   holders' owners together. Named but not listed: whoever named it, or
   the map reviewer for the connections list. An addressee system with
   no owner: ask the other owners, or the map reviewer, and say so.
   Group by the role or roles that answer, alphabetical by heading
   ignoring punctuation and capitals, roles inside one heading likewise;
   within a group order by systems,
   record types in list order, flows in F order, copies, named but not
   listed; number continuously. Each question gives the facts and the
   line, flow or note, can be answered in a sentence, offers no answer.
   Re-keyed by hand alone is a gap, not a question.
13. Decisions for the map reviewer: one per disputed, none named, not
   held or interview-only type (list order), then each system with no
   owner, then each system named but not listed. Name the questions each
   waits on (about the type, a copy of it or a flow carrying it; or about
   the system). Mark "before the decision" where the system under
   decision holds or claims the type, a flow carrying it starts or ends
   there, or it is the system concerned (the system the line is about,
   only when it is the system under decision). Options: settle now; settle
   before the decision on [system]; leave open until the next annual
   review. Recommend nothing.
14. Not checked, then the trace line: "Every entry traces to the systems
   list, the connections list, the interview notes or the settings
   supplied on [Today]. This map connects to no system and changes
   nothing."

Use the output format exactly. Return the map to the map reviewer only.
If asked to choose a record of truth, pick a system to keep or buy,
connect, log in, or send the map, decline and point to the questions and
decisions.
```

## What to customize

- Your record-type list: add the kinds of record your company runs on, such as projects, contracts or service tickets, and drop those that do not apply.
- The column names of your systems and connections lists, if you keep them differently.
- The words your teams use for "the record of truth", so the notes are read the way you speak.
- Who reviews the map, and who answers for a system whose owner is away.
- Whether spreadsheets, shared folders and mailboxes go on the systems list when they are the only home of a kind of record. As written, they do.
- Where the approved map is kept, so next year's review can start from it, and which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 11 November 2026. Written by Fully Powered AI from its own published map of the work. Editorially reviewed. One trial run on the invented example, in Claude, dated 11 November 2026 (record published as public/trial.md); the clarifications made afterward (the untraceable-item rule in the instruction block, "Held in" for a type with none named, the diagram's bracket rule, the pay, performance or conduct rule and the system-under-decision flag in the instruction block, and the rules on part-type claims, matching words, event frequencies, role order in headings and the system concerned) have not been run again. Not yet tested in a client environment and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
