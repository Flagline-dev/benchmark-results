# Adding a result set

This repository holds multiple benchmark result sets. Keep each published run
self-contained so the root index stays a stable map.

## Directory convention

```text
<benchmark-slug>/
  README.md
  <YYYY-MM-DD>-<variant>/
    README.md
    metrics.md
    <subset>.md
```

- Use a short kebab-case benchmark slug, for example `moderation-bench`.
- Use a date plus a short variant, for example `2026-11-19-light`.
- Do not overwrite a published run. A rerun, a different level, or a different
  preset gets a new directory.
- If a benchmark has no subsets, `metrics.md` can carry the detailed tables and
  the run README can link to it directly.

## Required run details

The run `README.md` must state:

- benchmark name and upstream URL, including the upstream commit if the code
  is forked;
- the Flagline code commit or release used;
- preset ID and version, decision level, and the date;
- the backend model string returned by the API;
- how many items were scored and how coverage was reduced, if at all;
- a content note when the source corpus can contain harmful material.

The run `metrics.md` must state the positive class and whether `flag`, `block`,
or both count as Unsafe. Include the confusion counts, not only precision and
recall, so readers can recompute the numbers.

## Privacy and safety

- Do not include API keys, tokens, or request bodies.
- Do not reproduce source post bodies when a stable identifier and a link are
  enough. Link to the public source and include the exact identifier.
- Do not include personal data that is not already part of the public benchmark
  record.
- Keep per-item failure logs free of request text and credentials.

## Indexing

Add one row to the benchmark's `README.md` run table and one row to the root
`README.md` table. The root table points at the latest run; the benchmark table
lists every run.

## Checks

Before pushing:

- confirm every relative link resolves;
- confirm the reported metrics match the underlying tables;
- confirm no secret or post body is present;
- confirm the run directory is new rather than an overwrite.
