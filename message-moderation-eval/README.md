# Message Moderation Eval, compact workload (schema v4)

Evaluation of Flagline and OpenAI on the compact workload of
[`flagline/message-moderation-eval`](https://huggingface.co/datasets/flagline/message-moderation-eval).

The compact workload is 10,000 unique English standalone messages in
one provider-neutral 29-category taxonomy. Each row has one canonical
`category`, one evidence band, one difficulty, and an optional contrast pair.
Schema v4 replaces half the rows from v3.

| Field | Meaning |
|---|---|
| `label` | positive, negative, borderline, or proxy |
| `difficulty` | baseline or hard |
| `contrast_id` | shared ID for an exact contrast pair, or null |

## Coverage

The providers do not support the same category set.

| Provider | Categories | Rows | Strict rows |
|---|---:|---:|---:|
| Flagline | 21 of 29 | 8,462 | 5,256 |
| OpenAI | 13 of 29 | 5,577 | 3,592 |
| Shared | 5 of 29 | 4,039 | 2,695 |

The shared categories are harassment, hate, self-harm, sexual, and violence.
Only the shared rows are a paired comparison.

## Runs

| Run | Provider | Coverage | Rows | Strict rows | Micro F1 | Macro F1 | Decisive pair accuracy |
|---|---|---|---:|---:|---:|---:|---:|
| [2026-11-21 v4 flagline-light](2026-11-21-v4-flagline-light/README.md) | Flagline | 21 of 29 categories | 8,462 | 5,256 | 0.7815 | 0.8055 | 47.0% |
| [2026-11-21 v4 openai](2026-11-21-v4-openai/README.md) | OpenAI | 13 of 29 categories | 5,577 | 3,592 | 0.6402 | 0.6322 | 17.5% |

Side-by-side: [comparison.md](comparison.md).

## Scoring

- Strict metrics use only positive and negative rows.
- Baseline and hard rows are reported separately.
- Borderline rows are reported as a review or flag rate, not as errors.
- Proxy rows and proxy pairs are reported separately from decisive pairs.
- A decisive contrast pair counts as correct only when both messages are
  correct. Singletons at the workload boundary are skipped.
- Flagline uses the primary preset for each canonical category: social-standard
  for the five shared categories and spam, then the preset that defines the
  specialized category. The exact mapping is in the harness repository.
- Flagline runs at `light` because the key used for this run permits only
  light. The dataset is authored at Standard. This is a material limitation.
- OpenAI uses `omni-moderation-latest`; its 13 category booleans map directly
  to the canonical categories.
- Unsupported categories are not imputed. They are reported as unsupported.

## Dataset

| Band | Rows |
|---|---:|
| positive | 2,822 |
| negative | 3,331 |
| borderline | 3,334 |
| proxy | 513 |

The compact workload includes 527 families and
1,671 contrast IDs. Half the rows are `hard`.

## Content note

This repository contains labels, scores, and per-item tables. It does not
reproduce message bodies. The dataset includes abusive language, self-harm and
crisis language, and descriptions of serious injuries.

## Rights

The dataset is published by Flagline on Hugging Face. Result tables are
provided for evaluation and research use.
