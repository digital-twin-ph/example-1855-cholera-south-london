# Snow's South London water supply study, 1854

A worked-example repository for [Fieldwork](https://github.com/digital-twin-ph/fieldwork).
It carries the figures from John Snow's comparison of two water companies, transcribed from
the 1855 publication, with their provenance and their limits.

**There is no map here, and there is a map in the book.** Snow's Map 2 shows "the boundaries of
the Registrar-General's districts on the south side of the Thames in London, and also the water
supply of those districts" — which is this study, drawn. What this repository carries is the
figures behind it. The 32 sub-districts below are the units that map was drawn on, so these rows
are mappable in principle; doing it needs 1851 registration sub-district boundaries from somewhere
else, under whatever terms that source carries.

The study's power is still not spatial. It is a contrast between populations whose houses were
intermingled street by street, and Snow says so: the companies' mains ran down the same roads, so
the boundary that matters is not one a map can draw.

## The figures

Table IX, the first seven weeks of the epidemic:

| | Number of houses | Deaths from cholera | Deaths in each 10,000 houses |
| --- | ---: | ---: | ---: |
| Southwark and Vauxhall Company | 40,046 | 1,263 | 315 |
| Lambeth Company | 26,107 | 98 | 37 |
| Rest of London | 256,423 | 1,422 | 59 |

### By sub-district

Table IX is three rows because it is a summary. Tables VIII and XII give the 32 sub-districts it
summarises, in `data/table-viii-sub-districts-seven-weeks.csv` and
`data/table-xii-sub-districts-1849-1854.csv`.

| Table | Columns | What it adds |
| --- | --- | --- |
| **VIII** | sub-district, population in 1851, deaths in the seven weeks to 26 August, whether the supply was partly computed | A **population** denominator, so a rate per 1,000 people is possible where Table IX offers only deaths per house |
| **XII** | sub-district, deaths in 1849, deaths in 1854, water supply | The **exposure** per unit, and the **same units measured twice** — Lambeth moved its intake upstream in 1852, so 1849 is before and 1854 is after |

Both tables carry the same 32 sub-districts in the same three groups — the first 12 supplied by
Southwark and Vauxhall only, the next 16 by both companies, the last 4 by Lambeth only — so they
join on `sub_district`. The group is a printed column in Table XII; in Table VIII it is the blank
lines between blocks and Snow's surrounding text, so it is recorded only in the file that prints
it.

The asterisked rows in Table VIII are Snow's: *"The sub-districts in which the supply is partly
founded on computation, are marked with an asterisk."* They are kept as `supply_partly_computed`
because a figure partly computed is not the same kind of number as one counted.

And the first four weeks, where Snow's own reading is that cholera was *"fourteen times as
fatal"* among Southwark and Vauxhall's customers:

| | Number of houses | Fatal attacks | Fatal attacks in each 10,000 houses |
| --- | ---: | ---: | ---: |
| Southwark and Vauxhall Company | 40,046 | 286 | 71 |
| Lambeth Company | 26,107 | 14 | 5 |

The per-10,000 columns are Snow's, not recomputed here, so this transcription can be checked
against the source rather than against arithmetic performed on its behalf.

### A 36-person error, and where it actually came from

Transcribing the 32 rows and adding them up: the deaths column summed to **1,514**, exactly the
printed total, and all six of Table XII's group totals came out exactly. The populations summed to
**486,900** against a printed **486,936** — 36 short.

Three independent sources settle it, and none of them blames Snow:

| Source | Lambeth Church (2nd), population 1851 |
| --- | ---: |
| Project Gutenberg e-text, Table VIII | 26,748 |
| Project Gutenberg e-text, Table VII (same column) | **26,784** |
| Coleman (2019), transcribed from the archive.org scan | **26,784** |
| Center for Spatial Data Science, `subdistricts` dataset | **26,784** |
| Required by the total printed at the foot of both tables | **26,784** |

So the slip is in the **e-text**, not in Snow's book. The figure here is 26,784, and the column now
sums to its printed total.

This is worth recording rather than quietly fixing, because the rule that produced the error was a
good one. "Transcribe as printed, never correct" is what keeps a transcription checkable — and
applied to a *digitisation* rather than to the book, it faithfully reproduced somebody else's typo.
The check that caught it was arithmetic the source itself supplies.

### The whole table, verified against two independent transcriptions

Every figure in `data/table-viii-sub-districts-seven-weeks.csv` has been compared, cell by cell,
with [Coleman's transcription](https://github.com/tscoleman/SnowCholera) (BSD-2-Clause, made from
a different scan) and with the Center for Spatial Data Science's `subdistricts` dataset:

- **224 of 224 cells** — 32 sub-districts across 7 columns — match the CSDS dataset exactly.
- All seven column totals match the totals Snow prints.

What that establishes is that three people reading the same 1855 table got the same numbers. It
does not establish that the numbers are right, because all three read Snow.

### One of the five printed rates does not follow from the columns beside it

Dividing the columns as printed:

| | Quotient per 10,000 houses | Snow printed |
| --- | ---: | ---: |
| Southwark and Vauxhall, seven weeks | 315.39 | 315 |
| Lambeth, seven weeks | 37.54 | 37 |
| Rest of London, seven weeks | 55.46 | **59** |
| Southwark and Vauxhall, four weeks | 71.42 | 71 |
| Lambeth, four weeks | 5.36 | 5 |

Four of the five are the quotient with the fraction dropped. Lambeth's 37.54 is the only one that
distinguishes the rules, and it was printed as 37, so the column reads as truncated rather than
rounded.

Rest of London is not reproduced under either rule. A rate of 59 per 10,000 houses from 1,422
deaths implies about 241,000 houses, not the 256,423 printed next to it. Which of the two cells is
wrong cannot be settled from this table, and this repository does not guess: both are transcribed
as printed, and the discrepancy is recorded here instead of being smoothed away.

This matters for what the figures are used for. 315 against 37 is the contrast Snow drew, and it
survives either reading -- the ratio is about 8.4 whether the rates are truncated or not. The Rest
of London row is a bystander in that comparison, which may be why its arithmetic went unchecked for
as long as the figure has been quoted. Anything computing from this file should divide the first two
columns and say so, not reproduce 59.

## Why this is a separate repository

Because a repository boundary is a licence boundary. Fieldwork is Apache-2.0 and cannot carry
data it may not transform; an example in its own repository carries its own terms and is
imported rather than shipped.

In this case the terms turned out to be none at all. The publication is from 1855 and is in the
public domain, and the figures are facts. The same numbers are available inside HistData (GPL)
and causaldata (MIT), and taking them from either would have adopted that digitisation's terms
for data that is otherwise unencumbered. Transcribing from the original inherits nothing, so
this repository can be used by a project under any licence. The transcription itself is CC0.

## The three dates, which do not agree

- **Deaths**: the first seven weeks of the 1854 epidemic (and separately the first four).
- **Houses**: a return made to Parliament covering **1 January to 31 December 1853**.
- **Population**: the census of **1851**, which is what Tables VII and VIII count people by.
- **Publication**: 1855.

So the sub-district tables disagree by three years rather than one: 1854 deaths over an 1851
population. Table XII is the exception and the reason it is worth having — 1849 deaths and 1854
deaths are two measurements of the same units, so a comparison between them does not depend on a
denominator at all.

A rate computed from these states an 1854 numerator over an 1853 denominator. That is a property
of the study, not a flaw in the transcription, and anything computing it should say so. Fieldwork's
`rate` widget refuses to compute at all unless `numeratorPeriod` and `denominatorVintage` are both
stated, and reports whether they agree — this is the data that machinery was written for.

## What this repository does not yet contain

A Fieldwork workflow bundle. The widget gap is closed — `rate` reads a long table as of its 0.2.0
release on 2026-10-24, so these rows no longer need geometry to be computed over — and what
remains is the workflow document itself. When it exists the bundle lands here as
`fieldwork-workflow-bundle.json.gz` and is loaded through Fieldwork's import.

**Boundaries for the 32 sub-districts.** Snow's Map 2 drew them; the plain-text source this
repository transcribes from carries an illustration placeholder and no coordinates. Mapping these
rows means 1851 registration sub-district boundaries from an external source, which would arrive
with its own licence — the situation this repository's separation exists to handle.

The manifest format by which Fieldwork would list example repositories is not defined yet; see
experiment 127 in the Fieldwork repository.

## Limits

Read `provenance.json`. The short version: a rate per 10,000 **houses** is not a rate per person,
"Rest of London" is not a control group, exposure was unascertained in a number of cases, and a
company-level rate is not an individual's risk.

Table VIII answers the first of those and not the rest: it gives a population, so a rate per 1,000
people is available for the 32 sub-districts. It does not make the sub-district an exposure. In
the middle 16, both companies supplied the same sub-district — that is the whole point of Snow's
design, and it means a sub-district-level rate there is a mixture of two exposures and not a
measure of either. The 12 and the 4 at the ends are the ones where the unit and the exposure
coincide.

Snow knew the limit and worked past it by going house to house, which is what Table IX counts and
why it is a different kind of evidence from Table VIII rather than a coarser version of it.

### Independently found, twice

Coleman's transcription carries its own arithmetic check against Table IX, and it flags exactly the
two cells flagged above:

```
#Lambeth Company,37.54,38,37,PROBLEM
#Rest of London,55.46,55,59,PROBLEM
```

Two people working from different scans, who had not seen each other's work, arrived at the same
two numbers and the same two problems. That is as close to confirmation as a transcription gets:
it rules out a reading error here and leaves the discrepancy in the source, where it belongs.
