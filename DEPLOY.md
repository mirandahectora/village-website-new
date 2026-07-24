# Village — deploy notes

Static site, no build step. Four files: `index.html`, `privacy.html`, `terms.html`, `netlify.toml`.

## Current configuration

- Site URL: `https://villagefinance.netlify.app/` (set in `canonical` and `og:url`)
- Contact address: `hector.miranda@yale.edu` (contact mailto, form error fallback, both stub pages)

No placeholders remain. Ready to deploy as-is.

## Option A — drag and drop (fastest)

Zip the folder, drop it on https://app.netlify.com/drop. Live in about ten seconds on a `*.netlify.app` subdomain.

## Option B — CLI

```bash
npm install -g netlify-cli
netlify login
netlify deploy --dir . --prod
```

## Option C — Git (recommended for anything ongoing)

Push the folder to a repo, then in Netlify: **Add new site → Import an existing project**. Build command: leave empty. Publish directory: `.` Every push to `main` redeploys.

## The contact form

It uses Netlify Forms. Netlify detects the `data-netlify="true"` attribute at deploy time and provisions a form named `village-contact` — nothing to configure, no backend, no third-party script.

- Submissions land under **Forms → village-contact** in the Netlify dashboard.
- Set up email notifications at **Site configuration → Forms → Form notifications**, or wire an outgoing webhook to Slack.
- `netlify-honeypot="bot-field"` catches most spam without a CAPTCHA. If spam gets through, add Netlify's built-in reCAPTCHA.
- The form posts via `fetch` so the page shows the success line in place rather than navigating away. If JavaScript fails, it falls back to a normal POST.

Free tier allows 100 submissions per month. Worth watching once pilot outreach starts.

## Custom domain

**Domain management → Add a domain**, then point your registrar's nameservers at Netlify or add the CNAME they give you. HTTPS provisions automatically via Let's Encrypt.

## One thing to check with counsel

Step 3 of "How it works" says pooled balances sit at a regulated U.S. partner bank. The brief's own hard rules say not to describe bank relationships, so these two instructions collide. I kept the copy verbatim as specified, and it names no institution — but it is the one line on the page worth a second look before launch.
