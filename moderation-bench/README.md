# ModerationBench

[ModerationBench](https://github.com/ayanmaj92/moderation-bench) is a
multimodal content moderation benchmark built around Bluesky posts and the
S0-S10 Bluesky taxonomy. The upstream benchmark evaluates vision-language
models on post text plus images and video.

Flagline's moderation API accepts text only, so the Flagline run is text-only.
The runner and hydrator live in the code fork,
[Flagline-dev/moderation-bench](https://github.com/Flagline-dev/moderation-bench).
That fork's `FLAGLINE.md` documents the method and the limitations.

## Runs

| Run | Date | Preset | Level | Scored | Accuracy | Recall | F1 |
|---|---|---|---:|---:|---:|---:|---:|
| [2026-11-19 light](2026-11-19-light/README.md) | 2026-11-19 | Social standard v1 | light | 3,443 | 0.8066 | 0.4602 | 0.5785 |

The run directory contains the headline numbers, coverage, caveats, detailed
metrics, and every scored post. Published runs are immutable; a rerun gets a
new directory rather than overwriting an existing one.

## Reading the results

- `flag` and `block` both count as Unsafe in the binary report. Use the
  decision counts to separate review flags from blocks.
- The `safe` subset has no Unsafe ground-truth posts, so precision and recall
  are undefined there.
- The ground truth is Bluesky policy, not Flagline's Social standard policy.
  Policy disagreement is not automatically a model error.
- The text-only run cannot see images or video. Image-dependent categories
  have much lower recall than text-heavy categories.
