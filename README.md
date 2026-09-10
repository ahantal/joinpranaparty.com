# Prana Party — Landing Page

A single-page, static landing site for the first **Prana Party**, a free virtual
breathwork gathering hosted by **Luisa Fernanda** and **Ali C. Hantal**.

**Event:** Friday, September 18, 2026 · 5:30 PM to 7:30 PM EDT · Online · Free · All levels welcome

## Files

| Path | Purpose |
| --- | --- |
| `index.html` | The entire page — markup, styles, and JS are inline. No build step. |
| `specs.md` | Full site specification — content, form contract, design tokens, open items. Keep it current. |
| `images/experience-prana-party.jpg` | Wide experiential photo shown below the hero. |
| `images/atbliss-foundation-logo.png` | @ Bliss Foundation logo in the footer (links to atbliss.org). |
| `images/hero-prana-party.jpg` | Old promo banner — now only the social (og:/twitter:) preview image. |
| `images/host-luisa-fernanda.jpg`, `images/host-ali-hantal.jpg` | Host portraits. |
| `images/source/` | Original supplied graphics kept for reference (not served). |
| `CNAME` | Custom domain for GitHub Pages (`joinpranaparty.com`). |

## Registration form (Web3Forms)

The form posts to `https://api.web3forms.com/submit`. The Web3Forms `access_key`
is set in the hidden input near the top of the `<form>` in `index.html` — swap it
there if the destination inbox ever changes.

Submitted fields: `first_name`, `last_name`, `email`, `mobile_phone`, plus a hidden
`subject` of `Prana Party Registration - September 18, 2026` and a `botcheck`
honeypot for spam protection.

The form validates required fields and email format on the client, shows a
`Joining…` loading state, prevents duplicate submissions, replaces itself with a
success message on completion, and shows an inline error message if the request
fails.

## Local preview

Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

## Deployment (GitHub Pages)

1. Push to `https://github.com/ahantal/joinpranaparty.com`.
2. Repo **Settings → Pages** → deploy from the default branch, root.
3. Point the `joinpranaparty.com` DNS at GitHub Pages; the `CNAME` file is already in place.
