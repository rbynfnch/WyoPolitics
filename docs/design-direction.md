# Design Direction

> **DRAFT v0.1.** Records how the visual concepts (Nov 2026) map to the rules in `CLAUDE.md` and `docs/site-brief.md`. The brief wins any conflict.

## Keep from the concepts

- The overall feel: cream background, clean cards, serif headings, generous spacing.
- Name and tagline (pending owner confirmation): **Wyoming Politics**, "Follow the Record. Decide for Yourself."
- Bill "At a Glance" sidebar (all code-filled facts).
- Official source links on bill pages (bill text, fiscal note, committee minutes).
- Methodology layout with side navigation and the four-principle row.
- Newsletter page layout, with the form disabled until a vendor is approved.

## Change everywhere

| Concept | Change to | Why |
|---|---|---|
| Navy blue primary color | Near-black headings plus one muted ochre or sage accent | Brief: no red or blue |
| Photo heroes (mountains, cabins, capitol) | Plain text headers or a flat graphic | Brief: no stock photos |
| VOTE button, U.S. flag, bucking horse | Remove | No patriotic imagery or animal mascots. The bucking horse is also a trademarked state symbol |
| Header search box | Omit until Phase E (Pagefind), or a link to a search page | No JS without approval |
| Tabs on bill and legislator pages | One page with in-page anchor links | Works without JS and prints |
| "2h ago" timestamps | Absolute dates | Static site would go stale |
| Green checkmark bullets on bill effects | Fact / Explanation / Unknowns labels | Checks read as endorsement |
| Red/green YES/NO pills | Text plus a distinct shape icon, neutral color | No red, no color-only meaning |

## Out of scope (cut)

- Elections, State Budget, Government Structure, News, unemployment and other non-legislative items.
- "Top Story" (editorial pick). Use latest Tier 1 explainers by date.
- "Find your representative" by address (needs a third-party lookup). Use a district list.
- Statewide, County, and U.S. officials tabs.
- Party filter with colored dots.
- Legislator party-line percentage ring, "Key Issues", "Promises" (scores and editorial labels).
- "Key votes", "Key takeaways", "Explore by issue", "Your rep's vote" column.
- All campaign finance and "Follow the Money" content (CLAUDE.md rule 7).
- "Why it matters", "How it could affect you", and the lightbulb prediction callouts (rules 2 and 5).

## Missing from the concepts (required)

Fact / Explanation / Unknowns labels and section cites, ReviewLine, SourceList with Last checked, StaleBanner, CorrectionNote, VoteTable with voice-vote notes, "Why this bill got a full explainer", Tier 2 and Tier 3 layouts, `/bills/`, `/qualified/`, `/how-we-choose/`, `/corrections/`, `/request/`, 404, and the SAMPLE DATA banner.

## Open decisions

- Accent color: ochre or sage.
- Header: plain text or credited real photography.
- Legislator headshots: all or none; check wyoleg.gov photo licensing first.
- Final name, tagline, logo.
