# OpenAI metrics

## Native strict

| Slice | n | P | R | F1 | Acc |
|---|---|---|---|---|---|
| All strict | 3,592 | 0.8799 | 0.5032 | 0.6402 | 0.7272 |
| Baseline | 1,795 | 0.9762 | 0.7102 | 0.8222 | 0.8518 |
| Hard | 1,797 | 0.7119 | 0.2964 | 0.4186 | 0.6027 |

## Macro

| Slice | Categories | P | R | F1 | Acc |
|---|---|---|---|---|---|
| All strict | 11 | 0.9152 | 0.5613 | 0.6322 | 0.7381 |
| Baseline | 11 | 0.9866 | 0.7691 | 0.8159 | 0.8775 |
| Hard | 11 | 0.7994 | 0.3535 | 0.3832 | 0.5990 |

## Contrast pairs

| Slice | Pairs | Correct | Accuracy | Negative flag rate | Proxy flag rate | Expected behavior |
|---|---|---|---|---|---|---|
| Decisive (positive/negative) | 864 | 151 | 17.5% | - | - | - |
| Proxy (negative/proxy) | 64 | - | - | 0.0% | 0.0% | 0.0% |

## Per category

| Category | Strict | Pos | Neg | P | R | F1 | Acc | Baseline acc | Hard acc | Borderline n / flag | Proxy n / flag |
|---|---|---|---|---|---|---|---|---|---|---|---|
| harassment | 771 | 387 | 384 | 1.000 | 0.401 | 0.572 | 0.699 | 0.831 | 0.567 | 384 / 0.0% | 0 / n/a |
| harassment_threatening | 128 | 64 | 64 | 1.000 | 0.547 | 0.707 | 0.773 | 0.953 | 0.594 | 64 / 0.0% | 0 / n/a |
| hate | 512 | 256 | 256 | 1.000 | 0.398 | 0.570 | 0.699 | 0.898 | 0.500 | 256 / 0.0% | 0 / n/a |
| hate_threatening | 128 | 64 | 64 | 1.000 | 0.250 | 0.400 | 0.625 | 0.750 | 0.500 | 64 / 0.0% | 0 / n/a |
| illicit | 128 | 64 | 64 | 0.942 | 0.766 | 0.845 | 0.859 | 1.000 | 0.719 | 64 / 0.0% | 0 / n/a |
| illicit_violent | 64 | 0 | 64 | n/a | n/a | n/a | 1.000 | 1.000 | 1.000 | 65 / 0.0% | 64 / 31.2% |
| self_harm | 513 | 257 | 256 | 0.925 | 0.864 | 0.893 | 0.897 | 1.000 | 0.794 | 256 / 0.0% | 0 / n/a |
| self_harm_intent | 129 | 64 | 65 | 0.714 | 0.938 | 0.811 | 0.783 | 1.000 | 0.569 | 64 / 6.2% | 0 / n/a |
| self_harm_instructions | 128 | 64 | 64 | 0.960 | 0.375 | 0.539 | 0.680 | 0.797 | 0.562 | 64 / 0.0% | 0 / n/a |
| sexual | 513 | 256 | 257 | n/a | 0.000 | 0.000 | 0.501 | 0.500 | 0.502 | 256 / 0.0% | 0 / n/a |
| sexual_minors | 64 | 0 | 64 | n/a | n/a | n/a | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 64 / 0.0% |
| violence | 386 | 193 | 193 | 0.696 | 0.808 | 0.748 | 0.728 | 0.923 | 0.531 | 192 / 12.5% | 0 / n/a |
| violence_graphic | 128 | 64 | 64 | 0.914 | 0.828 | 0.869 | 0.875 | 1.000 | 0.750 | 64 / 0.0% | 0 / n/a |

## Bands

| Band | Rows | Flagged | Flag rate |
|---|---|---|---|
| positive | 1,733 | 872 | 50.3% |
| negative | 1,859 | 119 | 6.4% |
| borderline | 1,857 | 28 | 1.5% |
| proxy | 128 | 20 | 15.6% |

## Latency

| p50 | p95 | Sum of request time |
|---:|---:|---:|
| 1.385s | 11.370s | 19128.2s |
