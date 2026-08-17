# Putting carolinapaintingmn.com live

Written for someone who has never used GitHub or Vercel. No command line required — there's a browser-only path for every step. Budget about 20 minutes.

You already have the two things that usually hold people up: the domain (`carolinapaintingmn.com`, registered on Vercel) and a real phone number on the page. So this is genuinely just uploading files.

---

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | The website itself. One file, all the text and styling. |
| `huriel-family.jpg` | The photo on the homepage. |
| `og-image.jpg` | The preview card that appears when someone shares your link in a text, on Facebook, or on Nextdoor. |
| `favicon.svg`, `apple-touch-icon.png`, `icon-512.png` | The little icon in the browser tab and on phone home screens. |
| `robots.txt`, `sitemap.xml` | Tells Google it's allowed to list your site. |
| `vercel.json` | Tells Vercel to cache your images so the site loads fast. |
| `DEPLOY.md` | This guide. |

**Keep all of these together.** `index.html` looks for the images in the same folder, so if you move one without the others the photo will disappear.

---

## Step 1 — Put the files on GitHub

GitHub is free storage for code. Vercel watches it and republishes your site whenever the files change. You never have to touch it again after this.

1. Go to **github.com** and sign up (free) if you don't already have an account.
2. Click the **+** in the top-right → **New repository**.
3. Name it `carolina-painting-website`.
4. Choose **Public** or **Private** — either works with Vercel. Private is fine if you'd rather it not be browsable.
5. Do **not** tick "Add a README file." Leave the extras alone.
6. Click **Create repository**.
7. On the next screen, find the link that says **"uploading an existing file"** and click it.
8. Drag **every file from this folder** into the browser window — all of them at once, `index.html` included.
9. In the "Commit changes" box at the bottom, type `First version of the website`, then click **Commit changes**.

That's GitHub done. You should see your files listed.

> **Note on the file structure:** the files must sit at the *top level* of the repository, not inside a `site` sub-folder. If you accidentally end up with `site/index.html`, Vercel won't find the homepage. Easiest fix is to delete the repo and re-upload the files individually rather than dragging the folder itself.

---

## Step 2 — Deploy it on Vercel

1. Go to **vercel.com** and log in with the account that owns your domain.
2. From the dashboard, click **Add New… → Project**.
3. Click **Import Git Repository**, and connect your GitHub account when it asks. Grant access to the repo you just made.
4. Find `carolina-painting-website` in the list and click **Import**.
5. On the configuration screen, **change nothing.** Framework Preset should say "Other" and there's no build command needed — this is a plain HTML site, so Vercel just serves the files as-is.
6. Click **Deploy**.

Wait about thirty seconds. You'll get a confetti screen and a temporary address like `carolina-painting-website-xyz.vercel.app`. Click it and confirm the site looks right.

---

## Step 3 — Attach your real domain

Because you bought the domain through Vercel, this part is unusually easy — no DNS records to copy by hand.

1. In your new project, go to **Settings → Domains**.
2. Type `carolinapaintingmn.com` and click **Add**.
3. Vercel will recognise that you already own it and wire up the DNS itself. When asked, also add the `www.carolinapaintingmn.com` version and let Vercel redirect it to the main one.
4. Give it a few minutes. The HTTPS certificate is issued automatically — you don't need to buy one.

Visit **https://carolinapaintingmn.com**. That's your site, live.

---

## Step 4 — Make the contact form actually work

Right now the form on the page looks fine but goes nowhere. It needs somewhere to send submissions. This is free and takes two minutes.

1. Go to **formspree.io** and sign up.
2. Create a new form. Formspree gives you an endpoint that looks like `https://formspree.io/f/abcdwxyz`.
3. In GitHub, open `index.html`, click the pencil icon to edit, and use Ctrl+F / Cmd+F to find `YOUR_FORMSPREE_ENDPOINT`.
4. Replace that text with your endpoint URL. Keep the quote marks around it.
5. Click **Commit changes**.

Vercel republishes automatically within a minute or so. Test it by submitting the form yourself.

Until you do this, the phone number is your working contact route — which is fine, since most homeowners call rather than fill in forms anyway.

---

## Step 5 — A few things worth doing the same day

- **Google Business Profile.** Now that you have a live URL, add it. This is the single highest-value free thing for a local trade — it's what puts you in "painters near me" and on Maps.
- **Test the phone link on a real phone.** Open the site on your mobile and tap the green button. It should open the dialer with (612) 405-2692 ready to go.
- **Send yourself the link in a text message.** You should see the preview card with your name, the photo, and the phone number. That card is what everyone sees when your link gets shared, so it's worth confirming it looks right.
- **Set up email on the domain.** Vercel registers domains but doesn't host email. Google Workspace is the usual route — you'd add its MX records under Vercel's DNS settings for the domain. Once you have an address, add it to the footer of `index.html` (there's a comment marking the spot).

---

## How to change the site later

Everything is one file. To edit any text:

1. Open the repo on GitHub → click `index.html` → click the pencil icon.
2. Make your edit, scroll down, **Commit changes**.
3. Vercel redeploys in under a minute. No other steps.

**To add work photos:** upload your images to the repo (name them `work-1.jpg` through `work-4.jpg`), then in `index.html` find the comment `TO ADD PHOTOS LATER`. Delete the honest "no gallery yet" block above it and uncomment the grid underneath. Instructions are written inline right there.

**To add reviews:** find the comment block `REVIEWS SECTION`. I removed that section deliberately rather than leaving a fake-sounding placeholder quote, which costs more trust than having no reviews at all. Once you have two or three real Google reviews, paste them in there.

---

## Deploying the job-manager app (separately, later)

The app in `painting-business-app.zip` is a different animal — it needs a build step and your Supabase keys. Don't mix it into this repo. When you're ready:

1. Make a **second** GitHub repo, `carolina-painting-app`, and upload the contents of the zip's `web/` folder.
2. New Vercel project → import that repo.
3. Framework Preset: **Vite**. Build command `npm run build`. Output directory `dist`.
4. Under **Environment Variables**, add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` with your Supabase values. This matters — `.env` files aren't uploaded to GitHub on purpose, so Vercel needs them set here or the app will load to a blank screen.
5. Give it its own address: **Settings → Domains → `app.carolinapaintingmn.com`**.

Keeping the marketing site and the internal app on separate addresses means a mistake in one can never take down the other, and customers never stumble into your job records.

---

## If something goes wrong

**The site loads but the photo is broken.** The image files didn't get uploaded, or ended up in a sub-folder. Check the repo — `huriel-family.jpg` should sit right next to `index.html`.

**Vercel says "404 — page not found."** Your files are probably one level too deep. `index.html` must be at the top of the repository, not inside a folder.

**The domain shows a Vercel error page.** DNS can take a few minutes to settle. If it's still failing after fifteen, check **Settings → Domains** for a warning next to the domain name.

**Edits aren't appearing.** Check the **Deployments** tab in Vercel. If the newest one is red/failed, click it to read the log. If it's green, try a hard refresh (Cmd+Shift+R or Ctrl+Shift+R) — your browser is probably showing a cached copy.

**The preview card in text messages is wrong or missing.** Some apps cache these aggressively. Facebook has a "Sharing Debugger" tool that forces a refresh; for iMessage, it usually sorts itself out within a day.
