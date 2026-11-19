# Metrics

Pooled and per-subset numbers for the 2026-11-19 OpenAI `omni-moderation-latest` text-only
run. Unsafe is the positive class; `flagged` is OpenAI's binary decision.

## Pooled

| n | TP | TN | FP | FN | Precision | Recall | F1 | Accuracy | Flag rate |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 3,443 | 496 | 2,224 | 226 | 497 | 0.6870 | 0.4995 | 0.5784 | 0.7900 | 21.0% |

## Confusion by subset

| Subset | TN | FN | FP | TP |
|---|---:|---:|---:|---:|
| [moderated](moderated.md) | 66 | 372 | 80 | 317 |
| [near-moderated](near-moderated.md) | 419 | 114 | 94 | 170 |
| [random](random.md) | 758 | 11 | 36 | 9 |
| [safe](safe.md) | 981 | 0 | 16 | 0 |

## Recall by annotated Bluesky category

A post can carry more than one category, so the totals exceed the number of
Unsafe posts.

| Code | Name | Hit | Total | Recall |
|---|---|---|---:|---:|---:|
| S1 | porn | 37 | 61 | 60.7% |
| S2 | sexual | 64 | 236 | 27.1% |
| S3 | sexual-figurative | 22 | 189 | 11.6% |
| S4 | self-harm | 25 | 86 | 29.1% |
| S5 | nudity | 11 | 97 | 11.3% |
| S6 | intolerant | 59 | 73 | 80.8% |
| S7 | graphic-media | 41 | 93 | 44.1% |
| S8 | rude | 194 | 205 | 94.6% |
| S9 | threat | 115 | 128 | 89.8% |

Categories S3 sexual-figurative, S5 nudity, and S2 sexual are the weakest
without media. S7 graphic-media does better than the Flagline run because
OpenAI can flag graphic text descriptions even without the image. S8 rude and
S9 threat are text-heavy and transfer well.

## Decisions by subset

| Subset | not_flagged | flagged | Top OpenAI categories on flagged rows |
|---|---:|---:|---|
| [moderated](moderated.md) | 438 | 397 | harassment 228, violence 78, sexual 60, self-harm 13, self-harm/intent 5, hate 5, harassment/threatening 5, sexual/minors 1, self-harm/instructions 1, hate/threatening 1 |
| [near-moderated](near-moderated.md) | 533 | 264 | harassment 149, violence 56, sexual 37, self-harm 8, harassment/threatening 5, self-harm/intent 4, hate 2, sexual/minors 2, hate/threatening 1 |
| [random](random.md) | 769 | 45 | harassment 23, violence 14, sexual 5, harassment/threatening 1, illicit/violent 1, self-harm/intent 1 |
| [safe](safe.md) | 981 | 16 | violence 16 |

## Media split

| Slice | Accuracy | n |
|---|---:|---:|
| Text only | 88.8% | 2,081 |
| With media | 64.0% | 1,362 |

Media means the post had an image or video. OpenAI's API can accept images, but
this run sent text only. A text-bearing post can carry an irrelevant image, so
this split is descriptive, not a clean causal estimate.

## Latency

| p50 | p95 | p99 | Total request time |
|---:|---:|---:|---:|
| 0.794s | 3.735s | 7.596s | 5004.2s |

## Caveats

- Text only: no image or video was sent.
- Bluesky ground truth versus OpenAI's fixed 13-category taxonomy. Policy
  disagreement is not automatically a model error.
- OpenAI's decision thresholds are opaque; this is one fixed operating point.
- The API returned `omni-moderation-latest`. A later run may use a different revision.
- Coverage is not random: deleted and media-only posts are absent.
