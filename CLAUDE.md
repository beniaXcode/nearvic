# profile.nearvic.com

Personal landing page for **Yahia Mohamed Benabbou** — Senior DevOps & DevSecOps Engineer,
Cloud Solutions Architect, SRE. Based in Rabat, Morocco (GMT+1).

Single static file: `index.html`. No build step, no dependencies, no framework.
Everything (CSS, JS, SVG icon sprite) is inline. Keep it that way unless there's a
concrete reason not to — the whole point is that it deploys anywhere by copying one file.

## Audience and job of the page

Written for engineering leaders, CTOs and technical recruiters hiring **remote senior
infrastructure contractors** in Europe, the US and the Gulf. Its job is to convince a
reader in ~30 seconds that Yahia can be trusted with production infrastructure, then
give them a way to make contact.

It is a contractor pitch, not a CV. Prose stays plain and active; the design carries the
personality.

## Positioning decisions (don't silently reverse these)

- **Roles over industries.** The hero lists roles Yahia takes (Senior DevOps Engineer,
  Senior DevSecOps Engineer, Cloud Solutions Architect, SRE, Platform Engineer), not a
  client-sector list. A hiring manager should find their own job title in the first screen.
- **No single-industry framing.** An earlier draft led with banking; it was too narrow.
  Work spans delivery platforms, sovereign cloud, GPU compute, migration, platform
  engineering and product engineering. Case-study labels are by *discipline*, not client type.
- **Security is present-tense but not overclaimed.** DevSecOps is a service line and a role,
  backed by real pipeline-security work. CKS / AWS Security Specialty are not held yet, so
  the page must not imply they are.
- **Held and unheld certifications never mix.** The `#credentials` section carries two lists:
  `.certs` (held, solid rules, amber year) and `.road` (in preparation, dashed rules, muted
  status, panel background, explicit "not yet held" label). Never move an entry up to `.certs`
  before it is actually earned, and never drop the disclaimer paragraph. The career strategy
  doc advises leading with the "Cloud Security Architect" title *now* — that advice is
  deliberately not followed here, because the page's value is that every claim survives checking.
- **The engagement section states terms, not credentials.** `#engagement` describes how work is
  scoped, how access is granted, and how it is handed over. It must not claim a legal entity,
  professional insurance, or invoicing capability that does not exist yet (see open items).
- **No client names.** All engagements are "withheld under NDA". Do not add employer or
  client names without explicit confirmation.
- **Every metric on the page is real.** 99.9% availability, −70% provisioning time, 50+
  clusters, +60% deploy frequency, −80% production vulnerabilities, 95% pre-prod
  remediation, −35% cost, 15+ certifications. Never invent or round up a new one.

## Design system

Derived from `#191970` (midnight blue), the colour already used across Yahia's LaTeX
resume. Amber phosphor `#FFB020` is the **only** accent — the sysadmin CRT colour and the
"needs attention" state in monitoring stacks. Do not introduce a second accent hue.

- **Light is the default theme.** Dark is a toggle. Both live in CSS custom properties on
  `:root` and `[data-theme="dark"]`. Add new colours as tokens in both blocks, never as
  hardcoded hex in a rule.
- `--amber` is for fills, dots and rules. `--amber-ink` is the *readable* amber for text and
  changes per theme (`#9E5D00` light, `#FFB020` dark). Use the right one or contrast breaks.
- The dark **left gutter rail** is the signature element — a drafting-sheet gutter holding
  the monogram, availability status, scroll-spy nav, theme toggle and a title block. It stays
  dark in both themes; it's the identity anchor. On <860px it collapses to a top bar.

### Typography — read this before touching headings

Display is **Schibsted Grotesk**, body **Instrument Sans**, data/labels **IBM Plex Mono**.

A previous version used Archivo at weight 900 with `-0.042em` tracking and the words
visually collapsed into each other. Heavy weights need *more* letter space, not less.
Current settings are deliberate:

- `h1` — weight 800, `letter-spacing: -.019em`, `word-spacing: .035em`, `line-height: 1.07`
- `h2` — weight 700, `letter-spacing: -.012em`, `line-height: 1.16`
- mono labels — `letter-spacing` between `.09em` and `.16em`. Above `.2em` it reads as
  spaced-out gibberish rather than a technical label.

Don't tighten tracking past these values or the same bug returns.

### Motion

Restrained. Hero staggers in once on load (`.lift` + `.d1`–`.d6`); sections fade up once via
IntersectionObserver (`.rise` → `.in`); the availability dot pulses. Everything is disabled
under `prefers-reduced-motion`. Keep it that way.

## Open items

- **GPU case study outcomes are placeholders** — "Scale / Cost / ISO" where every other case
  has hard numbers. Replace with real node counts, throughput or utilisation figures.
- **Certification name conflict.** LinkedIn's About section claims *AWS Solutions Architect
  Professional* and *OCI Solutions Architect Professional*; the resume says *AWS SA Associate*
  and *OCI Architect*. The page uses the conservative version. Confirm which is correct.
- **Theme choice does not persist** across reloads — it's in-memory only. Add
  `localStorage.getItem/setItem('theme', ...)` around `setTheme()` in the inline script.
- **Nearvic is not a registered entity — it is a domain only** (confirmed Jul 2026). The page
  therefore stays first-person throughout and makes no company claim. This is the single biggest
  commercial blocker: procurement at larger European and Gulf clients frequently cannot onboard an
  individual, only a supplier. Until an entity exists, `#engagement` offers contracting "through
  your existing contractor-management or employer-of-record provider" as the honest workaround.
  When a Moroccan auto-entrepreneur registration or SARL AU exists, add: company line in the
  contact block, invoicing currency, and professional liability insurance (RC Professionnelle) —
  each of those is a trust signal the page currently cannot make.
- **Certification roadmap entries need confirming.** The four entries in `.road` (CKS, AWS Security
  Specialty, AWS SA Professional, CCSP) were taken from the 2026–2028 career strategy document,
  not from Yahia directly. The strategy assumed a March 2026 start with CKS earned by June 2026;
  that has not happened. Confirm which are genuinely in progress versus planned, and consider
  adding target quarters, before treating this list as accurate.
- References are quoted from LinkedIn recommendations. Confirm permission before launch.

## Deployment

Static host, one file. Netlify, Cloudflare Pages, Vercel or GitHub Pages all work.
Target domain: **profile.nearvic.com**. Contact email: **yahia.benabbou@nearvic.com**.

Test both themes and the <860px breakpoint before shipping any visual change.
