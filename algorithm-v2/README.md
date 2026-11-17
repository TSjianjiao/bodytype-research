# Algorithm v2 test vectors

`algorithm_version: "2"` · units: cm · 15 synthetic vectors · updated 2026-11-17

These vectors are checked against the live Bodytype v2 implementation
(`rules.ts`, `thresholds.ts`, `stability.ts`). The CSV is byte-identical to the
site download:
<https://bodytype.org/data/research/bodytype-algorithm-v2/test-vectors.csv>

## Columns

| Column | Meaning |
| --- | --- |
| `id` | Vector number (1–15). |
| `bust_cm` | Bust girth, field `upper`. |
| `waist_cm` | Waist girth. |
| `high_hip_cm` | High-hip girth, field `highHips`. |
| `hips_cm` | Hip girth. |
| `label` | Expected label id. |
| `stability_radius_cm` | Single-field stability radius in cm; `0` means the input sits on a rule boundary. |
| `reachable_labels` | Semicolon-separated label ids reachable at that radius; empty if none. |
| `note` | Human-readable remark. |

All fields are quoted; rows end with LF; the file is UTF-8 without BOM.

## Rule order and thresholds

1. Inverted triangle: `bustToHip > 1.05` (strict).
2. Pear: `bustToHip < 0.95` (strict).
3. Apple: `0.95 ≤ bustToHip ≤ 1.05` and `waistToHip ≥ 0.88` (inclusive).
4. Hourglass: `0.95 ≤ bustToHip ≤ 1.05`, `waistToHip ≤ 0.80`, `highHipToHip ≤ 0.95` (inclusive).
5. Rectangle: all remaining balanced cases.

Display/implementation constants: `VERY_CLOSE_CM = 1`, `HIDE_PROXIMITY_CM = 3`,
`MAX_STABILITY_CM = 60`, `RADIUS_PRECISION_CM = 0.01`.

The stability radius shifts one field at a time (bisection, quantized to
0.01 cm); it is a geometric distance, not a probability or measurement-error
model.

## Known representation note

Ratios are compared exactly in v2 (no unit-round-trip tolerance). A boundary
value such as `0.95` can differ by a floating-point epsilon after cm→in→cm
conversion in other languages; the published vectors use the site's exact cm
comparison. This is documented behavior, not a hidden tolerance.

## Position prompts

Vectors 11 and 12 trigger measurement-position prompts (high hip above hips, or
high hip at/below waist). The label still uses the entered value; the prompt is
not a medical warning.

## Verification

Run `sha256sum -c SHA256SUMS` in this directory.

Regeneration and cross-checks run in the site repository
(`scripts/analysis/gen-alg-vectors.mjs`, `scripts/analysis/check-alg-vectors.mjs`,
`pnpm verify:rules`). After any rule change, update this CSV, the site CSV and
the schema together, and raise the algorithm version.
