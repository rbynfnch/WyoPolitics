# Methodology

> **DRAFT v0.1. Not yet binding.** This becomes binding when the owner removes this notice.
> Items marked **[DECIDE]** need an owner decision. This page is published on the site at `/methodology/`, so it is written for readers.

## What we do

We translate Wyoming legislative records into plain English. For each bill we cover, we explain what it does, what it costs according to the official fiscal note, how legislators voted on recorded roll calls, and what is not known.

We do not tell you what to think about a bill. We do not endorse or oppose bills, candidates, parties, or organizations.

## What we don't do

- We don't predict whether a bill will pass or what it will do in practice beyond what its text and fiscal note say.
- We don't describe anyone's motives.
- We don't score, grade, or rank legislators.
- We don't pick "key votes."
- We don't publish campaign contributor data. (Wyoming law, W.S. 22-2-113(c), limits commercial use of information copied from campaign finance reports.)

## Three kinds of statements

Every explainer separates three kinds of statements. Each is labeled on the page.

| Label | Meaning | Where it comes from |
|---|---|---|
| **Fact** | Bill numbers, sponsors, status, dates, vote counts, individual votes, dollar figures. | Copied by software from official records. Never written or recalled by a person or an AI model. |
| **Explanation** | A plain-English description of what a section of the bill does. | Written from the bill text. Every explanation cites the bill section it describes (for example, "Sec. 3"). |
| **Unknowns** | Things the record does not answer. | Listed openly instead of guessed. |

If an explanation cannot be matched to a specific section of the bill, we delete it. We do not soften it or keep it.

## Sources

In order of preference:

1. The Wyoming Legislature's official website (wyoleg.gov): bill text, amendments, digests, fiscal notes, roll calls.
2. Official documents from state agencies cited in the bill or fiscal note.
3. Public statements by named people or organizations, used only in the supporters and opponents sections, always attributed and linked.

We link to every source. We quote only short phrases from other publications and paraphrase the rest.

### Votes

Not every vote in the Legislature is recorded. Voice votes have no record of how individual legislators voted. When a stage was decided by voice vote, we say so. We never infer how an individual voted.

## How we choose which bills to explain

Every bill gets a basic listing. Some get a short explainer (Tier 2) or a full explainer (Tier 1). The rules are published in full at [How We Choose](/how-we-choose/) and are applied by software, not by editors. Bills that qualify but have not been written up yet appear on the public [Qualified, not yet explained](/qualified/) list with the date they qualified.

## How explainers are made

1. Software downloads official records and detects changes.
2. Software assigns each bill a tier using the published rules.
3. An AI model drafts the plain-English explanation from the bill text.
4. A separate AI check, plus automated checks, compare every statement against the bill and our checklist. Anything without a matching bill section is removed.
5. **A named human reviewer reads and approves every item.** Nothing is published without a reviewer's name, a review date, and a passing check. Each page shows "Reviewed by [name] on [date]."

We disclose AI use because it is part of how this work gets done. Responsibility for what we publish belongs to the human reviewer and to us. Reviewers are named in full on every page they approve.

### Drafting and checking rules, in plain language

- The AI writes words, never facts. Numbers, names, dates, and votes are filled in by software from official records.
- Every explanation must point to the section of the bill it describes. If it can't, it is deleted.
- No opinion words, predictions, guesses about motives, or recommendations.
- The checking step is a separate AI call with its own instructions, plus automated tests. It can only delete statements, not rewrite them.
- Explainers are approved one at a time. Basic listings, which contain only official data, can be approved in a batch.

## Supporters and opponents

On full explainers we summarize public arguments for and against a bill.

- Arguments come only from public, attributable statements: testimony, press releases, op-eds, official letters. Each one is linked.
- Both sides use the same format, length limits, and design.
- The order of the two sides follows a fixed rule, not our judgment: supporters first for even-numbered bills, opponents first for odd-numbered bills.
- If we find no public statement for one side, we say: "We found no public statements [supporting/opposing] this bill as of [date]." We never invent an argument to fill the gap.

## Keeping pages current

Bills change. When a bill we've explained is amended or changes status, software flags the page. Until it is re-reviewed, the page shows a notice that the bill has changed since our last review. Every page shows a "Last checked" date.

## Corrections

We will make mistakes. When we do:

- **Substantive corrections** (a wrong fact, a wrong explanation, a missing or wrong citation) get a visible note at the top of the page saying what changed and when, and an entry in the public [corrections log](/corrections/).
- **Minor fixes** (typos, formatting, broken links) are made without a note.
- We never silently rewrite a published fact.
- The full edit history of every published page is public. Published content is automatically copied to a public repository, where every change is recorded. **[DECIDE] public repository link, once it exists.**

To report an error, email **[DECIDE] corrections address on the site's domain, once the name is chosen.**

## Same rules for everyone

Every check, template, and rule applies equally to every legislator, party, and organization. Party appears only as text, never as color.

## Funding and conflicts of interest

This project is run by Elevartemis, which funds its initial costs. An editorial firewall separates the project's content from Elevartemis's other work.

- We accept no grants, no government funding, and no money from candidates, campaigns, or political committees.
- There are no ads at launch.
- If ads or sponsors are added later, they will be clearly labeled, and sponsors will never see or approve content before it is published.

Any conflict of interest relevant to a specific bill is disclosed in a visible block directly under that bill page's title.

**[DECIDE]** Whether to disclose the owners' political donations.
