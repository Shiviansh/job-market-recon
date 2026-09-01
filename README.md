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
**See what a run produces: [docs/EXAMPLE-OUTPUT.md](docs/EXAMPLE-OUTPUT.md)**

---

## Requirements — read before setting up

**You need Claude with the ability to browse the web.** This works in:

- **Claude Code** (CLI)
- **Claude Cowork** (desktop app)
- Any Claude setup with a browser or web-fetch tool available

**It will not work by pasting `SKILL.md` into a normal claude.ai chat.** The skill opens job boards,
reads stipend filters and verifies links. Without browser access it has nothing to work with.

Also worth knowing before you start:

- **Setup takes about 15 minutes** — mostly filling in your profile honestly.
- **A full nine-site sweep takes a while** and is not cheap in tokens. Every listing gets opened and
  verified, which is the point, but it isn't instant.
- **It drafts; it does not apply.** No forms submitted, no emails to employers.
- **Nothing here is a database.** It reads live job boards. If a board changes its layout, the notes
  in `config/sites.india.json` may go stale — update them and open a PR.

---

## Install

### Easiest way — let Claude do it

Paste this into Claude Code or Cowork:

> Set up the job search skill from https://github.com/Shiviansh/job-market-recon — read the README
> and SKILL.md, install it, and walk me through filling in my profile.

Claude will read the repo, put the files where they belong, create the folders it needs, and ask you
the profile questions one at a time instead of leaving you to fill in a JSON file alone. This is the
recommended route unless you specifically want to do it by hand.

### By hand

**Claude Code**

```bash
mkdir -p ~/.claude/skills/job-market-recon
cp SKILL.md ~/.claude/skills/job-market-recon/
cp -r config ~/.claude/skills/job-market-recon/
```

**Claude Cowork (Windows)** — put `SKILL.md` and the `config` folder in your skills directory, then
restart the app. If you're unsure where that is, ask Claude "where do I install a skill?" inside the
app.

**Then, in the same folder you want to work in:**

```bash
mkdir -p tracker digests
```

Copy `config/profile.template.json` to `config/profile.json` and fill it in. The template has
comments explaining every field.

Then just ask Claude: **"run the market survey for my profile"** or **"run a job search."**

---

## First run

Do the **market survey** first, before any job searching. It takes about ten minutes and it may
change what you do next more than any individual listing will. It reads the pay-band counts on each
board's own stipend filter and reports the distribution for your field.

Then run a sweep. The first one will find a lot; later ones only surface what's new.

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

Two more verdicts were wrong for a different reason entirely: a board recorded as having "no hardware
category" had 126 embedded listings, of which 19 in 20 wanted 5–25 years' experience. Another
recorded as "dry" had 51 listings on a page that needed scrolling. Both corrections are in
[docs/METHOD.md](docs/METHOD.md).

---

## Files

```
SKILL.md                            the skill itself — install this
config/profile.template.json        copy to profile.json and fill in
config/sites.india.json             nine site adapters: what works, what breaks
docs/MARKET-REPORT-INDIA-2026.md    the stipend survey
docs/EXAMPLE-OUTPUT.md              what a run looks like
docs/METHOD.md                      what broke and why
```

`config/profile.json`, `tracker/` and `digests/` are gitignored. They contain personal data. Keep
them that way.

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

Copy `config/sites.india.json`, rewrite the entries, and open a PR. Each entry records what a site is
good for, what breaks on it, and which query shapes work — that accumulated per-site knowledge is
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
