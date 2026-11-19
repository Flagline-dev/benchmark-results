# Metrics

Pooled and per-subset numbers for the 2026-11-19 Flagline `light` run.
Unsafe is the positive class; `flag` and `block` both count as Unsafe.

## Pooled

| n | TP | TN | FP | FN | Precision | Recall | F1 | Accuracy | Flag rate |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 3,443 | 457 | 2,320 | 130 | 536 | 0.7785 | 0.4602 | 0.5785 | 0.8066 | 17.0% |

## Confusion by subset

| Subset | TN | FN | FP | TP |
|---|---:|---:|---:|---:|
| [moderated](moderated.md) | 87 | 402 | 59 | 287 |
| [near-moderated](near-moderated.md) | 463 | 122 | 50 | 162 |
| [random](random.md) | 775 | 12 | 19 | 8 |
| [safe](safe.md) | 995 | 0 | 2 | 0 |

## Recall by annotated Bluesky category

A post can carry more than one category, so the totals exceed the number of
Unsafe posts.

| Code | Name | Hit | Total | Recall |
|---|---|---|---:|---:|---:|
| S1 | porn | 39 | 61 | 63.9% |
| S2 | sexual | 79 | 236 | 33.5% |
| S3 | sexual-figurative | 28 | 189 | 14.8% |
| S4 | self-harm | 27 | 86 | 31.4% |
| S5 | nudity | 17 | 97 | 17.5% |
| S6 | intolerant | 48 | 73 | 65.8% |
| S7 | graphic-media | 4 | 93 | 4.3% |
| S8 | rude | 176 | 205 | 85.9% |
| S9 | threat | 108 | 128 | 84.4% |

Categories S3 sexual-figurative, S5 nudity, and S7 graphic-media are
image-dependent and are the clearest casualties of the text-only run. S8 rude
and S9 threat are text-heavy and transfer well.

## Decisions by subset

| Subset | allow | flag | block | Top categories on flagged rows |
|---|---:|---:|---:|---|
| [moderated](moderated.md) | 489 | 318 | 28 | harassment 162, sexual 76, violence 45, hate 37, self-harm 23, spam 3 |
| [near-moderated](near-moderated.md) | 585 | 197 | 15 | harassment 105, sexual 46, violence 26, hate 19, self-harm 12, spam 4 |
| [random](random.md) | 787 | 27 | 0 | sexual 11, harassment 10, violence 2, hate 2, spam 2 |
| [safe](safe.md) | 995 | 2 | 0 | violence 1, sexual 1 |

## Media split

| Slice | Accuracy | n |
|---|---:|---:|
| Text only | 90.7% | 2,081 |
| With media | 65.3% | 1,362 |

Media means the post had an image or video. Flagline never saw it. A
text-bearing post can carry an irrelevant image, so this split is descriptive,
not a clean causal estimate.

## Latency

| p50 | p95 | p99 | Total request time |
|---:|---:|---:|---:|
| 1.029s | 1.524s | 2.856s | 3914.2s |

## Caveats

- Text only: images and video were never sent.
- Bluesky ground truth versus Flagline's six-category Social standard policy.
  Policy disagreement is not automatically a model error.
- `light` raises thresholds by 0.10 and does not escalate. Do not compare
  these numbers to a standard or heavy run.
- The API returned `decision-models/baseten-elephant-9b-latest`. The revision is not pinned in the response.
- Coverage is not random: deleted and media-only posts are absent.
