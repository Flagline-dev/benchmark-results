# OpenAI metrics

## Native strict metrics

| Micro P | Micro R | Micro F1 | Micro Acc | Macro F1 |
|---:|---:|---:|---:|---:|
| 1.0000 | 0.7617 | 0.8647 | 0.8908 | 0.8180 |

## Bands

| Band | Rows | Flagged | Flag rate |
|---|---|---|---|
| positive | 705 | 537 | 76.2% |
| negative | 833 | 0 | 0.0% |
| borderline | 833 | 4 | 0.5% |
| proxy | 128 | 20 | 15.6% |

## Per-category

| Preset | Category | Unified | Pos | Neg | P | R | F1 | Acc | Borderline n / flag | Proxy n / flag |
|---|---|---|---|---|---|---|---|---|---|---|
| omni-moderation-latest | harassment | harassment | 65 | 64 | 1.000 | 0.754 | 0.860 | 0.876 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | harassment/threatening | harassment_threatening | 64 | 64 | 1.000 | 0.750 | 0.857 | 0.875 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | hate | hate | 64 | 64 | 1.000 | 0.781 | 0.877 | 0.891 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | hate/threatening | hate_threatening | 64 | 64 | 1.000 | 0.438 | 0.609 | 0.719 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | illicit | illicit | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | illicit/violent | illicit_violent | 0 | 64 | n/a | n/a | n/a | 1.000 | 65 / 0.0% | 64 / 31.2% |
| omni-moderation-latest | self-harm | self_harm | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | self-harm/instructions | self_harm_instructions | 64 | 64 | 1.000 | 0.672 | 0.804 | 0.836 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | self-harm/intent | self_harm_intent | 64 | 65 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 6.2% | 0 / n/a |
| omni-moderation-latest | sexual | sexual | 64 | 64 | n/a | 0.000 | 0.000 | 0.500 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | sexual/minors | sexual_minors | 0 | 64 | n/a | n/a | n/a | 1.000 | 64 / 0.0% | 64 / 0.0% |
| omni-moderation-latest | violence | violence | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| omni-moderation-latest | violence/graphic | violence_graphic | 64 | 64 | 1.000 | 0.984 | 0.992 | 0.992 | 64 / 0.0% | 0 / n/a |

## Per unified category

| Unified category | Pos | Neg | P | R | F1 | Acc |
|---|---|---|---|---|---|---|
| harassment | 65 | 64 | 1.000 | 0.754 | 0.860 | 0.876 |
| harassment_threatening | 64 | 64 | 1.000 | 0.750 | 0.857 | 0.875 |
| hate | 64 | 64 | 1.000 | 0.781 | 0.877 | 0.891 |
| hate_threatening | 64 | 64 | 1.000 | 0.438 | 0.609 | 0.719 |
| illicit | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 |
| illicit_violent | 0 | 64 | n/a | n/a | n/a | 1.000 |
| self_harm | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 |
| self_harm_instructions | 64 | 64 | 1.000 | 0.672 | 0.804 | 0.836 |
| self_harm_intent | 64 | 65 | 1.000 | 1.000 | 1.000 | 1.000 |
| sexual | 64 | 64 | n/a | 0.000 | 0.000 | 0.500 |
| sexual_minors | 0 | 64 | n/a | n/a | n/a | 1.000 |
| violence | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 |
| violence_graphic | 64 | 64 | 1.000 | 0.984 | 0.992 | 0.992 |

## Latency

| p50 | p95 | Sum of request time |
|---:|---:|---:|
| 1.340s | 11.388s | 8062.5s |

## Notes

- Strict metrics use positive and negative rows only.
- Borderline and proxy rows are reported as flag rates, not as positives.
- `omni-moderation-latest` is a rolling alias.
