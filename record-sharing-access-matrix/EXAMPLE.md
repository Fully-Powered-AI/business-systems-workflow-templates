# Record sharing access matrix: an invented example

*Illustrative example with invented data.* The company, the CRM, the roles, the rule names and the owners below are all invented. Wyndhollow Trade Supply is an invented distributor. Its CRM owner has an approved access policy and runs the matrix on Tuesday 10 November 2026, before the CRM administrator configures anything. First come the inputs the CRM owner supplied, in full, then the matrix the capability returned.

## The inputs

### 1. Settings

```
System: Wyndhollow CRM
Review date: Tuesday 10 November 2026
Access order, lowest to highest: None, Read, Edit, Full
Run by: the CRM owner
```

### 2. Sharing export

```
record_type,role,user_group,current_access,source,detail
Accounts,Sales rep,internal,Edit,base setting,
Accounts,Sales manager,internal,Edit,base setting,
Accounts,Support rep,internal,Read,base setting,
Accounts,Finance analyst,internal,Read,base setting,
Accounts,Partner user,external,Read,sharing rule,Partner-owned accounts
Contacts,Sales rep,internal,Edit,inherited,Accounts
Contacts,Support rep,internal,Read,base setting,
Contacts,Customer portal user,external,None,base setting,
Opportunities,Sales rep,internal,Edit,base setting,
Opportunities,Sales manager,internal,Edit,base setting,
Opportunities,Finance analyst,internal,None,base setting,
Opportunities,Partner user,external,None,base setting,
Quotes,Sales rep,internal,Edit,inherited,Opportunities
Quotes,Finance analyst,internal,Read,base setting,
Quotes,Partner user,external,Read,platform fixed,
Cases,Support rep,internal,Full,base setting,
Cases,Finance analyst,internal,Read,sharing rule,Finance billing cases
Cases,Customer portal user,external,Read,sharing rule,Own cases only
Cases,Partner user,external,None,base setting,
```

### 3. Approved access policy

```
record_type,role,user_group,approved_access,exception_ref
Accounts,Sales rep,internal,Read,
Accounts,Sales manager,internal,Edit,
Accounts,Support rep,internal,Read,
Accounts,Partner user,external,None,
Contacts,Sales rep,internal,Edit,
Contacts,Support rep,internal,Edit,
Contacts,Customer portal user,external,Read,
Opportunities,Sales rep,internal,Edit,
Opportunities,Sales manager,internal,Full,
Opportunities,Finance analyst,internal,Read,
Opportunities,Partner user,external,Read,EXC-07
Quotes,Sales rep,internal,Edit,
Quotes,Finance analyst,internal,Read,
Quotes,Partner user,external,None,
Cases,Support rep,internal,Full,
Cases,Sales rep,internal,Read,
Cases,Customer portal user,external,Read,
Cases,Partner user,external,None,
```

### 4. System-owner list

```
record_type,system_owner
Accounts,Sales operations lead
Contacts,Sales operations lead
Opportunities,Sales operations lead
Quotes,Finance manager
Cases,Support lead
```

## The output

**SHARING ACCESS MATRIX: Wyndhollow CRM, Tuesday 10 November 2026**

**For:** the CRM owner, for the system owners, the CRM administrator and security. Access order, lowest to highest: None, Read, Edit, Full. Nothing has been changed or granted.

**Compared:** 19 export rows, 18 policy rows, 5 record types, 6 roles (4 internal, 2 external). Not supplied: none.

**Tie-out:** 18 policy rows = 5 widen + 2 narrow + 7 stay the same + 4 unknown. 19 export rows = 17 matched to a policy row + 2 outside the policy.

**Widens: 5**

- P07. Contacts, Customer portal user (external): None → Read. Current comes from base setting.
- P11. Opportunities, Partner user (external): None → Read. Current comes from base setting. Exception EXC-07.
- P06. Contacts, Support rep (internal): Read → Edit. Current comes from base setting.
- P09. Opportunities, Sales manager (internal): Edit → Full. Current comes from base setting.
- P10. Opportunities, Finance analyst (internal): None → Read. Current comes from base setting.

**Narrows: 2**

- P04. Accounts, Partner user (external): Read → None. Current comes from sharing rule: Partner-owned accounts.
- P01. Accounts, Sales rep (internal): Edit → Read. Current comes from base setting.

**Stays the same: 7**

- P17. Cases, Customer portal user (external): Read. Current comes from sharing rule: Own cases only.
- P18. Cases, Partner user (external): None.
- P02. Accounts, Sales manager (internal): Edit.
- P03. Accounts, Support rep (internal): Read.
- P08. Opportunities, Sales rep (internal): Edit.
- P13. Quotes, Finance analyst (internal): Read.
- P15. Cases, Support rep (internal): Full.

**Unknown: 4**

- P14. Quotes, Partner user (external): export shows Read, policy proposes None. Why unknown: set by the platform.
- P05. Contacts, Sales rep (internal): export shows Edit, policy proposes Edit. Why unknown: inherited from Accounts; P01 (Accounts, Sales rep) narrows.
- P12. Quotes, Sales rep (internal): export shows Edit, policy proposes Edit. Why unknown: inherited from Opportunities; P08 (Opportunities, Sales rep) stays the same.
- P16. Cases, Sales rep (internal): export shows no row, policy proposes Read. Why unknown: no export row.

**Outside the policy: 2**

- X04. Accounts, Finance analyst (internal): Read. Comes from base setting.
- X17. Cases, Finance analyst (internal): Read. Comes from sharing rule: Finance billing cases.

**Affected record types**

- Accounts: 0 widen, 2 narrow, 2 stay the same, 0 unknown.
- Contacts: 2 widen, 0 narrow, 0 stay the same, 1 unknown.
- Opportunities: 3 widen, 0 narrow, 1 stay the same, 0 unknown.
- Quotes: 0 widen, 0 narrow, 1 stay the same, 2 unknown.
- Cases: 0 widen, 0 narrow, 3 stay the same, 1 unknown.

**Decisions**

System owners confirm the intended access (9 items; a row with an exception also appears under security):

- Sales operations lead: P01, P04, P06, P07, P09, P10, P11, X04.
- Support lead: X17.

Question for P items: Is the proposed access what you intend for this role on this record type? Question for X items: Should the policy gain a row for this access, or should the access go?

CRM administrator resolves the unknowns before anything is implemented (4 items): P05, P12, P14, P16. Question: What does this role get on this record type today, and can the policy's access be reached by changing the configuration?

Security rules on the exceptions (1 item): P11, EXC-07. Question: Does the exception stand?

This matrix compares an export with a policy. It changes no setting, grants no access and recommends nothing. The system owners confirm intended access, the CRM administrator implements what they approve, and security rules on exceptions.
