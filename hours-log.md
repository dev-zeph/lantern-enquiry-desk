# Hours log

## Monday Nov 16 (5 hours)

Value: 3.5 h
Ran the group call with Rob, Carla and Sam, then went through Carla's sheet, Sam's quote list and the form emails. Same-day quotes won 5 of 8 and quotes that took 3+ days won 2 of 20, so slow replies and slow quotes look like the bigger leak, not the ads. Sam confirmed big quotes wait until Sunday with no word to the customer, and the last big win picked Lantern for "the first clear number". Next: Carla's follow-up on rebate referrals and lost vs still deciding.

Usability: 1 h
Asked Sam how he'd want work to reach him. No apps and no logins, he tried one in the spring and never opened it. He reads email at lunch and at night, and Carla's booking emails already have the format he trusts. Next: ask Carla why the spring app didn't stick and how much time she has each day for a list.

Viability: 0.5 h
Found out Carla runs info@, Rob owns the website and anything technical, and nobody will share passwords. Also learned the repair rules: Lantern units go to Carla, other brands get a polite no. Next: ask Rob who would approve a connection and what they spend today.

Feasibility: 0 h
Nothing tested yet. Read the form setup and the channels only. Next: test a form to auto-reply in under 20 minutes on a free plan.

Monday plan saved in the portal.

## Tuesday Nov 17 (4 hours)

Value: 1.5 h
Ran Carla's follow-up and found the missing record: 22 home show names from Oct 3 to 5 that nobody has called, still in Rob's truck. Root cause is ownership, not ads: nobody owns an enquiry the whole way, and nothing is tracked after a visit is booked. Posted the six answers and what I'll build. Next: Rob's follow-up on photos of his notes and the home show.

Usability: 0.5 h
Carla quit the spring app after 3 weeks because Rob and Sam never updated it. Her limits: about an hour a month of upkeep, no code, she changes it herself, one place on her phone. So the build asks nothing new of Rob and Sam: email in, and a phone page that opens on "Needs you". Next: test the hand-off and reply edit against the 10 minutes.

Feasibility: 1.5 h
Wrote v1 on one free Google account: the form and inbox are checked every 5 minutes, it sorts new install, rebate, Lantern repair and other brand, merges repeat emails, replies, and reads photos into rows. Tested the sorting rules on sample messages and all were right. Next: set it up on the test account and run the 7 tests.

Viability: 0.5 h
The Claude API needs a card, so I switched photo reading to Gemini's free tier. Gemini's free tier may use what's sent, which needs to go in the approver note. The tool keeps no home addresses, only what Carla needs plus the rebate file number. Next: ask Rob who approves the connection and the data.

## Wednesday Nov 18 (5 hours)

Value: 1 h
Ran Rob's follow-up. The home show names moved him off the ads: "maybe I've been looking at the ads when some of it's on us." His guess of about 10 calls a week means roughly 1 in 20 of his calls reach Carla's sheet. His win is one real customer who signs, which can't happen this week, so I'll show the path working and point to the home show names. Next: tie his win to the demo.

Usability: 1 h
Rob won't do anything over 10 seconds with one thumb. He texts notepad photos to Carla and would send them to an email address "if it's as quick as a text". Commercial work goes to Rob, never Sam, and has to reach his phone. Next: test a real photo from a phone and time Carla's hand-off.

Feasibility: 2 h
Finished the first version of the software and added the commercial rule: business enquiries go to Rob with their own reply and a hand-off email. Checked all the sorting rules on sample messages. Started setup on the test Google account: Sheet, script and Carla's phone page. Next: finish setup, get the photo key and run the 8 tests before Thursday 5 PM.

Viability: 1 h
Kevin, Rob's brother-in-law, owns info@ and the website. He refused an app that read all their email last year, wants a one-page note (reads, sends, keeps), and takes about a week. I chose to keep reading all of info@, so the note has to say that plainly, with a narrower setup as the fallback. Cost: ideally $0, never over $20 a month. Next: write Kevin's note and the cost maths.

## Thursday Nov 19 (6 hours)

Value: 0.5 h
Checked Volta's test rules against what Lantern told us. An enquiry is handled right only if, within 20 minutes, it has an owner, a next step and the reply Lantern would want. So I added a Next step to every row, like "Carla: call to book Sam's visit (by Mon Nov 23)". Anything that arrives after Thursday 2:30 PM is promised for Monday, because that's when Carla is back. Next: watch the overnight test and count how many were handled right.

Usability: 1 h
Carla's page now shows the next step on every card, and has buttons to change it and to check for new enquiries straight away. I removed empty cards left over from tests. Rob can now log a call by emailing the inbox with "Call" in the subject, as well as sending a photo, and he gets "Got it: 1 added" back. Next: write Carla's one-page guide and time her hand-off against the 10 minutes.

Feasibility: 3.5 h
Rules alone missed tricky messages, so AI now sorts every enquiry and Lantern's rules check its answer. Business words always go to Rob. The polite no only goes out when it's certain the unit isn't Lantern's. Anything unclear gets a holding reply, never silence. Gemini's free models were retired or took 2 to 3 minutes per call. I switched sorting to Claude Opus 5.5, with Gemini and the rules as fallbacks, and Claude sorted all four tricky test messages right in 1 to 4 seconds. Next: leave it running untouched from 10 PM for the overnight test.

Viability: 1 h
Shared the list with Volta as a viewer and posted the form link and inbox with no password. I fixed the settings so the alarm goes to a test address. The Claude API isn't free, so the plan has to show the cost for the busiest month against Gemini's free tier and rules only. Next: Kevin's one-page note, which has to say that message text is sent to the AI to be sorted.
