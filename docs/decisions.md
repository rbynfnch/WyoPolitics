# Decisions Log

> **How to use this file.** Check it before asking the human any question.
> - Do not re-ask anything under **Decided** or **Defaults**.
> - **Defaults** are used unless the human objects. When you rely on one, mention it in your summary so the human can change it.
> - Anything not listed here: batch all your questions into **one numbered list**, each with your recommended default. Then continue with the parts of the work that don't depend on the answers.
> - Record every new decision here when the human makes it.

## Decided

- **Parent and structure:** The project is an Elevartemis project with its own brand and an editorial firewall. A separate nonprofit is a later question, not a launch question.
- **Pipeline stack:** Python 3.11+, Pydantic, pytest, SQLite. Developed in Git Bash on the owner's Windows PC.
- **Site:** Static site generated from approved JSON. Astro unless the human says otherwise.
- **Hosting of code:** GitHub.
- **Approval:** A human reviews every published item. Content goes live only through a pull request the human merges.
- **Batch approval:** The reviewer may approve Tier 3 listings in a batch. Tier 2 and Tier 1 items are approved individually.
- **Supporter/opponent order:** Supporters first on even-numbered bills, opponents first on odd-numbered bills. Update the methodology, explainer template, and site brief so all three match.
- **Campaign finance:** No contributor-level data until the human confirms legal clearance in writing (W.S. 22-2-113(c)).
- **Operating goal:** About 6 hours a week of human time once running. Be ready before the 2027 general session, which convenes January 12, 2027.

## Defaults (use unless the human objects)

1. **Close-vote rule:** Use a percentage of members voting, not a fixed number of votes, because the House has 62 members and the Senate 31. Placeholder: decided by 10% or less.
2. **Fiscal notes with no single figure** ("indeterminate", ranges, none): count as $0 for tiering. The page states that the fiscal note gave no figure.
3. **Reader requests:** Removed from launch criteria. Revisit once a request form exists and gaming safeguards are designed. Update `tier-criteria.md` so the "at least two criteria" rule matches the remaining criteria.
4. **Tier thresholds:** Placeholders stay ($10M for a major-cost enactment, $1M for moderate cost). Tune them by running the rules against the 2025 and 2026 sessions once ingestion exists. Set weekly capacity from measured review time. Current rough guess: 1 to 2 hours per Tier 1 item and 20 to 30 minutes per Tier 2 item. These are unmeasured.
5. **Reviewer names:** Full names shown on bill pages.
6. **Error reports:** A dedicated email address on the site's domain. No form vendor at launch.
7. **Repository visibility:** Private pipeline repo. `content/` is automatically mirrored to a separate public repo, which becomes the public audit trail. Update the wording in `CLAUDE.md` and `docs/methodology.md` to say so. Describe the drafting and checking rules in plain language in the methodology.
8. **Funding page text:** Initial costs are funded by Elevartemis. No grants, government funding, or money from candidates, campaigns, or political committees. No ads at launch. If ads or sponsors are added later, they are labeled and sponsors never see or approve content before it publishes.
9. **Conflict disclosure on bill pages:** A visible disclosure block directly under the title, per `docs/methodology.md` section 10.
10. **Models:** Names live in `config.toml`. Start with Claude models: a mid-tier model for drafting, a stronger separate model for verification. Add a second vendor for verification only if testing shows it catches errors the first misses.

## Still open (ask the human, batched)

- Site name, tagline, and logo direction.
- Hosting provider (compare current free-tier limits first).
- Newsletter, form, and analytics vendors.
- Astro versus Hugo, if the human wants to revisit it.
- Whether to disclose the owners' political donations.
- Any item previously marked "confirm against real data". It stays open until real bill data exists to check against.

## Rules that are not up for discussion

The nine hard rules in `CLAUDE.md` and the standards in `docs/methodology.md`. If a task seems to require breaking one, stop and ask. Do not treat these as defaults.
