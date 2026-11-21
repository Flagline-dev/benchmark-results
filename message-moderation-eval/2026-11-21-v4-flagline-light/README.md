# Flagline on Message Moderation Eval v4

Flagline with the primary preset for each canonical category, level `light`.

- **Supported categories:** 21 of 29
- **Provider rows:** 8,462
- **Strict rows:** 5,256
- **Level:** light. The key used for this run permits only light; the dataset is
  authored at Standard.
- **Backend model:** `decision-models/baseten-elephant-9b-latest`
- **Failures:** 0
- **Latency:** p50 1.460s, p95 11.399s, sum
  28802.4s

## Native strict metrics

| Slice | n | P | R | F1 | Acc |
|---|---|---|---|---|---|
| All strict | 5,256 | 0.9528 | 0.6624 | 0.7815 | 0.8282 |
| Baseline | 2,627 | 1.0000 | 0.8087 | 0.8942 | 0.9113 |
| Hard | 2,629 | 0.8873 | 0.5164 | 0.6528 | 0.7452 |

## Highlights

- Baseline F1 is **0.8942**; hard F1 is
  **0.6528** against baseline accuracy
  0.9113 and hard accuracy
  0.7452.
- Decisive pair accuracy is **47.0%**.
  A pair counts only when both messages are correct.
- Strongest categories: profanity F1
  **1.0000**, spam is the weakest at
  **0.3405**.
- Proxy rows are flagged at **79.5%**;
  borderline rows at **7.4%**.

## Macro

| Slice | Categories | P | R | F1 | Acc |
|---|---|---|---|---|---|
| All strict | 15 | 0.9719 | 0.7341 | 0.8055 | 0.8538 |
| Baseline | 15 | 1.0000 | 0.8813 | 0.9209 | 0.9406 |
| Hard | 15 | 0.9360 | 0.5869 | 0.6585 | 0.7670 |

Macro F1 averages 15 categories with
positive support.

## Contrast pairs

| Slice | Pairs | Correct | Accuracy | Negative flag rate | Proxy flag rate | Expected behavior |
|---|---|---|---|---|---|---|
| Decisive (positive/negative) | 1216 | 571 | 47.0% | - | - | - |
| Proxy (negative/proxy) | 192 | - | - | 10.4% | 63.5% | 53.6% |

## Per category

| Category | Strict | Pos | Neg | P | R | F1 | Acc | Baseline acc | Hard acc | Borderline n / flag | Proxy n / flag |
|---|---|---|---|---|---|---|---|---|---|---|---|
| harassment | 771 | 387 | 384 | 1.000 | 0.687 | 0.815 | 0.843 | 0.896 | 0.790 | 384 / 0.0% | 0 / n/a |
| hate | 512 | 256 | 256 | 0.823 | 0.816 | 0.820 | 0.820 | 1.000 | 0.641 | 256 / 1.6% | 0 / n/a |
| sexual | 513 | 256 | 257 | 1.000 | 0.961 | 0.980 | 0.981 | 1.000 | 0.961 | 256 / 0.0% | 0 / n/a |
| violence | 386 | 193 | 193 | 1.000 | 0.275 | 0.431 | 0.637 | 0.742 | 0.531 | 192 / 0.0% | 0 / n/a |
| self_harm | 513 | 257 | 256 | 1.000 | 0.895 | 0.945 | 0.947 | 1.000 | 0.895 | 256 / 0.0% | 0 / n/a |
| spam | 769 | 385 | 384 | 1.000 | 0.205 | 0.341 | 0.602 | 0.706 | 0.499 | 384 / 3.4% | 0 / n/a |
| profanity | 128 | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 | 65 / 73.8% | 0 / n/a |
| cheating | 128 | 64 | 64 | 1.000 | 0.688 | 0.815 | 0.844 | 1.000 | 0.688 | 64 / 0.0% | 0 / n/a |
| grooming | 64 | 0 | 64 | n/a | n/a | n/a | 1.000 | 1.000 | 1.000 | 64 / 10.9% | 64 / 76.6% |
| personal_info | 64 | 0 | 64 | n/a | n/a | n/a | 0.922 | 1.000 | 0.844 | 64 / 60.9% | 64 / 87.5% |
| bullying | 128 | 64 | 64 | 1.000 | 0.875 | 0.933 | 0.938 | 1.000 | 0.875 | 64 / 0.0% | 0 / n/a |
| scams | 256 | 128 | 128 | 0.959 | 0.367 | 0.531 | 0.676 | 0.766 | 0.586 | 128 / 25.0% | 0 / n/a |
| impersonation | 128 | 64 | 64 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 | 64 / 20.3% | 0 / n/a |
| fraud | 256 | 128 | 128 | 1.000 | 0.773 | 0.872 | 0.887 | 1.000 | 0.773 | 128 / 0.0% | 0 / n/a |
| counterfeit | 128 | 64 | 64 | 0.892 | 0.906 | 0.899 | 0.898 | 1.000 | 0.797 | 65 / 24.6% | 0 / n/a |
| prohibited_goods | 64 | 0 | 64 | n/a | n/a | n/a | 0.844 | 1.000 | 0.688 | 65 / 6.2% | 64 / 85.9% |
| doxxing | 64 | 0 | 64 | n/a | n/a | n/a | 0.922 | 1.000 | 0.844 | 64 / 15.6% | 64 / 87.5% |
| credential_leak | 128 | 64 | 64 | 1.000 | 0.672 | 0.804 | 0.836 | 1.000 | 0.672 | 64 / 0.0% | 0 / n/a |
| malware | 64 | 0 | 64 | n/a | n/a | n/a | 1.000 | 1.000 | 1.000 | 64 / 1.6% | 64 / 64.1% |
| threats | 128 | 64 | 64 | 0.905 | 0.891 | 0.898 | 0.898 | 1.000 | 0.797 | 65 / 0.0% | 0 / n/a |
| account_takeover | 64 | 0 | 64 | n/a | n/a | n/a | 1.000 | 1.000 | 1.000 | 65 / 33.8% | 65 / 75.4% |

## Bands

| Band | Rows | Flagged | Flag rate |
|---|---|---|---|
| positive | 2,438 | 1,615 | 66.2% |
| negative | 2,818 | 80 | 2.8% |
| borderline | 2,821 | 209 | 7.4% |
| proxy | 385 | 306 | 79.5% |

## Files

- [metrics.md](metrics.md) for the same tables.
- [items.md](items.md) for all 8,462 Flagline rows.
- [comparison.md](../comparison.md) for the shared-category comparison.

## Caveats

- Light thresholds are 0.10 above Standard.
- The primary preset mapping uses social-standard for the shared categories and
  spam, and the preset that defines each specialized category otherwise.
- Unsupported canonical categories are not imputed.
