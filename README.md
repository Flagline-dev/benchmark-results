# Benchmark results

Published result sets from Flagline benchmark evaluations. Each benchmark has
its own directory, and each run inside it is kept as an immutable snapshot with
its configuration, metrics, and per-item tables.

| Benchmark | Latest run | n | Accuracy | Recall | F1 |
|---|---|---:|---:|---:|---:|
| [ModerationBench](moderation-bench/README.md) | [2026-11-19 light](moderation-bench/2026-11-19-light/README.md) | 3,443 | 80.7% | 46.0% | 57.9% |

## Layout

```text
README.md                         this index
CONTRIBUTING.md                   how to add a result set
<benchmark-slug>/
  README.md                       benchmark overview and run list
  <YYYY-MM-DD>-<variant>/
    README.md                     run configuration, coverage, headline
    metrics.md                    pooled and detailed metrics
    <subset>.md                   per-item tables, when the benchmark has subsets
```

The current tree contains one benchmark, ModerationBench. New benchmarks get
a new top-level directory; new runs of an existing benchmark go inside its
directory. See [CONTRIBUTING.md](CONTRIBUTING.md) before adding one.

## Content and rights

Result pages contain labels, scores, and links to public source posts. They do
not reproduce post bodies. Some linked posts contain harmful content; the
labels are the benchmark's, not Flagline's.

The benchmark data and labels come from the upstream benchmarks and their
cited sources. The companion code repositories state the relevant licenses.
Result tables are published for evaluation and research use.
