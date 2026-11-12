# Record sharing access matrix

When an approved access policy has to reach the CRM, the system owner lays the current sharing setup beside the proposed one, by record type and by role, internal and external. Every change is a question for its owner; inherited and platform-fixed settings are marked unknown.

*Workflow template · Business systems and integrations · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflow templates/record-sharing-access-matrix/)*

## The outcome

The people who must agree to a sharing change see its effect before anyone touches a setting. For every record type and every role, internal or external, the matrix shows what the export says people have today, what the approved policy says they should have, and whether the change widens access, narrows it or leaves it alone.

Some rows cannot be judged from an export. Access a record type takes from another record type, a setting the platform fixes, a role the export does not list for that record type and two export rows that disagree are all marked unknown, with the reason, and are never guessed. Access the export grants that the policy does not mention is listed apart, so nothing hides outside the policy.

The system owners confirm the access they intend. The CRM administrator resolves the unknowns and implements only what the owners have confirmed. Security rules on any exception. The assistant changes no setting and grants no access.

## Who starts the work, and when

The CRM owner or the CRM administrator starts it once an access policy has been approved and before anyone configures it. It runs again when the policy changes or when the export is refreshed after a first round of changes. The system owners, the CRM administrator and security each read their own part of the result.

## What they supply

- **The sharing export:** one row for each record type and role, with whether the role is internal or external, the access it has today, where that access comes from and the detail of the rule behind it.
- **The approved access policy:** one row for each record type and role, with the access the policy gives and, where one exists, the reference of an approved exception.
- **The system-owner list:** who confirms the intended access for each record type.
- **The settings:** the system's name, the review date and the order of the access levels, from lowest to highest.

The export holds settings, not people. No customer records, individual user names or passwords belong in it.

## What comes out

One dated matrix in a fixed order, with a tie-out line that accounts for every policy row and every export row. Then five lists: access that widens; access that narrows; access that stays the same; unknowns, each with its reason; and access in the export that the policy does not mention. External roles come first in each list. A count by record type shows which parts of the CRM the change reaches. The decisions close the matrix, grouped by system owner, CRM administrator and security.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Business systems and integrations](https://fullypowered.ai/functions/business-systems-and-integrations/), where the CRM owner turns an approved policy into configuration.
- [Information security](https://fullypowered.ai/functions/information-security/), which owns the policy and any exception to it.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where partner and customer portals put external users into the CRM.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where who sees which client record is a daily question.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/), where distributors and partners reach opportunity and quote records.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/), where sharing settings have grown over years and nobody holds the whole picture.
- [Acquisitions and integration](https://fullypowered.ai/situations/acquisitions-and-integration/), when two sets of access rules have to become one.

The reading of user accounts against staff lists is a different piece of work; [learning system access review](https://fullypowered.ai/workflows/learning-system-access-review/) does it for a learning system. This workflow template reads sharing settings against a policy and looks at no individual's account.

## What has to change for your company

Name your record types and roles exactly as your CRM does, because the assistant matches names and does not guess at near misses. Decide the order of your access levels and what each one means in your system. Agree who owns each record type and who may rule on an exception. Decide which settings your platform fixes, so the administrator can answer the unknowns quickly. Fix the export's columns once. It runs in ChatGPT, Claude, Copilot or Gemini from files you supply; it needs no connection to the CRM.

## What has been checked

Fully Powered AI wrote this workflow template. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026, and the record of that run is published with it. The run was not blind: the model had seen the example's published output before it worked the matrix again from the inputs. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a sharing change your administrator has already worked through, with cases written in advance: a role missing from the export, two export rows that disagree, an inherited setting whose parent also changes, an exception with no owner. The administrator checks every row against the CRM before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/) sets those cases up.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete workflow template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the workflow template drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related workflow templates

- [Learning system access review](https://fullypowered.ai/workflow templates/learning-system-access-review/)
- [Pilot acceptance-test preparation](https://fullypowered.ai/workflow templates/pilot-acceptance-test-preparation/)
- [Temporary change register](https://fullypowered.ai/workflow templates/temporary-change-register/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
