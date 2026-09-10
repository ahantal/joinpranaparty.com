# Prana Party — Website

Static two-page site for the first **Prana Party**, a free virtual Soma+IQ™ breathwork
gathering hosted by **Luisa Fernanda** and **Ali C. Hantal**, brought to you by
**@ Bliss Foundation**.

**Event:** Friday, September 18, 2026 · 5:30 PM to 7:30 PM EDT · Online · Free · All levels welcome

`specs.md` is the full living specification — read it first.

## Files

| Path | Purpose |
| --- | --- |
| `index.html` | Landing page. One inline `<script>` (registration + calendar logic). |
| `prepare/index.html` | Preparation page, served at `/prepare/`. |
| `assets/site.css` | Shared styles for both pages — design tokens + all components. |
| `prana-party.ics` | Calendar file for "Add to Apple Calendar" (embeds the Zoom URL). |
| `specs.md` | Full site specification. Keep it current. |
| `images/experience-prana-party.jpg` | Wide experiential photo below the hero. |
| `images/prana-party-social.jpg` | 1200×630 social-share card (og:/twitter: image). |
| `images/atbliss-foundation-logo.png` | @ Bliss Foundation footer logo (links to atbliss.org). |
| `images/host-*.jpg` | Host portraits. |
| `images/hero-prana-party.jpg` | Old promo banner — no longer shown. |
| `images/source/` | Original supplied graphics (not served). |
| `CNAME` | Custom domain for GitHub Pages. |

## Registration (Web3Forms)

Posts JSON to `https://api.web3forms.com/submit`. `access_key` is in the hidden input
near the top of the `<form>` in `index.html`. Fields: `first_name`, `last_name`,
`email`, `mobile_phone`, `participant_release` (`Agreed`), hidden `subject` /
`from_name`, and a `botcheck` honeypot. Client-side validation → `Joining…` state →
duplicate-submit guard → on success the form is replaced by the confirmation panel
(Zoom button + Google/Apple/Outlook calendar + prepare link) and a
`pranaPartyRegistered` localStorage flag keeps that panel on return visits until the
event passes.

## Zoom link

Not present in the landing-page HTML (base64 in the script, written to hrefs only after
registration). It is deliberately reachable via `/prana-party.ics` and `/prepare/` —
see `specs.md` §7.

## Local preview

Serve from the repo root so absolute paths resolve:

```bash
python3 -m http.server 8000
# http://localhost:8000/  and  http://localhost:8000/prepare/
```

## Deployment (GitHub Pages)

Push to `main`. **Settings → Pages** deploys from `main` / root; `CNAME` keeps the
domain. `/prepare` 301s to `/prepare/`; `.ics` serves as `text/calendar`.
