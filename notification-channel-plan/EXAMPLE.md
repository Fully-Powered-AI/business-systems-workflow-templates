# Notification channel plan: an invented example

*Illustrative example with invented data.* An invented 30-person bike and kayak hire company, Company A, plans the notifications for five events. The people are invented too: Priya, the integration owner, and Marcus, the service owner. Company A's compliance lead answers consent questions.

## What the person supplies

**Settings.** Service: Company A hire desk. Today: Thursday 12 November 2026. Integration owner: Priya. Service owner: Marcus. Consent and communication requirements: the compliance lead. Urgency scale, confirmation windows and channel suitability: the defaults.

**Event definitions.** Export with the headers Event, Trigger, Can fire between, Recipient group, Urgency, Needs confirmation, Confirmation sign, Escalation role:

- Booking confirmed, Payment marked paid in the booking system, any time, Customer, Same day, No, none, none.
- Equipment not returned, Return not scanned 30 minutes after the booked end time, up to 18:30, Duty manager, Immediate, Yes, Duty manager taps "Taken" in the staff app, Operations lead.
- Weather closure, Operations lead sets the site to closed, any time, Customer (bookings that day), Immediate, No, none, none.
- Low stock of helmets, Stock count below 5, weekdays 08:00 to 17:00, Stock clerk, Routine, No, none, none.
- Damage reported, Staff form submitted, any time, Duty manager, (blank), No, none, none.

**Recipient preferences.** Export with the headers Recipient group, Channels they have, Preference order, Reachable hours:

- Customer, text and email, text then email, any time.
- Duty manager, staff app and text and phone call, staff app then text then phone call, 07:00 to 19:00.
- Operations lead, text and phone call and email, phone call then text, 07:00 to 21:00.
- Stock clerk, staff app and email, email, weekdays 08:00 to 17:00.

**Channel list.** Export with the headers Channel, In place, Reply handled by, Delivery status reported:

- Text, yes, none (one-way), yes.
- Email, yes, Front desk (inbox read 09:00 to 17:00), no.
- Staff app, yes, none, yes.
- Phone call, no, none, no.

**Approved constraints.** Export with the headers Constraint, Applies to, Approved by:

- No customer text before 08:00 or after 20:00, Customer, Service owner.
- No payment amounts in a text, Customer, Service owner.
- Text only where the booking record shows text agreement, Customer, Compliance lead.

## What comes out

```
NOTIFICATION CHANNEL PLAN: Company A hire desk

For: Priya, integration owner, who approves the design; Marcus, service owner, who approves message rules and timing. Prepared: Thursday 12 November 2026, from 5 event definitions, recipient preferences, a channel list of 4 channels, 3 constraints.
Urgency scale: Immediate = someone acts within minutes; Same day = within the working day; Routine = next working day or later. Confirmation windows: Immediate 15 minutes, Same day 2 hours, Routine next working day. Defaults used: urgency scale, confirmation windows, channel suitability by urgency.
Events: 5 (4 planned, 1 not planned). Channels used: text, email, staff app. Questions: 12.

E1 Booking confirmed
Trigger: Payment marked paid in the booking system. Can fire: any time.
Urgency: Same day.
Told: Customer, by text; by email where the booking record shows no text agreement (K3).
Confirmation: not needed.
Timing: Text at once between 08:00 and 20:00; a payment made outside those hours is held until the next 08:00 (K1). Customers with no text agreement are emailed at once.
Fallback: text not delivered, as the text service reports: email. Customers reached by email only: none possible, because email reports no delivery.
Escalation: not needed.
Reply handling: text, replies unread. Email, Front desk, inbox read 09:00 to 17:00.
Repeat rule: not stated.
Delivery evidence: text, delivery report. Email, sending accepted only, which is not proof of delivery.
Constraints applied: K1, the text is held outside 08:00 to 20:00; K2, the text carries no payment amount; K3, email only where the booking record shows no text agreement.
Open points: Q6, Q7, Q9, Q11, Q12.

E2 Equipment not returned
Trigger: Return not scanned 30 minutes after the booked end time. Can fire: up to 18:30.
Urgency: Immediate.
Told: Duty manager, by staff app.
Confirmation: needed. Sign: Duty manager taps "Taken" in the staff app. Window: 15 minutes.
Timing: minutes after the trigger. 0: staff app to the Duty manager. 15: text to the Duty manager if not confirmed. 30: text to the Operations lead if not confirmed. 45: stop. Latest case: trigger at 18:30, steps at 18:30, 18:45 and 19:00, stop at 19:15. The Duty manager is reachable until 19:00 and the Operations lead until 21:00, so every step falls in reachable hours.
Fallback: text to the Duty manager at 15 minutes.
Escalation: Operations lead, by text at 30 minutes. Phone call, their first preference, is not in place. Email, which the Operations lead has and which is in place, is not in their preference order and is not used (Q5).
Reply handling: staff app, the tap on "Taken" is the confirmation and is read; any other reply there is unread. Text, replies unread, so a reply to the text confirms nothing.
Repeat rule: not stated.
Delivery evidence: staff app and text, delivery report. Confirmation, the tap on "Taken" only.
Constraints applied: none.
Open points: Q1, Q2, Q3, Q4, Q5, Q6, Q11.

E3 Weather closure
Trigger: Operations lead sets the site to closed. Can fire: any time.
Urgency: Immediate.
Told: Customer (bookings that day), by text; by email where the booking record shows no text agreement (K3).
Confirmation: not needed.
Timing: Text at once between 08:00 and 20:00; a closure set outside those hours is held until the next 08:00 (K1). Customers with no text agreement are emailed at once.
Fallback: text not delivered, as the text service reports: email. Customers reached by email only: none possible, because email reports no delivery.
Escalation: not needed.
Reply handling: text, replies unread. Email, Front desk, inbox read 09:00 to 17:00.
Repeat rule: not stated.
Delivery evidence: text, delivery report. Email, sending accepted only, which is not proof of delivery.
Constraints applied: K1, the text is held outside 08:00 to 20:00; K2, the text carries no payment amount, which changes nothing in this event; K3, email only where the booking record shows no text agreement.
Open points: Q6, Q8, Q9, Q11, Q12.

E4 Low stock of helmets
Trigger: Stock count below 5. Can fire: weekdays 08:00 to 17:00.
Urgency: Routine.
Told: Stock clerk, by email. The staff app, which the Stock clerk has and which is in place, is not in their preference order and is not used (Q5).
Confirmation: not needed.
Timing: at once. Every firing falls inside the Stock clerk's hours.
Fallback: none possible, because email reports no delivery.
Escalation: not needed.
Reply handling: email, Front desk, inbox read 09:00 to 17:00.
Repeat rule: not stated.
Delivery evidence: email, sending accepted only, which is not proof of delivery.
Constraints applied: none.
Open points: Q5, Q6.

Events not planned
E5 Damage reported: urgency not stated. Q10.

Channels
Text: in place. Delivery status reported: yes. Replies: unread, no reader named. Used by: E1, E2, E3.
Email: in place. Delivery status reported: no. Replies: Front desk, inbox read 09:00 to 17:00. Used by: E1, E3, E4.
Staff app: in place. Delivery status reported: yes. Replies: the tap on "Taken" is the confirmation and is read (E2); any other reply is unread. Used by: E2.
Phone call: not in place. Delivery status reported: no. Replies: unread. Used by: none; skipped in E2.

Constraints applied
K1 No customer text before 08:00 or after 20:00. Applies to: Customer. Approved by: Service owner. Used in: E1, E3.
K2 No payment amounts in a text. Applies to: Customer. Approved by: Service owner. Used in: E1, E3.
K3 Text only where the booking record shows text agreement. Applies to: Customer. Approved by: Compliance lead. Used in: E1, E3.

Questions for the owners: 12
For Priya, integration owner
Q1. E2. The confirmation sign is the Duty manager's tap on "Taken", and the text at 15 minutes has no reply route, so a reply to it confirms nothing. Should the text carry a way to confirm?
Q2. E2. If nobody has confirmed 45 minutes after the trigger, the plan stops and nobody further is told. Who, if anyone, is told next?
Q3. E2. The only confirmation sign supplied is the Duty manager's tap on "Taken". If the Operations lead takes the matter on, how is that confirmed?
Q4. E2. The Operations lead's first preference, phone call, is not in place, so the plan uses text. Is text acceptable for an escalation?
Q5. E2, E4. The Operations lead has email and the Stock clerk has the staff app. Both are in place but not in their preference orders, so neither is used. Email reports no delivery, so a failed email to the Operations lead would not be seen; the staff app reports delivery. May either be used as well or instead?
For Marcus, service owner
Q6. E1 to E4. No repeat rule was supplied. If a trigger fires twice for the same payment, closure, return or stock count, should the person be told twice?
Q7. E1. A payment made after 20:00 is texted at 08:00 the next day under K1, although the urgency is Same day. Is a next-morning text acceptable? Customers with no text agreement are emailed at once.
Q8. E3. A closure set before 08:00 or after 20:00 is texted at the next 08:00 under K1, although the urgency is Immediate. Customers with no text agreement are emailed at once. Should closures be an exception to K1, or is the hold intended?
Q9. E1, E3. Customers whose booking record shows no text agreement get email only. Email reports no delivery, and its replies are read from 09:00 to 17:00. Is that enough, or should someone reach those customers another way?
Q10. E5. Damage reported has no urgency. What is it?
For the compliance lead, who answers consent and communication requirements
Q11. E1, E2, E3. Replies to texts, and any reply in the staff app other than the tap on "Taken", are unread. Who reads a reply that asks to stop or makes a complaint, and within what time?
Q12. E1, E3. The plan applies K3 as written and gives no view on whether it is enough. Is its wording complete?

Draft for Priya's approval of the design and Marcus's approval of message rules and timing. Nothing has been sent, connected or changed, and no message wording has been written.
```

Every line traces to the event definitions, recipient preferences, channel list and constraints supplied above, and to the default urgency scale, confirmation windows and channel suitability.
