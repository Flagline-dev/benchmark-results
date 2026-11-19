# Flagline metrics

## Per-label

| Code | Category | Known | Pos | TP | TN | FP | FN | P | R | F1 | Acc |
|---|---|---|---|---|---|---|---|---|---|---|---|
| S | sexual | 984 | 237 | 210 | 735 | 12 | 27 | 0.946 | 0.886 | 0.915 | 0.960 |
| H | hate | 771 | 162 | 118 | 563 | 46 | 44 | 0.720 | 0.728 | 0.724 | 0.883 |
| V | violence | 1,450 | 94 | 61 | 1,325 | 31 | 33 | 0.663 | 0.649 | 0.656 | 0.956 |
| HR | harassment | 1,444 | 76 | 50 | 1,291 | 77 | 26 | 0.394 | 0.658 | 0.493 | 0.929 |
| SH | self-harm | 1,447 | 51 | 43 | 1,383 | 13 | 8 | 0.768 | 0.843 | 0.804 | 0.985 |
| S3 | sexual/minors | 994 | 85 | 77 | 756 | 153 | 8 | 0.335 | 0.906 | 0.489 | 0.838 |
| H2 | hate/threatening | 761 | 41 | 38 | 596 | 124 | 3 | 0.235 | 0.927 | 0.374 | 0.833 |
| V2 | violence/graphic | 1,447 | 24 | 8 | 1,339 | 84 | 16 | 0.087 | 0.333 | 0.138 | 0.931 |

## Overall

| View | TP | TN | FP | FN | P | R | F1 | Acc |
|---|---|---|---|---|---|---|---|---|
| Flagline aligned union | 338 | 291 | 46 | 80 | 0.8802 | 0.8086 | 0.8429 | 0.8331 |
| Flagline API decision | 338 | 289 | 48 | 80 | 0.8756 | 0.8086 | 0.8408 | 0.8305 |

## Confusion summary

The per-label table above carries TP, TN, FP, and FN for each known-label
subset. The overall table uses the 755 fully labeled rows.

## Latency

| p50 | p95 | Sum of request time |
|---:|---:|---:|
| 0.798s | 4.486s | 3236.6s |

## Notes

- A missing label is unknown, never negative.
- Flagline's six-category policy cannot distinguish S from S3, H from H2, or V
  from V2.
- Per-label predictions use the effective `light` flag thresholds.
