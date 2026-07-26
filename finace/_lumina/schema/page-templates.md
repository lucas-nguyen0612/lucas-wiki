# Page Templates

Full YAML frontmatter templates and section structure for each wiki page type.
Managed by the Lumina installer. Open this file when README.md instructs.

---

## Source page — `wiki/sources/<slug>.md`

```yaml
---
type: source
title: "Full title here"
slug: source-slug
date_added: YYYY-MM-DD
authors:
  - Author Name
source_type: paper   # paper | article | book | podcast | note | other
importance: 3        # 1=niche  2=useful  3=field-standard  4=influential  5=seminal
confidence: high     # high | medium | low
tags: []
ranking:             # optional; written by /lumi-research-rank. Omit until the paper is ranked.
  # Flat map of scalars (one level only, like external_ids). Only include keys you have.
  influential_citations: 42   # Semantic Scholar influentialCitationCount
  citation_count: 318         # Semantic Scholar citationCount
  citation_source: semantic-scholar
  citation_fetched: YYYY-MM-DD
  venue_name: "NeurIPS"
  venue_tier: "CORE A*"       # free-form; agent-estimated, NOT authoritative
  venue_source: llm-estimated
  venue_estimated: YYYY-MM-DD
  scite_supporting: 12        # only when SCITE_API_KEY is set
  scite_contrasting: 1
  scite_mentioning: 64
  scite_fetched: YYYY-MM-DD
  altmetric_score: 287        # only when ALTMETRIC_API_KEY is set
  altmetric_fetched: YYYY-MM-DD
  quality_correctness: 4      # 4C rubric, 1-5 each (LLM-assessed)
  quality_clarity: 5
  quality_contribution: 4
  quality_context: 3
  quality_source: llm
  quality_assessed: YYYY-MM-DD
---
```

**Sections:**
- `## Summary` — 2–4 sentence abstract in your own words
- `## Key claims` — bulleted list of the source's central assertions
- `## Evidence` — notable data, experiments, or arguments supporting the claims
- `## Related concepts` — wikilinks to concept pages
- `## Related sources` — wikilinks to other source pages
- `## People` — wikilinks to person pages
- `## Open questions` — unanswered questions this source raises
- `## Ranking` — *(optional; managed by `/lumi-research-rank`)* human-readable influence signals and the 4C quality scorecard (Correctness, Clarity, Contribution, Context) with one-line rationales. Each figure states its source and date. The scorecard lives inside a managed region bounded by `<!-- lumina:ranking -->` and `<!-- /lumina:ranking -->`; only that region is rewritten on refresh. Free-text notes you add outside those markers (or inside `<!-- user-edited -->` markers) are preserved.
- `## Notes` — free-form notes (user-owned; mark with `<!-- user-edited -->` to preserve on upgrade)

---

## Concept page — `wiki/concepts/<slug>.md`

```yaml
---
type: concept
title: "Concept name"
slug: concept-slug
date_added: YYYY-MM-DD
confidence: high
tags: []
---
```

**Sections:**
- `## Definition` — one-paragraph plain-language definition
- `## Variants` — named variations with brief descriptions
- `## Key sources` — wikilinks to sources that introduce or use this concept
- `## Related concepts` — wikilinks
- `## Mentioned in` — summaries and outputs that reference this concept
- `## Notes`

---

## Person page — `wiki/people/<slug>.md`

```yaml
---
type: person
title: "Person Name"
slug: person-slug
date_added: YYYY-MM-DD
affiliation: ""
tags: []
---
```

**Sections:**
- `## Overview` — one paragraph on this person's relevance to the wiki
- `## Key sources` — sources authored by or featuring this person
- `## Key concepts` — concepts strongly associated with this person
- `## Notes`

---

## Summary page — `wiki/summary/<slug>.md`

```yaml
---
type: summary
title: "Area summary title"
slug: summary-slug
date_added: YYYY-MM-DD
confidence: medium
tags: []
---
```

**Sections:**
- `## Overview` — 3–5 sentences orienting a reader new to this area
- `## Key themes` — recurring patterns across sources in this area
- `## Sources covered` — wikilinks
- `## Key concepts` — wikilinks
- `## Open questions` — synthesis-level questions
- `## Notes`

---

## Reading note — `wiki/readings/<source-slug>/<nn>-<unit-slug>.md`

Written by `/lumi-ingest` for long sources (books, theses, 50+ page documents),
one note per chapter/part. The source page links to its notes through
`annotated_by` connections; notes are not listed in `wiki/index.md`.

```yaml
---
id: readings/<source-slug>/<nn>-<unit-slug>
title: "Part N: Title (pp. from–to)"
type: reading
created: YYYY-MM-DD
updated: YYYY-MM-DD
source: source-slug
part: N
pages: "from-to"     # optional; omit for sources without page numbers
---
```

**Sections:**
- Opening line (before any heading): `Part N of [[sources/<source-slug>]] (pp. from–to).` — the body wikilink keeps the note reachable and non-orphaned
- `## Question this unit answers` — the one question the chapter/part addresses
- `## Key terms` — terms the author defines or uses in a special sense, with page cites
- `## Propositions` — the unit's leading claims, each with a page cite
- `## Arguments` — premises → conclusion, page-cited
- `## Evidence` — data, examples, or experiments offered
- `## Quotes` — verbatim quotes only, each as `"exact words" (p. N)` — these are machine-checked against the source
- `## Tensions and links` — where this unit contradicts, extends, or depends on other units
- `## Open questions`
