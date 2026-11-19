# ModerationBench: OpenAI omni-moderation run

Text-only evaluation of OpenAI's `omni-moderation-latest` against
ModerationBench's Bluesky Safe/Unsafe labels.

- **Run date:** 2026-11-19
- **Code:** [Flagline-dev/moderation-bench-openai](https://github.com/Flagline-dev/moderation-bench-openai)
- **Upstream benchmark:** [ayanmaj92/moderation-bench](https://github.com/ayanmaj92/moderation-bench)
- **Endpoint:** `POST https://api.openai.com/v1/moderations`
- **Model:** `omni-moderation-latest`
- **Scored posts:** 3,443 text-bearing posts out of 3,988 seeds
- **Text only:** no image or video was sent
- **Policy:** OpenAI's fixed 13-category taxonomy, no preset or level

## Headline

| Subset | n | Precision | Recall | F1 | Accuracy | Flag rate |
|---|---:|---:|---:|---:|---:|---:|
| [moderated](moderated.md) | 835 | 0.7985 | 0.4601 | 0.5838 | 0.4587 | 47.5% |
| [near-moderated](near-moderated.md) | 797 | 0.6439 | 0.5986 | 0.6204 | 0.7390 | 33.1% |
| [random](random.md) | 814 | 0.2000 | 0.4500 | 0.2769 | 0.9423 | 5.5% |
| [safe](safe.md) | 997 | n/a | n/a | n/a | 0.9840 | 1.6% |
| **All** | **3,443** | **0.6870** | **0.4995** | **0.5784** | **0.7900** | **21.0%** |

OpenAI's `flagged` is the provider's own binary decision. Unlike the Flagline
run, there is no separate `flag` and `block`: a flagged item is simply Unsafe
for this report. The `safe` subset has no Unsafe ground-truth posts, so its
precision and recall are undefined, not a meaningful zero.

Confusion counts across all subsets: **496 TP, 2,224
TN, 226 FP, 497 FN**. Pooled accuracy
**79.0%**, precision **0.6870**,
recall **0.4995**, F1 **0.5784**.

## What the run shows

- Text-heavy categories transfer: S8 rude **94.6%**,
  S9 threat **89.8%**, and S6 intolerant
  **80.8%** recall.
- Image-dependent categories still suffer without media: S3
  sexual-figurative **11.6%**, S5 nudity
  **11.3%**, and S2 sexual
  **27.1%**.
- S7 graphic-media recall is **44.1%**. The
  provider can flag text descriptions of graphic violence even without seeing
  an image.
- Accuracy on text-only posts is **88.8%** across all
  subsets. On posts with media it is **64.0%**.
- Every request succeeded. There were no provider, API, or invalid-response
  failures.

## Coverage

| Subset | Seeds | Fetched | Missing | No text | Scored | Text only | With media |
|---|---:|---:|---:|---:|---:|---:|---:|
| moderated | 1,000 | 920 | 80 | 85 | 835 | 347 | 488 |
| near-moderated | 988 | 906 | 82 | 109 | 797 | 310 | 487 |
| random | 1,000 | 853 | 147 | 39 | 814 | 693 | 121 |
| safe | 1,000 | 997 | 3 | 0 | 997 | 731 | 266 |
| **All** | **3,988** | **3,676** | **312** | **233** | **3,443** | **2,081** | **1,362** |

Missing posts are posts Bluesky's public AppView no longer returns. No-text
posts are image- or video-only. The scored set is identical to the Flagline
run's, so the two result sets compare the same items.

## Category mapping

| OpenAI category | Bluesky code |
|---|---|
| `sexual` | S2 |
| `sexual/minors` | S2 |
| `harassment` | S8 |
| `harassment/threatening` | S9 |
| `hate` | S6 |
| `hate/threatening` | S6 |
| `illicit` | S10 |
| `illicit/violent` | S10 |
| `self-harm` | S4 |
| `self-harm/intent` | S4 |
| `self-harm/instructions` | S4 |
| `violence` | S9 |
| `violence/graphic` | S7 |

Only S0 versus non-S0 feeds the binary report. The mapping is a diagnostic
convenience, not a claim that the taxonomies are equivalent.

## Read the details

- [metrics.md](metrics.md) for pooled confusion, per-category recall, decisions,
  media split, and latency.
- [comparison.md](../comparison.md) for the Flagline versus OpenAI comparison.
- [moderated.md](moderated.md), [near-moderated.md](near-moderated.md),
  [random.md](random.md), [safe.md](safe.md) for every scored post.

## Method and caveats

- Text only. OpenAI's omni model accepts images, but no image was sent. This
  keeps the comparison with the Flagline text-only run apples to apples.
- Policy mismatch. The ground truth is Bluesky's policy and taxonomy; OpenAI
  applies its own fixed categories. A disagreement is not automatically a model
  error.
- No custom policy or level. OpenAI's decision thresholds are opaque; this is a
  single fixed operating point.
- The API returned `omni-moderation-latest`. A later run may use a different revision.
- The endpoint is published as free, but it requires an API key and is subject
  to the account's rate limits.
- Coverage is not random: deleted and media-only posts are absent.
- Post bodies are not reproduced in this repository. Each row links to the
  public Bluesky post and includes its exact `at://` URI.

## Rights

The benchmark data and labels come from
[ModerationBench](https://github.com/ayanmaj92/moderation-bench) and its cited
sources. The companion code fork is GPL-3.0. These result tables are provided
for evaluation and research use.
