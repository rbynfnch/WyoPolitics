# [Site Name]: Wyoming Government in Plain English

A nonpartisan information project that translates Wyoming legislative records into plain English. We explain what bills do, what they cost, how legislators voted, and what is unknown. We do not tell readers what to think. Reliability and neutrality matter more than speed or volume.

## Binding documents (read these before any content work)

- Editorial standard: @docs/methodology.md
- Which bills get which coverage: @docs/tier-criteria.md
- Page templates, writing rules, verifier checklist, output schema: @docs/explainer-template.md
- Settled decisions, adopted defaults, and open items: @docs/decisions.md

These documents are binding. If a task conflicts with them, stop and ask. Do not resolve the conflict yourself.

Before any work in `site/`, also read `docs/site-brief.md`, the website build brief. It is deliberately not imported here, so it only loads when needed.

## Hard rules (never break these)

1. **Code handles facts, the LLM handles language.** Bill numbers, sponsors, statuses, dates, vote counts, individual votes, and dollar figures come from official data and are inserted by code. A model never generates or "recalls" them.
2. **Every explanatory statement cites a bill section.** If a statement can't be matched to a source, delete it. Do not soften it or keep it.
3. **Nothing publishes without human approval.** The publish step must refuse any item missing a reviewer name, a review date, and a passing verifier result. Content reaches the live site only through a GitHub pull request that the human reviews and merges. Never push content directly to the main branch and never merge your own pull request. Enforce this in code and with branch protection, not just in these instructions.
4. **No editorial judgment in tiering.** Apply `tier-criteria.md` exactly. Do not promote, demote, or reorder bills. If a rule is ambiguous, flag it.
5. **No opinions.** No judgment words, predictions, motives, or recommendations in generated content, except inside attributed quotations.
6. **No invented sources or arguments.** If no public statement is found for one side, write the "no public statements found" line from the template. Never pad.
7. **No contributor-level campaign finance data.** Wyoming law (W.S. 22-2-113(c)) restricts commercial use of information copied from campaign reports, and this project may carry ads or sponsors. Do not ingest, store, or publish it until the human confirms legal clearance in writing.
8. **Never reproduce long passages from third-party sources.** Paraphrase and link. Quote only short phrases.
9. **Same treatment for everyone.** Any check, template, or rule applied to one legislator, party, or organization applies to all.

## How the system works

Pipeline, one module per stage under `src/`:

1. `ingest/`: pulls bill data from official or licensed sources on a schedule and detects changes. Code only, no LLM.
2. `triage/`: assigns tiers from the published criteria and writes a decision log. Code only.
3. `draft/`: LLM drafts Tier 2 and Tier 1 content as JSON matching the schema in the explainer template.
4. `verify/`: a separate LLM pass plus code checks every item against the verifier checklist. The verifier must be a different call from the drafter, with its own prompt.
5. `stale/`: detects amended or changed bills and flags published pages for update.
6. `newsletter/`: assembles the weekly brief from published items for human editing.
7. `publish/`: validates approved items, writes them as JSON into `content/` on a new git branch, and opens a pull request. Enforces rule 3. It never merges.

Data flows one way. Later stages read earlier stages' outputs and never rewrite them.

## Website and content contract

The public site is a **static site** generated from `content/`. **[CONFIRM]** Astro is the current choice. Hugo is the alternative.

- The pipeline and the site share only the JSON files in `content/`. The site never calls an LLM, an API, or a database at build or run time.
- JSON shapes are defined once as Pydantic models in `src/schemas/`, and exported as JSON Schema files into `schemas/`. The site build validates every file in `content/` against them and **fails the build** on any mismatch.
- Every published item must include: `bill_id`, `tier`, `rule_version`, `reviewed_by`, `reviewed_at`, `verifier_passed`, `last_checked`, and source links. Items missing any of these fail validation.
- `content/` is committed to git on purpose. The git history is the public audit trail for edits and corrections.
- Corrections: a substantive fix adds an entry to `content/corrections/` and a visible note on the page, per `docs/methodology.md`. Never silently rewrite a published fact.
- Newsletter sign-up, reader-request form, and site search use third-party services or small embeds. Don't add one without asking.
- The site contains no secrets and no tracking or ad code until the human approves the specific vendor.

## Repo layout

- `docs/`: binding documents (above)
- `src/`: pipeline modules (above), plus `src/schemas/` for the Pydantic models
- `schemas/`: exported JSON Schema files used to validate content
- `content/`: approved, published JSON. Committed to git. The only input to the site.
- `site/`: the static site source (templates, components, styles). No pipeline logic.
- `prompts/`: versioned prompt files for the drafter and verifier. Never inline prompts in code.
- `tests/fixtures/`: 2026 session bills, fiscal notes, and roll calls for testing
- `data/`: raw downloads and generated output. Gitignored.
- `logs/`: run logs. Gitignored.
- `config.toml`: model name, thresholds, data source settings

## Environment

- Runs on the owner's **Windows PC**, using **Git Bash**. Give commands in bash syntax with forward slashes. Avoid PowerShell-only commands. Use `pathlib` in Python so paths work on Windows.
- The repo is hosted on **GitHub**. Never commit `.env`, `data/`, `logs/`, or API keys. Check `.gitignore` before the first commit and before adding any new output folder.
- Pipeline stack: Python 3.11+, Pydantic for schemas and validating all LLM output, pytest for tests, SQLite for local storage. Manage dependencies with a lockfile and a virtual environment. Python is confirmed. Don't add other frameworks without asking.
- Site stack: Node with Astro **[CONFIRM]**, kept inside `site/` with its own lockfile.
- Secrets (API keys) live in `.env`, which is gitignored. Never print, log, or commit secrets.
- Commands **[FILL IN once the tooling exists]**:
  - Run tests: `pytest`
  - Run triage: `python -m src.triage`
  - Run the full weekly pipeline: `python -m src.run_weekly`
  - Validate content against schemas: `python -m src.validate_content`
  - Build the site: `cd site && npm run build`

## Data sources

- Primary: the Legislature's own site (wyoleg.gov) for bill text, amendments, digests, fiscal notes, and roll calls.
- Possible bulk sources: Open States and LegiScan **[verify licensing and terms before relying on either]**.
- Before writing any scraper, check the site's terms and robots.txt. Rate-limit requests, identify the bot, and cache responses.
- Roll calls are not recorded for every vote. Voice votes have no individual votes. Represent this accurately and never infer how an individual voted.

## Working style

- For any change touching more than one module, or any change to a prompt, schema, or tier rule, make a plan first and wait for approval.
- Write tests first for anything in `triage/`, `verify/`, and `publish/`. Tier logic needs a test per criterion and for the tie-breaker order.
- Test against `tests/fixtures/` before touching live data. Never test against production publishing.
- Keep prompts in `prompts/` with a version number. Log the prompt version, model, input hashes, and output for every LLM call so any published item can be audited.
- Model names, providers, and settings for each role (drafter, verifier, newsletter, cheap tasks) live in `config.toml`. Never hardcode a model name. Route all model calls through one small wrapper so a provider or model can be swapped by editing config. Log the exact model name with every call.
- Prefer small, boring, deterministic code. If something can be a function, don't make it an LLM call.
- When data looks wrong or a source format changes, stop and report. Do not guess or patch around it.
- Don't add dependencies, scrapers, or services without asking.

## What to do when unsure

First check `docs/decisions.md` and the other documents in `docs/`. Don't ask about anything already decided or covered by a default there.

Then sort the question:

- **Editorial, legal, safety, or accuracy questions** (what a bill does, tier rules, publish gate, campaign finance data, anything touching the hard rules): stop, say what is unclear, and ask. A wrong plain-English explanation of a bill does more harm than no explanation. When in doubt, leave it out and flag it for the human.
- **Implementation details** (file names, internal structure, library choices within the approved stack): pick the simplest reasonable option, proceed, and say what you chose in your summary.

When you do need answers, ask once. Give one numbered list, each item with your recommended default, and keep working on anything that doesn't depend on the answers. Record answers in `docs/decisions.md`.

## Changing these instructions

Add a rule here when the same mistake happens twice. Keep this file under about 200 lines, and move detail into `docs/` and import it with an @ reference.
