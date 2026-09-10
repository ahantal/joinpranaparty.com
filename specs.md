# Prana Party — Site Specification

Living spec for **JoinPranaParty.com**, the landing page for the first Prana Party.
Update this file whenever the page, content, or deployment changes.

- **Last updated:** 2026-09-10
- **Live URL:** https://joinpranaparty.com/
- **Repo:** https://github.com/ahantal/joinpranaparty.com
- **Status:** Live. Registration form pending a real-device end-to-end test (see [§9](#9-open-items)).

---

## 1. Purpose & goal

A focused, single-page event landing site. The **one goal** is to get visitors to
register for the event. Every section funnels toward the registration form; there is
no site navigation.

Tone: welcoming, grounded, natural, intimate, community-oriented. Not overly spiritual,
not commercial, not corporate SaaS.

## 2. The event

| Field | Value |
| --- | --- |
| Name | **PRANA PARTY** |
| Descriptor | A Free Virtual Soma+IQ™ Breathwork Gathering (hero line). Meta descriptions and the hero image still read "A Free Virtual Breathwork Gathering". |
| Date | **Friday, September 18, 2026** |
| Time | **5:30 PM to 7:30 PM EDT** |
| Location | Online |
| Price | Free |
| Level | All levels welcome |
| Hosts | Luisa Fernanda · Ali C. Hantal |

Host names are always written in full: **Luisa Fernanda** and **Ali C. Hantal**
(never "Ali Hantal"). The hero graphic has "ALI HANTAL" baked into the image and
cannot be edited without re-exporting the artwork.

Date/time string is used **verbatim and consistently** everywhere on the page.
The supplied promo graphics mention a monthly "third Friday" cadence — this is
intentionally ignored; the site is scoped to the single Sept 18 event.

## 3. Tech stack & architecture

- **Single static file:** `index.html` — all HTML, CSS (`<style>` in `<head>`), and
  JS (`<script>` before `</body>`) inline. No build step, no framework, no dependencies.
- **Fonts:** Google Fonts — Cormorant Garamond (display), Mulish (body/UI), Sacramento
  (script accents). Loaded via `<link>` with `preconnect`.
- **Hosting:** GitHub Pages, `main` branch, root. Custom domain via `CNAME` file.
- **Analytics:** none.
- **No cookies, no localStorage, no third-party scripts** other than Google Fonts.

### File layout

```
index.html                     The entire page
CNAME                           joinpranaparty.com
README.md                       Contributor / deploy notes
specs.md                        This file
.gitignore                      .DS_Store, logs, node_modules
images/
  hero-prana-party.jpg          Hero banner (cropped from promo-main.png)
  host-luisa-fernanda.jpg       Host portrait (from promo-main.png)
  host-ali-hantal.jpg           Host portrait (from promo-main.png)
  source/
    promo-main.png              Original promo graphic (reference; not served)
    IMG_7816.AVIF               Original brand graphic (reference; not served)
    IMG_7817.AVIF               Original brand graphic (reference; not served)
```

## 4. Page structure

In document order:

1. **Hero** — logo wordmark, descriptor (*"A Free Virtual Soma+IQ™ Breathwork Gathering"*),
   date/time/format lines, primary CTA
   *"Join the Prana Party"*, script line *"Come breathe with us."*, then the hero
   banner image. Centered layout.
2. **What is it?** — sun motif, eyebrow, large statement:
   *"A free, virtual space to breathe, share, and celebrate the power of breath together."*
   → *"No experience is needed."* → *"Just you and your breath."* (script accent)
3. **How it works / Who is it for?** — two-column feature band with line icons.
   - *How it works:* guided breathwork for clarity, connection, and vitality, then time
     to connect and share; accessible for first-timers and experienced breathers alike.
   - *Who is it for?:* Everyone — breathwork-curious or seasoned. *"Come as you are."*
4. **Event highlight** — deep-green full-bleed band: date, time, pills
   (Online / Free / All Levels Welcome), secondary CTA *"Reserve My Spot"*.
5. **Your Hosts** — eyebrow, *"Luisa Fernanda & Ali C. Hantal"*, two square portraits with
   script name captions. No bios or credentials (do not invent any).
6. **Registration** (`#register`) — see [§6](#6-registration-form).
7. **Footer** — *PRANA PARTY*, *Breathe. Connect. Celebrate.*, *© 2026 Prana Party · JoinPranaParty.com*.

Both CTAs smooth-scroll to `#register` and move focus to the First Name field
(respects `prefers-reduced-motion`).

## 5. Visual design

| Token | Value | Use |
| --- | --- | --- |
| `--cream` | `#f4f0e4` | Primary background |
| `--paper` | `#faf7ef` | Alternate section / input background |
| `--green` | `#3d4a32` | Headings, primary accents, event band |
| `--green-deep` | `#2f3a27` | Footer, button hover |
| `--green-soft` | `#5c6b4c` | Secondary text, icon strokes |
| `--gold` | `#c08a3e` | Primary CTA buttons |
| `--gold-deep` | `#a9772f` | Eyebrows, script accents, CTA hover |
| `--ink` | `#39402f` | Body text |
| `--ink-soft` | `#5b6150` | Muted body text |

- **Type:** Cormorant Garamond for all `h1`–`h3` and large statements; Mulish for body,
  labels, buttons; Sacramento for short script accents and host names.
- **Shape:** pill buttons (`border-radius:999px`), 12–20px rounded inputs/cards, soft
  long-throw shadows.
- **Motifs:** inline-SVG sunrise/rays divider, inline-SVG line icons (heart, people).
  Botanical elements come from the hero image itself.
- **Imagery:** only the supplied Prana Party art — no stock photography, no generated
  substitutes, no psychedelic breathwork imagery.

## 6. Registration form

**Heading:** *Join the Prana Party*
**Sub:** *Reserve your spot for our free virtual breathwork gathering on Friday, September 18.*
**Above fields:** *Fields marked with \* are required.*

### Fields (this list is exhaustive — add no personal-info fields)

| Label | `name` | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| First Name * | `first_name` | text | Yes | `autocomplete="given-name"` |
| Last Name * | `last_name` | text | Yes | `autocomplete="family-name"` |
| Email * | `email` | email | Yes | must validate as an email address |
| Mobile Phone Number | `mobile_phone` | tel | No | labelled "(optional)" |
| Participant Acknowledgment & Release * | `participant_release` | checkbox | Yes | value `Agreed`; never pre-checked; see below |

**Explicitly excluded:** address, city, birthday, time zone, gender, comments/message,
breathwork experience, newsletter checkbox, marketing consent.

### Participant Acknowledgment & Release

Sits **between the Mobile Phone field and the submit button**, in a subtly bordered
`--paper` box (`.release`) with smaller (~0.82rem) but readable text and generous
line spacing — integrated into the form, not a legal wall.

- **Title:** *Participant Acknowledgment & Release*
- **Body (two paragraphs):** voluntary wellness practice / take responsibility for own
  well-being / no medical, psychological, or therapeutic treatment / releases
  **Luisa Fernanda, Ali C. Hantal, Prana Party, and its facilitators and organizers**
  from claims arising from voluntary participation, to the extent permitted by law.
  (Full wording lives in `index.html`.)
- **Required checkbox**, asterisked, not pre-checked:
  *"I have read, understand, and agree to the Participant Acknowledgment & Release above. \*"*
- Submitting is blocked until it is checked. Failure message:
  *"Please confirm that you have read and agree to the Participant Acknowledgment &
  Release before joining."*
- On a valid submission the checkbox contributes `participant_release=Agreed` to the
  Web3Forms payload, recording consent.

### Hidden inputs

| `name` | Value |
| --- | --- |
| `access_key` | `c3595d27-6d11-4842-aa55-2113d1a27bac` |
| `subject` | `Prana Party Registration - September 18, 2026` |
| `from_name` | `Prana Party Registration` |
| `botcheck` | honeypot checkbox inside a `display:none` wrapper (unchecked = human) |

### Submit button

- Text: **JOIN THE PRANA PARTY** — visually prominent (gold, full width).
- On submit: disabled + label changes to **Joining…**; a `submitting` flag blocks
  duplicate submissions.

### Behaviour

1. `submit` is intercepted (`novalidate` on the form; JS owns validation).
2. Client-side checks, in order: all three required text fields non-empty; email matches
   `/^[^\s@]+@[^\s@]+\.[^\s@]+$/`; the Participant Acknowledgment & Release checkbox is
   checked. Any failure shows an inline message, no request sent.
3. Request: `POST https://api.web3forms.com/submit`, `Content-Type: application/json`,
   `Accept: application/json`, body = JSON object of all form fields.
4. **Success** (`response.ok && data.success`): form is hidden, the success panel is
   revealed and scrolled into view.
5. **Failure** (bad response or network error): inline error message, button re-enabled,
   `submitting` reset. No redirect, no generic error page.

### Success panel copy

> ## You're in! 🎉
> **We're excited to breathe with you.**
> You'll receive the information you need for the Prana Party at the email address you provided.
> **Friday, September 18, 2026**
> **5:30 PM to 7:30 PM EDT**

### Error message copy

> Something went wrong while submitting your registration. Please try again.

## 7. Responsive & accessibility

- Breakpoints: `≤820px` collapses the feature band to one column; `≤560px` bumps base
  font, stacks host portraits, tightens gutters. No horizontal scroll at 320–1280px
  (verified).
- Mobile priorities (traffic is largely from Instagram / social): readable hero, faces
  not awkwardly cropped, large tap targets, full-width inputs, no tiny text.
- `<img>` elements have width/height attributes; below-fold images are `loading="lazy"`.
- Form inputs have associated `<label>`s; error text is a `role="alert"` live region;
  focus-visible outline on the primary button; `*` markers are `aria-hidden`.
- Honours `prefers-reduced-motion` (disables smooth scroll).

## 8. SEO & metadata

- `<title>`: **Prana Party | Free Virtual Breathwork Gathering**
- Meta description: *Join Prana Party, a free virtual breathwork gathering with Luisa
  Fernanda and Ali C. Hantal. Friday, September 18, 2026 from 5:30 PM to 7:30 PM EDT. All
  levels welcome.*
- Open Graph + Twitter card tags set (title, description, `og:image` = hero image,
  `og:url` = `https://joinpranaparty.com/`).
- `<link rel="canonical">` → `https://joinpranaparty.com/`.
- Inline SVG favicon (green rounded square, "P").
- `theme-color` `#3d4a32`.

## 9. Deployment

1. Commit to `main`, `git push origin main`.
2. GitHub Pages (Settings → Pages → deploy from `main` / root) rebuilds automatically;
   build takes ~1 min. `CNAME` keeps the custom domain bound.
3. Verify: `curl -sI https://joinpranaparty.com/` → `HTTP/2 200`.

Attribution for commits: `Co-Authored-By: Claude Sonnet 5 <noreply@anthropic.com>`.

## 10. Open items

- [ ] **Real-device end-to-end test of the registration form.** Web3Forms / Cloudflare
      blocks datacenter and headless-browser traffic, so submission could not be verified
      from the build environment. Submit once from a phone/laptop, confirm the success
      panel appears and the notification email arrives.
- [ ] If the notification email does not arrive, confirm the Web3Forms account email is
      **verified** (submissions are not delivered until it is).
- [ ] Confirm `https_enforced` is on in GitHub Pages settings once the domain's TLS cert
      is issued.

## 11. Change log

| Date | Change |
| --- | --- |
| 2026-09-10 | Initial landing page built and deployed; assets derived from supplied promo art. |
| 2026-09-10 | Web3Forms access key added. |
| 2026-09-10 | Registration switched to JSON submission (Web3Forms canonical client-side spec). |
| 2026-09-10 | Added `specs.md`. |
| 2026-09-10 | Host name updated to "Ali C. Hantal" across all page copy, alt text, and metadata. |
| 2026-09-10 | Hero descriptor changed to "A Free Virtual Soma+IQ™ Breathwork Gathering". |
| 2026-09-10 | Added Participant Acknowledgment & Release block + required `participant_release` checkbox above the submit button. |
