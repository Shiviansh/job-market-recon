# Method notes

What broke, what worked, and why the skill is shaped the way it is. Written from roughly a week of
live sweeps across nine Indian job boards and two very different candidate profiles.

---

## 1. Vocabulary is the dominant variable

This cost three wrong verdicts before the pattern was obvious.

Job boards do not match on meaning. They match on strings, and on several of them a common word in
the query swamps the technical term. Searching "vlsi internship" on one board returned
digital-marketing internships, because *internship* is the high-frequency token and *vlsi* is
nearly noise to its index. The same board returned real listings for "embedded systems".

Three corrections from the build:

- Naukri: "RTL design verification fresher" → dental designers, loan officers, medical billing.
  "embedded systems internship" → 120 relevant results. Same site, same day.
- Prosple: "machine learning" → 0 results. "AI" → 87. "machine learning intern" → 40.
- Prosple again: "embedded" → 2. "electronics" → 18.

**Rule adopted:** try at least three phrasings per site before recording any verdict, prefer the
two-word technical phrase, and log which query worked so the next run starts there rather than
rediscovering it.

## 2. Two verdicts were wrong for reasons that had nothing to do with vocabulary

Worth separating, because they need different fixes.

**"No hardware category at all."** False. The board had 126 embedded listings. What made it useless
was that nineteen of twenty page-one results wanted 5–25 years of experience. The right verdict was
"experienced-hire platform", not "no hardware".

**"Dry, roughly zero results."** False. The category pages were long SEO pages that render results
below the fold. The first screen was unrepresentative. Scrolling and extracting from the DOM found
51 embedded and 31 robotics listings.

**Rule adopted:** a verdict must state *why*, specifically. "Dry" is not a finding; "126 listings,
19 of 20 at 5+ years" is. Vague verdicts hide their own errors.

## 3. Verification is not optional

A large share of what boards return is dead. Measured examples:

- Four of four listings sampled from one aggregator were closed — one nine months prior, one
  unchanged for over two years, one wrong country, one filled.
- Two links pointed at pages the employer had already removed from its own careers index.
- One listing quoted a stipend while contradicting itself on eligibility, because it was a stale
  copy of an earlier hiring cycle.

**Rule adopted:** open every candidate URL before it enters the pool. Anything that 404s, says
closed, has vanished from the employer's own index, or contradicts itself is logged as rejected
rather than surfaced.

## 4. Boards are survey instruments, not just search engines

The most valuable output of the whole exercise came from *not* applying a filter.

Several boards show a count per pay band before you apply it. Reading those counts turns a category
page into a pay distribution for the field. That is how "89% of advertised embedded internships in
India are unpaid" and "the entire VLSI intern category has zero roles above ₹25,000" were
established — numbers that change a student's strategy far more than any individual listing.

**Rule adopted:** the market survey runs first, before matching, and again monthly.

## 5. State the uncomfortable result

When a user's pay floor eliminates their entire market, returning an empty list is a failure of
communication. They will conclude the tool is broken, or that they searched wrong.

**Rule adopted:** if the floor removes everything, say so explicitly, give the number, and name the
routes that do pay — rather than silently returning nothing.

## 6. Silence must be distinguishable from failure

On an unattended schedule, "no email arrived" is ambiguous between *nothing was found* and *the run
never happened*. Both occurred during the build; one was caused by editing a scheduled task after
its fire time had passed, which silently rolled it forward.

**Rule adopted:** send a digest on every run, including zero-result runs, naming which sites were
checked.

## 7. Small mechanical failures cost real time

- **CSV and commas.** Glassdoor URLs contain commas. Written unquoted into a CSV, the field splits
  and every link truncates silently. The links looked fine in the file and 404'd when opened.
- **URL slug encoding.** Glassdoor's slug form encodes the keyword's character offsets
  (`KO6,29`). Change the keyword without changing the numbers and the page 404s. Use the plain
  query-parameter form instead.
- **Script extraction gets blocked.** Several sites blocked DOM extraction but rendered fine
  visually. Falling back to screenshots recovered them; giving up would have produced another false
  "dry" verdict.

## 8. Honest gaps make the tool useful rather than dangerous

Every recorded role states what the candidate lacks for it. This is the difference between a
research assistant and a résumé-inflation machine. If a JD requires Kubernetes, UVM, or a published
paper and the candidate has none, that belongs in the note — so the human can decide whether the
stretch is worth taking, and so nothing false ends up in an application.

## 9. Ship criteria, not accusations

Both markets surveyed contained organisations selling courses as internships. The *patterns* are
documented in the skill because they generalise and they protect people.

Company names are deliberately absent. Pattern-matching from listing text is not proof, and a public
repository accusing named businesses of fraud is a liability its author does not need. Give people
the tells; let them judge.
