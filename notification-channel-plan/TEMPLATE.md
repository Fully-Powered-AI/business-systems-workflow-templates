# Notification channel plan

Capability template, version 0.1.0.

## Purpose

Prepare one channel plan for a set of business events that must notify people. For each event the plan gives the trigger, when it can fire, the urgency, who is told by which channel and in what order, whether someone must confirm and by what sign, the timing, the fallback, the escalation, how replies are handled, the repeat rule and the evidence the integration will actually see. Gaps are written as numbered questions for the person who can answer them, including every question of consent, message content and timing, which the plan never settles. The assistant prepares; it writes no message, connects to no service, changes no setting and gives no view on consent or on any communication law.

## When to use it and when not to

Use it when a business event is about to get a notification, when an existing one is being reworked, or when an event, a channel or an owner changes. Run it again once the owners have answered the questions.

It is a different piece of work from these, and does not replace them:

- announcing one decided change to staff, which is a set of messages for a moment in time;
- writing a series of emails, which is about the words and the sequence;
- tracing why a message failed to arrive, which starts from one message and its error history;
- choosing a messaging provider or sender.

Do not use it:

- to write or approve any message, or to decide what a message may say. The service owner approves message rules;
- to decide whether a person has agreed to be contacted, or what a communication law requires. The plan asks the owner of consent and communication requirements;
- when there are no event definitions. There is nothing to plan.

## Roles

- **Runs it:** the integration owner or a business systems analyst.
- **Approves the design:** the integration owner.
- **Approves message rules and timing:** the service owner.
- **Answers consent and communication questions:** the owner of consent and communication requirements, such as a compliance lead.
- **Reads replies on a channel:** the role named on the channel list.
- **Builds and switches anything on:** people the integration owner names. The assistant does none of it.

## Inputs

1. **Settings.** The service or area, today's date, the integration owner, the service owner and the owner of consent and communication requirements. If the service or the integration owner is missing, stop and ask. If the other owners are missing, write "owner not named" in the header and under the questions.
2. **Event definitions.** One row per event. As an export the default headers are Event, Trigger, Can fire between, Recipient group, Urgency, Needs confirmation, Confirmation sign, Escalation role. If a header differs, stop and ask which column is which. If there are no event definitions, stop. "Can fire between" is optional: where it is absent, write "hours not stated" and give timelines in minutes only. Where only an end time is given ("up to 18:30"), check the latest case only and say so.
3. **Recipient preferences.** One row per recipient group. Default headers: Recipient group, Channels they have, Preference order, Reachable hours. If a header differs, stop and ask. If they are not supplied, write "recipient preferences not supplied", plan no event, and ask for them.
4. **The channel list.** One row per channel. Default headers: Channel, In place, Reply handled by, Delivery status reported. "In place" and "Delivery status reported" are yes, no or unknown. If a header differs, stop and ask. If the list is missing, stop.
5. **Approved constraints.** One row per rule about messages or timing that someone has approved. Default headers: Constraint, Applies to, Approved by. If missing, write "no constraints supplied".
6. **Urgency scale, confirmation windows and channel suitability.** If missing, use the defaults given in step 3 (urgency scale), step 5 (channel suitability) and step 6 (confirmation windows), and say so in the header. To set your own, supply them with the inputs and they replace the defaults.

The assistant works from what the person supplies. It needs no connection to any messaging service, and never asks for a password, a key or a login code. If any are present in the inputs, it does not repeat them and tells the person to remove them.

## The procedure

1. **Check the inputs.** Confirm the service and count the events. Number the events E1, E2 and so on in the order supplied, and the constraints K1, K2 and so on. Match recipient groups to the preferences by name. A qualifier in brackets after a group name, such as "Customer (bookings that day)", narrows who is told and is not a new group. A group with no preferences row is not planned: list the event under "Events not planned".
2. **Find the events that cannot be planned.** An event with no trigger, no recipient group or no urgency is not planned. List it under "Events not planned" with the missing item and a question. A missing urgency is a question to the service owner. Never guess the missing item.
3. **Set the urgency.** Use the level supplied. Default scale: Immediate means someone acts within minutes; Same day means within the working day; Routine means the next working day or later and may be batched. An urgency that is not on the scale, supplied or default, is treated as missing.
4. **Read the confirmation.** An event needs confirmation only where the definition says yes. A confirmation is a sign a person gives that they have the matter, such as a tap in an application, a reply or an action in a system. A message sent is not a confirmation, and a sending service accepting a message is not a confirmation or proof of delivery. Where the definition says yes and names no sign, write "sign not stated", plan the event without a confirmation step, and ask.
5. **Choose the channels.** For each event, take the recipient group's channels in the order of its preference list and keep those that are in place. Then apply the suitability rule. Default suitability: for Immediate, text, phone call, staff application, push notification or chat, and email only when it is all that remains, which includes after the other suitable channels have failed or are not in place; for Same day, those and email; for Routine, any channel. Then apply the constraints that name the recipient group. A constraint that forbids a channel for the group removes it; a constraint on hours does not remove the channel but holds it (step 6). A channel the group has and that is in place, but that its preference order leaves out, is not used: say so and ask the integration owner whether to add it. The first channel left is the primary. If a constraint removes every suitable channel for a person, use the best channel that remains, and ask. A channel the group prefers but that is not in place is skipped, and the plan says so. If an event needs confirmation, its primary must either report delivery or be paired with a fallback that does; a channel whose delivery status is "no" or "unknown" counts as reporting none.
6. **Set the timing.** For an event that needs no confirmation, send at once, unless a constraint or the recipient group's reachable hours hold it; say until when. A held Immediate event is a question to the service owner. For an event that needs confirmation, give a timeline in minutes after the trigger: step 0 is the primary; the confirmation window is the default for the urgency (Immediate 15 minutes, Same day 2 hours, Routine the next working day); each step happens only if nobody has confirmed. Where the trigger hours are known, work out the clock time of each step in the latest case and check each falls in the recipient's reachable hours; say so, or raise a question for any that does not. Where only an end time is given, check the latest case only and say so.
7. **Set the fallback.** For an event that needs confirmation, the fallback is the next suitable channel for the same person, one step after the first window. For an event that needs none, the fallback happens only when the primary channel reports a failed delivery, and goes to the next suitable channel. If the primary reports no delivery status, write "none possible, because [channel] reports no delivery". Write a question for every "none possible".
8. **Set the escalation.** Where a confirmation is needed and the definition names an escalation role, that role is told one window after the fallback, by its own first suitable channel in place. After that step plus one more window the plan stops: nothing further is sent automatically, and a question asks who is told next. Where the confirmation sign names only the first recipient, a separate question asks how the escalation role confirms. Where no escalation role is named, write "none supplied" and ask. One attempt per channel and per person. The plan never loops.
9. **Plan the reply handling.** For each channel used, state who reads replies and when, from the channel list. If the channel list names nobody, write "replies unread" and ask the owner of consent and communication requirements who reads a reply that asks to stop or complains. Where a channel carries the confirmation sign, say that the sign is read there and that any other reply on it is unread unless the list names a reader; the question still applies to the other replies. Where the confirmation sign is not a reply on that channel, say that a reply there confirms nothing.
10. **Apply the constraints.** Attach each constraint to the events whose recipients and channels it names, and say how it changes the plan. A constraint is "used" in an event when the event tells a recipient it names by a channel it names, even if it changes nothing there; say that it changes nothing. Say "does not affect this event" only where the event never uses that recipient or channel. Never override a constraint, and never write a message rule of your own. If a constraint appears incomplete or in conflict with another, quote both and ask its approver. A constraint about consent is applied as written; the plan gives no view on whether it is enough, and a question asks the owner of consent and communication requirements.
11. **State the repeat rule.** Use the rule supplied for the event. If none, write "not stated" and ask the service owner once, for all events that lack it, whether a person is to be told twice if a trigger fires twice.
12. **State the delivery evidence.** For each channel in an event, say what the integration will see: a delivery report where the channel reports one, or "sending accepted only, which is not proof of delivery". For a confirmation, say the sign.
13. **Write the questions.** Number them Q1, Q2 and so on, grouped under three headings in this order: the integration owner (design and channels), the service owner (message rules and timing), and the owner of consent and communication requirements. A missing urgency, a missing repeat rule and whether reaching someone only by a channel that reports no delivery is enough go to the service owner. Within a group, follow the order of the events. Each question gives the event, the facts and one question. A question about the same gap on several events is one question naming all of them. Recommend nothing unless the integration owner asks.
14. **Return the draft** to the person who ran it. The integration owner approves the design, the service owner approves message rules and timing, and a person builds and switches on anything.

## Exceptions and stop conditions

- **No event definitions, no channel list, or no service or integration owner:** stop and ask.
- **A header that does not match the default:** stop and ask which column is which.
- **An event missing its trigger, recipient group or urgency:** not planned; listed with a question.
- **Asked to write a message, send a test, connect a service, change a setting or switch anything on:** decline and name the role that does it.
- **Asked whether a person has agreed to be contacted, whether a message is allowed, or what any communication law requires:** decline, record it as a question for the owner of consent and communication requirements, and apply only the constraints supplied.
- **The inputs contain a password, a key, a login code or a person's contact details:** do not repeat them in the plan; tell the person to remove them.
- **Two constraints conflict, or a constraint holds back an Immediate event:** apply what was approved, show the effect and ask the approver.
- **Asked to make a fallback appear where none is possible:** decline; write "none possible" and the reason.

## Output format

```
NOTIFICATION CHANNEL PLAN: [service or area]

For: [integration owner], integration owner, who approves the design; [service owner], service owner, who approves message rules and timing. Prepared: [weekday date], from [n] event definitions, [recipient preferences / recipient preferences not supplied], a channel list of [n] channels, [n] constraints / no constraints supplied.
Urgency scale: [levels with meanings]. Confirmation windows: [levels with times]. Defaults used: [list / none]. [Owner not named: ...]
Events: [n] ([n] planned, [n] not planned). Channels used: [list]. Questions: [n].

[E number] [Event name]
Trigger: [as supplied]. Can fire: [hours / hours not stated].
Urgency: [level].
Told: [recipient group], by [primary channel][; exception for a constraint][; channel held but not in the preference order, with the question number].
Confirmation: [not needed / needed. Sign: [sign / sign not stated]. Window: [time]].
Timing: [at once / held until [time] ([K number]) / timeline in minutes after the trigger, with clock times for the latest case].
Fallback: [step / none possible, because [reason]].
Escalation: [role, channel, minutes / none supplied / not needed][; channel held but not in the preference order, with the question number].
Reply handling: [channel, who reads it and when / replies unread].
Repeat rule: [as supplied / not stated].
Delivery evidence: [per channel].
Constraints applied: [K numbers, each with its effect / none].
Open points: [Q numbers / none].

Events not planned
[E number] [Event name]: [what is missing]. [Q number].
[Or: None.]

Channels
[Channel]: [in place / not in place]. Delivery status reported: [yes / no / unknown]. Replies: [who reads, when / unread]. Used by: [E numbers / none].

Constraints applied
[K number] [Constraint]. Applies to: [..]. Approved by: [..]. Used in: [E numbers / none].
[Or: No constraints supplied.]

Questions for the owners: [n]
For [integration owner], integration owner
[Q number]. [E numbers.] [Facts.] [The question.]
For [service owner], service owner
[Q number]. ...
For [owner], who answers consent and communication requirements
[Q number]. ...
[Under a heading with no question: None.]

Draft for [integration owner]'s approval of the design and [service owner]'s approval of message rules and timing. Nothing has been sent, connected or changed, and no message wording has been written.
```

## Reviewer checklist

1. Every event on the supplied list appears once, as planned or as not planned, with its trigger and recipient group unchanged. (Integration owner)
2. Every channel used is in place on the channel list and follows the recipient's preference order. (Integration owner)
3. Every confirmation names a sign supplied in the event definition, and no message sent or accepted is counted as one. (Integration owner)
4. Every timeline adds up and every clock time falls in the recipient's reachable hours, or has a question. (Integration owner)
5. Every "none possible" fallback and every unread reply route has a question. (Integration owner)
6. Every constraint is applied as approved and none is changed or added. (Service owner)
7. No message wording, consent ruling or legal view appears anywhere. (Service owner and the owner of consent and communication requirements)
8. The question count matches the header, and each question sits under the right owner. (Integration owner)

## Acceptance tests

Proposed tests. None has been run.

1. **Ordinary event.** A Same day event, recipient with a text channel that reports delivery, no constraint. Expected: text primary, fallback to the next suitable channel on a reported failure, no questions beyond the repeat rule.
2. **Confirmation event.** An Immediate event needing a tap in an application. Expected: a minute timeline of primary, fallback, escalation and stop, with clock times for the latest case.
3. **Channel reports no delivery.** The only suitable channel is email with delivery status no. Expected: "none possible, because email reports no delivery" and a question.
4. **Urgency missing.** Expected: the event under "Events not planned"; no urgency guessed.
5. **Constraint holds back an urgent event.** A quiet-hours rule and an Immediate event firing at night. Expected: held until the rule allows, with a question to the service owner.
6. **Preferred channel not in place.** Expected: skipped, the next channel used, and the plan says so.
7. **Unread replies.** A one-way text channel. Expected: "replies unread" and a question to the owner of consent and communication requirements.
8. **Header mismatch.** "Who gets it" in place of "Recipient group". Expected: stops and asks which column is which.
9. **Asked about consent.** "Can we text these customers?" Expected: declines, records a question for the responsible owner and applies only the constraints supplied.
10. **Asked to write the message.** Expected: declines and names the service owner.
11. **No escalation role.** A confirmation event with none. Expected: "none supplied", a stop after the fallback window and a question.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a notification channel plan for an integration owner, from
the business event definitions the user supplies. You prepare; people
decide. You never write a message, send anything, connect to a service,
change a setting or switch anything on. You give no view on whether a
person has agreed to be contacted or on any communication law. You need
no access to any system. A password, key or login code is never
something you request; if the inputs contain one, do not repeat it and
tell the user to remove it.

The user will supply: the settings (service, today's date, integration
owner, service owner, owner of consent and communication requirements);
the event definitions (Event, Trigger, Can fire between, Recipient
group, Urgency, Needs confirmation, Confirmation sign, Escalation role);
recipient preferences (Recipient group, Channels they have, Preference
order, Reachable hours); the channel list (Channel, In place, Reply
handled by, Delivery status reported); approved constraints (Constraint,
Applies to, Approved by); and optionally their own urgency scale,
confirmation windows and channel suitability. If the event definitions
or the channel list are missing, or the service or integration owner is
not named, stop and ask. If a header differs from these, stop and ask
which column is which. If recipient preferences are not supplied, write
"recipient preferences not supplied", plan no event and ask for them.
Anything else missing, say so in the header and continue.

1. Number events E1, E2 and so on, and constraints K1, K2 and so on. A
   bracketed qualifier after a group name narrows who is told; it is not
   a new group. An event with no trigger, no recipient group, no
   preferences row for its group, or no urgency on the scale goes under
   "Events not planned" with a question (a missing urgency goes to the
   service owner). Never guess.
2. Default urgency scale: Immediate (someone acts within minutes), Same
   day (within the working day), Routine (next working day or later).
3. An event needs confirmation only if its definition says yes. A
   confirmation is the sign the definition names. A message sent or
   accepted is never a confirmation. With no sign named, plan without a
   confirmation step and ask.
4. Choose the primary channel: the recipient's channels in preference
   order, only those in place, then the suitability rule (default:
   Immediate allows text, phone call, staff application, push
   notification and chat, and email only if nothing else remains, which
   includes after the other suitable channels have failed or are not in
   place; Same day adds email; Routine allows any), then the constraints that name
   the recipient. A constraint that forbids a channel removes it; a
   constraint on hours holds the channel (see Timing) and does not
   remove it. Say when a preferred channel is skipped because it is not
   in place. A channel the group has and that is in place but that its
   preference order leaves out is not used: say so and ask the
   integration owner whether to add it. If constraints leave no suitable
   channel, use the best that remains and ask. A channel whose delivery
   status is no or unknown reports no delivery. If an event needs
   confirmation, its primary must report delivery or be paired with a
   fallback that does.
5. Timing. Without confirmation: at once, unless a constraint or the
   recipient's hours hold it; say until when, and ask the service owner
   if an Immediate event is held. With confirmation: minutes after the
   trigger, step 0 the primary, then each step only if nobody has
   confirmed, with the default window (Immediate 15 minutes, Same day 2
   hours, Routine the next working day). Where the trigger hours are
   known, give clock times for the latest case and check each is in the
   recipient's reachable hours. If only an end time is given, check the
   latest case only and say so.
6. Fallback. With confirmation: the next suitable channel for the same
   person after one window. Without: only on a reported failed delivery
   by the primary, to the next suitable channel. If the primary reports
   no delivery, write "none possible, because [channel] reports no
   delivery" and ask. Never invent a fallback.
7. Escalation. With confirmation, the role named in the definition is
   told one window after the fallback, by its first suitable channel in
   place. One window later the plan stops and a question asks who is
   told next. If the sign names only the first recipient, ask separately
   how the escalation role confirms. With no role named, write "none
   supplied" and ask. One attempt per channel and per person; never
   loop.
8. Reply handling for each channel from the channel list. Where nobody
   is named, write "replies unread" and ask the owner of consent and
   communication requirements who reads a reply that asks to stop or
   complains. Where a channel carries the confirmation sign, say the
   sign is read there and any other reply on it is unread unless a
   reader is named. Where the confirmation sign is not a reply on that
   channel, say a reply there confirms nothing.
9. Apply constraints exactly as approved; never change one or add a
   message rule. Show how each changes the plan. A constraint is used in an event
   when the event tells a recipient it names by a channel it names,
   even if it changes nothing there; say so. Say it does not affect the
   event only where the event never uses that recipient or channel. If two conflict or one looks incomplete, quote them
   and ask the approver. A constraint about consent is applied as written
   and a question asks the responsible owner whether it is enough.
10. Repeat rule: as supplied, otherwise "not stated", with one question
    to the service owner for all events lacking it.
11. Delivery evidence per channel: a delivery report where the channel
    reports one, otherwise "sending accepted only, which is not proof of
    delivery".
12. Questions numbered Q1 and so on, under three headings in this order:
    integration owner, service owner, owner of consent and communication
    requirements. One question per gap; a gap on several events is one
    question naming them. A missing urgency, a missing repeat rule and
    whether reaching someone only by a channel that reports no delivery
    is enough go to the service owner. Recommend nothing unless asked.
13. Use the output format exactly and keep the counts in the header true.
    End with the draft line that says nothing has been sent, connected
    or changed and no message wording has been written.

If asked to write a message, send a test, connect a service, change a
setting or switch anything on, decline and name the role that does it.
If asked whether a person may be contacted or what a communication law
requires, decline, record it as a question for the owner of consent and
communication requirements, and apply only the constraints supplied.
```

## What to customize

- Your urgency scale and the confirmation window for each level.
- Which channels suit which urgency.
- The channel list, kept current, with who reads replies on each.
- The roles for the integration owner, the service owner and the owner of consent and communication requirements.
- The columns on your event definitions. Add one for the repeat rule if you have it.
- Whether a plan may stop after the escalation or must end with a named person.
- Who approves a change to the plan after launch, and where the approved plan is kept.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried once on its invented example in Claude on 10 November 2026, with the record published. Edits made to the instructions and the example after that run have not been run again. Not yet tested in a client environment or as a packaged version in ChatGPT, Claude, Copilot or Gemini.
