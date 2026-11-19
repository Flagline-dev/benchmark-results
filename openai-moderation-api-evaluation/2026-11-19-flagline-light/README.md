# Flagline on the moderation validation set

Flagline Social standard v1 at level `light`, text only.

- **Endpoint:** `https://flagline.dev/v1/moderations`
- **Preset:** Social standard v1 (`bcd22897-1047-57ce-92d4-c884c54062f8`)
- **Level:** light
- **Backend model:** `decision-models/baseten-elephant-9b-latest`
- **Samples:** 1,680
- **Requests:** 1,680, zero failures
- **Wall clock:** about 9 minutes
- **Latency:** p50 0.798s, p95 4.486s,
  sum 3236.6s

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

Macro P **0.5183**, R
**0.7413**, F1
**0.5741**.

## Overall

| View | TP | TN | FP | FN | P | R | F1 | Acc |
|---|---|---|---|---|---|---|---|---|
| Flagline aligned union | 338 | 291 | 46 | 80 | 0.8802 | 0.8086 | 0.8429 | 0.8331 |
| Flagline API decision | 338 | 289 | 48 | 80 | 0.8756 | 0.8086 | 0.8408 | 0.8305 |

The aligned union uses the five dataset-mapped categories. The API decision
uses Flagline's own `flag` or `block` outcome, which can also be triggered by
spam.

## Thresholds

| Category | Light flag threshold |
|---|---:|
| sexual | 0.60 |
| hate | 0.50 |
| violence | 0.55 |
| harassment | 0.55 |
| self-harm | 0.45 |

Dataset labels map to categories: `S` and `S3` to sexual, `H` and `H2` to
hate, `V` and `V2` to violence, `HR` to harassment, `SH` to self-harm.

## Reading the numbers

- S sexual is strong: F1 **0.9150**.
- Self-harm is strong: F1 **0.8037**.
- S3 sexual/minors has high recall but low precision because Flagline's sexual
  category is broad and cannot isolate the minor-specific slice.
- H2 and V2 show the same effect: the parent category catches the content but
  also catches many non-subcategory items.
- HR harassment has low precision: many non-harassment items pass the broad
  harassment threshold.
- Missing labels are excluded, not treated as negative.

## Files

- [metrics.md](metrics.md) for confusion counts and overall tables.
- [items.md](items.md) for all 1,680 per-item rows.
- [comparison.md](../comparison.md) for the OpenAI side-by-side.
