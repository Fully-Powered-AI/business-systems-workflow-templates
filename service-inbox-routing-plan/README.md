# Service inbox routing plan

When a new service inbox is being set up, the service owner gets a routing plan: each approved address, the queue it should reach and who owns it, checks to run before it goes live, and the wrong-address risks, loop risks and unconfirmed queue owners still open. Nothing is configured.

*Capability template · Business systems and integrations · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/service-inbox-routing-plan/)*

## The outcome

Before a new service inbox goes live, the service owner can see on one page where every approved address leads. Each address has a queue it should reach, a named owner for that queue and a short list of checks someone can run once the setup is done. Where the company's current settings already send an address somewhere else, the plan shows the path step by step and says what would have to change.

The plan also lists what could go wrong, in plain terms. An address that looks almost like another one, a forward that ends in one person's mailbox, a chain of forwards that comes back to where it started, an automatic reply that could be answered by another automatic reply, a queue whose owner nobody has confirmed. Nothing is smoothed over: a gap stays a gap until a person fills it.

The systems administrator approves any configuration. The service owner accepts how the routing will behave before the inbox is switched on. The AI assistant changes no mailbox, address, rule or setting, and sends no test message.

## Who starts the work, and when

The service owner, or the person helping them, starts it when a new service inbox needs a routing plan and the list of addresses has been approved. It can be run again whenever the list, a queue owner or the current settings change, so the plan always shows what is still open.

The systems administrator supplies the current settings and makes any change. The queue owners confirm that they own their queues.

## What they supply

- **Plan settings:** the business, the service, the service owner, the administrator, the date, the company's email domains, the planned activation date and a line saying what the system does with automatic messages such as out-of-office replies.
- **The approved addresses,** one row each, with its purpose, who approved it and when, the queue it should reach and whether it sends an automatic reply.
- **The current settings:** every address, alias, forward and mailbox that exists today and where each delivers.
- **The queues,** with an owner, whether the owner has confirmed, opening hours and a backup.
- **Test scenarios,** if the service owner already has some: what is sent to which address and where it should land.

No connection to a mail system is needed, and the capability never asks for a password, a login code or a key.

## What comes out

One plan in a fixed order. It opens with a summary and gives a block for each approved address: its purpose, the queue and owner, the path it takes today, the proposed routing and the change the administrator would need to consider. It then lists the queues, the other addresses found in the current settings, the checks to run before activation, and a numbered register of wrong-address risks, loop risks, unconfirmed queue owners and other gaps.

It ends with the two decisions that belong to people and a line saying nothing has been created, changed or sent.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Business systems and integrations](https://fullypowered.ai/functions/business-systems-and-integrations/), where the owner of the systems has to know what a new address will do before it is switched on.
- [Customer support and service](https://fullypowered.ai/functions/customer-support-and-service/), where a service inbox feeds a queue that people have to staff.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where support and billing inboxes multiply with each product.
- [Ecommerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where returns, refunds and order questions each get their own address.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where a shared client inbox replaces a partner's own mailbox.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/), when addresses accumulate faster than anyone records where they go.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/), where old forwards and aliases still sit under the new setup.

It does not sort the mail that arrives ([inbox triage](https://fullypowered.ai/capabilities/inbox-triage/)), set reply targets ([support service level definition](https://fullypowered.ai/capabilities/support-service-level-definition/)) or sort tickets once they exist ([support ticket triage](https://fullypowered.ai/capabilities/support-ticket-triage/)). It covers the step before those: where each address leads.

## What has to change for your company

- **Your domains.** List every domain that counts as yours, so the plan can tell an internal address from one outside.
- **Your words.** Use the kinds your mail system uses for an address, alias, forward, shared mailbox and personal mailbox, or rename them once to the defaults. When a header does not match, the assistant stops and asks.
- **Your queues and owners.** Name each queue as your help desk does, and say who owns it and who covers.
- **Your automatic messages.** State once what your system does with out-of-office replies and bounces, so the plan can check for loops.
- **Your sign-off.** Decide who is the systems administrator and who is the service owner for each inbox.

## What has been checked

Fully Powered AI wrote this capability template. It was editorially reviewed on 10 November 2026. It was tried once on its invented example, on an earlier wording of the instructions, in Claude on 10 November 2026; the run was not blind, and the record is published with it. It has not been tested in a client environment or as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on an inbox your administrator has already set up, with cases written in advance: a forward that loops, an address one letter from another, a queue with an unconfirmed owner, an automatic reply with no stated handling. The administrator checks every path against the real settings before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/capabilities/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete capability template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the capability drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related capabilities

- [Inbox triage](https://fullypowered.ai/capabilities/inbox-triage/)
- [Support service level definition](https://fullypowered.ai/capabilities/support-service-level-definition/)
- [Support ticket triage](https://fullypowered.ai/capabilities/support-ticket-triage/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
