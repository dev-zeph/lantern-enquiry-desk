# Lantern enquiry desk v1: setup

Everything is on the sprint test Google account. No card anywhere.

1. Sign in to the test account. Create a new Google Sheet called "Lantern enquiries".
2. In the Sheet: Extensions > Apps Script.
   - Replace everything in Code.gs with build/Code.gs.
   - Click + > HTML, name it Index (no .html), and paste build/Index.html.
   - Project Settings (gear icon): set the time zone to (GMT-04:00) Atlantic Time - Halifax.
3. Photo reader key: go to aistudio.google.com on the test account > Get API key > Create. If it asks for a card or billing, stop and tell Claude.
   Then in Apps Script, Project Settings > Script properties > Add: GEMINI_API_KEY = the key.
4. In the editor, choose `setup` from the function menu and click Run. Approve the permissions (Advanced > Go to project, because it's your own unverified script).
   - This creates the tabs, the Google Form, and the 5-minute and hourly triggers.
   - The form link is in the Log tab.
5. People tab: replace the example.com addresses with test addresses you control. Rob's row is the address photos are sent from. It must be a different address from the test inbox, because the desk ignores mail it sent itself.
   Settings tab: set "Alarm email" to a test address.
6. Deploy > New deployment > Web app. Execute as: Me. Who has access: Anyone with Google account. Copy the URL. That's Carla's phone page.

## First tests (send these yourself, note the times)
1. Form: new install ("quote for a mini split"). Expect: reply within 5 to 10 minutes, row type New install.
2. Email from another test address: "our unit is icing up, you installed it last year". Expect: holding reply, Repair - Lantern unit, Needs you.
3. Email: "heat pump stopped working, it came with the house". Expect: holding reply (not the polite no), Needs you.
4. Same sender as test 2 emails again with a photo. Expect: no new reply, a note added to the first row.
5. Email: "referred by my energy advisor, file number EN-48213". Expect: rebate reply, file number in its own column.
6. From Rob's address, email the home show photo. Expect: up to 22 rows, a "Got your photo" email back, and no replies to anyone on the sheet.
7. On the phone page: change one enquiry's owner to Sam (hand-off email sent) and change a status.
8. Email or form: "We run a bakery on Main St and want heat pumps for our shop". Expect: commercial reply, Owner Rob, and a "Passed to you" email to Rob's address (never Sam).
