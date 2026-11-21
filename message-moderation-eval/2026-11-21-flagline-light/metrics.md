# Flagline metrics

## Native strict metrics

| Micro P | Micro R | Micro F1 | Micro Acc | Macro F1 |
|---:|---:|---:|---:|---:|
| 0.9973 | 0.8791 | 0.9345 | 0.9434 | 0.9163 |

## Bands

| Band | Rows | Flagged | Flag rate |
|---|---|---|---|
| positive | 2117 | 1861 | 87.9% |
| negative | 2498 | 5 | 0.2% |
| borderline | 2501 | 190 | 7.6% |
| proxy | 385 | 358 | 93.0% |

## Per-slice

| Preset | Category | Unified | Pos | Neg | P | R | F1 | Acc | Borderline n / flag | Proxy n / flag |
|---|---|---|---|---|---|---|---|---|---|---|
| dating | harassment | harassment | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| dating | impersonation | impersonation | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 20.3% | 0 / n/a |
| dating | scams | scams | 64 | 64 | 1.000 | 0.734 | 0.847 | 0.867 | 64 / 43.8% | 0 / n/a |
| dating | sexual | sexual | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| dating | spam | spam | 64 | 64 | 1.000 | 0.703 | 0.826 | 0.852 | 64 / 0.0% | 0 / n/a |
| developer-community | credential-leak | credential_leak | 64 | 64 | 1.000 | 0.984 | 0.992 | 0.992 | 64 / 0.0% | 0 / n/a |
| developer-community | doxxing | doxxing | 0 | 64 | n/a | n/a | n/a | 1.000 | 64 / 0.0% | 64 / 98.4% |
| developer-community | harassment | harassment | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| developer-community | hate | hate | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| developer-community | malware | malware | 0 | 64 | n/a | n/a | n/a | 1.000 | 64 / 0.0% | 64 / 75.0% |
| developer-community | spam | spam | 65 | 64 | 1.000 | 0.585 | 0.738 | 0.791 | 64 / 0.0% | 0 / n/a |
| gaming-chat | cheating | cheating | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| gaming-chat | harassment | harassment | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| gaming-chat | hate | hate | 64 | 64 | 1.000 | 0.984 | 0.992 | 0.992 | 64 / 0.0% | 0 / n/a |
| gaming-chat | profanity | profanity | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 65 / 75.4% | 0 / n/a |
| gaming-chat | spam | spam | 64 | 64 | 1.000 | 0.594 | 0.745 | 0.797 | 64 / 0.0% | 0 / n/a |
| kids-safe | bullying | bullying | 64 | 64 | 1.000 | 0.766 | 0.867 | 0.883 | 64 / 0.0% | 0 / n/a |
| kids-safe | grooming | grooming | 0 | 64 | n/a | n/a | n/a | 1.000 | 64 / 4.7% | 64 / 98.4% |
| kids-safe | personal-info | personal_info | 0 | 64 | n/a | n/a | n/a | 1.000 | 64 / 25.0% | 64 / 87.5% |
| kids-safe | self-harm | self_harm | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| kids-safe | sexual | sexual | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 1.6% | 0 / n/a |
| kids-safe | violence | violence | 65 | 65 | 1.000 | 0.969 | 0.984 | 0.985 | 64 / 0.0% | 0 / n/a |
| marketplace | counterfeit | counterfeit | 64 | 64 | 0.928 | 1.000 | 0.962 | 0.961 | 65 / 40.0% | 0 / n/a |
| marketplace | fraud | fraud | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| marketplace | prohibited-goods | prohibited_goods | 0 | 64 | n/a | n/a | n/a | 1.000 | 65 / 6.2% | 64 / 98.4% |
| marketplace | scams | scams | 64 | 64 | 1.000 | 0.953 | 0.976 | 0.977 | 64 / 40.6% | 0 / n/a |
| marketplace | spam | spam | 64 | 64 | 1.000 | 0.078 | 0.145 | 0.539 | 64 / 0.0% | 0 / n/a |
| social-standard | harassment | harassment | 65 | 64 | 1.000 | 0.785 | 0.879 | 0.891 | 64 / 0.0% | 0 / n/a |
| social-standard | hate | hate | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| social-standard | self-harm | self_harm | 65 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| social-standard | sexual | sexual | 64 | 65 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| social-standard | spam | spam | 64 | 64 | 1.000 | 0.547 | 0.707 | 0.773 | 64 / 9.4% | 0 / n/a |
| social-standard | violence | violence | 64 | 64 | 1.000 | 0.812 | 0.897 | 0.906 | 64 / 0.0% | 0 / n/a |
| support-inbox | account-takeover | account_takeover | 0 | 64 | n/a | n/a | n/a | 1.000 | 65 / 15.4% | 65 / 100.0% |
| support-inbox | fraud | fraud | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| support-inbox | harassment | harassment | 65 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| support-inbox | self-harm | self_harm | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 0.0% | 0 / n/a |
| support-inbox | spam | spam | 64 | 64 | 1.000 | 0.516 | 0.680 | 0.758 | 64 / 12.5% | 0 / n/a |
| support-inbox | threats | threats | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 65 / 0.0% | 0 / n/a |

## Per unified category

| Unified category | Pos | Neg | P | R | F1 | Acc |
|---|---|---|---|---|---|---|
| account_takeover | 0 | 64 | n/a | n/a | n/a | 1.000 |
| bullying | 64 | 64 | 1.000 | 0.766 | 0.867 | 0.883 |
| cheating | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 |
| counterfeit | 64 | 64 | 0.928 | 1.000 | 0.962 | 0.961 |
| credential_leak | 64 | 64 | 1.000 | 0.984 | 0.992 | 0.992 |
| doxxing | 0 | 64 | n/a | n/a | n/a | 1.000 |
| fraud | 128 | 128 | 1.000 | 1.000 | 1.000 | 1.000 |
| grooming | 0 | 64 | n/a | n/a | n/a | 1.000 |
| harassment | 322 | 320 | 1.000 | 0.957 | 0.978 | 0.978 |
| hate | 192 | 192 | 1.000 | 0.995 | 0.997 | 0.997 |
| impersonation | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 |
| malware | 0 | 64 | n/a | n/a | n/a | 1.000 |
| personal_info | 0 | 64 | n/a | n/a | n/a | 1.000 |
| profanity | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 |
| prohibited_goods | 0 | 64 | n/a | n/a | n/a | 1.000 |
| scams | 128 | 128 | 1.000 | 0.844 | 0.915 | 0.922 |
| self_harm | 193 | 192 | 1.000 | 1.000 | 1.000 | 1.000 |
| sexual | 192 | 193 | 1.000 | 1.000 | 1.000 | 1.000 |
| spam | 385 | 384 | 1.000 | 0.504 | 0.670 | 0.752 |
| threats | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 |
| violence | 129 | 129 | 1.000 | 0.891 | 0.943 | 0.946 |

## Latency

| p50 | p95 | Sum of request time |
|---:|---:|---:|
| 1.181s | 7.379s | 20227.1s |

## Notes

- Strict metrics use positive and negative rows only.
- Borderline and proxy rows are reported as flag rates, not as positives.
- The run uses light thresholds (`flagThreshold + 0.10`). The dataset is
  authored at Standard.
- Presets are inline copies pinned to the dataset taxonomy hashes, including
  Kids safe v2.
