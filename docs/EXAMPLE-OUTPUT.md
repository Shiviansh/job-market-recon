# What a run actually produces

Anonymised output from a real sweep, so you can see what you're setting up before you commit to it.
Company names are replaced; the structure, phrasing and honesty are unchanged.

---

## 1. Market survey — the first thing it does

You get this before any matching. It runs once at setup and again monthly.

```
MARKET SURVEY — embedded systems internships, India
Source: Naukri stipend filter, read without applying it

Total listings              120
  Unpaid                    107   (89%)
  ₹0–10k                      2
  ₹10–20k                     8
  ₹20–30k                     0
  ₹30–40k                     2

Clearing your ₹25,000 floor:  2 of 120

Cross-check — Internshala, same category: 44 listings, 1 above ₹25,000.

WHAT THIS MEANS FOR YOU
Your floor is not filtering this market, it is eliminating it. Both remaining
roles belong to the same employer. If you hold ₹25,000, your realistic routes
are corporate intern programmes, government and research schemes, and funded
startups posting to their own ATS — not job boards.

Compare: the machine learning category on the same site carries 644 listings,
and roughly 20% of a 50-listing sample clears the same floor.
```

That's the part that changes what you do. Everything below is ordinary job search.

---

## 2. The digest — every run after that

```
JOB DIGEST — 26 Aug 2026
9 sites swept · 12 new roles · 1 deadline inside 7 days

⚠ DEADLINE — TOMORROW, 27 Aug
   [Company A] — Robotics Software Engineer (ROS2) Intern — Gurugram
   ₹30,000/month · 0–2 yrs · 3 openings · 100+ applicants already
   Fit 88. The JD asks you to "integrate embedded firmware and hardware
   interfaces with higher-level robotic software" — that is the exact
   intersection of your two profiles, and most applicants can't claim it.
   Gap: none material. Apply today.
   → [link]

CLEARS YOUR PAY FLOOR (3)

1. [Company B] — VLSI / ASIC Design Intern — Ahmedabad — ₹35,000/month
   Fit 84. The only VLSI internship above your floor found on any of the nine
   sites. Notably it did NOT come from a VLSI category page — every one of
   those is unpaid. It surfaced through a keyword search.
   Gap: they list a Backend/Physical Design track. You have no PD, STA or
   place-and-route experience. Target the Frontend track only.
   → [link]

2. [Company C] — Embedded Software Intern — Bengaluru — pay not stated
   Fit 82. Processing-system side of AMD SoCs, writing low-level software that
   interfaces with custom hardware logic. Kept despite unstated pay because the
   employer is credible.
   Gap: JD mentions TCP and networking; not on your resume.
   → [link]

3. [Company D] — ROS Engineer — Noida — ₹4.5–8 LPA — 0–2 yrs
   Fit 78. Skill list is ROS, Git, Linux, Python, C++ — a direct match.
   Found on a site this tool had previously written off; see the yield note.
   → [link]

BELOW FLOOR OR PAY UNSTATED (2)

- [Company E] — Embedded Engineer Intern — Jaipur — ₹10,000–12,000
  Below floor, listed because it's in your city: zero relocation, could run
  alongside term time.
- [Company F] — Electronics & Embedded Intern — posted 24h ago — pay unstated
  Gaps: PCB design and soldering, neither on your resume.

SCREENED OUT (4)

- [Company G] — "live project internship with job placement", Pune ×3 listings
  → training-provider pattern
- [Company H] — performance-gated stipend, fully virtual, certificate as the
  headline benefit → verify before engaging

REJECTED AS DEAD (4)
Four listings from one aggregator were opened and found closed — one shut nine
months ago, one unchanged for over two years, one wrong country, one filled.

PER-SITE YIELD
  Site 1  6 of 12 new finds — best of the run
  Site 2  3 new
  Site 3  2 new
  Site 4  1 new
  Site 5  0 — 126 listings but 19 of 20 want 5–25 years
  Site 6  0 — counts inflated, fresher filter doesn't discriminate
  Site 7  0 — query pollution, see yield ledger
  Site 8  0 new
  Site 9  0 new
```

---

## 3. The yield ledger — how it gets better

`tracker/platform_yield.md` accumulates across runs. This is what a corrected
entry looks like, and it is the most useful file in the whole thing:

```
Site 5 — CORRECTION. "No hardware category at all" was wrong.
The category exists with 126 listings. What kills it is seniority: 19 of 20
page-one results want 5–25 years. Unusable, but for a different reason than
recorded. Detail pages also require a login.

Site 6 — CORRECTION. "Dry, ~0 results" was wrong.
Category pages are long SEO pages that render below the fold. The first screen
is unrepresentative. Scrolling and extracting from the DOM found 51 embedded
and 31 robotics listings. Produced one of this run's best finds.
```

Over a few runs this becomes a genuinely useful map of which boards deserve your
time — and it works whether or not you keep using the tool.

---

## 4. The pool — `tracker/job_pool.csv`

One row per role ever seen, so nothing resurfaces twice. Columns:

```
tier, score, company, role, location, experience, pay, deadline,
source_platform, verified_on, status, notes, url
```

The `notes` field always names what you're missing for that role. That is
deliberate — it's what stops this becoming a résumé-inflation machine.
