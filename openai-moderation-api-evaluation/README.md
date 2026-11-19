# OpenAI moderation API evaluation

Evaluation of Flagline and OpenAI on the
[OpenAI Moderation API Validation Dataset](https://huggingface.co/datasets/mmathys/openai-moderation-api-evaluation),
from the paper [A Holistic Approach to Undesired Content Detection](https://arxiv.org/abs/2208.03274).

The dataset has 1,680 English prompts and eight binary labels. It is
text-only. A missing label means **unknown**, not negative. Per-label metrics
use only rows where that label is present; overall metrics use the
**755** rows where all eight labels are present.

## Runs

| Run | Provider | Model | Samples | Macro F1 | Overall F1 | Overall accuracy |
|---|---|---|---:|---:|---:|---:|
| [2026-11-19 flagline-light](2026-11-19-flagline-light/README.md) | Flagline | Social standard v1, light | 1,680 | 0.5741 | 0.8429 | 0.8331 |
| [2026-11-19 openai](2026-11-19-openai/README.md) | OpenAI | omni-moderation-latest | 1,680 | 0.6432 | 0.8022 | 0.7589 |

Side-by-side: [comparison.md](comparison.md).

## Dataset

| Code | Category | Known | Positive | Missing |
|---|---|---|---|---|
| S | sexual | 984 | 237 | 696 |
| H | hate | 771 | 162 | 909 |
| V | violence | 1,450 | 94 | 230 |
| HR | harassment | 1,444 | 76 | 236 |
| SH | self-harm | 1,447 | 51 | 233 |
| S3 | sexual/minors | 994 | 85 | 686 |
| H2 | hate/threatening | 761 | 41 | 919 |
| V2 | violence/graphic | 1,447 | 24 | 233 |

Known plus missing equals 1,680 for every label. The positive counts are the
support used by recall.

## Reading the results

- **Macro F1** averages the eight per-label F1 scores. It rewards a system that
  can tell `S` from `S3`, `H` from `H2`, and `V` from `V2`.
- **Overall F1 and accuracy** are computed on the 755
  fully labeled rows for the aligned union of the eight labels. They answer a
  different question: is this item unsafe at all?
- Flagline's Social standard policy has six broad categories. It cannot
  distinguish `S` from `S3`, `H` from `H2`, or `V` from `V2`; those pairs share
  one score and threshold. This is the main structural difference in the
  per-label comparison.
- OpenAI's eight matching category booleans are used directly. The aligned
  union ignores categories the dataset does not label, such as `illicit`.
- Both runs are text only. The dataset has no media.

## Content note

This repository contains labels, scores, and per-item tables for a dataset of
moderation examples. It does not reproduce prompt bodies. Some source examples
contain harmful content; the labels are the dataset's, not Flagline's.

## Rights

The dataset is MIT licensed; see the upstream
[moderation-api-release](https://github.com/openai/moderation-api-release)
repository. Result tables are published for evaluation and research use.
