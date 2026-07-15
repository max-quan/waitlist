Palo Alto Restaurant Membership — Waitlist Page
A single-page waitlist landing page for a Palo Alto restaurant BOGO membership
concept ($9/month, unlimited BOGO redemptions at partner restaurants). Built
as one self-contained HTML file — no build step, no dependencies.
Files
`waitlist.html` — the landing page itself. Open it directly in any browser,
or view it through Claude's artifact panel.
What it does
Displays a short, "mysterious" pitch with the $9/month price called out
Collects email signups
Shows a live count of how many people have joined
Shows a thank-you confirmation screen after signup
Includes a hidden admin view to see and export collected emails
Viewing collected emails
Open the page with `?admin=1` added to the URL, e.g.:
```
waitlist.html?admin=1
```
This shows every collected email in a text box, with Copy All and
Download CSV buttons.
⚠️ This is not real authentication — it's just a URL trick. Anyone who
has the link and knows to add `?admin=1` can see the list. Don't share the
live link publicly without keeping that in mind. If this gets real traffic,
put actual auth in front of the admin view before it matters.
Important limitation: where emails actually get saved
This page uses Claude's built-in artifact storage (`window.storage`) to save
emails. That storage only exists when the page is viewed inside a Claude.ai
artifact (the chat side panel, or a shared Claude artifact link).
If you download `waitlist.html` and open it locally, or host it yourself on
a real domain (Vercel, Netlify, GitHub Pages, etc.), `window.storage` won't
exist — the page will still look like it works (the thank-you screen still
shows), but no email will actually be saved anywhere, since there's
nothing on a static host to save it to.
If you want this live on a real URL and actually collecting emails, you
have two options:
Swap the storage calls for a real form backend (e.g., Formspree, Google
Forms embedded, Mailchimp's signup API, or a simple serverless function
writing to a database/spreadsheet).
Keep using this purely as a Claude artifact link for now (fine for
testing/small-scale collection), and migrate later once you're ready to
host it properly.
Ask if you want help wiring up a real backend for this — it's a quick swap.
Tech notes
No `<form>` element is used on purpose — Claude's artifact preview runs in
a sandboxed iframe that can block native form submission, so the button
uses a plain click handler instead. Don't reintroduce a `<form>` wrapper
around the email input/button without testing it in the artifact panel
first.
Fonts: Fraunces (display) + Work Sans (body), loaded from Google Fonts.
No external JS dependencies.
