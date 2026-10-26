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

**One file is an exception, and it is the one that makes the maps work.**
`geo/sub-districts-csds.geojson` carries the 32 sub-district polygons and is redistributed
unmodified under the **BSD 2-Clause Licence**, Copyright (c) 2019 Thomas Coleman. Everything else
here is CC0. The full licence text, the source and the boundary lineage are in `NOTICE.txt`.

That exception is the mechanism working, not a compromise of it. BSD-2 asks for attribution and
nothing more: it does not restrict who may receive a map made from these boundaries, which is
precisely what ruled out the alternatives below. A repository that carries its own terms can
accept a file like this; Fieldwork itself could not.

## The project

`fieldwork-project.json.gz` is a Fieldwork **project document**: an investigation and the
questions asked of it. Import it through Fieldwork's import control, or open it from the Worked
examples section of the Project tab. It carries its own data, so it runs offline with nothing
else fetched.

It lands as a project with five workflows rather than a loose canvas.

### Deaths per 1,000 people, by sub-district

Table VIII's counts over Table VIII's 1851 population — the thing Table IX cannot give you, whose
denominator is houses, and deaths per house is not a mortality rate. A `table_input`, a `rate`
reading it as a table, and a `table_output` that also carries the ranked chart.

The rate declares what it is a rate of, because Fieldwork refuses to compute one otherwise: the
numerator covers the seven weeks ending 26 August 1854, the denominator is the census of 1851, and
the two are three years apart. No rate is reported below a denominator of 1,000 people.

St. Olave (6.61), St. James Bermondsey (6.51) and St. Saviour (6.34) lead; Brixton (0.62), Putney
(0.19) and Dulwich (0.00) trail. The top four are Southwark and Vauxhall's alone.

### The ground: 32 sub-districts

The boundaries, as a study area of **33 parts** — 32 sub-districts, one of which (Streatham)
carries its Knight's Hill exclave — drawn on a map. 2,182 vertices as published, with each part
named, and BSD-2 attribution carried on the node rather than left in a file beside it.

Every part shares a border with another. Fieldwork refused that until 2026-10-24: a study area
would not hold units that touch, which is what administrative units tiling their ground always do.

### Cholera in 1849 compared with 1854

Table XII, both years, by sub-district — the before and after across Lambeth moving its intake
upstream in 1852.

**Counts, not rates, and deliberately.** A rate needs a denominator for each year and this
repository holds one population, the 1851 census. Using it for 1849 deaths would assert a frame
two years out and call the result a rate, which is exactly what the rate widget exists to refuse.
Snow compared the counts here; so does this.

### Deaths per 1,000 people, mapped

The first workflow's rates, put onto the second workflow's boundaries and shaded: the choropleth
this repository argued for in prose until 2026-10-25, when Fieldwork gained a widget that can join
a table to the named parts of a study area.

**A rate and not a count.** A count would mostly show where people lived, which is the map Snow
did not need; the denominator is what makes the figure an argument.

The join matches on the sub-district name, ignoring punctuation and spacing. That is not a
convenience: on the raw published strings only **23 of 32** match, because the table writes
`St. George, Camberwell` where the boundaries write `St. George  Camberwell`. After folding, all
32 match exactly, so nothing here needs a similarity threshold.

The figure draws **33 parts for 32 sub-districts** — Streatham is two polygons and both take its
rate, which is true of a rate and would not be true of a count. Five quantile classes, so each
holds about the same number of sub-districts and the shade shows rank rather than magnitude; the
breaks are printed on the figure and are values that occur in the data.

Dulwich sits in the lowest class at 0.00 and Putney at 0.19. Neither is a quiet place on this map
because cholera spared it; both are small, and a rate over a small denominator is unstable. The
figure does not say that, and a reader should.

### Deaths per house, by water company

Table IX, which is the comparison Snow's argument actually rests on: houses supplied by the
Southwark and Vauxhall Company against houses supplied by the Lambeth Company, in the same
streets, in the same weeks.

**Rate ratio 8.40**, with a 95% interval of **6.84 to 10.32**. The interval is a log-normal
approximation over the event counts, checked against an independent implementation
(`statsmodels`) in the validation lab — which found, on its first run, that this application had
been using a rounded 1.9600 for the normal quantile instead of 1.959963984540054.

**The table is the output, not the ratio.** A reader checks a summary against the counts it came
from, so the step emits the four cells — 1,263 deaths among 40,046 houses, 98 among 26,107 — and
carries the ratio alongside. The published `deaths_per_10000_houses` column is deliberately not
imported: it is Snow's own arithmetic, and a workflow that read his answer would be checking
nothing.

**Why the company is the exposure, which has to be said rather than assumed.** Being a Southwark
and Vauxhall customer is not what anybody thinks caused cholera. The exposure is **water drawn
from the reach of the Thames that received London's sewage**, and the company is a *proxy* for
it: by 1854 the two firms took their water from different places, Lambeth having moved its intake
upstream in 1852 to draw above the tidal reach, while Southwark and Vauxhall still drew from the
tidal river into which the city's sewers discharged. Snow's argument is about the water, and the
company is the label the data happens to carry.

The proxy is a good one for a reason that is also about the setting rather than the data: the two
companies' pipes ran **intermingled in the same streets**, so their customers were otherwise
alike — same neighbourhoods, same trades, same houses, often next door to one another. That is
what makes the comparison worth making, and it is not something any interval can tell you.

So the direction of this comparison encodes a hypothesis. Southwark and Vauxhall is the *compared*
group because it is the one believed exposed; Lambeth is the *reference* because it had moved
upstream. Reverse them and the arithmetic gives 0.12, the same finding stated backwards.

*What this repository does not record:* where exactly each intake stood. The move upstream in 1852
is in the table notes and in Snow's own account; the specific works are not in any file here, so
nothing above should be read as this repository's evidence for them.

**Per house, and that matters.** A house can have more than one death, so this is a rate and not
a risk: there is no "house without a death" to count, and the interval is Poisson rather than
binomial. It is also why this ratio (8.40) differs from the per-person one in the choropleth
workflow's supply groups (5.35) over the same outbreak — the denominators count different things,
and both are stated.

One assumption to meet before an audience does: a Poisson interval treats the events as
independent, and cholera is transmitted. Deaths that cluster are over-dispersed, so this interval
is narrower than the data warrants.

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

**A georeferenced plate, and the supply zones.** Those map layers in `geo/` are still for other
tools: nothing in Fieldwork reads them onto a canvas.

The boundaries are no longer in that position. Until 2026-10-25 this section also said that
`geo/sub-districts-csds.geojson` had no door into the application and that the 32 sub-districts
could not be joined to these figures. Both are now false — the boundaries land as a study area of
33 named parts, and `join_table_to_area` puts the rates onto them. The sentence is recorded here
rather than deleted because the gap it described is what the join was built to close.

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

## References

Every figure and every coordinate in this repository came from somewhere. This lists each source,
what it was used **for**, and its terms — including the sources that were examined and *not* used,
because the reason one was rejected is part of the evidence.

### The primary source

- **Snow, J. (1855).** *On the Mode of Communication of Cholera*, second edition. London: John
  Churchill. **Tables VII, VIII, IX and XII**, and **Map 2**.
  Public domain. Everything here is a transcription of, or a measurement taken from, this work.

### The digitisations transcribed from

- **Project Gutenberg eBook 72894**, produced from Google Books scans of the 1855 second edition.
  `https://www.gutenberg.org/ebooks/72894` ·
  text sha256 `8269bfd70fced302b136966707112d455169f2bdb4d5a40229c23c20ecb88669`
  *Used for:* every figure in `data/`. Note that the Table VIII population of Lambeth Church (2nd)
  is mistyped in this e-text; see above.
- **Project Gutenberg 72894, images edition**, `images/i_map2_large.jpg`, 5000 × 3934,
  sha256 `c5dd7255ddab6cebd960f13f9658a2dba6f7cb8397b3d03963c369d2886b985b`.
  *Used for:* the georeference in `geo/` and the supply zones traced from the colour washes.
- **Wellcome Collection L0063432**, the same plate at 6004 × 4896, CC-BY 4.0, via Wikimedia
  Commons. *Examined and not used for the tracing:* it is the higher-resolution scan, but its
  colours are closer to the aged paper and separate less cleanly than Gutenberg's, which appear to
  have been corrected. It remains the better scan for line work.

### Independent verification

- **Coleman, T. (2019).** *Causality in the Time of Cholera: John Snow as a Prototype for Causal
  Inference.* Working paper, SSRN `https://papers.ssrn.com/abstract=3262234`.
  Data: `https://github.com/tscoleman/SnowCholera`, **BSD-2-Clause**, transcribed from the
  Internet Archive scan `b28985266`.
  *Used for:* an independent check of Tables VIII and XII, and corroboration of the two Table IX
  discrepancies, which his own arithmetic check flags.
- **Coleman, T. (2020).** *John Snow, Cholera, and South London Reconsidered.* Working paper,
  SSRN `https://papers.ssrn.com/abstract=3696028`.
- **Falcone, M., Koschinsky, J., Vinten-Johansen, P., Coleman, T., and Anselin, L. (2023).**
  *John Snow & the Cholera Epidemic in Mid-19th Century London: 8 Datasets With Documentation for
  Use in GeoDa*, version 4, 9 March 2023. Center for Spatial Data Science, University of Chicago.
  Dataset 8, `subdistricts`. `https://geodacenter.github.io/data-and-lab/snow8/` · **BSD 2** as
  stated in its documentation.
  *Used for:* the cell-by-cell verification reported above — 224 of 224 — and as an independently
  georeferenced check on this repository's placement of Map 2.
  **Redistributed here** unmodified as `geo/sub-districts-csds.geojson`; see `NOTICE.txt`.

### Geography

- **Koch, T. and Denike, K. (2006).** *Rethinking John Snow's South London study: A Bayesian
  evaluation and recalculation.* Social Science and Medicine 63(1), 271–283.
  The sub-district boundaries in the CSDS dataset originate here, shared by the authors and
  modified by CSDS after georeferencing Map 2 in QGIS with about thirty control points. Koch and
  Denike's own terms are not stated in that documentation.
- **OpenStreetMap contributors**, via the Nominatim geocoder, ODbL.
  *Used for:* the four control-point coordinates in `geo/map2-georeference.json`. Four coordinates
  are not a substantial extract of that database, so no share-alike obligation is asserted; the
  attribution is recorded because the figures came from somewhere.

### Examined and not used

- **Satchell, M., Shaw-Taylor, L.M.W.S., Wrigley, E.A., Kitson, P.K. and Newton, G.H. (2023).**
  *1851 England and Wales census registration subdistricts.* UK Data Archive, SN 852945,
  DOI `10.5255/UKDA-SN-852945`. 3,316 polygons for all 2,182 registration sub-districts of England
  and Wales, derived from Kain and Oliver's parish maps.
  **The right units, and unusable here.** It is released under the UK Data Service End User
  Licence, whose clause 4 forbids giving access to the data *or to any dataset derived from it*
  except to registered users. That reaches a practitioner's own output: a map made by joining
  these figures to those boundaries could not be handed to a response team. The restriction is not
  about commercial use, and a non-commercial project does not escape it.
- **Great Britain Historical GIS Project.** *Great Britain Historical Database: Digital Boundaries
  for Registration Districts of England and Wales, 1851–1911.* UK Data Service SN 9032,
  CC-BY-SA 4.0, open.
  **Permissively licensed, and the wrong units.** It carries registration *districts*, not
  sub-districts. Aggregating the 32 sub-districts to those districts destroys the contrast the
  study is about: the Camberwell registration district alone contains sub-districts from all three
  of Snow's water-supply groups.
