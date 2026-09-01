---
name: job-market-recon
description: Survey what a job market actually pays before applying to it, then run repeatable multi-site sweeps that verify every listing is live. Use when the user says find jobs, job search, internship search, what does this field pay, or job digest.
---

# Job Market Recon

Two jobs, in this order.

**First, survey the market.** Most job tools skip straight to matching. That is backwards. Before
anyone applies anywhere, they should know what the field actually pays and whether their salary
floor is realistic or silently eliminates their entire market. Boards expose this through their own
stipend and salary filters, and almost nobody reads it.

**Then, find and verify roles.** Sweep the configured sites, filter against a profile, and open
every candidate link before recording it — because a large share of what boards return is dead.

## Setup

1. Copy `config/profile.template.json` to `config/profile.json` and fill it in.
2. Pick a site config from `config/` (India ships by default; see `sites.india.json`).
3. Make sure `tracker/` and `digests/` directories exist. Create them if not.

On the first run, if `tracker/job_pool.csv` or `tracker/platform_yield.md` do not exist, create them
— the pool with a header row, the ledger empty. Do not treat their absence as an error.

`config/profile.json` and everything under `tracker/` and `digests/` are gitignored. Keep them that
way — they contain personal data.

**This skill needs browser or web-fetch access.** It opens job boards, reads their stipend filters
and verifies every link. If those tools are unavailable, say so and stop rather than producing a
digest from memory or guesswork.

---

## Phase 1 — Market survey

Run this on the first use, and again monthly. It is cheap and it changes strategy more than any
individual listing will.

For each of the user's target categories, on every site that exposes a pay filter:

1. Open the category with no pay filter. Record the total.
2. Read the pay-band filter counts without applying them — most boards show a count per band.
3. Record the full distribution: unpaid, and each band.

Then report it plainly:

```
EMBEDDED SYSTEMS INTERNSHIPS — {site}, {date}
Total: 120
Unpaid: 107 (89%)
₹10-20k: 8
₹30-40k: 2
Above your ₹25,000 floor: 2 of 120
```

**Say the uncomfortable thing.** If the user's floor eliminates 98% of their market, tell them
directly and name the alternative routes, rather than returning an empty list and letting them
conclude nothing exists. A floor that removes the bottom fifth of a market is a filter; a floor that
removes all of it is a strategy problem, and those need different responses.

---

## Phase 2 — The vocabulary probe

**Never judge a site on one query.** This is the single most important rule here, and it was learned
by getting it wrong repeatedly.

Real examples from the India build:

| Site | Bad query | Result | Better query | Result |
|---|---|---|---|---|
| Naukri | "RTL design verification fresher" | dental designers, loan officers, data entry | "embedded systems internship" | 120 clean results |
| Prosple | "machine learning" | 0 | "AI" | 87 |
| Prosple | "embedded" | 2 | "electronics" | 18 |
| Shine | "vlsi internship" | digital-marketing internships | "embedded systems" | real listings |

The failure mode: on some sites a common word in the query ("internship", "fresher") dominates the
match and swamps the technical term. On others, the site's taxonomy simply does not contain the
phrase you used.

**Rule: try at least three phrasings per site before recording a verdict.** Prefer the two-word
technical phrase. Record which query worked in the yield ledger so the next run starts there.

---

## Phase 3 — Filter and score

Apply the profile's hard filters first — these are rejections, not deductions:

- Graduation year or batch explicitly excludes the candidate
- Required experience exceeds the profile ceiling
- Seniority markers in the title: senior, staff, principal, lead, architect, head, VP, chief
- Work-rights or citizenship requirements the candidate cannot meet
- Anything matching the training-mill patterns below

Then score survivors on title match, core skill overlap, domain fit, seniority fit, location and
employer quality. Weight these in the profile, not in this file.

### Training-mill detection

Some markets are thick with organisations selling courses as internships. These are the recurring
tells. Two or more together means verify before engaging; do not name-and-shame publicly.

- A stipend that is "performance-based" or reserved for "top interns"
- Fully virtual cohorts with fixed start dates
- A certificate presented as the headline benefit
- "With job placement" or "placement guarantee" in the listing
- The words *training*, *academy*, *institute* or *upskilling* in the company's self-description
- Any fee, deposit, or registration charge — this alone is disqualifying
- Requests for identity documents or bank details before an offer

### Never paper over gaps

Every recorded role states what the candidate is missing. A tool that hides gaps produces
applications that waste everyone's time and teaches the user nothing. If a JD wants Kubernetes,
UVM, or a published paper and the candidate has none, that goes in the note.

---

## Phase 4 — Verify before recording

**Open every candidate URL before it enters the pool.** This is not optional and it is where most
job tools fail.

From real runs: one board returned four listings of which four were dead. One role had closed nine
months earlier. Another had sat unchanged for over two years. Two links pointed at pages the
employer had removed from its own careers index. One listing quoted a stipend while contradicting
itself on eligibility, because it was a stale copy of an earlier cycle.

Reject and log — do not surface — anything that 404s, says closed, has vanished from the employer's
own listing index, or contradicts itself.

---

## Phase 5 — Deduplicate and record

Match on (company, normalised role title) against `tracker/job_pool.csv`. Only genuinely new
listings reach the digest.

Record: tier, score, company, role, location, experience, pay, deadline, source platform,
verification date, an honest note naming gaps, and the URL.

**CSV note.** Some job-board URLs contain commas — Glassdoor's do. Wrap every URL field in double
quotes or the column splits and the link truncates silently.

---

## Phase 6 — The yield ledger

Maintain `tracker/platform_yield.md`. Every run, for every site, record: the query used, the volume
returned, how many were new and usable, and how that compares to the last run.

**Record your own wrong verdicts.** When a site was written off and later turns out to work, write
down what was misjudged and why. Real examples worth keeping in the file:

- "No hardware category at all" — wrong. The category existed with 126 listings; the problem was
  that 19 of 20 were 5-25 years' experience. Unusable, but for a different reason than recorded.
- "Dry, ~0 results" — wrong. The category pages were long SEO pages that needed scrolling and DOM
  extraction, not a first-screen read.

This ledger is what makes the skill improve rather than repeat itself. It is also the most useful
thing to hand a human who wants to search manually.

---

## Phase 7 — Digest

Write `digests/YYYY-MM-DD.md` and, if configured, email it.

Order: deadlines inside seven days first, then roles clearing the pay floor, then roles below it or
with pay unstated, then anything the training-mill filter caught, then per-site yield.

**Send a digest even when nothing was found**, naming the sites checked. On an unattended schedule,
silence is indistinguishable from failure.

---

## Boundaries

These are defaults. Loosening them is the user's decision, made explicitly.

- **Draft, do not send.** No applications, no emails to employers, no form submissions without
  per-item human approval.
- **No account creation.** If a site demands a login, report that and move on.
- **No bot-check or CAPTCHA circumvention.** Report the blocked site.
- **No bulk extraction against a logged-in account.** This is what gets accounts restricted. Keep
  logged-in sites to light, human-paced reading.
- **Never invent** an email address, a metric, a skill, or a URL.
- **Respect each site's terms.** This tool reads public listings at human pace. It is not a scraper
  and should not be run as one.
