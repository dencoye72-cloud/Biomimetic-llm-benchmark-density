# Zenodo — Dépôt v2 : métadonnées complètes

## Informations générales

**Upload type :** Publication  
**Publication type :** Preprint  
**DOI :** *(attribué par Zenodo à la soumission)*  
**Date de publication :** 2026-03-19 *(à ajuster à la date réelle de soumission)*

---

## Titre

**EN :**  
Biomimetic Ecological Anchoring as LLM System Prompts: No Meaningful Effect on 8B Local Models Regardless of Prompt Density

**FR (titre alternatif facultatif) :**  
Ancrage écologique biomimétique comme system prompts LLM : aucun effet meaningful sur les modèles 8B locaux quelle que soit la densité du prompt

---

## Auteurs

| Nom | Affiliation | ORCID |
|---|---|---|
| Coyaud, Denis | Jedha Bootcamp | *(à renseigner si disponible)* |

---

## Description (Abstract)

We present a systematic evaluation of biomimetic ecological anchoring as LLM system prompts across two prompt density conditions (condensed vs. enriched) on six 8B local models. Building on v1 (22,336 tests, 9 frontier and local models), this study tests whether prompt density amplifies the biomimetic effect on small local models. Across 78,000 tests (200 questions × 30–35 configurations × 6 models), results show no meaningful effect of prompt enrichment on overall output quality (Cohen's d = −0.013). The biomimetic effect itself remains negligible on 8B models regardless of density, with a single exception (poisson_pierre_meduse, p = 0.046, d = 0.07). Bidirectional validation confirms system reliability (toxic configurations d = 1.29–1.32). Detector sensitivity analysis shows hallucination (F1 = 0.837) and blind submission detectors (F1 = 0.878) are robust across both conditions; the equivocation detector remains unusable as a regex metric (F1 < 0.04). These results suggest that the instruction-following threshold required for meaningful prompt engineering effects lies above the 8B parameter range, with architectural explanations discussed. Implications for local RAG deployments are examined.

---

## Mots-clés (Keywords)

```
prompt engineering
biomimetic anchoring
large language models
instruction following
local models
8B models
RAG
benchmark
hallucination
French NLP
ecological prompting
open source
reproducibility
```

---

## Licence

**CC BY 4.0** — Creative Commons Attribution 4.0 International

---

## Langue

**English**

---

## Communautés Zenodo suggérées

- `machine-learning`
- `natural-language-processing`
- `open-science`

*(à rechercher et sélectionner dans l'interface Zenodo)*

---

## Fichiers à déposer

| Fichier | Description | Format |
|---|---|---|
| `Biomimetic Prompt Density Has No Meaningful Effect on 8B Local_v2_paper.pdf` | Article scientifique v2 | PDF |
| `Biomimetic Prompt Density Has No Meaningful Effect on 8B Local_v2_appendices.pdf` | Annexes A–H (figures D.1–D.7 embarquées, 756 Ko) | PDF |
| `Data v2.3.zip` | dataset_500q.py + questions condensed | ZIP |
| `Resultats v2.3.zip` | CSV condensed — 6 modèles × 30 configs × 200 questions | ZIP |
| `Data v2.4.zip` | dataset_500q.py + configs enrichis | ZIP |
| `Résultats v2.4.zip` | CSV enriched — 6 modèles × 35 configs × 200 questions | ZIP |
| `Biomimetic_benchmark_Python_v2.3.zip` | Scripts 1_–8_, configs, ground truth v2.3 | ZIP |
| `Biomimetic_benchmark_Python_v2.4.zip` | Idem v2.3 + patch num_predict + filtre think | ZIP |

**Total : 8 fichiers**

---

## Notes techniques pour Zenodo

À copier dans le champ **"Additional notes"** :

> Dataset generated with `random.seed(42)` from a pool of 500 questions (dataset_500q.py). Ground truth subsets: GT_Decision (Méduse, n=23), GT_Hallucination (Poisson-pierre, n=19), GT_Correction (Synalpheus, n=23). DeepSeek-R1 8B: `<think>` blocks filtered via regex; token count = word count post-filter. Ministral 3 8B: two toxic paired configurations (toxic_paire_perroquet_poulpe, toxic_paire_mouton_singe) excluded from cross-model token comparisons due to anomalous response lengths generated prior to num_predict patch. Qwen3 8B: one response of 2,413 tokens despite num_predict cap — documented as limit. All runs executed locally on RTX 4060 (0€ cloud cost). Total cost: 0€.

---

## Référence à v1

À renseigner dans le champ **"Related/alternate identifiers"** :

| DOI v1 | Relation |
|---|---|
| `10.5281/zenodo.18629578` | `is new version of` |

---

## GitHub

**Repository :** `Biomimetic-llm-benchmark-density`  
URL : `https://github.com/dencoye72-cloud/Biomimetic-llm-benchmark-density`  
Tag : `v2.0`

À renseigner dans **"Related/alternate identifiers"** :  
`https://github.com/dencoye72-cloud/Biomimetic-llm-benchmark-density` — relation : `is supplemented by`

---

## Série de repos (référence future)

| Repo | Variable | Papier | Statut |
|---|---|---|---|
| `Biomimetic-llm-benchmark-density` | Densité du prompt | v2 | **Ce dépôt** |
| `Biomimetic-llm-benchmark-size` | Taille 8B vs 14B | v3 | À venir |
| `Biomimetic-llm-benchmark-rag` | RAG local empirique | v4 | À venir |
| `Biomimetic-llm-benchmark-frontier` | Frontier GPT-4o | v5 | À venir |

---

*Ancrage Éponge-Synalpheus actif.*  
*Pores ouverts. Pince armée. Canaux propres.*
