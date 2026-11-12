# Record sharing access matrix

Workflow template, version 0.1.0.

## Purpose

Lay the CRM's current sharing setup, from an export, beside the setup an approved access policy proposes, by record type and by role, internal and external. Each policy row is sorted as widening, narrowing, staying the same or unknown, and access the export grants that the policy does not mention is listed apart. Access that comes from another record type, access the platform fixes, a missing export row and export rows that disagree are marked unknown with the reason. The assistant prepares the matrix; it changes no setting, grants no access, approves nothing and decides nothing.

## When to use it and when not to

Use it when an access policy has been approved and has to reach the CRM's configuration, before anyone changes a setting. Run it again when the policy changes, or on a fresh export after a first round of changes.

Do not use it:

- to write or change the access policy. The policy is supplied, approved and owned by others;
- to review individual user accounts, dormant users or leavers. That is a different piece of work; see learning system access review for one example;
- to say what the effective access is where the export cannot show it. Those rows stay unknown for the administrator to resolve;
- to change a setting, grant an exception or switch anything on.

## Roles

- **Runs it:** the CRM owner or the CRM administrator.
- **Confirms the intended access for a record type:** its system owner.
- **Resolves the unknowns and, once the owners have confirmed, implements the change:** the CRM administrator.
- **Rules on exceptions to the policy:** security.
- **Receives the matrix:** business systems, security and application owners.

## Inputs

1. **The sharing export,** one row for each record type and role. Default headers: `record_type,role,user_group,current_access,source,detail`. `user_group` is internal or external. `source` is one of: base setting (what the role gets by default or through its permission set), sharing rule, inherited (taken from another record type; `detail` names it), platform fixed (a setting the platform does not let the administrator change). For a sharing rule, `detail` names the rule. If the export is missing, stop. If a header does not match, stop and ask which column is which. Do not guess.
2. **The approved access policy,** one row for each record type and role. Default headers: `record_type,role,user_group,approved_access,exception_ref`. `exception_ref` is blank unless security has approved an exception for that row. If it is missing, stop. If a header does not match, stop and ask.
3. **The system-owner list.** Default headers: `record_type,system_owner`. If missing, write "owner list not supplied" and put every item under "owner not assigned".
4. **The settings:** the system's name, the review date, who is running it and the order of the access levels, lowest to highest. Default order: None, Read, Edit, Full. If the name or date is missing, use "system not named" or "date not given". If who is running it is missing, write "run by: not given". If the order is missing, use the default and say so.

The assistant works from files and notes the person supplies. It needs no connection to the CRM and never asks for a password or a login code. If the export holds an individual's name, a customer record or a secret, it does not repeat it; it tells the person to remove it from the source.

## The procedure

1. **Check the inputs.** Confirm the headers. Confirm every `current_access` and `approved_access` value is on the access-level order; if one is not, stop and ask for a mapping. Trim spaces and ignore capital letters when matching names, and match nothing else. If a record type or role in the policy appears nowhere in the export, stop and ask whether it is named differently. A record type or role that is only in the export is not an error; its rows are listed as outside the policy. If the same record type and role are marked internal in one file and external in the other, stop and ask.
2. **Number the rows.** Number the policy rows P01, P02 and so on in the order given. Number the export rows X01, X02 and so on in the order given; the numbers are used only for export rows outside the policy.
3. **Match.** For each policy row, find the export rows with the same record type and role.
4. **Sort each policy row into exactly one group,** taking the first rule that applies:
   1. No matching export row: Unknown, "no export row".
   2. Matching rows show different levels: Unknown, "export rows disagree", with each level and source.
   3. Any matching row has a source of inherited, or platform fixed, or a source not on the list: Unknown, with the reason "inherited from [record type]", "set by the platform" or "source [value] not recognised". An inherited row also states what the parent row did: take the policy row for the named parent record type and the same role, and say it widens, narrows or stays the same, or that it is unknown or not in the policy.
   4. Otherwise compare the levels on the order. Proposed above current: Widens. Proposed below current: Narrows. Equal: Stays the same.
5. **Find the outside rows.** Every export row whose record type and role match no policy row is outside the policy. List it with its level and source.
6. **Order each list.** External roles first, then internal, each in policy order (outside rows in export order).
7. **Count by record type.** For each record type in the policy, count its rows in each group. The counts add up to the policy rows.
8. **Tie out.** Policy rows = widen + narrow + stay the same + unknown. Export rows = export rows matched to a policy row + export rows outside the policy. If either fails, stop and report the figures.
9. **Assign the decisions.**
   - System owners: every widening, every narrowing and every outside row, under the owner of its record type. A record type with no owner is "owner not assigned".
   - CRM administrator: every unknown.
   - Security: every policy row that carries an exception reference, whatever group it is in.
10. **Return the draft** to the person who ran it. The system owners confirm, the administrator resolves the unknowns, and a person decides what happens next. Recommend nothing unless asked.

## Exceptions and stop conditions

- **Export or policy missing, a header that does not match, an access level off the order, a policy name found nowhere in the export, or a user group that disagrees:** stop and ask.
- **The tie-out fails:** stop; report the figures and the difference.
- **Two policy rows for the same record type and role:** stop and ask which stands.
- **A policy row for a role that the export shows under other record types but not this one:** the name matches, so it is not a mismatch; the row is Unknown, "no export row".
- **Asked to change a setting, grant or remove access, approve an exception, or say what a user can see today:** decline. Name the role that decides: the system owner for intent, the administrator for implementation, security for exceptions.
- **Asked to guess an inherited or platform-fixed result:** decline; the row stays unknown.
- **The export or notes contain a password, a login code, an individual's record or a secret:** do not repeat it; tell the person to remove it from the source.

## Output format

```
SHARING ACCESS MATRIX: [system], [review date]

For: [who ran it], for the system owners, the CRM administrator and security. Access order, lowest to highest: [levels]. Nothing has been changed or granted.

Compared: [n] export rows, [n] policy rows, [n] record types, [n] roles ([n] internal, [n] external). Not supplied: [list / none].

Tie-out: [n] policy rows = [n] widen + [n] narrow + [n] stay the same + [n] unknown. [n] export rows = [n] matched to a policy row + [n] outside the policy.

Widens: [n]
[P-number]. [Record type], [role] ([internal / external]): [current] → [proposed]. Current comes from [source, with its detail]. [Exception [ref].]

Narrows: [n]
[P-number]. [Record type], [role] ([internal / external]): [current] → [proposed]. Current comes from [source, with its detail]. [Exception [ref].]

Stays the same: [n]
[P-number]. [Record type], [role] ([internal / external]): [level]. [Current comes from [sharing rule, with its detail].] [Exception [ref].]

Unknown: [n]
[P-number]. [Record type], [role] ([internal / external]): export shows [level / no row / each level with its source], policy proposes [level]. Why unknown: [reason]. [Exception [ref].]

Outside the policy: [n]
[X-number]. [Record type], [role] ([internal / external]): [level]. Comes from [source, with its detail].

Affected record types
[Record type]: [n] widen, [n] narrow, [n] stay the same, [n] unknown.

Decisions
System owners confirm the intended access ([n] items; a row with an exception also appears under security):
[Owner]: [ids].
Question for P items: Is the proposed access what you intend for this role on this
record type? Question for X items: Should the policy gain a row for this access, or
should the access go?
CRM administrator resolves the unknowns before anything is implemented ([n] items):
[ids]. Question: What does this role get on this record type today, and can the policy's access be reached by changing the configuration?
Security rules on the exceptions ([n] items): [id, exception reference]. Question: Does the exception stand?

This matrix compares an export with a policy. It changes no setting, grants no
access and recommends nothing. The system owners confirm intended access, the CRM
administrator implements what they approve, and security rules on exceptions.
```

Where a list is empty, print "None." under its heading. On a Stays the same row print the source only when it is a sharing rule, so the rule that holds the access shows; for any other source print the level alone. On an Unknown row where the export rows disagree, print each level with its source in place of the single level, for example "export shows Read from base setting and Edit from sharing rule: Finance billing cases, policy proposes Read". In the decisions, list only owners with items; if nobody has any, print "None." under the line. Where a row's detail is empty, print the source alone, for example "Current comes from base setting." Count roles as the different role names across both files, not role entries per record type. Count the owner items by the ids listed, so a row with an exception is counted under its owner and again under security. List the ids for each owner in number order, P items before X items. Bullets for the rows under each heading are fine.

## Reviewer checklist

1. Every policy row appears once, in one group, and the tie-out is arithmetically correct. (CRM administrator)
2. Every export row is either matched to a policy row or listed as outside the policy. (CRM administrator)
3. Every Widens and Narrows row is true against the access order and the export values. (CRM administrator)
4. Every unknown has a reason, and none of them has been resolved by guessing. (CRM administrator)
5. Each inherited row names its parent and the parent row's result. (CRM administrator)
6. External roles come first in every list. (CRM administrator)
7. Every item is assigned to the right owner, and every exception reference appears under security. (System owners, security)
8. The matrix changes nothing and recommends nothing. (CRM owner)

## Acceptance tests

Proposed tests. None has been run.

1. **Ordinary change.** A complete export and policy with some widening, some narrowing and some rows unchanged. Expected: each row in the right group; tie-out correct.
2. **Inherited access.** A record type takes its access from a parent whose row narrows in the same policy. Expected: Unknown, naming the parent and saying it narrows.
3. **Platform-fixed setting.** The export marks a row platform fixed and the policy proposes a lower level. Expected: Unknown, "set by the platform"; not Narrows.
4. **Missing export row.** A role in the policy has no row for one record type but appears elsewhere in the export. Expected: Unknown, "no export row".
5. **Disagreeing export rows.** Two rows for the same record type and role show Read and Edit. Expected: Unknown, "export rows disagree", with both levels.
6. **Access outside the policy.** An export row for a role and record type the policy does not mention. Expected: listed under Outside the policy and assigned to the system owner.
7. **Exception.** A policy row with an exception reference that also widens. Expected: under Widens for the system owner and under security's list.
8. **Header does not match.** The export calls `current_access` "level". Expected: stops and asks.
9. **Access level off the order.** The export says "Read/Write". Expected: stops and asks for a mapping.
10. **Role named differently.** The policy says "Sales Rep" and "Sales representative" appears in the export. Expected: stops and asks; does not match by guess.
11. **Asked to change a setting or approve an exception.** Expected: declines and names the role that decides.
12. **Nothing changes.** A policy identical to the export. Expected: every row under Stays the same, empty lists print "None.", and no decisions beyond any unknowns.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a record sharing access matrix for the people who run a CRM.
You never change a setting, grant or remove access, approve an exception,
or decide anything the matrix lists. You never ask for a password or a
login code.

The user will supply: the sharing export (default headers record_type,
role, user_group, current_access, source, detail); the approved access
policy (record_type, role, user_group, approved_access, exception_ref);
the system-owner list (record_type, system_owner); and the settings: the
system's name, the review date, who is running it and the order of the
access levels, lowest to highest (default None, Read, Edit, Full). If the export or the policy
is missing, stop and say so. If a header does not match, an access level
is not on the order, a record type or role in the policy appears nowhere in the export, a
user group disagrees, or two policy rows have the same record type and
role, stop and ask. Match names after trimming spaces and ignoring capital
letters, and in no other way; do not guess or match near names. If the
owner list is missing, write "owner list not supplied" and put every item
under "owner not assigned". If the system name or the review date is
missing, write "system not named" or "date not given"; if who is running
it is missing, write "run by: not given". If the access
order is missing, use the default and say so.

1. Number the policy rows P01, P02 and so on in the order given, and the
   export rows X01, X02 and so on.
2. For each policy row, find the export rows with the same record type and
   role, and put the row in exactly one group, taking the first rule that
   applies:
   - no matching export row (even if the role appears under other record
     types): Unknown, "no export row";
   - matching rows show different levels: Unknown, "export rows
     disagree", with each level and source;
   - any matching row is inherited, platform fixed, or has a source you
     do not recognise: Unknown, with the reason; for an inherited row,
     name the parent record type and say whether the policy row for that
     parent and the same role widens, narrows or stays the same, or is
     unknown or not in the policy;
   - otherwise compare on the access order: proposed above current is
     Widens, below is Narrows, equal is Stays the same.
3. List every export row that matches no policy row as outside the policy.
4. Within each list, put external roles first, then internal, in policy
   order (outside rows in export order). Count each record type's rows in
   each group.
5. Tie out: policy rows = widen + narrow + stay the same + unknown, and
   export rows = matched + outside. If either fails, stop and report the
   figures.
6. Assign decisions: widenings, narrowings and outside rows to the system
   owner of the record type ("owner not assigned" if none); unknowns to
   the CRM administrator; every row with an exception reference to
   security. List the ids for each owner in number order, P items before
   X items. Count the items by the ids listed; a row that also appears
   under security counts in both lists.
7. Use the output format exactly. Print "None." under any empty list.
   Where a row's detail is empty, print the source alone ("Current comes
   from base setting."). On a Stays the same row print the source only
   when it is a sharing rule ("Current comes from sharing rule: [name]").
   On an Unknown row where the export rows disagree, print each level with
   its source in place of the single level. Count roles as the different role names across
   both files. Recommend nothing unless asked. Bullets are fine.

Never resolve an inherited or platform-fixed row by guessing. If asked to
change a setting, approve an exception or say what a user can see today,
decline and name the role that decides: the system owner for intent, the
CRM administrator for implementation, security for exceptions. Do not
repeat a password, a login code, an individual's record or a secret that
appears in the files; tell the person to remove it.
```

## What to customize

- Your record types and roles, spelled as your CRM spells them.
- The order and meaning of your access levels.
- The export's columns, and which values your CRM uses for where access comes from.
- Who owns each record type and who rules on exceptions.
- Which settings your platform fixes, so the administrator can answer the unknowns.
- Where the approved matrix is kept and who may see it.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried on its invented example in Claude on 10 November 2026; that run was not blind, and its record is published with the profile. Not tested in a client environment.
