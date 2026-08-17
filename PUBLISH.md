# Publish this site — paste into a Claude Code session

Publish the static site in this folder to **https://carolinapaintingmn.com**.

## Facts you need
- The site is **plain static HTML**. No build step, no framework, no dependencies.
  `index.html` is at the root of this folder and references the images relatively.
- The domain **carolinapaintingmn.com is already registered in my Vercel account.**
  So DNS and the TLS certificate are handled inside Vercel — no external DNS
  provider, no records to copy by hand.
- I'm logged into Vercel and GitHub in the browser on this machine.

## What to do
1. Put this folder's contents at the **top level** of a new GitHub repo
   (suggested name `carolina-painting-website`). Public or private both work.
   The files must sit at the repo root — if `index.html` ends up nested inside a
   sub-folder, Vercel serves a 404.
2. Import that repo into Vercel as a new project. Framework preset: **Other**.
   No build command, no output directory — it's static.
3. In the project's **Settings → Domains**, add both `carolinapaintingmn.com`
   and `www.carolinapaintingmn.com`, with www redirecting to the apex.
4. Verify in a real browser once it's live: the page loads over HTTPS, the family
   photo renders, and the phone button is a working `tel:` link.

## Known-incomplete, don't "fix" it silently
- The contact form's `action` is the literal string `YOUR_FORMSPREE_ENDPOINT`,
  so submitting does nothing. That's deliberate and documented — it needs a
  Formspree account I haven't set up. **Leave it and tell me**, or ask me to
  create the account. The phone number is the working contact route meanwhile.
- There's no email address on the site yet (Zoho is set up but the address isn't
  wired in). There are marked comment spots in `index.html` for it.
- `DEPLOY.md` in this folder is the long-form runbook if you want the detail.
