# Record sharing access matrix: tried once on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example in [example.md](example.md): the settings, the sharing export (19 rows), the approved access policy (18 rows) and the system-owner list for the invented company Wyndhollow Trade Supply. No client data was used. The model did not write the template.

## A limit on this trial

This record describes a third run of the same model, made on 10 November 2026 after the independent review of the second. Since the second run the instruction block and output format were extended in three small ways: the settings now include who is running it (with the fallback "run by: not given"), a Stays the same row prints its source when that source is a sharing rule, and an Unknown row whose export rows disagree prints each level with its source. Before that, between the first and second runs, the instruction block had been extended (matching rules, stop on two policy rows for one record type and role, the fallbacks for a missing owner list, system name or date, export order for outside rows) and the open points below were settled in the template; the invented company was renamed. None of the runs was blind. In each, the model saw the example's published output before it produced its own. The matrix below was worked out again from the inputs, row by row, and checked by counting, but treat its agreement with the published example as a consistency check, not independent confirmation. A blind run, made by a model that has not seen the example's output, has not been done.

## What came out

The model followed the instruction block and the output format. Every part of the format was produced.

**SHARING ACCESS MATRIX: Wyndhollow CRM, Tuesday 10 November 2026**

For: the CRM owner, for the system owners, the CRM administrator and security. Access order, lowest to highest: None, Read, Edit, Full. Nothing has been changed or granted.

Compared: 19 export rows, 18 policy rows, 5 record types, 6 roles (4 internal, 2 external). Not supplied: none.

Tie-out: 18 policy rows = 5 widen + 2 narrow + 7 stay the same + 4 unknown. 19 export rows = 17 matched to a policy row + 2 outside the policy.

Widens: 5
- P07. Contacts, Customer portal user (external): None → Read. Current comes from base setting.
- P11. Opportunities, Partner user (external): None → Read. Current comes from base setting. Exception EXC-07.
- P06. Contacts, Support rep (internal): Read → Edit. Current comes from base setting.
- P09. Opportunities, Sales manager (internal): Edit → Full. Current comes from base setting.
- P10. Opportunities, Finance analyst (internal): None → Read. Current comes from base setting.

Narrows: 2
- P04. Accounts, Partner user (external): Read → None. Current comes from sharing rule: Partner-owned accounts.
- P01. Accounts, Sales rep (internal): Edit → Read. Current comes from base setting.

Stays the same: 7
- P17. Cases, Customer portal user (external): Read. Current comes from sharing rule: Own cases only.
- P18. Cases, Partner user (external): None.
- P02. Accounts, Sales manager (internal): Edit.
- P03. Accounts, Support rep (internal): Read.
- P08. Opportunities, Sales rep (internal): Edit.
- P13. Quotes, Finance analyst (internal): Read.
- P15. Cases, Support rep (internal): Full.

Unknown: 4
- P14. Quotes, Partner user (external): export shows Read, policy proposes None. Why unknown: set by the platform.
- P05. Contacts, Sales rep (internal): export shows Edit, policy proposes Edit. Why unknown: inherited from Accounts; P01 (Accounts, Sales rep) narrows.
- P12. Quotes, Sales rep (internal): export shows Edit, policy proposes Edit. Why unknown: inherited from Opportunities; P08 (Opportunities, Sales rep) stays the same.
- P16. Cases, Sales rep (internal): export shows no row, policy proposes Read. Why unknown: no export row.

Outside the policy: 2
- X04. Accounts, Finance analyst (internal): Read. Comes from base setting.
- X17. Cases, Finance analyst (internal): Read. Comes from sharing rule: Finance billing cases.

Affected record types
- Accounts: 0 widen, 2 narrow, 2 stay the same, 0 unknown.
- Contacts: 2 widen, 0 narrow, 0 stay the same, 1 unknown.
- Opportunities: 3 widen, 0 narrow, 1 stay the same, 0 unknown.
- Quotes: 0 widen, 0 narrow, 1 stay the same, 2 unknown.
- Cases: 0 widen, 0 narrow, 3 stay the same, 1 unknown.

Decisions

System owners confirm the intended access (9 items; a row with an exception also appears under security):
- Sales operations lead: P01, P04, P06, P07, P09, P10, P11, X04.
- Support lead: X17.

Question for P items: Is the proposed access what you intend for this role on this record type? Question for X items: Should the policy gain a row for this access, or should the access go?

CRM administrator resolves the unknowns before anything is implemented (4 items): P05, P12, P14, P16. Question: What does this role get on this record type today, and can the policy's access be reached by changing the configuration?

Security rules on the exceptions (1 item): P11, EXC-07. Question: Does the exception stand?

This matrix compares an export with a policy. It changes no setting, grants no access and recommends nothing. The system owners confirm intended access, the CRM administrator implements what they approve, and security rules on exceptions.

## What was observed

- Every required part of the format was produced, and the two tie-outs add up (18 policy rows; 19 export rows). Nothing in the run called for a stop: the headers matched, every level was on the access order, every policy name appears in the export and no user group disagreed. No stop condition was tested by this run.
- The output has the same groups, counts, ordering, owners and wording as the published example. Because the model had seen that example first (see the limit above), this is a consistency check, not independent confirmation.
- The one line that differs from the second run is P17, which now shows its source, the sharing rule "Own cases only", as the extended format asks. The new rule for disagreeing export rows was not exercised, because the example has none; the fallback for a missing "run by" was not exercised either, because the example supplies it.
- No fact appears in the output that is not in the inputs. The "For" line takes the CRM owner from the settings line "Run by".
- The first run found six places where the instructions were open. The template now settles five: an empty detail prints the source alone; roles are counted as the different role names across both files; owner items are counted by the ids listed, so a row with an exception counts under its owner and again under security; ids within an owner go in number order, P items before X items; and an owner with no items is left out. This run followed those rules and they gave the same figures and wording as before (6 roles, 9 owner items, base-setting rows printed without detail). The sixth, that an inherited row is Unknown even when its level equals the proposed level (P05, P12), was already clear in the template; the model did so, and a reader may still expect "Stays the same".
- The acceptance tests in the template are marked as proposed and not yet run. This trial exercised tests 1, 2, 3, 4, 6 and 7 only in the sense that the example contains those cases (ordinary change, inherited access, platform-fixed, missing export row, outside the policy, an exception). It did not exercise the stop conditions, the nothing-changes case, or declining a request to change a setting.
- This is three runs of one model on one invented example. It does not show how the template behaves with a real CRM export, a different product or a larger file.
