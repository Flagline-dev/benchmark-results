# Flagline vs OpenAI on Message Moderation Eval

Both systems scored their own provider rows from the same compact workload.
Strict metrics use positive and negative rows only.

## Native summary

| Provider | Strict rows | Slices | Micro P | Micro R | Micro F1 | Micro Acc | Macro F1 |
|---|---|---|---|---|---|---|---|
| Flagline, light | 4,615 | 39 | 0.9973 | 0.8791 | 0.9345 | 0.9434 | 0.9163 |
| OpenAI, omni-moderation | 1,538 | 13 | 1.0000 | 0.7617 | 0.8647 | 0.8908 | 0.8180 |

Macro F1 uses only slices with positive support: 33 for Flagline, 11 for
OpenAI. Proxy-only slices are excluded from macro F1.

## General-purpose comparison

Flagline `social-standard` versus OpenAI on the five shared unified categories.
The rows are different, so this compares category concepts, not paired items.

| Unified | Flagline pos / n | Flagline P | Flagline R | Flagline F1 | OpenAI pos / n | OpenAI P | OpenAI R | OpenAI F1 |
|---|---|---|---|---|---|---|---|---|
| harassment | 65 / 129 | 1.000 | 0.785 | 0.879 | 65 / 129 | 1.000 | 0.754 | 0.860 |
| hate | 64 / 128 | 1.000 | 1.000 | 1.000 | 64 / 128 | 1.000 | 0.781 | 0.877 |
| self_harm | 65 / 129 | 1.000 | 1.000 | 1.000 | 64 / 128 | 1.000 | 1.000 | 1.000 |
| sexual | 64 / 129 | 1.000 | 1.000 | 1.000 | 64 / 128 | n/a | 0.000 | 0.000 |
| violence | 64 / 128 | 1.000 | 0.812 | 0.897 | 64 / 128 | 1.000 | 1.000 | 1.000 |

## All-preset comparison

Flagline rows from all seven presets, aggregated by unified category, versus
OpenAI on the same shared categories. This mixes presets with different
policies; use the per-preset tables for policy context.

| Unified | Flagline pos / n | Flagline P | Flagline R | Flagline F1 | OpenAI pos / n | OpenAI P | OpenAI R | OpenAI F1 |
|---|---|---|---|---|---|---|---|---|
| harassment | 322 / 642 | 1.000 | 0.957 | 0.978 | 65 / 129 | 1.000 | 0.754 | 0.860 |
| hate | 192 / 384 | 1.000 | 0.995 | 0.997 | 64 / 128 | 1.000 | 0.781 | 0.877 |
| self_harm | 193 / 385 | 1.000 | 1.000 | 1.000 | 64 / 128 | 1.000 | 1.000 | 1.000 |
| sexual | 192 / 385 | 1.000 | 1.000 | 1.000 | 64 / 128 | n/a | 0.000 | 0.000 |
| violence | 129 / 258 | 1.000 | 0.891 | 0.943 | 64 / 128 | 1.000 | 1.000 | 1.000 |

## Band behavior

| Provider | Positive flag rate | Negative flag rate | Borderline flag rate | Proxy flag rate |
|---|---:|---:|---:|---:|
| Flagline | 87.9% | 0.2% | 7.6% | 93.0% |
| OpenAI | 76.2% | 0.0% | 0.5% | 15.6% |

Positive flag rate is recall; negative flag rate is the false-positive rate.
Borderline and proxy rows are not ground-truth positives and are not part of
strict precision or recall.

## Highlights

- Native strict micro F1 is **0.9345** for Flagline and
  **0.8647** for OpenAI. Macro F1 is
  **0.9163** for Flagline over 33 slices
  and **0.8180** for OpenAI over 11
  slices.
- Precision is **0.9973** for Flagline with
  5 false positives on 2,498
  negative rows. OpenAI has **1.0000** precision with
  0 false positives on 833
  negative rows.
- Recall is **0.8791** for Flagline and
  **0.7617** for OpenAI. Both systems are conservative;
  Flagline finds more positives.
- On the five shared categories, Flagline is ahead on harassment, hate, and
  sexual, self-harm ties, and OpenAI is ahead on violence. OpenAI predicts no
  sexual positives in its 64 positive sexual rows, so its
  sexual F1 is 0.0 with undefined precision.
- The weakest strict slice is marketplace spam for
  Flagline (F1 0.1449) and sexual for OpenAI
  (F1 0.0000).
- Flagline flags 93.0% of
  proxy rows and 7.6%
  of borderline rows. OpenAI flags
  15.6% and
  0.5%. These are
  behavioral differences, not accuracy scores.

## Reading the results

- Flagline's macro F1 averages 33 preset/category slices
  with positive support out of 39. OpenAI's macro F1 averages
  11 categories with positive support out of 13. The slice
  sets are not the same, so compare the shared-category table for a
  like-for-like view.
- Flagline's broad categories can catch a category concept while also flagging
  adjacent categories. The per-slice tables show how much precision that costs.
- The dataset is authored at Standard, but Flagline ran at light. A standard
  rerun requires a key that permits standard.
- `family` groups correlated variants; rows are not independent.

## Read the runs

- [Flagline 2026-11-21 light](2026-11-21-flagline-light/README.md)
- [OpenAI 2026-11-21](2026-11-21-openai/README.md)
