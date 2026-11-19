# ModerationBench: Flagline light run

Text-only evaluation of Flagline's general-purpose moderation policy against
ModerationBench's Bluesky Safe/Unsafe labels.

- **Run date:** 2026-11-19
- **Code:** [Flagline-dev/moderation-bench](https://github.com/Flagline-dev/moderation-bench)
- **Upstream benchmark:** [ayanmaj92/moderation-bench](https://github.com/ayanmaj92/moderation-bench)
- **Preset:** Social standard v1 (`bcd22897-1047-57ce-92d4-c884c54062f8`)
- **Level:** light
- **Backend model returned by the API:** `decision-models/baseten-elephant-9b-latest`
- **Scored posts:** 3,443 text-bearing posts out of 3,988 seeds
- **Text only:** Flagline did not receive images or video

## Headline

| Subset | n | Precision | Recall | F1 | Accuracy | Flag rate |
|---|---:|---:|---:|---:|---:|---:|
| [moderated](moderated.md) | 835 | 0.8295 | 0.4165 | 0.5546 | 0.4479 | 41.4% |
| [near-moderated](near-moderated.md) | 797 | 0.7642 | 0.5704 | 0.6532 | 0.7842 | 26.6% |
| [random](random.md) | 814 | 0.2963 | 0.4000 | 0.3404 | 0.9619 | 3.3% |
| [safe](safe.md) | 997 | n/a | n/a | n/a | 0.9980 | 0.2% |
| **All** | **3,443** | **0.7785** | **0.4602** | **0.5785** | **0.8066** | **17.0%** |

`flag` and `block` both count as Unsafe. The `safe` subset has no Unsafe
ground-truth posts, so its precision and recall are undefined, not a
meaningful zero. The pooled row is not an average of the four subset rows.

Confusion counts across all subsets: **457 TP, 2,320 TN,
130 FP, 536 FN**. Pooled accuracy
**80.7%**, precision **0.7785**,
recall **0.4602**, F1 **0.5785**.

## What the run shows

- Text-heavy categories transfer: S8 rude **85.9%** recall and S9 threat
  **84.4%** recall. S6 intolerant is **65.8%**.
- Image-dependent categories collapse: S7 graphic-media **4.3%**, S3
  sexual-figurative **14.8%**, S5 nudity **17.5%**, S2 sexual **33.5%**.
  Flagline never saw the media. This is the largest limitation of the run.
- `light` is permissive: **43**
  of 3,443 decisions were `block`, and 40 of those
  43 were on Unsafe ground truth. Counting only `block` as Unsafe
  gives **4.0%** recall.
- Accuracy on text-only posts is **90.7%** across all
  subsets. On posts with media it is **65.3%**. A text-bearing
  post can carry an irrelevant image, so this is descriptive, not a clean
  causal estimate.
- Every request succeeded. There were no provider, API, or degraded responses.

## Coverage

| Subset | Seeds | Fetched | Missing | No text | Scored | Text only | With media |
|---|---:|---:|---:|---:|---:|---:|---:|
| moderated | 1,000 | 920 | 80 | 85 | 835 | 347 | 488 |
| near-moderated | 988 | 906 | 82 | 109 | 797 | 310 | 487 |
| random | 1,000 | 853 | 147 | 39 | 814 | 693 | 121 |
| safe | 1,000 | 997 | 3 | 0 | 997 | 731 | 266 |
| **All** | **3,988** | **3,676** | **312** | **233** | **3,443** | **2,081** | **1,362** |

Missing posts are posts Bluesky's public AppView no longer returns. No-text
posts are image- or video-only. The scored set covers **82.3%** of Unsafe
ground-truth posts and **88.1%** of Safe posts, so coverage is not random.

## Read the details

- [metrics.md](metrics.md) for pooled confusion, per-category recall, media
  split, decisions, and latency.
- [moderated.md](moderated.md), [near-moderated.md](near-moderated.md),
  [random.md](random.md), [safe.md](safe.md) for every scored post, including
  all mismatches.

## Method and caveats

- Flagline is text-only. Images and video were never sent. This is a deviation
  from the benchmark's vision-language design.
- The ground truth is Bluesky's policy and S0-S10 taxonomy. The run uses
  Flagline's six-category Social standard policy. A policy disagreement is not
  automatically a model error. The S-code shown in each row is a one-to-one
  diagnostic mapping; only S0 versus non-S0 feeds the binary label.
- `light` raises both thresholds by 0.10 and never escalates to the second
  model tier. Do not compare these numbers to a standard or heavy run.
- The deployed API returned `decision-models/baseten-elephant-9b-latest`. The model revision is not pinned in
  the response, so a later run may differ.
- Post bodies are not reproduced in this repository. Each row links to the
  public Bluesky post and includes its exact `at://` URI. Some linked posts
  contain harmful content; the labels are the benchmark's, not Flagline's.

## Rights

The benchmark data and labels come from
[ModerationBench](https://github.com/ayanmaj92/moderation-bench) and its cited
sources. The companion code fork is GPL-3.0. These result tables are provided
for evaluation and research use; see the upstream repository for dataset
rights and attribution.
