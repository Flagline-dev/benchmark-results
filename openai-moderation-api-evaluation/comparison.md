# Flagline vs OpenAI on the moderation validation set

Both systems scored the same 1,680 prompts. Per-label metrics use
only rows where that label is known; the overall table uses the
755 fully labeled rows.

## Per-label

| Code | Category | Pos | Flagline P | Flagline R | Flagline F1 | OpenAI P | OpenAI R | OpenAI F1 | Delta F1 |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| S | sexual | 237 | 0.946 | 0.886 | 0.915 | 0.935 | 0.785 | 0.853 | -0.062 |
| H | hate | 162 | 0.720 | 0.728 | 0.724 | 0.796 | 0.772 | 0.784 | +0.060 |
| V | violence | 94 | 0.663 | 0.649 | 0.656 | 0.344 | 0.947 | 0.504 | -0.152 |
| HR | harassment | 76 | 0.394 | 0.658 | 0.493 | 0.199 | 0.868 | 0.324 | -0.169 |
| SH | self-harm | 51 | 0.768 | 0.843 | 0.804 | 0.769 | 0.980 | 0.862 | +0.058 |
| S3 | sexual/minors | 85 | 0.335 | 0.906 | 0.489 | 0.724 | 0.741 | 0.733 | +0.244 |
| H2 | hate/threatening | 41 | 0.235 | 0.927 | 0.374 | 0.885 | 0.561 | 0.687 | +0.312 |
| V2 | violence/graphic | 24 | 0.087 | 0.333 | 0.138 | 0.636 | 0.292 | 0.400 | +0.262 |

Delta is OpenAI minus Flagline in F1 points. Positive values favor OpenAI.

Macro averages: Flagline P **0.5183**,
R **0.7413**, F1
**0.5741**. OpenAI P
**0.6610**, R
**0.7432**, F1
**0.6432**.

OpenAI wins the per-label macro because it can separate the subcategories:
S3 sexual/minors, H2 hate/threatening, and V2 violence/graphic. Flagline's
broad categories give it high recall but low precision on those three slices.
Flagline is stronger on S sexual, V violence, and HR harassment.

Treat H2 (41 positives) and V2 (24 positives) as low-support slices. A few
mistakes move those numbers substantially.

## Overall, fully labeled rows

| View | TP | TN | FP | FN | P | R | F1 | Acc |
|---|---|---|---|---|---|---|---|---|
| Flagline aligned union | 338 | 291 | 46 | 80 | 0.8802 | 0.8086 | 0.8429 | 0.8331 |
| OpenAI aligned union | 369 | 204 | 133 | 49 | 0.7351 | 0.8828 | 0.8022 | 0.7589 |
| Flagline API decision | 338 | 289 | 48 | 80 | 0.8756 | 0.8086 | 0.8408 | 0.8305 |
| OpenAI flagged | 369 | 203 | 134 | 49 | 0.7336 | 0.8828 | 0.8013 | 0.7576 |

On the "any unsafe" task, Flagline is more precise and has higher F1 and
accuracy; OpenAI has higher recall. The two views are not contradictory:
Flagline is conservative overall, while OpenAI is better at the per-label
taxonomy, especially the subcategories Flagline cannot represent.

## Method

- **Flagline:** Social standard v1 at `light`. A label is predicted when the
  mapped category score meets the effective light flag threshold. The overall
  union uses sexual, hate, violence, harassment, and self-harm; spam is
  excluded because the dataset has no spam label.
- **OpenAI:** `omni-moderation-latest`. The eight dataset-aligned category
  booleans are used directly. The overall union excludes `illicit` and the
  other OpenAI-only categories.
- **Overall rows:** only the 755 rows with all eight labels
  present. Missing labels are never treated as negative.
- **Text only:** the dataset has no media.

## Read the runs

- [Flagline 2026-11-19 light](2026-11-19-flagline-light/README.md)
- [OpenAI 2026-11-19](2026-11-19-openai/README.md)
