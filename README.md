# Bodytype research

Public, reproducible research artifacts for [Bodytype.org](https://bodytype.org)'s
deterministic body type styling rules.

## Current release

| Release | Tag | Contents |
| --- | --- | --- |
| Algorithm v2 test vectors 1.0.0 | `algorithm-v2-v1.0.0` | Method summary, 15 synthetic test vectors, JSON schema |

The narrative method page is the canonical source:
<https://bodytype.org/research/bodytype-algorithm-v2>

## What this repository is

`algorithm-v2/` documents the v2 rule set itself: the four girth inputs, three
ratios, five ordered rules, threshold constants, equality semantics, and 15
synthetic test vectors with their expected labels and single-field stability
radii. The CSV here is byte-identical to the site download at
`https://bodytype.org/data/research/bodytype-algorithm-v2/test-vectors.csv`.

## How it differs from the boundary sensitivity dataset

The separate repository
[`bodytype-boundary-sensitivity`](https://github.com/TSjianjiao/bodytype-boundary-sensitivity)
and its Zenodo record (concept DOI `10.5281/zenodo.24283465`) contain a
669,858-point synthetic rule-space scan that measures how often ±0.5/±1/±2 cm
shifts change the label. This repository is the rule definition and a small
reproducible vector set; the other is a large-scale sensitivity scan. They share
the same v2 thresholds but are different artifacts with different DOIs. Neither
contains user measurements.

## Files

- `algorithm-v2/test-vectors.csv` — 15 vectors, all fields quoted, UTF-8, LF.
- `algorithm-v2/schema.json` — column definitions and `algorithm_version: "2"`.
- `algorithm-v2/README.md` — columns, thresholds, rule order, regeneration notes.
- `algorithm-v2/SHA256SUMS` — checksums for the three files above.

## Licenses

- Documentation and any code: MIT (`LICENSE`).
- Synthetic data, tables and figures: CC BY 4.0 (`LICENSE-DATA`).

Any reuse must credit **Bodytype.org** and link to <https://bodytype.org>.

## Citation

See `CITATION.cff`. Zenodo version DOI: `10.5281/zenodo.24304074` (concept DOI
`10.5281/zenodo.24304073`). Record: <https://zenodo.org/records/24304074>.
The GitHub release tag is `algorithm-v2-v1.0.0`.

## Scope and limits

Deterministic styling rules, not a trained model, not an ASTM/FFIT/BSAS
classification, and not a medical or health assessment. The method page received
an internal method review; it is not external peer review or professional
certification. No user measurements are included.
