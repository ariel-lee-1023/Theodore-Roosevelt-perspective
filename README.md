# Theodore-Roosevelt-perspective

A distilled **perspective skill** for LLM agents: reason and write about public duty, government and
business, war and preparedness, character and effort, executive action, and the settlement of the
American continent the way Theodore Roosevelt (1858–1919) does — take the question, strip the
claimant's class or party badge off it, ask whether the thing proposed is *decent* and whether it is
*practicable*, translate every fine sentiment into the deed and the machinery it would require, and
then say plainly what the duty is and who has to do it.

The skill is written in English, in the first person, as a voice rather than a set of instructions
about a voice. It is designed to be dropped into any agent that supports file-based skills, or
pasted in as a system prompt.

It was produced with [persona-distiller](https://github.com/ariel-lee-1023/persona-distiller) from
roughly 2.53M tokens of source material, 1.12M words of it Roosevelt's own.

---

## Repository layout

```
Theodore-Roosevelt-perspective/
├── SKILL.md                                       # the core persona — self-contained
├── references/
│   ├── clusters/
│   │   ├── c01-strenuous-life.md                  # public doctrine 1899–1901: exhortation, national
│   │   │                                          #   duty, war and expansion argued to an audience
│   │   ├── c02-formation-and-private-record.md    # boyhood, the Assembly, the ranch; and the terse
│   │   │                                          #   1877–1886 diaries as the private extreme
│   │   ├── c03-executive-apprenticeship-and-1898.md # Civil Service, Police, Navy, Albany, Cuba
│   │   ├── c04-the-presidency.md                  # trusts, labor, conservation, Panama, the courts,
│   │   │                                          #   foreign policy, stewardship
│   │   ├── c06-winning-of-the-west-i-iii.md       # settlement as narrative history — the thesis,
│   │   │                                          #   the backwoodsmen, the Revolution in the West
│   │   ├── c07-winning-of-the-west-iv.md          # Louisiana, the Mississippi question, the later
│   │   │                                          #   Indian wars
│   │   └── c08-letters-to-his-children.md         # writing to a child — a separate register family
│   ├── frameworks.md                              # named constructs and standing verdicts (lookup)
│   └── voice.md                                   # the measured expressive system — load before
│                                                  #   sustained prose
├── fidelity-ledger/
│   ├── provenance.md                              # honesty ledger: element → source → score → gate
│   │                                              #   status; human-facing, never loaded at runtime
│   └── episodic.md                                # attested one-off happenings not used as anchors
├── fidelity.json                                  # machine-readable twin of the ledger's test results
├── CHANGELOG.md
├── LICENSE
├── NOTICE.md
└── README.md
```

`SKILL.md` alone is enough for most questions. Load a reference file only when a register needs finer
grain — the loading hints are at the bottom of `SKILL.md`.

`frameworks.md` and `voice.md` are the two **standing modules**: what the person thinks with, and how
the person sounds. The core carries only enough style to *frame* an answer in the voice, not enough
to *write* one at length — so **load `voice.md` before writing more than a paragraph or two of
sustained prose in this voice.** It holds the three register families, the trigger→shift modulation
rules, the avoid-list, and the measured `style_metrics` baselines the style-match test compares
against.

The cluster numbering has gaps because eleven segmented clusters produced seven modules. `c02`
absorbs the diaries, `c03` absorbs *The Rough Riders*, `c06` absorbs *The Winning of the West*
volumes II–III. Each merged module declares both cluster ids so the provenance tags in
`frameworks.md` still resolve.

---

## Usage

### As a Claude / Agent Skill

Clone the repository into your skills directory. The repository name already matches the skill name,
so `SKILL.md` lands at the root of a correctly named folder:

```bash
git clone https://github.com/ariel-lee-1023/Theodore-Roosevelt-perspective.git \
  ~/.claude/skills/Theodore-Roosevelt-perspective
```

The agent reads the YAML frontmatter in `SKILL.md` to decide when to trigger, then pulls the
reference files on demand.

### As a plain system prompt

Paste the body of `SKILL.md` (everything after the frontmatter) as your system prompt. Append one or
two reference files when the topic calls for them. Do not paste `fidelity-ledger/provenance.md` or
`fidelity-ledger/episodic.md` into the prompt — they are metadata about the distillation, and putting
them in context degrades the voice.

---

## Design notes

Five constraints shaped this version, and they are worth knowing before you edit it.

**The coinages are rare and must stay rare.** This is the single most important thing about imitating
Roosevelt, and almost every imitation gets it backwards. Across 1.12M words of his own writing, *the
strenuous life* appears 6 times, *the square deal* 12, *the big stick* 6, *ignoble ease* 4, *peace at
any price* twice, *the man with the muck-rake* once. *Malefactors of great wealth* and *New
Nationalism* appear **zero** times and are excluded from this package entirely. What he actually
lives in is plain: *duty* 275, *efficiency* and its family 185, *practical* and its family 184,
*decency* 86, *righteousness* 52, *manliness* 54, *self-respect* 34. A copy that opens every
paragraph with a coinage is not talking like Roosevelt; it is talking like a man who has read about
Roosevelt. The core states these counts and forbids the decoration.

**Refusals carry the identity.** The section *What I will not concede* is the centre of gravity: nine
positions the persona holds at a cost — enforcing the law with no protected class when party
influence expects otherwise, refusing to trade appointments for party reward, taking neither labor
nor capital as a client, giving corporations their exact rights and no more, refusing peace at any
price, refusing to put down a responsibility once acquired, stopping violence *before* bargaining
over its grievances, going through formal channels to make a command failure public when silence
would have been comfortable, and refusing to recode continental conquest as something other than
conquest. A copy that keeps the vocabulary and drops the refusals is not this persona.

**Contestation lengthens the sentence.** The reflex assumption is that an angry Roosevelt gets
clipped and staccato. He does the opposite: booster-bearing sentences run 38.79 words against 31.36,
and contestation-marker sentences 37.86 against 29.43. Under challenge the sentence has to carry the
opposing error, the condition and the imperative before the verdict falls, so it expands. Any
imitation that tightens under pressure has the modulation backwards.

**Three register families, and the gaps are the fingerprint.** First-person witness and advocate
(the speeches, the autobiography, the war narrative), third-person narrative history (*The Winning of
the West*), and letters to his children. Second-person reference runs 4.82 / 16.01 / 136.18 per 10k
words across them — a 28× spread. First-person runs 43.29 / 367.35 / 419.32. Semicolons roughly
double in the narrative history. An imitation that hits the means and flattens those gaps is not this
voice. The full table is in `references/voice.md`; a blind discrimination test scored 0.90 on
separating them.

**The unpleasant material is recorded, not softened.** Roosevelt's reading of continental conquest as
a test of a "vigorous and masterful race" is load-bearing for how he narrates the West, and it is
kept. Removing it would produce a fluent persona that agrees with a modern reader and is not the
subject. `NOTICE.md` states the position; this is documentation, not endorsement.

### Factual cutoff

The reasoning posture is time-independent. The *facts* are not. The firsthand corpus runs **1877–1913**
— diaries 1877–1886, the frontier history 1889–1896, the speeches and essays 1899–1901, the war
narrative 1899, the letters to the children 1898–1911, the autobiography 1913 — with nothing from
1887–1888 and nothing after 1913. The 1912 Progressive campaign, the European war, the postwar
settlement, and everything since fall outside it.

Host agents should **retrieve current facts first, then let the persona digest them through its
frameworks.** The voice is confident and fond of pronouncement, so this guard matters more here than
it would for a neutral assistant. `SKILL.md` part (4) of the loading note states the rule in the form
the host agent needs.

---

## Provenance and honesty

`fidelity-ledger/provenance.md` is an audit trail rather than documentation: all 48 core elements are
logged with source cluster, composite score, projection probe and cost-gate status, alongside the
weights used, the computed and realised budgets, the register distance matrix, every test result, and
an append-only batch log with a mandatory *not re-tested* field. It also records what was demoted and
where it went. `fidelity.json` carries the same test results in machine-readable form.

Headline results, all recorded with their limitations in the ledger: projection gate 0.875
(hit_2 0.75), final projection 0.958 (hit_2 0.917) on the same mask and graded non-blind; register
discrimination 0.90, separable; cost presence assertion pass, with 2 of 14 divergence pairs elevated
and 1 logged out; name audit pass on all 16 names, 9 of them thin; style-match reproduces the
contestation modulation to within a rounding error but over-boosts by 2.1–3.7× and runs 10–17% short
on sentence length. Four clusters received no masked projection item and are correspondingly less
well tested. `validate_package.py` passes with 0 errors and 0 warnings.

If you fold new material in, extend that ledger — the point of keeping it is that the distillation
stays checkable.

Roosevelt's own writing is public domain; the specific editions used are listed in `NOTICE.md`. The
corpus itself is not included in this repository and is excluded by `.gitignore`. One secondhand
biography was consulted for episodic and factual context only and was excluded by instruction from
all voice work.

## Contributing

Issues and pull requests are welcome, particularly for: the untested domains named above (the *Rough
Riders* narrative, the 1877–1886 diaries), a fold-in of the post-1913 material that would close the
temporal gap, an explicit booster budget in `voice.md` to correct the over-emphasis the style-match
test found, and an independently graded projection re-run on a fresh mask. Please update
`CHANGELOG.md` and `fidelity-ledger/provenance.md` alongside any change to `SKILL.md`.

---

MIT © 2026 Ariel Lee. [See LICENSE](LICENSE).

This license covers the original text in this repository. It does not extend to any referenced source
works, which remain the property of their respective copyright holders where copyright subsists.
