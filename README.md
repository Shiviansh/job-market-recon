# Job Market Recon

A Claude skill that surveys **what a job market actually pays** before it looks for jobs in it, then
runs repeatable multi-site sweeps that verify every listing is live.

Built and tested on Indian tech internships. The site configs are India-specific; the method is not.

---

## Why this exists

Most job tools go straight to matching. That skips the question worth asking first.

Running a stipend survey across nine Indian job boards in August 2026 produced this:

| Category | Total listings | Unpaid | Clearing ₹25,000/month |
|---|---|---|---|
| Embedded systems internships | 120 | 107 (89%) | 2 |
| Robotics internships | 105 | 82 (78%) | 0 |
| VLSI internships | 13 | 12 (92%) | **0** |
| Machine learning internships | 644 | — | ~20% of a 50-listing sample |

A student setting a ₹25,000 floor for AI roles filters out the bottom fifth of their market. The same
student setting the same floor for VLSI eliminates *all* of it. Those need completely different
strategies, and no job board will tell you which situation you are in.

**Full findings: [docs/MARKET-REPORT-INDIA-2026.md](docs/MARKET-REPORT-INDIA-2026.md)**

---

## What it does

1. **Market survey.** Reads pay-band counts off each board's own stipend filter and reports the
   distribution for your field. Run it before you commit to a salary floor.
2. **Vocabulary probing.** Tries several phrasings per site before concluding anything, because
   boards match wildly differently — see below.
3. **Filter and score** against a profile you define, with hard rejections for batch year,
   experience ceiling, seniority and training-mill patterns.
4. **Verify every listing** by opening it before recording. A large fraction of board results are
   dead.
5. **Deduplicate** against a running pool so each digest contains only genuinely new roles.
6. **Keep a yield ledger** recording which sites produce, which queries worked, and — importantly —
   which of its own past verdicts turned out wrong.
7. **Digest** to file, and optionally by email to yourself.

---

## The lesson that cost the most to learn

**Judge a board by its best query, not its first.** Three boards were written off during development
and had to be reinstated.

| Board | Failed query | Returned | Working query | Returned |
|---|---|---|---|---|
| Naukri | "RTL design verification fresher" | dental designers, loan officers | "embedded systems internship" | 120 clean results |
| Prosple | "machine learning" | 0 | "AI" | 87 |
| Shine | "vlsi internship" | digital-marketing roles | "embedded systems" | real listings |

On several boards a common word — *internship*, *fresher* — dominates the match and swamps the
technical term. The skill now tries at least three phrasings per site and records which one worked.

---

## Setup

```
config/profile.template.json  →  copy to config/profile.json and fill in
config/sites.india.json       →  or write your own for another region
tracker/                      →  created on first run, gitignored
digests/                      →  created on first run, gitignored
```

Install `SKILL.md` into your Claude skills directory, fill in the profile, and ask Claude to run a
job search.

**`config/profile.json`, `tracker/` and `digests/` are gitignored.** They contain personal data.
Keep them that way.

---

## What it will not do

These are defaults, and deliberate:

- **No applying.** It drafts; you send. No form submissions, no emails to employers.
- **No account creation.** If a site demands a login, it reports that and moves on.
- **No CAPTCHA or bot-check circumvention.**
- **No bulk extraction against a logged-in account** — that is what gets accounts restricted.
- **No invented data.** Not an email address, not a metric, not a URL.
- **No inflated résumés.** Every recorded role states what you are *missing* for it. A tool that
  hides gaps wastes your applications and teaches you nothing.

It reads public listings at human pace. It is not a scraper and should not be run as one. Respect
each site's terms; you are responsible for how you use it.

---

## Adding your region

Copy `config/sites.india.json`, rewrite the entries, and open a PR. Each site entry records what it
is good for, what breaks on it, and which query shapes work — that accumulated per-site knowledge is
most of the value here, and it only grows if people contribute it.

The market survey is worth running anywhere. If you produce pay-distribution data for another field
or country, that would be worth sharing too.

---

## Honest limitations

- **Advertised listings only.** Campus placement, referrals and direct careers-page hiring are
  invisible to this, and for large employers that is most of their intake.
- **Board tagging is imperfect.** A category is only as good as what employers tagged into it.
- **Findings go stale.** The site notes and market data are from August 2026. Re-verify.
- **India-shaped.** The nine default sites and the ₹ figures assume India. The method transfers; the
  configs do not.
- **No company blacklists.** Training-mill *criteria* are shipped; company names are not. Pattern
  matching is not proof, and publishing accusations about named businesses is not something a tool
  should do on your behalf.

---

## Licence

MIT. Use it, fork it, rip out the parts you want.
