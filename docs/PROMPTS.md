# Prompts

Copy-paste these. They cover everything the skill can do, roughly in the order you'd use them.

Nothing here is magic phrasing — plain language works. These just make sure you don't miss a feature
that exists.

---

## Getting started

**Install and set up**

> Set up the job search skill from https://github.com/Shiviansh/job-market-recon — read the README
> and SKILL.md, install it, and walk me through filling in my profile.

**Build a profile from a CV instead of typing it**

> Here's my resume. Read it and fill in config/profile.json from it — pull out my skills, projects
> and graduation year. Ask me about anything you can't tell from the CV, especially my pay floor and
> target locations. Be honest in known_gaps about what I'm missing.

**Two career directions, two profiles**

> I have two different resumes for two different fields. Set up a separate profile for each, and tag
> every role you find with which one fits it better.

---

## The market survey — do this first

**The main one**

> Run the market survey for my field before searching anything. Use each site's stipend filter to
> get the pay distribution, and tell me straight whether my pay floor is realistic or whether it
> eliminates my entire market.

**Sanity-check a number you're unsure of**

> I'm thinking of setting my floor at ₹20,000/month. Before I commit, show me what percentage of
> listings in my field actually clear that, and what I'd be giving up if I lowered it to ₹15,000.

**Compare two fields**

> Run the market survey for both machine learning and embedded systems, and put the pay
> distributions side by side. I want to see which field actually pays interns.

---

## Searching

**Full sweep**

> Run a full job search across all nine sites. Try at least three phrasings per site before deciding
> one is dry. Open every listing to check it's still live before you record it.

**Quick check**

> Just check Naukri and Glassdoor for anything new since the last run. Skip the rest.

**One site properly**

> Sweep only Glassdoor, but go deep — several pages, multiple query phrasings, and use the salary
> filter. Tell me the per-band counts.

**Deadline check**

> Look through my job pool and tell me anything with a deadline in the next 10 days, plus anything I
> logged over three weeks ago that I should probably follow up on or drop.

---

## Understanding what you got

**Explain a score**

> Why did you score the third one 62 and not higher? What specifically am I missing for it?

**The honest version**

> Of everything in my pool, which three would you actually apply to if you were me, and which are
> padding? Don't be diplomatic.

**Check your own work**

> Re-open the top five listings in my pool and confirm they're still live. Mark anything closed.

**Pattern check**

> Look across all the roles you've found. What skill comes up most often that I don't have? That's
> what I should learn next.

---

## Applications — it drafts, you send

**Draft, don't send**

> Draft an application email for the top role. Name my actual gaps for it honestly rather than
> hiding them. Don't send anything — show me first.

**Fill a form**

> Open this application form and fill in everything you can from my profile, then stop before submit
> so I can check it.

**Tailor without lying**

> Rewrite my resume summary for this specific JD. Only use things that are already true and on my
> CV — do not add a single skill I don't have.

---

## Running it on a schedule

**Set it up**

> Set up a scheduled job sweep every three days at a time I'm normally at my laptop, and email me
> the results. Draft only — never send applications.

**Two people, alternating**

> I'm running this for two people. Set up one sweep for each, on alternating days, and make sure
> each person's results only ever go to their own email.

**If a run seems to have been skipped**

> Did the scheduled sweep run today? If not, why — and run it now.

---

## Keeping it accurate

**Correct a site verdict**

> I searched Cutshort manually and found plenty of listings, but your yield ledger says it's dry.
> Re-check it properly — scroll the page, try different phrasings — and correct the ledger if you
> were wrong.

**Add a site**

> Add Instahyre to my site list. Work out which query shapes work, whether it needs a login, and
> record what breaks on it.

**Add your country**

> The site configs in this repo are India-only. Build me an equivalent for [country] — find the main
> job boards, test which queries work on each, and write a sites config in the same format.

---

## Getting the truth out of it

These matter more than the search prompts. The failure mode of any job tool is telling you what you
want to hear.

> Is my pay floor realistic for this field, or am I filtering out my entire market?

> Which of these am I actually underqualified for? I'd rather know now than after ten rejections.

> You've found 40 roles and I've applied to none. Is finding more the right next move, or should I
> stop searching and start applying?

> What's the strongest thing on my CV, and is it in the first three lines of my applications?

---

## What it won't do

Asking won't change these. They're in the skill deliberately.

- Submit applications or email employers without you approving each one
- Create accounts, solve CAPTCHAs, or log into job boards
- Invent a skill, a metric, an email address or a URL
- Hide a gap to make a role look like a better fit
- Bulk-extract from a site you're logged into — that's what gets accounts restricted
