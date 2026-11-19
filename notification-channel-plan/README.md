# Notification channel plan

Get one channel plan per business event: who is told, by which channel, with fallbacks and reply handling. Consent stays a question; nothing is sent.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See Notification channel plan on our website](https://fullypowered.ai/workflows/notification-channel-plan/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan). Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the invented ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Business systems and integrations · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/notification-channel-plan/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan)*

## The outcome

Before anyone builds the notification, the integration owner holds one plan that says, for each business event, what sets it off, how urgent it is, who is told, by which channel and in what order, and what happens when nobody answers. The gaps that usually surface after launch are written down first: a text that nobody reads replies to, an email that reports no delivery, an alert held back by a quiet-hours rule, an escalation with nobody at the end of it.

The plan is careful about what a send proves. A service accepting a message is recorded as acceptance, not delivery, and a message sent is never counted as a person confirming. Where the plan needs a rule about consent, message content or timing that nobody has supplied, it asks the responsible owner and does not guess. The integration owner approves the design; the service owner approves the message rules and timing. The AI assistant prepares the plan. It writes no message, connects to no service and changes no setting.

## Who starts the work, and when

The integration owner or business systems analyst starts it when a business event is about to get a notification, or when an existing one is being reworked. It can run again when an event is added, a channel changes or an owner answers one of the questions. The integration owner reads the plan, takes the design questions, and passes the rest to the service owner and to whoever owns consent and communication requirements.

## What they supply

- **The event definitions:** each event, what triggers it, when it can fire, who is told, how urgent it is, whether someone must confirm, and who it escalates to.
- **Recipient preferences:** the channels each group has and the order they prefer, with the hours they can be reached.
- **The channel list:** which channels are set up, who reads replies on each, and whether the channel reports delivery.
- **Approved messaging constraints,** each with who approved it.
- **The settings:** the service, today's date, the integration owner and service owner, and who answers consent questions. Your own urgency scale and confirmation windows, if you have them.

## What comes out

One plan in a fixed order. A header with the counts, then a block for each event: trigger, urgency, who is told by which channel, confirmation, timing, fallback, escalation, reply handling, repeat rule and the evidence the integration will see. Then the events that could not be planned and why, a note on each channel, the constraints applied, and numbered questions grouped by the person who must answer them.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Software technology](https://fullypowered.ai/industries/software-technology/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan), where product and billing events reach customers and on-call staff through several channels.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan), where order, stock and delivery events notify both customers and the team.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan), where a late or missing item has to reach the right person within minutes.
- [Business systems and integrations](https://fullypowered.ai/functions/business-systems-and-integrations/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan), which owns the connections that carry the events.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan), when notifications built one at a time begin to collide.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan), where old alerts still run and nobody remembers who reads the replies.

It is separate from [internal change announcement](https://fullypowered.ai/workflows/internal-change-announcement/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan), which announces one decided change to staff, and from [email sequence drafting](https://fullypowered.ai/workflows/email-sequence-drafting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan), which writes a series of emails. This plan writes no message; it decides how events reach people. [Appointment confirmation and no-show follow-up](https://fullypowered.ai/workflows/appointment-confirmation-and-no-show-follow-up/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan) prepares the contact for one kind of event.

## What has to change for your company

Set your urgency scale and how long each level waits for a confirmation. Decide which channels suit which urgency. Name the roles that answer consent questions and read replies. Keep the channel list current, because the plan can use only what it is told is in place. Agree who approves a change to the plan after launch. The plan gives no view on consent or on any communication law; those answers come from the people responsible for them.

## What has been checked

FullyPowered AI wrote this workflow template. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026, and the record is published with it. Small edits made to the instructions and the example after that run have not been run again. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on an event your integration owner already knows well, with cases written in advance: a channel that reports no delivery, an event with no urgency, a reply route nobody reads, a constraint that holds back an urgent message. The integration owner checks every line against the event definitions before anyone builds from it. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan) describes the record we keep.

- Written by FullyPowered AI.
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

- [Internal change announcement](https://fullypowered.ai/workflows/internal-change-announcement/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan)
- [Email sequence drafting](https://fullypowered.ai/workflows/email-sequence-drafting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan)
- [Appointment confirmation and no-show follow-up](https://fullypowered.ai/workflows/appointment-confirmation-and-no-show-follow-up/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=business-systems-notification-channel-plan&from=gh-notification-channel-plan).
