# Prana Party — Site Specification

Living spec for **JoinPranaParty.com**. Update this file whenever content, structure,
or deployment changes.

- **Last updated:** 2026-09-23
- **Live URL:** https://joinpranaparty.com/  ·  Prep page: https://joinpranaparty.com/prepare/
- **Repo:** https://github.com/ahantal/joinpranaparty.com
- **Status:** Live. Registration end-to-end still needs a real-device test (see [§12](#12-open-items)).

Participant journey: **Discover → Understand → Trust → Register → Save → Prepare → Join.**

---

## 1. Purpose & goal

A focused two-page event site. The **one goal** is registration. No site navigation
beyond a single "Prana Party" wordmark link on `/prepare/` back to home.

Tone: warm, human, natural, joyful, connected. Not spiritual-heavy, not commercial,
not corporate SaaS. Do not overbuild — no bios, testimonials, FAQs, pricing, pop-ups,
extra registration questions, or unrelated @ Bliss Foundation content.

## 2. The event

| Field | Value |
| --- | --- |
| Name | **PRANA PARTY** |
| Descriptor | **A Free Virtual Soma+IQ™ Breathwork Gathering** |
| Date | **Saturday, October 24, 2026** (changed 2026-09-24 from Friday, September 18, 2026) |
| Time | **5:30 PM to 7:30 PM EDT** (UTC−4; 21:30–23:30 UTC). End time assumed unchanged at 7:30 PM (2 hours); confirm with the site owner. |
| Location | Online via Zoom |
| Price | Free |
| Level | All levels welcome |
| Hosts | Luisa Fernanda · Ali C. Hantal |
| Brought to you by | @ Bliss Foundation |

- Host name is always written in full: **Luisa Fernanda** and **Ali C. Hantal**
  (never "Ali Hantal"), including in the release text.
- Partner org is always **"@ Bliss Foundation"** — never "At Bliss Foundation",
  "@Bliss Foundation", or "AtBliss".
- Date/time string is used verbatim everywhere.
- The supplied promo graphics mention a monthly "third Friday" cadence — ignored;
  the site is scoped to the single Sept 18 event.

## 3. Tech stack & architecture

- **Three static HTML pages**, no build step, no framework, no dependencies:
  `index.html` (landing + registration), `thankyou/index.html` (confirmation, served at
  `/thankyou/`), and `prepare/index.html` (served at `/prepare/`). Same page structure
  as atbliss.org and atbliss.org/breathewithme: landing with form → separate thank-you
  page → separate no-date prepare page.
- **Shared stylesheet:** `assets/site.css` — all design tokens + components. Each page
  adds only a handful of inline style overrides. `index.html` also has one inline
  `<script>` (registration + calendar logic).
- **Fonts:** Google Fonts — Cormorant Garamond (display), Mulish (body/UI),
  Sacramento (script accents). `<link>` + `preconnect`.
- **Hosting:** GitHub Pages, `main` branch, root. Custom domain via `CNAME`.
- `localStorage` is used for one flag only (`pranaPartyRegistered`, see [§8](#8-confirmation--thank-you-state)).
  No analytics, no cookies, no third-party scripts other than Google Fonts.

### File layout

```
index.html                     Landing page + registration form
thankyou/index.html            Confirmation page (/thankyou/)
prepare/index.html             Preparation page  (/prepare/)
assets/site.css                Shared styles for both pages
prana-party.ics                Calendar file (Apple Calendar); embeds the Zoom URL
CNAME                          joinpranaparty.com
README.md · specs.md · .gitignore
images/
  experience-prana-party.jpg   Wide experiential photo below the hero (from Hero-parana-party-2.jpeg)
  prana-party-social.jpg       1200×630 social-share card (event info; generated)
  atbliss-foundation-logo.png  @ Bliss Foundation footer logo — white text + gold mark, transparent
  love-your-wellth-logo.png    "Love Your Wellth" footer logo — transparent, navy text lightened to cream
  hero-prana-party.jpg         Old promo banner — no longer shown on the page
  host-luisa-fernanda.jpg / host-ali-hantal.jpg   Host portraits — 723×723, pre-cropped
                                square and centered on each host's face (not relying on
                                object-fit:cover's default 50/50 crop; see §4.7)
  source/                      Originals + full-res uploads kept for reference (not served)
Archives/                      Local backups — gitignored, not deployed
```

## 4. Landing page structure (`index.html`)

In document order:

1. **Hero** — "PRANA PARTY", descriptor *"A Free Virtual Soma+IQ™ Breathwork Gathering"*,
   date/time/format lines, primary CTA *"Join the Prana Party"*, script line
   *"Come breathe with us."*
2. **Experiential image** — wide photo, `.hero__figure`, rounded corners, subtle border
   + soft shadow. No text/overlay/caption.
3. **What is it?** — statement + *"No experience is needed."* + *"Just you and your breath."*
   Directly below, a secondary **Soma+IQ™** note (same section, thin divider):
   *"Soma+IQ™ is a somatic breathwork practice that uses conscious breathing to help us
   reconnect with the body, release what we are holding, and return to a more present
   state."* No medical/therapeutic claims.
4. **How it works / Who is it for?** — two-column band.
   - *How it works:* guided breathwork for clarity, connection, and vitality; accessible
     first-timer or experienced.
   - *Who is it for?:* Everyone. The old "Come as you are." line is now an understated
     script link **"Come as you are. →"** to `/prepare/`, with *"See how to prepare"*
     beneath it (not a button).
5. **What to expect** — 4 numbered stages, horizontal on desktop / stacked on mobile:
   **Arrive · Breathe · Connect · Celebrate**.
6. **Event highlight** — deep-green band: date, time, pills (Online / Free / All Levels
   Welcome), secondary CTA *"Reserve My Spot"* (smooth-scrolls to `#register`).
7. **Your Hosts** — *"Luisa Fernanda & Ali C. Hantal"*, two square portraits, script
   captions, then the line *"Two facilitators. One shared intention: creating a space to
   breathe, reconnect, and enjoy."* No bios.
   Portraits are pre-cropped to 723×723 squares (not left to the browser's default
   center-crop) — see file layout note above. When replacing a host photo: archive the
   raw upload and the previous photo under `images/source/`, crop/center manually
   (a quick pupil/nose measurement on a zoomed, gridded copy of the source beats
   eyeballing the thumbnail — see git history around 2026-09-11/12 for the iterations
   this took), save back to the same filename, and bump the `?v=` query on that `<img>`
   src so browsers/CDN don't keep serving the cached old file.
8. **Registration** (`#register`) — see [§6](#6-registration-form)–[§8](#8-confirmation--thank-you-state).
9. **Footer** — see [§9](#9-footer).

Both hero/highlight CTAs smooth-scroll to `#register` (respects `prefers-reduced-motion`).

## 5. Visual design

| Token | Value | Use |
| --- | --- | --- |
| `--cream` `#f4f0e4` | primary background |
| `--paper` `#faf7ef` | alternate section / input background |
| `--green` `#3d4a32` | headings, accents, event band |
| `--green-deep` `#2f3a27` | footer, button hover |
| `--green-soft` `#5c6b4c` | secondary text, icon strokes |
| `--gold` `#c08a3e` | primary CTA buttons |
| `--gold-deep` `#a9772f` | eyebrows, script accents, CTA hover |
| `--ink` `#39402f` / `--ink-soft` `#5b6150` | body / muted text |

- **Type:** Cormorant Garamond for `h1`–`h3` and large statements; Mulish for body,
  labels, buttons; Sacramento for short script accents.
- Pill buttons; 12–20px rounded cards/inputs; soft long shadows; inline-SVG sun motif
  and line icons. Imagery: supplied Prana Party art only.

## 6. Registration form

**Heading:** *Join the Prana Party*
**Sub (two lines):** *Reserve your spot for our free virtual breathwork gathering on
Saturday, October 24.* / *Register below and we'll give you everything you need to join
the gathering.*
**Above fields:** *Fields marked with \* are required.*

### Fields (exhaustive — add no personal-info fields)

| Label | `name` | Type | Required |
| --- | --- | --- | --- |
| First Name \* | `first_name` | text | Yes |
| Last Name \* | `last_name` | text | Yes |
| Email \* | `email` | email | Yes (regex-validated) |
| Mobile Phone Number | `mobile_phone` | tel | No |
| acknowledgment checkbox \* | `participant_release` | checkbox | Yes — value `Agreed`, never pre-checked |

Hidden inputs: `access_key` `c3595d27-6d11-4842-aa55-2113d1a27bac`,
`subject` `Prana Party Registration - October 24, 2026`,
`from_name` `Prana Party Registration`, plus a `botcheck` honeypot (`display:none`).

### Participant Acknowledgment & Release (`#acknowledgment`)

Sits between the Mobile Phone field and the submit button, in a subtly bordered
`--paper` box (`.release`), ~0.8rem text, line-height 1.7 — fully visible, not hidden
behind a link.

- Kicker **BEFORE WE BREATHE TOGETHER**, title **Participant Acknowledgment & Release**.
- Body: six paragraphs (voluntary wellness practice & possible effects → not appropriate
  for everyone / pregnancy + medical-history precautions → consult provider if serious
  condition/medication/uncertain → listen to your body, stop if unwell → not medical/
  psychological/psychiatric/therapeutic treatment → voluntary participation, releases
  **Luisa Fernanda, Ali C. Hantal, Prana Party, and its facilitators and organizers**).
  Full wording in `index.html`.
- Required checkbox, asterisked, not pre-checked:
  *"I have read, understand, and agree to the Participant Acknowledgment & Release above,
  including the health and pregnancy precautions. \*"*
- Submitting is blocked until checked. Message:
  *"Please confirm that you have read and agree to the Participant Acknowledgment &
  Release before joining."*
- On success the checkbox contributes `participant_release=Agreed` to the Web3Forms
  payload.

### Submit & behaviour

- Button **JOIN THE PRANA PARTY** → **Joining…** while processing; disabled + a
  `submitting` flag block duplicate submissions.
- `novalidate`; JS validates in order: required text fields → email regex → checkbox.
- Request: `POST https://api.web3forms.com/submit`, JSON body of all fields,
  `Content-Type`/`Accept: application/json`.
- Failure (bad response or network error): inline message
  *"Something went wrong while submitting your registration. Please try again."*
  Button re-enabled; no redirect.
- Success: store `pranaPartyRegistered`, hide the form, reveal the confirmation ([§8](#8-confirmation--thank-you-state)).

## 7. Zoom link exposure

The raw Zoom URL (`https://us06web.zoom.us/j/85480982399?pwd=…`) is **not** in the
landing-page HTML. It is base64 in `index.html`'s script and only written into link
hrefs after a successful registration (or when the `pranaPartyRegistered` flag is
present). It also appears, by necessity, in **two publicly fetchable places**:
`/prana-party.ics` and `/prepare/`. This is accepted (the brief is explicit): no fake
security is attempted. Restricting it to registrants would need a different mechanism.

## 8. Confirmation / thank-you page (`thankyou/index.html`, served at `/thankyou/`)

**Separated from the landing page 2026-09-24** so all three breathwork sites share one
structure. A successful registration sets `localStorage.pranaPartyRegistered` and
redirects to `/thankyou/`. An early script in `index.html`'s `<head>` sends returning
registrants straight to `/thankyou/` until the event passes (`Date.now() ≤ 2026-10-24
23:30 UTC`), then clears the flag. `/thankyou/` shows the confirmation panel only when
that flag is valid; otherwise a *"Not registered yet?"* card with a button to
`/#register`. *"Registering for someone else? Start a new registration"* clears the
flag and links to `/#register`. The event constants (`ZOOM_URL`, `EVENT`, calendar
builders) now live in `thankyou/index.html`; **`EVENT.endMs` there must match
`EVENT_END_MS` in `index.html` and `prepare/index.html`** (update all three for a new
event). Minimal top bar and the shared footer, like `/prepare/`.

1. **YOU'RE IN! 🎉** · *We're excited to breathe with you.* · **Saturday, October 24,
   2026 / 5:30 PM to 7:30 PM EDT / Online** · *Come as you are.* (script)
**2026-09-24: blocks 2 (How to prepare link) and 3 (Join on Zoom) were removed** at the site owner's request; the full preparation guide is in the panel, and the Zoom link reaches registrants through the confirmation email and the calendar entries. Under the calendar buttons: *"The Zoom link is in your confirmation email."*; the preparation guide ends with *"This preparation guide is also included in your confirmation email."* Current order: confirmation → Add to Calendar → preparation guide → reset link. Historical list:

2. **HOW TO PREPARE →** link to `/prepare/` + *"A few simple things to know before we
   breathe together."* — sits directly under "Come as you are.", above the Zoom button.
3. **JOIN PRANA PARTY ON ZOOM** — gold **Join on Zoom** button, new tab. Hint:
   *"Save this page or add Prana Party to your calendar below so you'll have the Zoom
   link when it's time to join."*
4. **ADD PRANA PARTY TO YOUR CALENDAR** — Google Calendar (template URL, new tab),
   Apple Calendar (`/prana-party.ics`), Outlook (outlook.live.com deeplink, new tab).
   Google/Outlook hrefs are built in JS on success; each embeds the Zoom URL and the
   `/prepare/` URL in the description.

**2026-09-23/24:** a preparation guide (`.success__prep`, eyebrow *"Before we breathe
together"*) now sits after block 4 (calendar), so the order is Join on Zoom → Add to
Calendar → preparation: the same
content as `/prepare/` (What you'll need, Give your body some space, What to expect,
A few minutes before, Listen to your body → `#acknowledgment`), with no date. Its
grids are collapsed to fit the narrow panel by `.success__prep` overrides in
`site.css` (stylesheet cache-buster bumped to `?v=11` on both pages). Keep it in sync
with `/prepare/`.

### Calendar event details (also `prana-party.ics`)

- Title: **Prana Party: Free Virtual Soma+IQ™ Breathwork Gathering**
- Start/End: `20261024T213000Z` / `20261024T233000Z` (UTC — renders correctly in any
  timezone). Location: *Online via Zoom*.
- Description: "Prana Party" / hosts line / **Join on Zoom:** + full Zoom URL /
  **Prepare for Prana Party:** + `https://joinpranaparty.com/prepare/` /
  "Breathe. Connect. Celebrate."

### Pending: Zoom link for October 24 (as of 2026-09-24)

The site is not being marketed yet (awaiting the business partner's approval). Until
the new Zoom link arrives:
- `thankyou/index.html`: `CALENDAR_READY = false`. The three calendar buttons are
  greyed out (`.btn.is-disabled`, no `href`) with *"Calendar links will be available
  here soon."*
- `prepare/index.html`: `ZOOM_READY = false`, so "Ready to breathe?" stays a
  registration link instead of turning into a Zoom link for registrants.
- `ZOOM_URL` in both files and the URL in `prana-party.ics` still hold the **old
  September 18 meeting** link.

**When the link arrives:** base64-encode it into `ZOOM_URL` in `thankyou/index.html`
and `prepare/index.html`, put it in `prana-party.ics` (URL and DESCRIPTION), set
`CALENDAR_READY` and `ZOOM_READY` to `true`, and update the auto-reply text.

## 9. Footer (all pages)

Deep-green band, centered:

- **PRANA PARTY** (serif caps) · *Breathe. Connect. Celebrate.* (gold script)
- small gap → label **BROUGHT TO YOU BY** → the two partner logos side by side on the
  green (`.footer__partners`, no panel, no divider). Both source files are 109px tall
  (user-sized); CSS matches them on height (109 desktop, 86 tablet, 70 small).
- *© 2026 Prana Party • JoinPranaParty.com*

- **@ Bliss Foundation** — `images/atbliss-foundation-logo.png` (white text + gold mark,
  transparent). It is the link: `https://www.atbliss.org/`, new tab,
  `rel="noopener noreferrer"`, `alt="@ Bliss Foundation"`,
  `aria-label="@ Bliss Foundation (opens in a new tab)"`.
- **Love Your Wellth** — `images/love-your-wellth-logo.png` (true RGBA PNG — do not
  palette-quantize, it leaves a matte). Built from the supplied transparent logo; its
  navy text was **lightened to cream** so it reads on the green (gold wreath/tagline
  untouched, transparency kept).
  Currently a non-linked `<img>` — **no URL supplied**; make it an `<a>` (new tab) when
  one is given. Originals in `images/source/` (`love-your-wellth-logo-original.png`,
  `love-your-wellth-logo_Transparent-original.png`).

No overflow at 320px.

## 10. Preparation page (`prepare/index.html`, served at `/prepare/`)

`<meta name="robots" content="noindex, follow">` (it contains the Zoom link). Same
visual system as the landing page, shared `site.css`, same footer. Minimal top bar:
"PRANA PARTY" wordmark → `/`.

**Rebuilt 2026-09-23 with the shared preparation content** agreed by the site owner
for every prepare page across joinpranaparty.com, atbliss.org, and
atbliss.org/breathewithme (canonical list in the atbliss.org repo's `specatbliss.md`,
`/prepare` section). **No date or time anywhere on the page**, so it never needs
updating per event (the hidden `EVENT_END_MS` Zoom-reveal cutoff in the script is the
only per-event value).

1. **Hero**: eyebrow *PREPARE FOR PRANA PARTY*, h1 *"A few simple things to know before
   we breathe together."*, script line *"Find a comfortable space. Bring your
   headphones. And come as you are."* No date.
2. **WHAT YOU'LL NEED**: 4 cards (Comfortable Clothing · A Comfortable Place to Lie
   Down · Headphones or Earbuds · A Quiet, Private Space) + wide **Zoom & Your Camera**
   card (camera check; frame chest and belly while lying down; emphasised note to turn
   off background blur and virtual backgrounds).
3. **GIVE YOUR BODY SOME SPACE**: *"Try not to eat a large meal 1 hour before the
   session."* (the site owner's chosen wording).
4. **WHAT TO EXPECT**: 3 stages with timing: **Arrive** (~15 min) · **Breathe** (~60
   min, guided through Soma+IQ™ The Journey; activation, allowing, nothing forced) ·
   **Share & Integrate** (~15 min).
5. **A FEW MINUTES BEFORE**: 8-item checklist (adds turning off phone notifications and
   joining a few minutes early), then *"Come as you are."* (script).
6. **LISTEN TO YOUR BODY**: health reminder + link to `/#acknowledgment`.
7. **READY TO BREATHE?**: green band, no date; CTA to `/#register` (becomes the Zoom
   link for registered visitors).
8. **QUESTIONS BEFORE WE BEGIN?**: unchanged.

The same content is embedded in the home page's confirmation panel (see §8).

**Auto-reply (Web3Forms, key `c3595d27-…`)**: should carry a short "How to prepare"
summary and a link to `https://joinpranaparty.com/prepare/`:

```
How to prepare:
- Wear loose, comfortable clothing.
- Find a quiet, private space and a mat or comfortable surface where you can lie on your back.
- Have headphones or earbuds ready.
- Check that Zoom, your camera, and your audio work, and turn off background blur and virtual backgrounds.
- Position your camera so your upper body can be seen while you lie down.
- Try not to eat a large meal 1 hour before the session.
- Turn off phone notifications and join a few minutes early.

Full preparation guide:
https://joinpranaparty.com/prepare/
```

Content is based on the supplied Somatic Breathwork Session Prep document.

## 11. SEO & metadata (landing page)

- `<title>`: **Prana Party | Free Virtual Soma+IQ™ Breathwork Gathering**
- Description: *Join Prana Party, a free virtual Soma+IQ™ breathwork gathering with
  Luisa Fernanda and Ali C. Hantal on Saturday, October 24, 2026 from 5:30 PM to 7:30
  PM EDT.*
- Open Graph + Twitter (`summary_large_image`); `og:image` / `twitter:image` =
  `https://joinpranaparty.com/images/prana-party-social.jpg` (1200×630, contains event
  info). Canonical `https://joinpranaparty.com/`. `theme-color` `#3d4a32`.
- JSON-LD `Event` (online, free, organizer @ Bliss Foundation, performers L.F. & A.C.H.).
  VirtualLocation URL is the site, **not** the Zoom link.

## 12. Responsive & accessibility

- No horizontal scroll at 320 / 375 / 768 / 1024 / 1280 on either page (verified).
- Stages: 4→2→1 columns; cards: 4→2→1; feature band 2→1; hosts 2→1.
- Buttons/checkbox have comfortable touch targets; inputs full-width; `role="alert"`
  live region for form errors; focus-visible outlines; `prefers-reduced-motion` honored.
- Links that open new tabs carry `rel="noopener noreferrer"`; the @ Bliss logo link has
  an explicit `aria-label`.

## 13. Deployment

1. Commit to `main`, `git push origin main`. GitHub Pages rebuilds (~1 min); `CNAME`
   keeps the domain. `.ics` is served as `text/calendar`; `/prepare` 301s to `/prepare/`.
2. Verify: `curl -sI https://joinpranaparty.com/` → 200; `/prepare/` → 200;
   `/prana-party.ics` → 200 `text/calendar`.
3. **Cache-busting:** `assets/site.css` and any host photo are referenced with a
   `?v=N` query string on both pages. Overwriting one of those files in place without
   bumping its `?v=` leaves browsers/CDN serving the stale cached copy even though the
   new bytes are live on the server — bump the version any time the file's *content*
   changes (not just when the filename does).

Commit attribution: `Co-Authored-By: Claude Sonnet 5 <noreply@anthropic.com>`.

## 14. Open items

- [ ] **Real-device end-to-end test of registration.** Web3Forms/Cloudflare blocks
      datacenter & headless traffic, so a live submit can't be verified from the build
      environment. Submit once from a phone/laptop: confirm the confirmation panel, the
      Zoom button, all three calendar buttons, and that the notification email arrives.
- [ ] If no email arrives, confirm the Web3Forms account email is **verified**.
- [ ] Spot-check the `.ics` opens in Apple Calendar with the Zoom link embedded.
- [ ] Confirm `https_enforced` in GitHub Pages settings.
- [ ] "Questions before we begin?" has no contact method — add one if the hosts want it.

## 15. Change log

| Date | Change |
| --- | --- |
| 2026-09-10 | Initial landing page built and deployed. |
| 2026-09-10 | Web3Forms key added; switched to JSON submission. |
| 2026-09-10 | Added `specs.md`. |
| 2026-09-10 | Name → "Ali C. Hantal" everywhere; hero descriptor → "…Soma+IQ™…". |
| 2026-09-10 | Added Participant Acknowledgment & Release + required checkbox. |
| 2026-09-10 | Swapped experiential image below the hero. |
| 2026-09-10 | Footer: "Brought to you by" + clickable @ Bliss Foundation logo. |
| 2026-09-10 | Major update: shared `site.css`; Soma+IQ note; "Come as you are →" link; What to Expect; hosts intention line; longer health release; post-registration confirmation with Zoom + Google/Apple/Outlook calendar; `prana-party.ics`; new `/prepare/` page; 1200×630 social image; metadata refresh; `utm_source=chatgpt.com` stripped from Zoom & @ Bliss links. |
| 2026-09-10 | `/prepare/`: "Set Up Your Camera" merged into "What You'll Need" as a full-width horizontal 5th box; its own section removed. |
| 2026-09-10 | `/prepare/`: "don't eat" window changed 2 hours → 1 hour. |
| 2026-09-10 | Footer partner logos reworked: dropped the cream panel; @ Bliss back to the white-text transparent logo; Love Your Wellth from the supplied transparent version with its navy text lightened to cream; both small, side by side on the green. |
| 2026-09-10 | Type-size pass: `.hero__come` +10%, `.lede .accent` +15%, `.footer__logo` +20% (then +10% more), `.footer__tag` +20%, `.footer__by` +10%. Briefly scoped the enlarged footer type to the home page only, then reverted to global (same on every page). |
| 2026-09-11 | Home confirmation panel: moved "How to prepare →" up to sit directly under "Come as you are.", above the Join on Zoom button (was after the calendar row). |
| 2026-09-11/12 | Replaced both host photos with new uploads, pre-cropped to 723×723 squares centered on each host's face (previously relied on the browser's default center-crop, which doesn't account for where the face actually sits in the source photo). Went through several rounds of recentering/re-zooming based on user feedback — final method: zoom into the source photo, measure the pupils/nose on a pixel grid, and set the crop from that instead of eyeballing the small thumbnail. Originals and full-res uploads archived under `images/source/`. |
| 2026-09-23 | `/prepare/` rebuilt with the shared preparation content (same as atbliss.org and /breathewithme) and all dates/times removed; same preparation guide added to the home confirmation panel under Join on Zoom (`.success__prep` in `site.css`, cache-buster `?v=11`); auto-reply prep summary recorded in §10. |
| 2026-09-24 | Confirmation panel: preparation guide moved below the calendar block (Join on Zoom → Add to Calendar → preparation). |
| 2026-09-24 | Confirmation panel: removed the How to prepare link and the Join on Zoom block; added the Zoom-link-in-email note under the calendar and the "also included in your confirmation email" line after the preparation guide (`site.css` v=12). **Note:** no auto-reply is configured for this form yet, so these notes depend on setting one up. |
| 2026-09-24 | Confirmation moved from an in-page panel on `index.html` to its own `/thankyou/` page (redirect on success, early redirect for returning registrants, not-registered fallback); event/calendar script moved with it; `site.css` v=13 (reset link style). Verified end to end in Chrome with a stubbed Web3Forms response. |
| 2026-09-24 | Next event set to Saturday, October 24, 2026, 5:30 to 7:30 PM EDT across the home page (meta, OG/Twitter, JSON-LD, hero, highlight band, registration intro, email subject), `/thankyou/` (date + calendar constants), `EVENT_END_MS`/`endMs` in all three pages, `prana-party.ics`, and README. Calendar buttons disabled and the prepare page's Zoom CTA held back until the new Zoom link arrives (see §8, Pending). `site.css` v=14. The social-share image `images/prana-party-social.jpg` still shows the old date. |
