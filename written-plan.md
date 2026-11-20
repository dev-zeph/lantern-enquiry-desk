# Lantern enquiry desk: written plan

## Whose account
Google account behind info@. Kevin installs it and approves the permission screen. Staff get access to the Sheet, never a password. If Kevin won't allow that, he forwards info@ to a desk-only Gmail account, so the desk sees only what's forwarded. This week it ran on a test account with made-up customers.

## Busiest-month cost
About 25 enquiries a week this fall. I allow 150 messages a month to be safe. Google Sheets, Forms, Gmail and Apps Script are $0.

- **A. Claude Opus 5.5 (ran this week):** 2,000 tokens in × $4/1M + 600 out × $20/1M = $0.02 a message, so **about $3 a month** (worst case about $15).
- **B. Claude Haiku 5.5:** 2,000 × $0.10/1M + 600 × $0.50/1M = $0.0005 a message, so **about $0.08 a month**.
- **C. Gemini free tier, or the rules alone:** **$0**, but Gemini was slow or busy this week and the rules miss tricky wording.

Photo reading uses Gemini's free tier, so it's $0. Recommendation: A. It stays under Rob's $20, and Rob needs to put about $10 of credit on Lantern's own Anthropic account. If that key fails, the desk falls back to C on its own.

## If it stops
An hourly check emails the Alarm address in Settings if the desk hasn't run for 30 minutes, or if a run errors. It sends at most one alarm every 3 hours. Carla's page always shows "last checked X min ago".

## Note for Kevin
- **Permission screen:** Gmail ("read, compose, send and permanently delete all your email". It's the only Gmail permission a script can use, and the desk never deletes), the enquiry Sheet and form, an external service (the AI), and running every 5 minutes while you're away.
- **Reads:** the info@ inbox and spam from the last 3 days, and the contact form.
- **Sends:** to customers, only Carla's replies from the Replies tab, which the AI picks but never writes. To staff, hand-off and alarm emails.
- **Changes:** it moves an enquiry out of spam. Nothing else.
- **Keeps:** one Sheet row per enquiry in Lantern's Drive, with name, email, phone, town, message, rebate number and status. It keeps no home addresses.
- **Leaves Lantern:** message text goes to Anthropic for sorting. Rob's photos go to Google Gemini's free tier, where Google may use them to improve its products.
- **Off switch:** delete the script's two triggers.

## Can't fix
- **Slow quotes:** same-day quotes won 5 of 8, and quotes that took 3 or more days won 2 of 20.
- **Unlogged calls and Facebook:** calls Rob never logs and Facebook messages stay invisible.
- **Kevin's approval:** without his yes, it can't run on info@.
- **The home show names:** the 22 names only help if someone calls them.
- **A signed customer:** that can't happen this week.
