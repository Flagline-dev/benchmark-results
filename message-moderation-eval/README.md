# Message Moderation Eval, compact workload

Evaluation of Flagline and OpenAI on the compact workload of
[`flagline/message-moderation-eval`](https://huggingface.co/datasets/flagline/message-moderation-eval).

The compact workload is 10,000 unique English standalone messages.
Every row targets one provider/preset/category slice and carries one evidence
band: positive, negative, borderline, or proxy. The dataset is synthetic and
balanced by band; it is not a prevalence sample.

| Provider | Rows | Slices |
|---|---:|---:|
| Flagline | 7,501 | 39 |
| OpenAI | 2,499 | 13 |

## Runs

| Run | Provider | Model | Provider rows | Macro F1 | Micro F1 | Micro accuracy |
|---|---|---|---:|---:|---:|---:|
| [2026-11-21 flagline-light](2026-11-21-flagline-light/README.md) | Flagline | 7 pinned system presets, light | 7,501 | 0.9163 | 0.9345 | 0.9434 |
| [2026-11-21 openai](2026-11-21-openai/README.md) | OpenAI | omni-moderation-latest | 2,499 | 0.8180 | 0.8647 | 0.8908 |

Side-by-side: [comparison.md](comparison.md).

## Scoring

- Strict metrics use only `positive` and `negative` rows.
- `borderline` and `proxy` rows are excluded from precision, recall, and F1.
  Their flag rates are reported separately.
- A negative for one category does not imply that other categories are
  negative.
- Flagline uses the seven active system presets as inline presets, pinned by
  the hashes in the dataset's `taxonomy.json`. Kids safe uses v2.
- Flagline runs at `light` because the key used for this run permits only
  light. The dataset is authored at Standard. This is a material limitation.
- OpenAI uses `omni-moderation-latest` and its category booleans directly.
- The general-purpose comparison uses Flagline's `social-standard` preset and
  OpenAI on five shared unified categories. The rows are different, so it is a
  category-level comparison, not a paired one.

## Dataset bands

| Band | Rows |
|---|---|
| positive | 2,822 |
| negative | 3,331 |
| borderline | 3,334 |
| proxy | 513 |

The compact workload includes 365 families. Rows from one family
are correlated variants; do not treat all rows as independent.

## Content note

This repository contains labels, scores, and per-item tables. It does not
reproduce message bodies. The dataset includes abusive language, self-harm and
crisis language, and descriptions of serious injuries.

## Rights

The dataset is published by Flagline on Hugging Face. The result tables are
provided for evaluation and research use.
