# What Indian tech internships actually pay

**A stipend survey across nine job boards, August 2026.**

Short version: if you are an ECE student looking for a VLSI internship in India, the entire
advertised market pays nothing. Not "pays badly" — of the thirteen VLSI internships listed on the
country's largest job board, twelve are unpaid and the thirteenth pays ₹10,000–20,000 a month.

Software and AI students are in a different economy on the same websites.

---

## How this was measured

Several Indian job boards expose a stipend filter that shows a **count per pay band before you
apply it**. That turns a job board into a survey instrument: open a category, read the bands, and
you have the pay distribution for that field.

- **Dates:** 24–28 August 2026
- **Boards:** Naukri, Internshala, Glassdoor India, Prosple, Weekday, Foundit, Cutshort, Hirist, Shine
- **Categories:** embedded systems, robotics, VLSI, machine learning, generative AI
- **Scope:** India, internships and 0–1 year roles
- **Method:** category page opened with no filter, band counts read off the filter panel

**Caveats, stated up front.** These are counts of *advertised* listings on public boards. They do
not include campus placement, referral hiring, or roles filled through a company's own careers page
— and for large semiconductor employers, that is most of their intake. A single board's category is
also only as good as its tagging. Treat these as the shape of the *advertised* market, which is what
a student browsing these sites actually encounters.

---

## The hardware numbers

**Naukri, 24–26 August 2026:**

| Category | Total listings | Unpaid | ₹10–20k | ₹20–30k | ₹30–40k | Clearing ₹25k |
|---|---|---|---|---|---|---|
| Embedded systems internships | 120 | **107 (89%)** | 8 | — | 2 | **2** |
| Robotics internships | 105 | **82 (78%)** | 10 | 3 | — | **0** |
| VLSI internships | 13 | **12 (92%)** | 1 | 0 | 0 | **0** |

**Internshala, same window:** the best-paying VLSI internship listed paid ₹4,000–5,000/month. The
robotics category had 22 listings, none above ₹25,000.

Two findings worth sitting with:

**Every ₹30,000+ robotics and embedded internship on Naukri belonged to a single employer.** Not a
sector, not a city — one company, advertising four roles. Remove that employer and the paid
advertised market for hardware internships in India is empty.

**The one VLSI internship found above ₹25,000 anywhere across all nine boards** did not come from
any board's VLSI category. It surfaced through a keyword search on Glassdoor — ₹35,000/month, in
Ahmedabad. Every listing inside the actual VLSI categories was unpaid.

---

## The software and AI numbers, for contrast

| Category | Source | Total | Clearing ₹25k |
|---|---|---|---|
| Machine learning internships | Naukri | 644 | not exhaustively sampled |
| Machine learning internships | Internshala | 50 sampled | 10 (20%) |
| Generative AI internships | Naukri | 75 | 8 in the ₹20–30k band, none above ₹30k |
| AI internships | Internshala | 50 sampled | 1 (2%) |

Same country, same websites, same week. An AI student sees 644 machine-learning internships on
Naukri; a VLSI student sees thirteen.

Note the split *within* AI too: the ML category is meaningfully better paid than the AI category, and
"generative AI" tops out lower than plain ML. Vocabulary changes the market you are looking at.

---

## What this means if you are the student

**Set your salary floor after the survey, not before.** A floor of ₹25,000 removes the bottom fifth
of the AI market. The same floor removes one hundred percent of the advertised VLSI market. Those
are different situations and they need different responses — the first is a filter, the second means
your strategy has to change.

**For hardware, the advertised board market is not where paid work is.** The routes that actually
pay:

1. **Formal corporate intern programmes** — the large semiconductor employers run structured
   intakes with real stipends, posted on their own career portals, not on job boards. They are
   seasonal, so calendar them.
2. **Government and research programmes** — national research fellowships, space and defence
   research internships, and university processor and robotics labs. Application windows are fixed
   and often months ahead of the placement.
3. **Well-funded deep-tech startups** — these post to their own applicant-tracking systems
   (Greenhouse, Lever, Ashby, Keka, Zoho Recruit), which is why board searches miss them. Search
   those ATS domains directly.

**For AI, the boards genuinely work.** There is enough advertised volume to work through listings
directly, and cold outreach is optional rather than necessary.

**Watch for training programmes wearing internship clothing.** Both the VLSI and AI spaces in India
have a dense population of organisations selling courses as internships. Recurring tells: a stipend
that is "performance-based" or reserved for "top interns", fully virtual cohorts with fixed start
dates, a certificate as the headline benefit, "with job placement" in the listing, or the words
*training*, *academy* or *institute* in the company's own description. Any fee, deposit or
registration charge is disqualifying on its own. So is any request for identity documents or bank
details before an offer.

---

## A methodological finding that surprised me

**Judge a job board by its best query, not its first.** Three separate boards were wrongly written
off during this survey and had to be reinstated.

| Board | Query that failed | What it returned | Query that worked | Result |
|---|---|---|---|---|
| Naukri | "RTL design verification fresher" | dental designers, loan officers, data entry | "embedded systems internship" | 120 clean results |
| Prosple | "machine learning" | 0 | "AI" | 87 |
| Shine | "vlsi internship" | digital-marketing internships | "embedded systems" | real listings |

The failure mode is consistent: on several boards a common word in the query — *internship*,
*fresher* — dominates the match and swamps the technical term. On others the site's taxonomy simply
does not contain the phrase you used.

Two further verdicts were wrong for a different reason: a board recorded as having "no hardware
category" in fact had 126 embedded listings, of which nineteen in twenty were 5–25 years'
experience. Another recorded as "dry" had 51 embedded and 31 robotics listings on a page that needed
scrolling before the results loaded.

**Also: a large share of what boards return is dead.** On one check, four of four sampled listings
from an aggregator were closed — one had shut nine months earlier, another had sat unchanged for
over two years. Open every listing before you spend effort on it.

---

## Reproduce this

The survey is about ten minutes per category. Open the category on a board with a stipend filter,
read the band counts off the filter panel without applying them, and write down the distribution.

The skill in this repository automates it, but the finding does not need automation — it needs
someone to look. Nobody had, which is why a market where 89% of advertised hardware internships pay
nothing was not common knowledge among the students applying to them.

If you run this for a field or region not covered here, the numbers would be worth sharing.

---

*Data collected August 2026. Job markets move; re-run before relying on these figures. Company names
are omitted deliberately — the point is the distribution, not any individual employer.*
