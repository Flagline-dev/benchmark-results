# Flagline vs OpenAI on Message Moderation Eval v4

Both providers scored the same 4,039 shared-category rows
from the compact workload. This is the paired comparison. Native results cover
different category sets and are not directly comparable.

## Shared categories

| Shared category | Strict | Pos / Neg | Flagline P | Flagline R | Flagline F1 | OpenAI P | OpenAI R | OpenAI F1 |
|---|---|---|---|---|---|---|---|---|
| harassment | 771 | 387 / 384 | 1.000 | 0.687 | 0.815 | 1.000 | 0.401 | 0.572 |
| hate | 512 | 256 / 256 | 0.823 | 0.816 | 0.820 | 1.000 | 0.398 | 0.570 |
| self_harm | 513 | 257 / 256 | 1.000 | 0.895 | 0.945 | 0.925 | 0.864 | 0.893 |
| sexual | 513 | 256 / 257 | 1.000 | 0.961 | 0.980 | n/a | 0.000 | 0.000 |
| violence | 386 | 193 / 193 | 1.000 | 0.275 | 0.431 | 0.696 | 0.808 | 0.748 |

## Shared summary

| View | n | P | R | F1 | Acc |
|---|---:|---:|---:|---:|---:|
| Flagline | 2,695 | 0.9571 | 0.7443 | 0.8374 | 0.8553 |
| OpenAI | 2,695 | 0.8807 | 0.4707 | 0.6135 | 0.7032 |

Macro F1 over the five shared categories: Flagline
**0.7980**, OpenAI
**0.5567**.

## Highlights

- Native strict F1 is **0.7815** for Flagline and
  **0.6402** for OpenAI. Native coverage differs,
  so use the shared table for the paired view.
- The hard split is much harder than baseline: Flagline F1
  **0.8942** on baseline and
  **0.6528** on hard; OpenAI
  **0.8222** and
  **0.4186**.
- On the shared categories, Flagline F1 is
  **0.8374** and OpenAI F1 is
  **0.6135**. Exact agreement is
  **72.8%**; Cohen's kappa is
  **0.3927**.
- Decisive pair accuracy on shared categories is
  **55.8%** for Flagline and
  **15.9%** for OpenAI. A pair counts only when both
  sides are correct.
- Flagline is stronger on shared harassment, hate, and sexual; self-harm is
  close; OpenAI is stronger on shared violence. OpenAI predicts no sexual
  positives in the shared sexual slice, so its shared sexual F1 is 0.0.
- Flagline flags **79.5%** of its proxy rows
  and **7.4%** of borderline rows.
  OpenAI flags **15.6%** and
  **1.5%**.
- Flagline's weakest native slices are spam, violence, and scams. OpenAI's
  weakest are sexual, hate/threatening, and self-harm/instructions.

## Hard and baseline

| Slice | Flagline F1 | OpenAI F1 | Flagline acc | OpenAI acc |
|---|---:|---:|---:|---:|
| Baseline | 0.9285 | 0.7955 | 0.9332 | 0.8263 |
| Hard | 0.7368 | 0.3888 | 0.7774 | 0.5801 |

These are the same shared-category rows, split by difficulty.

## Contrast pairs

| Provider | Decisive pairs | Correct | Pair accuracy |
|---|---:|---:|---:|
| Flagline | 672 | 375 | 55.8% |
| OpenAI | 672 | 107 | 15.9% |

A decisive pair is correct only when both messages are correct. Shared
categories have no proxy pairs.

## Agreement on shared strict rows

| | OpenAI Unsafe | OpenAI Safe |
|---|---:|---:|
| Flagline Unsafe | 518 | 531 |
| Flagline Safe | 203 | 1,443 |

Exact agreement is **72.8%**; Cohen's kappa is
**0.3927**.

## Native coverage

| Provider | Categories | Rows | Strict rows | Micro F1 | Macro F1 | Decisive pair accuracy |
|---|---:|---:|---:|---:|---:|---:|
| Flagline | 21 of 29 | 8,462 | 5,256 | 0.7815 | 0.8055 | 47.0% |
| OpenAI | 13 of 29 | 5,577 | 3,592 | 0.6402 | 0.6322 | 17.5% |

## Band behavior

| Provider | Positive flag rate | Negative flag rate | Borderline flag rate | Proxy flag rate |
|---|---:|---:|---:|---:|
| Flagline | 66.2% | 2.8% | 7.4% | 79.5% |
| OpenAI | 50.3% | 6.4% | 1.5% | 15.6% |

## Read the runs

- [Flagline v4 light](2026-11-21-v4-flagline-light/README.md)
- [OpenAI v4](2026-11-21-v4-openai/README.md)

## Caveats

- Flagline ran at light, not Standard.
- The providers support different category sets. Native macro F1 is not a
  like-for-like comparison.
- The data is synthetic and balanced by band and difficulty.
- Half the rows are hard; contrast pairs are scored only when both sides are
  correct.
- `family` groups correlated variants; rows are not independent.
