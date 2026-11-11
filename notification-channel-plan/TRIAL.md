# Notification channel plan: a trial on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example in [public/example.md](example.md) (a 30-person bike and kayak hire company, five events, four channels, three constraints). No client data was used. The run was done by an assistant that had not written the template. It read the complete template and the example's inputs only, followed the instruction block and the output format, produced the plan, and only then read the example's published output and the reviewer checklist to compare.

## What came out

```
NOTIFICATION CHANNEL PLAN: Company A hire desk

For: Priya, integration owner, who approves the design; Marcus, service owner, who approves message rules and timing. Prepared: Thursday 12 November 2026, from 5 event definitions, recipient preferences, a channel list of 4 channels, 3 constraints.
Urgency scale: Immediate = someone acts within minutes; Same day = within the working day; Routine = next working day or later. Confirmation windows: Immediate 15 minutes, Same day 2 hours, Routine next working day. Defaults used: urgency scale, confirmation windows, channel suitability by urgency. The compliance lead is named as the owner of consent and communication requirements.
Events: 5 (4 planned, 1 not planned). Channels used: text, email, staff app. Questions: 10.

E1 Booking confirmed
Trigger: Payment marked paid in the booking system. Can fire: any time.
Urgency: Same day.
Told: Customer, by text; by email where the booking record shows no text agreement (K3).
Confirmation: not needed.
Timing: at once. Text between 08:00 and 20:00; a payment marked paid outside those hours is held until 08:00 (K1). Email at once.
Fallback: text reported as not delivered: email. Customers reached by email only: none possible, because email reports no delivery.
Escalation: not needed.
Reply handling: text, replies unread. Email, Front desk reads the inbox 09:00 to 17:00.
Repeat rule: not stated.
Delivery evidence: text, delivery report. Email, sending accepted only, which is not proof of delivery.
Constraints applied: K1, K2, K3.
Open points: Q1, Q2, Q7, Q9, Q10.

E2 Equipment not returned
Trigger: Return not scanned 30 minutes after the booked end time. Can fire: up to 18:30.
Urgency: Immediate.
Told: Duty manager, by staff app.
Confirmation: needed. Sign: Duty manager taps "Taken" in the staff app. Window: 15 minutes.
Timing: minutes after the trigger. 0: staff app to the Duty manager. 15: text to the Duty manager if nobody has confirmed. 30: text to the Operations lead if nobody has confirmed. 45: stop. Latest case: trigger at 18:30, steps at 18:30, 18:45 and 19:00, stop at 19:15. The Duty manager is reachable 07:00 to 19:00 and the Operations lead 07:00 to 21:00, so every step falls in reachable hours.
Fallback: text to the Duty manager at 15 minutes. Phone call, their third preference, is not in place and is skipped.
Escalation: Operations lead, by text, at 30 minutes. Phone call, their first preference, is not in place and is skipped.
Reply handling: staff app, replies unread (no reader named); the tap on "Taken" is the only sign, and a reply there confirms nothing. Text, replies unread; a reply to a text confirms nothing.
Repeat rule: not stated.
Delivery evidence: staff app and text, delivery report. Confirmation: the tap on "Taken".
Constraints applied: none.
Open points: Q3, Q4, Q7, Q10.

E3 Weather closure
Trigger: Operations lead sets the site to closed. Can fire: any time.
Urgency: Immediate.
Told: Customer (bookings that day), by text; by email where the booking record shows no text agreement (K3).
Confirmation: not needed.
Timing: at once. Text between 08:00 and 20:00; a closure set outside those hours is held until 08:00 (K1). Email at once.
Fallback: text reported as not delivered: email, which is all that remains. Customers reached by email only: none possible, because email reports no delivery.
Escalation: not needed.
Reply handling: text, replies unread. Email, Front desk reads the inbox 09:00 to 17:00.
Repeat rule: not stated.
Delivery evidence: text, delivery report. Email, sending accepted only, which is not proof of delivery.
Constraints applied: K1, K2, K3.
Open points: Q1, Q2, Q7, Q8, Q9, Q10.

E4 Low stock of helmets
Trigger: Stock count below 5. Can fire: weekdays 08:00 to 17:00.
Urgency: Routine.
Told: Stock clerk, by email.
Confirmation: not needed.
Timing: at once. Every firing falls inside the Stock clerk's reachable hours (weekdays 08:00 to 17:00).
Fallback: none possible, because email reports no delivery.
Escalation: not needed.
Reply handling: email, Front desk reads the inbox 09:00 to 17:00.
Repeat rule: not stated.
Delivery evidence: email, sending accepted only, which is not proof of delivery.
Constraints applied: none.
Open points: Q2, Q5, Q7.

Events not planned
E5 Damage reported: urgency not supplied. Q6.

Channels
Text: in place. Delivery status reported: yes. Replies: unread, no reader named. Used by: E1, E2, E3.
Email: in place. Delivery status reported: no. Replies: Front desk, inbox read 09:00 to 17:00. Used by: E1, E3, E4.
Staff app: in place. Delivery status reported: yes. Replies: unread, no reader named (the tap on "Taken" is a sign, not a reply). Used by: E2.
Phone call: not in place. Delivery status reported: no. Replies: none named. Used by: none; skipped in E2.

Constraints applied
K1 No customer text before 08:00 or after 20:00. Applies to: Customer. Approved by: Service owner. Used in: E1, E3.
K2 No payment amounts in a text. Applies to: Customer. Approved by: Service owner. Used in: E1, E3.
K3 Text only where the booking record shows text agreement. Applies to: Customer. Approved by: Compliance lead. Used in: E1, E3.

Questions for the owners: 10
For Priya, integration owner
Q1. E1, E3. K3 allows a text only where the booking record shows text agreement. The inputs do not say the integration can see that on the record. Can it?
Q2. E1, E3, E4. Where email is the only channel (customers with no text agreement; the Stock clerk), email reports no delivery, so no fallback is possible. Is there another way to reach them, or is sending accepted the only evidence available?
Q3. E2. The only confirmation sign is the Duty manager's tap on "Taken" in the staff app, and the Operations lead has no staff app. If the Operations lead takes the matter on, how is that confirmed?
Q4. E2. If nobody has confirmed 45 minutes after the trigger, the plan stops and nobody further is told. Who is told next?
Q5. E4. The Stock clerk has the staff app, which reports delivery, but their preference order lists only email. May the staff app be used as a fallback?
Q6. E5. Damage reported has no urgency, so it is not planned. What is its urgency?
For Marcus, service owner
Q7. E1 to E4. No repeat rule was supplied. If a trigger fires twice, is the person to be told twice?
Q8. E3. A closure set before 08:00 or after 20:00 is texted at 08:00 under K1, although the urgency is Immediate. Is the hold intended, or may customers who have agreed to text be told by email at once?
For the compliance lead, who answers consent and communication requirements
Q9. E1, E3. The plan applies K3 as written and gives no view on whether it is enough. Is it enough?
Q10. E1, E2, E3. Replies to texts, and to the staff app in E2, have no reader named. Who reads a reply that asks to stop or complains?

Draft for Priya's approval of the design and Marcus's approval of message rules and timing. Nothing has been sent, connected or changed, and no message wording has been written.
```

## What was observed

- **Complete.** Every required part of the output format was produced. No stop condition was met. E5 was correctly left unplanned because its urgency was blank, and nothing was guessed. The header counts (5 events, 4 planned, 10 questions) match the body. All clock times were worked out and checked against reachable hours, and the phone call channel was skipped where it was not in place.
- **Close to the published example.** The plans for E1 to E4 match it in substance: the same primary and fallback channels, the same timeline for E2 (0, 15, 30, 45 minutes; 18:30, 18:45, 19:00, stop 19:15), the same "none possible" cases, the same constraints applied, the same unplanned event. Nothing in either output goes beyond the inputs and the stated defaults, except as noted below.
- **Differences from the example.** The example has 11 questions; this run has 10. This run adds a question about whether the integration can see text agreement on the booking record, and a separate question about using the staff app for the Stock clerk. The example instead asks whether the 15-minute text should carry a way to confirm, whether text is acceptable for the Operations lead's escalation, whether a next-morning text is acceptable for E1, and whether K3 covers a customer who withdraws agreement; this run did not ask those. The example puts the repeat-rule question to the integration owner and the email-only question to the service owner; this run put the repeat rule with the service owner and the email-only question with the integration owner. The example combines the stop and Operations-lead confirmation questions; this run splits them.
- **The example was corrected afterwards.** After this run the published example was edited: it now has 12 questions, its question numbers have changed, and some of the wordings quoted below and above (Q6, Q7 and Q11 of the earlier example) are gone. The comparison here describes the example as it stood at the time of the run. The template's instructions were also clarified a little after the run, and neither change has been run again. The earlier example is not published, so the comparison above cannot be checked against the current one and should be read as this run's own account. The bracketed placeholders and the "steps 3, 6 and 5" wording described in ambiguity 9 were removed from Input 6 after the run. Later edits (not run) also add a sentence for open-ended trigger hours (ambiguity 3), say outright that missing preferences plan no event (ambiguity 10) and say whether a constraint that changes nothing still counts as used.
- **A fact in the example not in the inputs.** The example's questions Q6 and Q7 say "Email goes at once" for a held text, which implies email goes to customers who have agreed to text. Its own "Told" lines send email only where there is no text agreement. The two statements disagree. The wording "withdraws agreement" in its Q11 is also not in the inputs. In this run's output, the statement that the Operations lead has no staff app is drawn from their listed channels (text, phone call, email), and the question about seeing text agreement on the record is a gap the inputs leave open, not a fact.

## Ambiguities and guesses

1. **Hold or switch channel.** Step 5 removes channels by constraint, but step 6 holds an event. K1 is a time rule on text. This run held the text until 08:00 and left email unaffected, and asked the service owner about the Immediate case. The template does not say which reading is intended.
2. **Email as a fallback for Immediate.** Suitability allows email for Immediate only "when it is all that remains". Whether email counts as remaining after a text has failed is not stated. This run allowed it.
3. **Open-ended trigger hours.** "Up to 18:30" has no start, though the header is "Can fire between". Only the latest case could be checked.
4. **Preference order shorter than channels held.** The Stock clerk has the staff app but lists only email. Step 5 says to follow the preference list, so the staff app was dropped silently. The template does not say to ask; this run asked.
5. **Escalation target and confirmation.** The sign is defined for the Duty manager only. Nothing says how the Operations lead confirms, or whether a late tap by the Duty manager still counts.
6. **Which owner receives a question.** A missing urgency, and the repeat rule, have no stated owner. This run chose the integration owner for urgency and the service owner for the repeat rule.
7. **Reply handling for the staff app.** The channel list says no one handles replies, but the staff app carries the confirmation tap. The wording "replies unread" next to a working confirmation is awkward.
8. **Prepared date.** The settings give Thursday 12 November 2026, which is not the day of this run. The date in the settings was used.
9. **Placeholder text.** Input 6 of the template contains the bracketed placeholders "[your urgency scale]", "[your confirmation windows]" and "[your channel suitability by urgency]", and refers to "steps 3, 6 and 5" in that order. It reads like unfinished text.
10. **A missing preferences row versus missing preferences.** The template says to plan no event when recipient preferences are not supplied, and the instruction block says to continue when anything else is missing. They agree, but the block is less explicit.

This trial was run once, on the invented example only. It is not a test in a client environment or in another product.
