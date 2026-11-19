# ModerationBench

[ModerationBench](https://github.com/ayanmaj92/moderation-bench) is a
multimodal content moderation benchmark built around Bluesky posts and the
S0-S10 Bluesky taxonomy. The upstream benchmark evaluates vision-language
models on post text plus images and video.

Flagline's moderation API accepts text only, so the Flagline run is text-only.
The OpenAI run uses the same text-only metadata for comparability, even though
its API can accept images. The runners and hydrator live in the code forks,
[Flagline-dev/moderation-bench](https://github.com/Flagline-dev/moderation-bench)
and
[Flagline-dev/moderation-bench-openai](https://github.com/Flagline-dev/moderation-bench-openai).
The Flagline fork's `FLAGLINE.md` and the OpenAI fork's `OPENAI.md` document the
methods and limitations.

## Runs

| Run | Date | Provider | Preset / model | Level | Scored | Accuracy | Recall | F1 |
|---|---|---|---|---:|---:|---:|---:|
| [2026-11-19 light](2026-11-19-light/README.md) | 2026-11-19 | Flagline | Social standard v1 | light | 3,443 | 0.8066 | 0.4602 | 0.5785 |
| [2026-11-19 openai](2026-11-19-openai/README.md) | 2026-11-19 | OpenAI | omni-moderation-latest | fixed | 3,443 | 0.7900 | 0.4995 | 0.5784 |

Side-by-side: [Flagline vs OpenAI](comparison.md).

The run directory contains the headline numbers, coverage, caveats, detailed
metrics, and every scored post. Published runs are immutable; a rerun gets a
new directory rather than overwriting an existing one.

## Reading the results

- `flag` and `block` both count as Unsafe in the Flagline run. Use the
  decision counts to separate review flags from blocks. OpenAI's `flagged` is
  a single binary decision.
- The `safe` subset has no Unsafe ground-truth posts, so precision and recall
  are undefined there.
- The ground truth is Bluesky policy, not Flagline's Social standard policy or
  OpenAI's fixed taxonomy. Policy disagreement is not automatically a model
  error.
- Both runs are text only. Image-dependent categories have much lower recall
  than text-heavy categories.
