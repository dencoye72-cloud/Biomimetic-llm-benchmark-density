# biomimetic-llm-benchmark-density

**Biomimetic Ecological Anchoring — Prompt Engineering Benchmark for Local LLMs**

Denis Coyaud — Independent Research, Architecte IA (Jedha Bootcamp)

---

## Overview

This repository contains all materials for the **biomimetic prompt engineering** research series. The core idea: instead of instructing a language model to "be concise," we ask it to behave as a marine organism whose natural biology embodies conciseness (e.g., a sponge that filters passively, with no brain and no verbosity).

The framework introduces:
- A **Core Marine 11** — 11 marine organisms each targeting a specific LLM behavioral defect
- A **toxic mirror set** — 9 non-marine animals used as negative controls to amplify defects
- A **bidirectional validation** methodology: if both directions (positive + toxic) show consistent effects, the metaphor mechanism is causal

---

## Papers

### v1 — Bidirectional Validation (Published)
*Biomimetic Ecological Anchoring: Bidirectional Validation of Metaphor-Driven LLM Behavior Across 9 Models*

22,336 tests — 9 models (6 local, 3 API) — 25 configurations — 100 questions
Main result: bidirectional validation confirmed, Cohen's d = 1.41 on defects (p < 10⁻³⁰⁰)

### v2 — Prompt Density Effect (This release)
*Biomimetic Prompt Density Has No Meaningful Effect on 8B Local Models: A Paired Comparison Across 6 Models and 30–35 Configurations*

78,000 tests — 6 local 8B models — 30 configs (condensed) / 35 configs (enriched) — 200 questions
Main result: enrichment produces no meaningful effect — Cohen's d = −0.013 on quality composite.
The ceiling is in instruction-following capacity, not prompt density.

---

## Repository Contents

| File | Description |
|---|---|
| `Biomimetic Prompt Density Has No Meaningful Effect on 8B Local_v2_paper.pdf` | Full paper — v2 |
| `Biomimetic Prompt Density Has No Meaningful Effect on 8B Local_v2_appendices.pdf` | Appendices A–H — prompts, questions, results, figures, statistics |
| `Data v2.3.zip` | Dataset — condensed condition (dataset_500q.py, 500 questions, 10 anchors) |
| `Data v2.4.zip` | Dataset — enriched condition (same questions + enriched prompt configs) |
| `Resultats v2.3.zip` | CSV results — v2.3 condensed (6 models × 30 configs × 200 questions) |
| `Résultats v2.4.zip` | CSV results — v2.4.1 enriched (6 models × 35 configs × 200 questions) |
| `Biomimetic_benchmark_Python_v2.3.zip` | Python scripts — condensed benchmark pipeline |
| `Biomimetic_benchmark_Python_v2.4.zip` | Python scripts — enriched benchmark pipeline (patched) |

---

## Models Tested (v2)

| Model | Provider | Size | Type |
|---|---|---|---|
| Llama 3.1 8B | Meta | 8B | Dense |
| Gemma 2 9B | Google | 9B | Dense |
| Qwen3 8B | Alibaba | 8B | Dense |
| Granite 3.3 8B | IBM | 8B | Dense |
| Ministral 3 8B | Mistral AI | 8B | Dense, 256k ctx |
| DeepSeek-R1 8B | DeepSeek | 8B | Reasoning (`<think>` filtered) |

All models run locally via Ollama on a single RTX 4060 8GB. Zero cloud dependency.

---

## Core Marine 11

| # | Organism | Biological Mechanism | LLM Defect Targeted |
|---|---|---|---|
| 1 | Sponge (Éponge) | Passive filtration, no brain | Verbosity |
| 2 | Jellyfish (Méduse) | Binary reaction in 10ms | Equivocation |
| 3 | Swordfish (Espadon) | Direct rostrum at 100 km/h | Digressions |
| 4 | Stonefish (Poisson-pierre) | Immobility = survival | Hallucination |
| 5 | Snapping Shrimp (Synalpheus) | 218 dB pistol snap, sentinel | Blind submission |
| 6 | Octopus (Poulpe) | 8 semi-autonomous arms | Repetition |
| 7 | Clownfish (Némo) | Maximum visibility | Jargon |
| 8 | Sea Turtle (Tortue) | Temporal navigation | Anachronism |
| 9 | Cuttlefish (Seiche) | 10⁶ chromatophore combinations | Stereotypy |
| 10 | Dolphin (Dauphin) | Context-adaptive echolocation | Universalism |
| 11 | Argonaut | Shell created only when needed | Structural rigidity |

---

## Key Results — v2

### Density Effect (main hypothesis)
| Metric | Condensed | Enriched | Cohen's d | Verdict |
|---|---|---|---|---|
| Quality Composite | 0.713 | 0.707 | −0.013 | Negligible |
| GT Exact Match | 0.953 | 0.926 | −0.111 | Negligible |
| GT Hallucination | 0.512 | 0.515 | +0.005 | No effect |
| Total Defects | 0.496 | 0.639 | +0.221 | Small (enriched worse) |

### Bidirectional Signal (stable across densities)
| Condition | Positive defects | Toxic defects | Cohen's d |
|---|---|---|---|
| v2.3 condensed | 0.29 | 0.97 | 1.32 |
| v2.4.1 enriched | 0.54 | 1.30 | 1.29 |

### Top Configuration
**poisson_pierre_meduse** (series architecture: stonefish + jellyfish) — top QUAL in both density conditions.
GT Hallucination: 0.793 (condensed), 0.737 (enriched) vs vanilla 0.547/0.490.

---

## Technical Notes

**DeepSeek-R1 8B:** internal `<think>...</think>` block filtered via regex before evaluation. Token count computed as word count post-filter.

**Ministral 3 8B:** 2 toxic configurations (`toxic_paire_perroquet_poulpe`, `toxic_paire_mouton_singe`) generated pre-patch — excluded from cross-model token comparisons. GT metrics unaffected.

**num_predict cap:** `num_predict: 1024` applied uniformly in v2.4.1 to prevent generation freeze on toxic triple configurations.

---

## Pipeline Scripts

```
1_   — Dataset preparation
2_   — Ecological prompt testing
3_   — Baseline testing
4_   — Ground truth evaluation
5_   — Paired test runner (main)
6_   — Paired analysis
7_   — Detector sensitivity analysis
8_   — Anchor depth analysis (condensed vs enriched comparison)

config_models.py          — Model configuration + Ollama calls
config_prompts.py         — Condensed system prompts (v2.3)
config_prompts_full.py    — Enriched system prompts (v2.4.1)
ground_truth_meduse.py    — GT Decision scoring
ground_truth_synalpheus.py — GT Correction + GT Hallucination scoring
metrics_analysis.py       — Aggregation and statistical analysis
dataset_500q.py           — 500-question pool (10 anchors × 50)
```

Reproducible: `random.seed(42)` throughout. All runs local, zero external API calls.

---

## Roadmap

| Paper | Variable | Status |
|---|---|---|
| v1 | Bidirectional validation — 9 models | Published |
| v2 | Prompt density — 6×8B | This release |
| v3 | Model size — 3×8B vs 3×14B | In progress |
| v4 | RAG local empirical | Planned |
| v5 | Frontier effect — GPT-4o | Planned |
| v6 | Dataset bestiaire — DOI | Planned |

---

## Citation

```
Coyaud, D. (2026). Biomimetic Prompt Density Has No Meaningful Effect on 8B Local Models:
A Paired Comparison Across 6 Models and 30–35 Configurations. Independent Research.
```

---

## License

This work is licensed under **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)**.

You are free to share and adapt the material for non-commercial purposes, provided you give appropriate credit and distribute any derivatives under the same license.

Full license: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

---

*Pores ouverts. Pince armée. Canaux propres.*
