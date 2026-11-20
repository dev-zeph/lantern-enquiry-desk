# Lantern enquiry desk: technical explainer

## 1. The problem

Lantern Heat Pumps, a six-person installer near Halifax, believes it has a lead problem. Rob spends $1,500 a month on ads and says the phone isn't ringing enough. The data says otherwise. About 25 enquiries a week come in, but Carla's sheet logs only about 15. Same-day quotes won 5 of 8, while quotes that took 3 or more days won 2 of 20. Lost quotes add up to about $227,000, and 22 home show names from October were never called.

The real problem is ownership. No one owns an enquiry from start to finish. Anything outside info@ has no owner. Nobody watches info@ from Thursday 2:30 PM to Monday. Once a visit is booked, nobody tracks the quote.

## 2. The people, and what each one needs

**Rob, the owner.** He takes calls on his cell from the roof, writes names on a notepad, and checks Facebook once a week. He won't do anything that takes more than 10 seconds with one thumb, but he'd email a photo "if it's as quick as a text". His win is one job won that would otherwise have been lost. His cost ceiling is $20 a month.

**Carla, the office.** She runs info@ and the enquiry sheet, Monday to Thursday until 2:30. She quit the spring app after 3 weeks because Rob and Sam never updated it, and she was typing everything twice. Her limits: everything in one place, on her phone, no code, she can change it herself, about an hour a month of upkeep, and no replies she has to clean up.

**Sam, the visits and quotes.** He does new installs only, wants work by email, and won't use apps or logins. Commercial jobs are never his.

**Kevin, the approver.** Rob's brother-in-law owns info@ and the website. Last year he refused an app that wanted to read all their email. He wants a one-page note covering what it reads, sends and keeps, and takes about a week to decide.

**The customer.** Today they wait a day or two for a reply, or until Monday. They need a fast, correct first reply, and the wrong reply would hurt: a Lantern customer told "we don't service that" is a lost customer.

## 3. The solution in one line

One shared list that fills itself. Every enquiry, from the form, the inbox, Rob's calls or Rob's photos, becomes one row with an owner and a next step. The right first reply goes out within minutes, day or night. Nobody types anything into it, and nobody learns a new app.

## 4. How it works

The parts:
- **Google Form:** the website's contact form.
- **Gmail inbox:** stands in for info@.
- **Google Sheet:** the shared list. Its tabs are Enquiries, Replies, People, Settings, Log and Seen.
- **Apps Script:** the engine, attached to the Sheet.
- **Carla's phone page:** an Apps Script web app.

Every 5 minutes, a trigger runs `run()`:
1. **Lock.** It takes a script lock, so two runs can never send two replies.
2. **Read new form rows.** A saved counter records how far down the form responses it has read.
3. **Read new email.** It reads the inbox and spam from the last 3 days, skipping anything listed in the Seen tab. It moves an enquiry out of spam if it finds one there.
4. **Staff or customer.** If the sender is listed in People, the email is a staff note (Rob's call or photo). Otherwise it's an enquiry.
5. **Repeat check.** If the same email address wrote within 14 days, the new message joins the first row as "New info" and no second reply goes out.
6. **Sort.** Claude classifies the message, and Lantern's rules check the answer (see section 5).
7. **Reply.** The desk sends the matching wording from the Replies tab, in the same email thread.
8. **Write the row.** The row gets the type, owner, status, Needs you flag, reply sent, notes (including which model sorted it and why) and the next step with a date.
9. **Hand off.** If the owner isn't Carla, the desk emails that person a "Passed to you" message with every detail.

Every hour, `healthCheck()` emails the alarm address if no run has happened in 30 minutes or a run errored. It sends at most one alarm every 3 hours.

## 5. The decisions, and why

**Google Sheets and Apps Script, not a new app.** Carla's spring app died because nobody updated it. A Sheet is something she already trusts, it costs $0, it keeps a full edit history (which Volta's test checks), and Sam and Rob never have to open it. Apps Script runs inside the same Google account, so nothing new needs hosting, signing up or paying for.

**Email as the only way in for staff.** Sam reads email, and Rob texts photos. So hand-offs arrive as emails, and Rob logs a call by emailing "Call" plus the details, or by sending a photo. Nobody needs a login or an app.

**A 5-minute trigger, plus a "Check now" button.** Volta allows 20 minutes, and 5 minutes leaves room for a slow AI call or a retry. A 1-minute trigger would burn through the roughly 90 minutes a day of free run time a personal Google account gets. "Check now" gives Carla, and the demo, an instant check.

**The AI sorts, but never writes.** We started with keyword rules, and they missed real wording like "you guys did our install, it died tonight". So Claude sorts every message into one of eight types, returns a confidence level and a reason, and says whether it's urgent. But the reply text always comes from Carla's Replies tab. That gives two things:
- the AI's flexibility in understanding messages;
- predictable emails that Carla controls, which was her "nothing I have to clean up" rule.

**Lantern's rules have the final say.** `decide_()` sits between the AI and the reply:
- If any business words appear, the enquiry goes to Rob, every time. This was Rob's rule: "commercial never goes to Sam".
- The polite no to other-brand repairs only goes out when the AI is highly confident and the rules found no sign it's a Lantern install. Turning away a real Lantern customer is the worst mistake the desk can make, so in any doubt it sends a holding reply instead.
- "Not an enquiry", which gets no reply, needs high confidence. A real person must never go unanswered because of a guess.
- Repairs with low confidence, or anything unclear, get a holding reply and the Needs you flag, so a human decides.

**Why Claude Opus 5.5.** We first tried Gemini's free tier. The 2.5 models had been retired, the Pro model had no free quota, and the Flash model took 2 to 3 minutes per call or returned "busy". That's too slow for a run that has to finish in 6 minutes. Claude Opus 5.5 sorted all four tricky test messages correctly in 1 to 4 seconds. It uses structured output, so the answer always comes back in a fixed JSON format, and low effort, which keeps it fast. The busiest month comes to about $3, within Rob's $20.

**Fallbacks.** If Claude fails, the desk tries Gemini, and if that fails, it uses the rules alone. Every run also has a time budget:
- it stops AI calls after 3 minutes or 12 calls;
- it stops taking new work after 4 minutes, and the next run picks up the rest.

So the desk degrades gently instead of crashing.

**The model can't be hijacked.** The sorting prompt tells the model to treat the email as data, not instructions. And since the model only picks a type, never the reply text, a hostile email can at worst get itself mis-sorted. It can never make the desk send words the desk wouldn't otherwise send.

**Next step on every row, with a date.** Volta defines "handled right" as including an owner and a next step. The date respects Carla's hours: anything after Thursday 2:30 reads "by Mon Nov 23", because promising Friday would be a lie.

**Repeat merging by email address over 14 days.** Carla said people often send the form and then email as well. Merging stops double replies and keeps one row per person.

**Photos read by AI, always checked by a human.** Rob's handwriting can be misread, so rows from photos are always flagged Needs you and marked "Check with Rob". The desk replies only to Rob ("Got it: 3 added") and never to the people on the sheet, because Rob has already spoken to them.

**What it keeps, and what it doesn't.** The desk keeps no home addresses, because Carla gets those herself when she books a visit. The rebate file number gets its own column, at Carla's request. Kevin's note states exactly what is read, what is sent, and what leaves Lantern.

## 6. Carla's page

It opens on **Needs you**: only what a human must do, and it empties as she works. **New** is anything nobody has acted on yet. **Still open** is everything up to Won or Lost, so quotes can't quietly disappear. **All** is the full history, with search. Changing the owner sends the hand-off email, and every card shows its next step.

## 7. The 5-minute demo

- **0:00 The problem (45 s):** about 25 enquiries a week but only 15 logged, the quote numbers, the 22 home show names, and the point that it's ownership, not leads.
- **0:45 The people (30 s):** Rob's thumb, Carla's spring app, Sam's email, Kevin's no.
- **1:15 Live (90 s):** Rob emails "Call" from his phone. Tap Check now and the row appears with owner Carla and a next step. Open a commercial row: owned by Rob, with the hand-off email.
- **2:45 Why it's right (60 s):** Claude sorts and the rules decide, and the overnight tests show how many of the 7 were handled correctly.
- **3:45 Proof (45 s):** the run history in Apps Script Executions and the Log tab, plus the Sheet's version history showing nobody touched it.
- **4:30 Plan (30 s):** about $3 a month, Kevin's note, and what it can't fix: slow quotes, unlogged calls, the home show names.
