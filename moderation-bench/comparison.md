# Flagline vs OpenAI on ModerationBench

Both runs scored the same **3,443** text-bearing posts from
ModerationBench, with no images or video. The difference is the provider's
decision, not the input set.

- **Flagline:** Social standard v1, level `light`, `flag` and `block` combined
  as Unsafe.
- **OpenAI:** `omni-moderation-latest`, `flagged` as Unsafe.

## Pooled

| Provider | Model | n | Precision | Recall | F1 | Accuracy | Flag rate |
|---|---|---:|---:|---:|---:|---:|---:|
| Flagline | social-standard v1, light | 3,443 | 0.7785 | 0.4602 | 0.5785 | 0.8066 | 17.0% |
| OpenAI | omni-moderation-latest | 3,443 | 0.6870 | 0.4995 | 0.5784 | 0.7900 | 21.0% |

The pooled F1 scores are essentially tied, but the trade-off is different:
OpenAI catches more Unsafe posts (higher recall) and produces more false
positives (lower precision). Flagline at `light` is more conservative.

## By subset

| Subset | n | Flagline accuracy | OpenAI accuracy | Flagline recall | OpenAI recall | Flagline F1 | OpenAI F1 |
|---|---:|---:|---:|---:|---:|---:|---:|
| moderated | 835 | 0.4479 | 0.4587 | 0.4165 | 0.4601 | 0.5546 | 0.5838 |
| near-moderated | 797 | 0.7842 | 0.7390 | 0.5704 | 0.5986 | 0.6532 | 0.6204 |
| random | 814 | 0.9619 | 0.9423 | 0.4000 | 0.4500 | 0.3404 | 0.2769 |
| safe | 997 | 0.9980 | 0.9840 | n/a | n/a | n/a | n/a |

## Recall by annotated Bluesky category

| Code | Name | Flagline | OpenAI | Delta |
|---|---|---|---:|---:|---:|
| S1 | porn | 63.9% | 60.7% | -3.3 pp |
| S2 | sexual | 33.5% | 27.1% | -6.4 pp |
| S3 | sexual-figurative | 14.8% | 11.6% | -3.2 pp |
| S4 | self-harm | 31.4% | 29.1% | -2.3 pp |
| S5 | nudity | 17.5% | 11.3% | -6.2 pp |
| S6 | intolerant | 65.8% | 80.8% | +15.1 pp |
| S7 | graphic-media | 4.3% | 44.1% | +39.8 pp |
| S8 | rude | 85.9% | 94.6% | +8.8 pp |
| S9 | threat | 84.4% | 89.8% | +5.5 pp |

Delta is OpenAI minus Flagline in percentage points.

OpenAI is stronger on text-heavy S6 intolerant, S8 rude, and S9 threat.
Flagline is stronger on S2 sexual, S3 sexual-figurative, and S5 nudity. Both
are weak on image-dependent categories because neither saw the image. OpenAI's
S7 graphic-media recall is much higher because it can flag graphic text
descriptions.

## Media split

| Slice | n | Flagline | OpenAI |
|---|---:|---:|---:|
| Text only | 2,081 | 90.7% | 88.8% |
| With media | 1,362 | 65.3% | 64.0% |

Media means the post had an image or video. Both runs sent text only; this
split is descriptive, not a clean causal estimate.

## Agreement

| | OpenAI Unsafe | OpenAI Safe |
|---|---:|---:|
| Flagline Unsafe | 516 | 71 |
| Flagline Safe | 206 | 2,650 |

Agreement is **92.0%**; Cohen's kappa is **0.7394**. They agree
on most items but disagree on 277 of
3,443, mostly because OpenAI flags more items.

## Decision profiles

| Provider | Not Unsafe | Unsafe | Breakdown |
|---|---:|---:|---|
| Flagline | 2,856 | 587 | 544 flag, 43 block |
| OpenAI | 2,721 | 722 | 722 flagged |

A Flagline `flag` is a review signal, not a block. OpenAI's `flagged` is its
final unsafe classification. The two "Unsafe" columns are not the same kind of
decision even when the binary metric treats them the same way.

## Read the runs

- [Flagline 2026-11-19 light](2026-11-19-light/README.md)
- [OpenAI 2026-11-19](2026-11-19-openai/README.md)
