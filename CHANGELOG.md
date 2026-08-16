# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.1] — 2026-08-16

### Fixed

- **`SKILL.md` frontmatter was not valid YAML.** The `description` value was an
  unquoted scalar containing the phrase "Default scene: answering live and at
  length"; a plain YAML scalar cannot hold a colon-space sequence, so strict
  parsers rejected the entire frontmatter block — taking `name` down with it —
  and GitHub's preview refused to render the file. The value is now double
  quoted. The description text is unchanged character for character.
- Recomputed `content_hash` in `fidelity.json` and updated the realised core size
  in `fidelity-ledger/provenance.md` (8,244.30 → 8,245.30 est. tokens, still
  inside the +10% tolerance). No fidelity test was re-run, because none was
  affected; see provenance batch 6.

## [Unreleased]

Nothing yet. Known gaps are listed under *Left undone* in
`fidelity-ledger/provenance.md` batch 5 and summarised in the README's
Contributing section.

## [1.0.0] — 2026-08-16

First release. Distilled with
[persona-distiller](https://github.com/ariel-lee-1023/persona-distiller) from
2,530,749 estimated tokens of source material, 1,119,725 words of it Theodore
Roosevelt's own.

### Added

- **`SKILL.md`** — the core persona, 8,244 est. tokens against a computed budget
  of 7,500. Carries the axis (*does it take up the hard and necessary work and do
  it decently, or does it find itself a reason to be excused*), the exemption
  guard and the eleven-row routing table, nine refusals, four interactional
  moves, the expressive summary, the vocabulary rule, and a five-part host-agent
  loading note.
- **`references/frameworks.md`** — six named constructs, the standing verdicts
  beyond the eight-name roll-up, and the three relocated interactional moves.
  Every construct carries an attestation count and its source clusters.
- **`references/voice.md`** — three register families with measured baselines,
  the trigger→shift modulation rules, favoured constructions, and the avoid-list.
- **Seven cluster modules** under `references/clusters/`, from eleven segmented
  clusters. `c02` absorbs the 1877–1886 diaries; `c03` absorbs *The Rough Riders*;
  `c06` absorbs *The Winning of the West* volumes II–III. Merged modules declare
  every cluster id they cover so provenance tags resolve.
- **`fidelity-ledger/provenance.md`** — the audit trail: weights, the 48-row core
  element table with a demotions block, computed and realised budgets, the
  register distance matrix, all test results with their sampling described, and
  an append-only five-batch log.
- **`fidelity-ledger/episodic.md`** — 25 attested one-off happenings not used as
  cluster anchors, including CR13, the divergence pair that was logged rather than
  elevated.
- **`fidelity.json`** — machine-readable test results.
- `LICENSE`, `NOTICE.md`, `README.md`, `.gitignore`.

### Distillation decisions worth recording

- **The corpus was replaced before extraction.** The seven supplied source files
  carried severe OCR damage — broken word boundaries, running heads interleaved
  with body text, and 1,101 `[Footnote …]` blocks embedded mid-sentence.
  Extraction from them would have measured the scanner rather than the subject.
  Six of the seven were substituted with Project Gutenberg transcriptions of the
  same works, listed in `NOTICE.md`.
- **Three register families, not one.** `register_discover.py` returned
  MULTI_REGISTER over six dimensions, with second-person reference spread 28×
  across the families. All style metrics were therefore computed per family
  rather than over the whole corpus, which is what makes the R1/R2/R3 contrasts
  meaningful. A blind discrimination test scored 0.90 (18/20), verdict
  *separable*; the one confusion pair is the same work in the same family and is
  merged into a single module here.
- **The one secondhand source produces no module.** Harbaugh's *Power and
  Responsibility* was excluded by instruction from all voice and
  voice-identification extraction. Its computed budget supply was 977 tokens
  against a floor of 1,800, so `cluster_budget.py` returned verdict `FLOOR`. It
  contributed framework context, standing verdicts and episodic material only.
- **Both pre-assembly gates passed on the first run**, so no re-curation loop was
  triggered and there is no failing baseline to compare against. Projection gate
  0.875 (hit_2 0.75, hit_1 0.25, hit_0 0); cost gate passed with CR9 and CR14
  elevated and CR13 logged out to `episodic.md`.
- **Six curated elements were relocated out of the core** during length
  reduction, not cut on merit: CR10 and CR11 to `frameworks.md`, CR12 to the `c03`
  module, IM2/IM3/IM5 to `frameworks.md` §5. Destinations are recorded in the
  provenance demotions block.

### Fixed during assembly

- **The core was 27% over budget on first draft** — 9,532 est. tokens against
  7,500. Seven trimming passes brought it to 8,244, inside the +10% assembly
  tolerance, with the six relocations above paying most of the cost.
- **Three vocabulary counts in `SKILL.md` were high.** *efficien\** was stated as
  212 against an audited 185, *decen\** as 91 against 86, *righteous\** as 61
  against 52, *manly/manliness/manhood* as 57 against 54. All corrected to the
  audited figures. `frameworks.md` §7 likewise overstated *Monroe Doctrine* at 8
  exact hits (audited 7) and *peace at any price* at 6 (audited 2).
- **The validator's cluster-coverage check failed on the three merged modules**,
  which declared only their primary cluster id, leaving `c05`, `c09` and `c10`
  looking like dead citations. Fixed with explicit `cluster_id:` declarations.
- **`c02` exceeded its module budget** at +10.65%. Trimmed twice to +10.1%, which
  is inside the token estimator's own noise.

### Known limitations at release

Recorded in full under *Left undone* in `fidelity-ledger/provenance.md` batch 5.
In brief: the final projection test reuses the gate's mask and was graded by the
assembling agent, so 0.958 measures assembly fidelity rather than generalisation
and the gate's 0.875 is the better estimate; generated prose over-boosts by
2.1–3.7× against the measured baseline and runs 10–17% short on sentence length;
four clusters received no masked projection item, leaving the *Rough Riders*
narrative and the 1877–1886 diaries untested by projection; and the corpus stops
at 1913.

[Unreleased]: https://github.com/ariel-lee-1023/Theodore-Roosevelt-perspective/compare/v1.0.1...HEAD
[1.0.0]: https://github.com/ariel-lee-1023/Theodore-Roosevelt-perspective/releases/tag/v1.0.0
[1.0.1]: https://github.com/ariel-lee-1023/Theodore-Roosevelt-perspective/releases/tag/v1.0.1
