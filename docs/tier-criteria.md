# Tier Criteria

> **DRAFT v0.1. Not yet binding.** `rule_version: 0.1.0`. This becomes binding when the owner removes this notice.
> All thresholds marked **[DECIDE]** are placeholders. Final values live in `config.toml` and are echoed here.
> Published on the site at `/how-we-choose/`, so it is written for readers.

## Purpose

Decide, without editorial judgment, how much coverage each bill gets. Software applies these rules exactly, records which rule fired, and writes a decision log. Nobody promotes, demotes, or reorders a bill by hand. If a rule is ambiguous for a bill, the bill is flagged for the owner and the ambiguity is resolved by changing these rules (with a new `rule_version`), never case by case.

## Tiers

| Tier | Coverage |
|---|---|
| **Tier 3** | Listing only: title, sponsors, status, last action, official links. Every bill gets at least this. |
| **Tier 2** | Short explainer: what the bill does, with section citations, fiscal note figures, status and votes, unknowns. |
| **Tier 1** | Full explainer: everything in Tier 2, plus current law vs. change, supporters and opponents, amendment history, and why the bill got a full explainer. |

## Inputs

Rules may use only these fields, all taken from official records:

- bill type and number (HB, SF, HJ, SJ, and so on)
- status and history of actions, with dates
- fiscal note: whether one exists and the dollar figures it states
- roll-call vote counts at each stage
- number of adopted amendments

Reader requests are **not** a launch criterion. They may be revisited once a request form exists and safeguards against coordinated requests are designed.

Rules may **not** use: topic, sponsor, sponsor's party, media coverage, or anyone's opinion of the bill's importance.

## Tier 1 criteria

A bill is Tier 1 if **any** of these is true:

- **T1-A Enacted with major cost.** The bill became law and its fiscal note states a total impact of at least **$10,000,000** (placeholder) in any single fiscal year or biennium (absolute value, all funds).
- **T1-B Constitutional amendment.** A joint resolution proposing a constitutional amendment passed both chambers (and so goes to voters).
- **T1-C Close recorded vote.** A third-reading or final-passage roll call in either chamber passed with a margin (yes minus no) of **10% or less** (placeholder) of members voting (yes plus no). A percentage is used because the House has 62 members and the Senate 31. Voice votes never meet this rule.
- **T1-D Budget bill.** The general appropriations bill for the session.

## Tier 2 criteria

A bill that is not Tier 1 is Tier 2 if **any** of these is true:

- **T2-A Passed one chamber.** It passed third reading in at least one chamber.
- **T2-B Moderate cost.** Its fiscal note states a total impact of at least **$1,000,000** (placeholder) (absolute value, all funds), regardless of status.

## Fiscal notes without a single figure

If a fiscal note is missing, says the impact is "indeterminate", or gives only a range, the bill's fiscal figure counts as $0 for every rule here. The bill page states that the fiscal note gave no figure.

## Thresholds

The dollar and percentage thresholds above are placeholders. They will be tuned once by running these rules against the 2025 and 2026 sessions, then fixed under a new `rule_version`. Final values live in `config.toml`.

## Tier 3

Every other bill.

## Capacity and tie-breakers

If more bills qualify for a tier than reviewers can cover in a week (weekly capacity per tier is set in `config.toml` from measured review time, with a target of about 6 hours of human time a week), qualifying bills are taken in this order. Bills not reached stay on the public "Qualified, not yet explained" list with the date they qualified.

1. The rule that fired, in the order listed above (T1-A before T1-B, and so on). If several fired, the earliest-listed one counts.
2. Earlier qualification date first.
3. Larger absolute fiscal note figure first (no fiscal note counts as $0).
4. Bill type in this order: HB, SF, HJ, SJ, other. **[DECIDE] confirm Wyoming bill-type codes against wyoleg.gov data**
5. Lower bill number first.

## Changes in status

- Tiers are recalculated whenever a bill's data changes.
- A bill can move up a tier. It never moves down once an explainer has been published; the published content stays and is marked for update if the bill changed.
- Each decision log entry records: `bill_id`, tier, every rule that fired, `rule_version`, input data hash, and timestamp.

## Changing these rules

Any change bumps `rule_version` and is recorded in this file's history. Published items keep the `rule_version` they were tiered under.
