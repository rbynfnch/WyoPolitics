# Website Build Brief

> **DRAFT v0.1.** Read this before any work in `site/`. Also read `CLAUDE.md` and the three binding documents in `docs/`.
> Items marked **[CONFIRM]** or **[DECIDE]** need a human answer. Ask; don't guess.

## Goal

Build a fast, accessible, static website that turns approved JSON in `content/` into plain-English Wyoming legislative pages. The site presents; it never decides. All facts arrive pre-verified from the pipeline. The site's job is to display them clearly and identically for every bill and legislator.

## Ground rules

- **Static output only.** No server, database, or runtime API calls. The site never calls an LLM.
- **Content comes only from `content/`.** Never hardcode bills, votes, names, or figures in templates.
- **Validate before building.** The build validates every JSON file against `schemas/` and fails on any mismatch or missing required field. Never loosen a schema to make a build pass. Report the mismatch instead.
- **No invented content.** If a field is missing, render the template's "not available" wording or fail validation. Never fill gaps with placeholder facts.
- **Zero client JavaScript by default.** Core content must work without JS. Add JS only for progressive enhancement (search, table sorting), and ask first.
- **No tracking, ads, or third-party scripts** until the human approves the specific vendor.
- **Check current docs** for Astro APIs before using them. Don't rely on memory of older versions.
- **Ask before adding any dependency.** Proposed set, subject to approval in your plan: `astro`, a JSON Schema validator such as `ajv`, `@astrojs/sitemap`, `@astrojs/rss`, and `pagefind` for search.

## Sample data and safety

- Until the schemas and real content exist, develop against fixtures in `site/fixtures/`, selected with a `CONTENT_DIR` environment variable. Production builds use `content/`.
- Fixtures must use **fictional** bill numbers, legislators, and organizations (for example "Sample Legislator"). Every fixture file has `"sample": true`.
- When `sample` content is present, every page shows a prominent **SAMPLE DATA** banner. The production build **fails** if any content file has `sample: true`.

## Design principles

- **Neutral and plain.** The site must not look left or right. No red/blue party coloring, no party colors in any chart or table, no animal mascots, no stock photos, no flags or patriotic imagery.
- **Identical treatment.** Supporters and opponents sections use the same component and styles. Legislators of every party use the same layout. Party appears only as text where the data includes it.
- **Do not use color alone** to carry meaning. Pair every state (Yes/No, Fact/Explanation/Unknown) with a text label and a distinct icon or shape.
- **Readable first.** Large type, generous spacing, short lines (about 65 characters), clear headings, one column on mobile.
- **Palette:** warm neutral background, near-black text, one muted accent that is not red or blue (for example ochre or sage). Define all colors and spacing as CSS variables in one tokens file.
- **Type:** system fonts or one self-hosted font. No external font requests.
- **Accessibility:** WCAG 2.2 AA minimum. Semantic HTML, skip link, visible focus states, keyboard navigation, sufficient contrast, descriptive link text, accessible tables, honors reduced-motion and font-size preferences. Include print styles, since people print bills explainers.

## Content types and pages

All routes derive from content files. Slugs use lowercase bill IDs (for example `/bills/hb0042/`).

| Route | Purpose | Source |
|---|---|---|
| `/` | Home: latest Tier 1 explainers, week's counts (computed from content), link to the qualified list, newsletter placeholder | all content |
| `/bills/` | Every bill (Tier 3 listing). Filter by chamber, status, tier. Default sort: bill number | all bills |
| `/bills/[id]/` | Bill page. Layout depends on tier (see below) | one bill |
| `/legislators/` | Every legislator, alphabetical by last name | legislators |
| `/legislators/[id]/` | Recorded roll-call votes on explained bills. No scores, no "key votes" | legislator plus votes |
| `/qualified/` | Public "Qualified, not yet explained" list with the date each qualified | triage output |
| `/methodology/` | Rendered from `docs/methodology.md` | docs |
| `/how-we-choose/` | Rendered from `docs/tier-criteria.md` | docs |
| `/corrections/` | Public corrections log | `content/corrections/` |
| `/about/` | Who we are, funding, conflicts, contact | config plus docs |
| `/newsletter/` | Sign-up placeholder (disabled until a vendor is approved) | none |
| `/request/` | Reader-request form placeholder (disabled until approved) | none |
| `/feed.xml` | RSS of new Tier 1 and Tier 2 items | content |
| 404, `robots.txt`, sitemap | Standard | generated |

### Bill page layouts

- **Tier 3:** listing fields only (title, sponsors, status, last action, official links).
- **Tier 2:** the Tier 2 template from `docs/explainer-template.md`.
- **Tier 1:** the full template, including "Why this bill got a full explainer".

Render sections in the order the content specifies, using `argument_order` from the JSON for supporters and opponents. Never compute your own ordering. (The pipeline sets it: supporters first on even-numbered bills, opponents first on odd-numbered bills.)

### Required components

- **LabeledSection:** wraps content with a visible label (Fact, Explanation, Unknowns) plus icon. Used consistently everywhere.
- **Citation:** renders section cites like "Sec. 3" as links or anchors to the official bill text where a URL exists.
- **SourceList:** official links and "Last checked" date.
- **ReviewLine:** "Reviewed by [name] on [date]". Required on every explained page.
- **StaleBanner:** shown when content marks a bill as changed since last review.
- **CorrectionNote:** shown at the top of a page when a correction exists for it.
- **VoteTable:** one row per legislator. Columns: name, party (text), district, vote. Default sort alphabetical by last name. Vote shown as text plus icon. Notes when a stage was decided by voice vote and has no individual votes. No coloring by party.
- **ConflictDisclosure:** rendered only when content includes one, as a visible block directly under the page title.

## SEO and discoverability

- Unique `<title>` and meta description per page. Plain-English H1s.
- Canonical URLs, Open Graph tags, sitemap, RSS.
- Structured data (JSON-LD) where it fits, using only facts present in the content.
- Fast loads and good mobile layout are the main SEO strategy here.

## Build phases

Do these in order. **Stop after each phase with the build passing, summarize what you did, and wait for approval.** Start by writing a plan for Phase A and wait for approval before coding.

**Phase A: Foundation**
Astro project in `site/`, design tokens, base layout (header, footer, skip link, navigation), content loader, schema validation step, fixtures, SAMPLE DATA banner and production guard.

**Phase B: Bills**
Bill index and bill pages for all three tiers, with all required components.

**Phase C: Legislators and votes**
Legislator index and pages, VoteTable, voice-vote notes.

**Phase D: Static and trust pages**
Methodology, how-we-choose, corrections, about, qualified list, 404, placeholders for newsletter and request forms.

**Phase E: Discovery and quality**
Search (Pagefind), sitemap, RSS, metadata, JSON-LD, print styles, accessibility audit, link check.

## Acceptance checks per phase

- `npm run build` passes with fixtures. A deliberately broken fixture makes it fail with a clear message.
- A production-mode build fails when sample content is present.
- Pages work with JavaScript disabled.
- No hardcoded bills, legislators, or figures in templates.
- Supporter and opponent sections are visually identical.
- Manual keyboard-only pass of the main pages. Accessibility tool run once added, with results reported honestly.
- Summarize any decision you made that the human should review.

## Open decisions for the human

- **[CONFIRM]** Astro vs Hugo.
- **[DECIDE]** Site name, tagline, and logo direction.
- **[DECIDE]** Hosting (for example a static host connected to GitHub). Compare current free-tier limits before choosing.
- **[DECIDE]** Newsletter, form, and analytics vendors. Don't add any until approved.
- **[DECIDE]** Whether the home page shows counts only or also a short "this week" list.
