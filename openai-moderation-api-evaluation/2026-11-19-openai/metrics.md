# OpenAI metrics

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

## Overall

| View | TP | TN | FP | FN | P | R | F1 | Acc |
|---|---|---|---|---|---|---|---|---|
| OpenAI aligned union | 369 | 204 | 133 | 49 | 0.7351 | 0.8828 | 0.8022 | 0.7589 |
| OpenAI flagged | 369 | 203 | 134 | 49 | 0.7336 | 0.8828 | 0.8013 | 0.7576 |

## Confusion summary

The per-label table above carries TP, TN, FP, and FN for each known-label
subset. The overall table uses the 755 fully labeled rows.

## Latency

| p50 | p95 | Sum of request time |
|---:|---:|---:|
| 0.784s | 4.541s | 2765.4s |

## Notes

- A missing label is unknown, never negative.
- The eight dataset-matching category booleans are used directly.
- The aligned union excludes OpenAI-only categories such as `illicit`.
