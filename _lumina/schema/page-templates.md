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

## Topic page — `wiki/topics/<slug>.md` (research pack)

Created via `/lumi-research-topic`.

```yaml
---
type: topic
title: "Topic name"
slug: topic-slug
date_added: YYYY-MM-DD
tags: []
---
```

**Sections:**
- `## Description`
- `## Key sources`
- `## Key concepts`
- `## Open questions`

---

## Foundation page — `wiki/foundations/<slug>.md` (research pack)

Terminal pages — receive inward links but do not write reverse links.

```yaml
---
type: foundation
title: "Foundation concept"
slug: foundation-slug
date_added: YYYY-MM-DD
tags: []
aliases: []
---
```

**Sections:**
- `## Definition`
- `## Background`
- `## Notes`

---

## Reflection page — `wiki/reflections/<slug>.md` (learning pack)

Created and updated via `/lumi-learning-reflect`. AI never writes reflection content.

```yaml
---
id: reflection-<slug>
title: "My understanding of <Concept Name>"
type: reflection
created: YYYY-MM-DD
updated: YYYY-MM-DD
related_concepts:
  - concept-slug
related_sources:
  - source-slug
evolution_count: 1
---
```

**Sections:**
- `## Current understanding` — **rewritable**: the user's latest thinking in their own words; AI may quote past versions to prompt reflection but never edits this section
- `## Evolution` — **append-only**: one dated entry per reflection session; never edit or delete entries

**Evolution entry format:**
```markdown
### YYYY-MM-DD — <brief label>
<What you wrote or changed in this session (1–3 sentences)>
```

**Boundary rule:** Reflection pages are **personal overlay** — they reference academic pages via frontmatter only (no wikilinks that create graph edges). Do not write `[[concept-slug]]` inline body links; reference concepts only in `related_concepts:` frontmatter. No reverse link is required from concept/source pages back to reflections.
