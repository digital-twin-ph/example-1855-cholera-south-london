# Snow's South London water supply study, 1854

A worked-example repository for [Fieldwork](https://github.com/digital-twin-ph/fieldwork).
It carries the figures from John Snow's comparison of two water companies, transcribed from
the 1855 publication, with their provenance and their limits.

**Nothing here is a map.** The study's power is not spatial: it is a contrast between two
populations whose houses were intermingled street by street. Mapping it would need 1850s
registration sub-district boundaries, which this repository does not have.

## The figures

Table IX, the first seven weeks of the epidemic:

| | Number of houses | Deaths from cholera | Deaths in each 10,000 houses |
| --- | ---: | ---: | ---: |
| Southwark and Vauxhall Company | 40,046 | 1,263 | 315 |
| Lambeth Company | 26,107 | 98 | 37 |
| Rest of London | 256,423 | 1,422 | 59 |

And the first four weeks, where Snow's own reading is that cholera was *"fourteen times as
fatal"* among Southwark and Vauxhall's customers:

| | Number of houses | Fatal attacks | Fatal attacks in each 10,000 houses |
| --- | ---: | ---: | ---: |
| Southwark and Vauxhall Company | 40,046 | 286 | 71 |
| Lambeth Company | 26,107 | 14 | 5 |

The per-10,000 columns are Snow's, not recomputed here, so this transcription can be checked
against the source rather than against arithmetic performed on its behalf.

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
- **Publication**: 1855.

A rate computed from these states an 1854 numerator over an 1853 denominator. That is a property
of the study, not a flaw in the transcription, and anything computing it should say so. Fieldwork's
`rate` widget refuses to compute at all unless `numeratorPeriod` and `denominatorVintage` are both
stated, and reports whether they agree — this is the data that machinery was written for.

## What this repository does not yet contain

A Fieldwork workflow bundle. `rate` currently requires a `points` input, and these are five rows
with no geometry to offer, so the computation cannot yet be expressed as a workflow. When that is
settled the bundle lands here as `fieldwork-workflow-bundle.json.gz` and is loaded through
Fieldwork's import.

The manifest format by which Fieldwork would list example repositories is not defined yet; see
experiment 127 in the Fieldwork repository.

## Limits

Read `provenance.json`. The short version: a rate per 10,000 **houses** is not a rate per person,
"Rest of London" is not a control group, exposure was unascertained in a number of cases, and a
company-level rate is not an individual's risk.
