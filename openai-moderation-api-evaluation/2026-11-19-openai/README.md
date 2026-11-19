# OpenAI on the moderation validation set

OpenAI `omni-moderation-latest`, text only.

- **Endpoint:** `https://api.openai.com/v1/moderations`
- **Model:** `omni-moderation-latest`
- **Samples:** 1,680
- **Requests:** 1,680; 20 were retried at a lower rate after the
  first pass exhausted retries. No failures remain.
- **Wall clock:** about 12 minutes plus a 31 second retry pass
- **Latency:** p50 0.784s, p95 4.541s,
  sum 2765.4s

## Per-label

| Code | Category | Known | Pos | TP | TN | FP | FN | P | R | F1 | Acc |
|---|---|---|---|---|---|---|---|---|---|---|---|
| S | sexual | 984 | 237 | 186 | 734 | 13 | 51 | 0.935 | 0.785 | 0.853 | 0.935 |
| H | hate | 771 | 162 | 125 | 577 | 32 | 37 | 0.796 | 0.772 | 0.784 | 0.911 |
| V | violence | 1,450 | 94 | 89 | 1,186 | 170 | 5 | 0.344 | 0.947 | 0.504 | 0.879 |
| HR | harassment | 1,444 | 76 | 66 | 1,102 | 266 | 10 | 0.199 | 0.868 | 0.324 | 0.809 |
| SH | self-harm | 1,447 | 51 | 50 | 1,381 | 15 | 1 | 0.769 | 0.980 | 0.862 | 0.989 |
| S3 | sexual/minors | 994 | 85 | 63 | 885 | 24 | 22 | 0.724 | 0.741 | 0.733 | 0.954 |
| H2 | hate/threatening | 761 | 41 | 23 | 717 | 3 | 18 | 0.885 | 0.561 | 0.687 | 0.972 |
| V2 | violence/graphic | 1,447 | 24 | 7 | 1,419 | 4 | 17 | 0.636 | 0.292 | 0.400 | 0.985 |

Macro P **0.6610**, R
**0.7432**, F1
**0.6432**.

## Overall

| View | TP | TN | FP | FN | P | R | F1 | Acc |
|---|---|---|---|---|---|---|---|---|
| OpenAI aligned union | 369 | 204 | 133 | 49 | 0.7351 | 0.8828 | 0.8022 | 0.7589 |
| OpenAI flagged | 369 | 203 | 134 | 49 | 0.7336 | 0.8828 | 0.8013 | 0.7576 |

The aligned union uses the eight dataset-matching category booleans. `flagged`
is OpenAI's own top-level decision and also includes categories the dataset
does not label, such as `illicit`.

## Reading the numbers

- S3 sexual/minors, H2 hate/threatening, and V2 violence/graphic are much
  stronger than in the Flagline run because OpenAI has those exact categories.
- S sexual, H hate, and SH self-harm are also strong.
- V violence has high recall but low precision: the category is broader than
  the dataset's "promotes or glorifies violence" definition.
- HR harassment has high recall but low precision for the same reason.
- V2 has only 24 positive examples; interpret the recall carefully.
- Missing labels are excluded, not treated as negative.

## Files

- [metrics.md](metrics.md) for confusion counts and overall tables.
- [items.md](items.md) for all 1,680 per-item rows.
- [comparison.md](../comparison.md) for the Flagline side-by-side.
