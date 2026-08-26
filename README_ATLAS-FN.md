# ATLAS-FN

**ATLAS-FN** is a reproducibility repository for the manuscript describing an AI-enabled, evidence-traceable framework for fetal-head ultrasound biometry.

ATLAS-FN is organized around a **Find–Confirm–Measure** workflow:

- **Find** localizes the fetal cranial region.
- **Confirm** records selected anatomical evidence, including the cavum septi pellucidi (CSP) and lateral ventricle (LV).
- **Measure** derives fetal-head biometry, including biparietal diameter (BPD), occipitofrontal diameter (OFD), and head circumference (HC).
- A linked evidence/provenance record preserves the processing states supporting each output.

This repository provides the computational notebooks used for data preparation, model development, locked internal evaluation, external evaluation, site-specific adaptation/model aggregation, and inference.

> **Scope:** ATLAS-FN is evaluated as a retrospective static-image methodological framework. The repository does not establish diagnostic accuracy, prospective clinical effectiveness, or autonomous assessment of complete clinical plane adequacy.

---

## Notebook workflow

Run the notebooks in the order shown below where the required source data and trained checkpoints are available.

| Notebook | Purpose | Main outputs |
|---|---|---|
| `01_DataPrep` | Data preparation, provenance checks, dataset reconciliation, and patient-/subject-exclusive partitioning | Analysis-ready datasets, split manifests, data-integrity outputs, scale/provenance fields |
| `02_CheckpointTraining` | Training and checkpoint generation for the Find, Confirm, and Measure components | Locked model checkpoints, training logs, model configurations |
| `03_MasterEvidence` | Primary internal evidence generation and locked-test evaluation across the Find–Confirm–Measure pathway | Internal localization, anatomical-evidence, biometry, availability, and provenance results |
| `04_ExtendedEvidence_TIES` | External evaluation, site-specific adaptation, and exploratory data-free parameter aggregation using TIES | FP/UCL external results, adaptation analyses, TIES aggregation and sensitivity analyses |
| `06_Inference` | Applies the locked ATLAS-FN components to eligible ultrasound frames and produces evidence-linked outputs | Per-frame Find, Confirm, Measure, scale/provenance, and output-availability records |

### 01 — Data preparation

The first notebook prepares the public fetal-ultrasound resources for ATLAS-FN analysis. It performs dataset reconciliation and integrity checks, links images to subject and reference information, validates identifiers, preserves annotation provenance, and constructs patient-/subject-exclusive partitions.

It also handles physical image scale. Where valid pixel-spacing metadata are available, these are retained. Where the prespecified fallback is used, the scale source is explicitly recorded rather than silently substituted.

**Key reproducibility outputs include:**

- subject and frame identifiers;
- train/validation/locked-test assignment;
- image/reference linkage;
- annotation provenance;
- pixel-spacing value and source;
- data-integrity and exclusion/reconciliation records.

---

### 02 — Checkpoint training

The second notebook trains the models used by the three ATLAS-FN components and records the final training configuration.

It includes:

- **Find:** YOLO-family fetal-head localization;
- **Confirm:** staged CSP/LV anatomical-evidence detection;
- **Measure:** segmentation-derived head geometry used for BPD/OFD/HC estimation.

The manuscript-associated checkpoints are identified by filename and cryptographic hash in the accompanying reproducibility material. Validation/checkpoint selection is kept separate from locked-test evaluation.

> The reported training environment and the hardware used for manuscript inference/runtime profiling are distinct and should not be interpreted as the same execution environment.

---

### 03 — Primary internal evidence and evaluation

The third notebook generates the principal evidence used for the locked internal evaluation of ATLAS-FN.

It links stage-specific outputs so that each measurement can be traced to:

1. cranial localization;
2. selected CSP/LV evidence;
3. measurement geometry;
4. physical scale;
5. checkpoint/model provenance; and
6. output-availability status.

The notebook supports the manuscript analyses of localization performance, Confirm performance, deterministic versus segmentation-derived biometry, and evidence-conditioned measurement performance.

**Important provenance note:** any post-development reconstruction, consistency, or drift-audit routines retained in this notebook are documented as audit procedures and should not be interpreted as primary model or hyperparameter selection on the locked test set.

---

### 04 — External evaluation, adaptation, and TIES

The fourth notebook extends evaluation beyond the development source.

It contains:

- external evaluation on the prespecified **FP** and **UCL** cohorts;
- site-specific adaptation analyses;
- comparison of upstream localization and downstream biometric performance after adaptation;
- exploratory data-free parameter aggregation using **TIES**; and
- sensitivity analyses across aggregation density settings.

These analyses are secondary technical evaluations. They do **not** establish multi-site clinical deployment readiness, privacy guarantees, or clinical effectiveness.

---

### 06 — Inference

The inference notebook is the practical entry point for applying the locked ATLAS-FN pipeline to eligible ultrasound frames.

Its intended role is to load the selected Find, Confirm, and Measure checkpoints, apply the prespecified preprocessing and inference settings, and return an evidence-linked record for each frame.

The output record is designed to retain, where applicable:

- source dataset / subject / frame identifiers;
- Find availability, localization and confidence;
- CSP/LV evidence status and confidence;
- measurement method and geometry;
- pixel spacing and scale provenance;
- BPD, OFD, and HC;
- checkpoint/model provenance; and
- final output-availability status.

Find/Confirm confidence values are computational scores and are **not** presented as calibrated clinical probabilities.

---

## Why notebook `05` is not included

The publication repository uses notebooks **01–04 and 06**. Notebook `06` is the dedicated inference notebook and replaces the earlier manuscript-reconstruction notebook that occupied the `05` position during development.

The numbering is retained to preserve correspondence with the final computational workflow and development record.

If a continuous public-facing numbering scheme is preferred, `06_Inference` can instead be renamed `05_Inference` before the first archived release. Once a DOI-linked release is created, filenames should remain stable.

---

## Recommended execution sequence

```text
01_DataPrep
    ↓
02_CheckpointTraining
    ↓
03_MasterEvidence
    ↓
04_ExtendedEvidence_TIES

For application of locked models to eligible images:
02_CheckpointTraining / released checkpoints
    ↓
06_Inference
```

The external/adaptation notebook is not required for routine inference.

---

## Data availability

The repository does not redistribute third-party fetal-ultrasound datasets.

The HC18 source-domain benchmark and the external FP/UCL resources should be obtained from their original public repositories and used according to their respective terms and licences. Dataset-specific preparation instructions and expected directory structures should be documented separately in `data/README.md`.

Users are responsible for complying with the original dataset licences and terms of use.

---

## Model checkpoints

Where redistribution is permitted, the manuscript-associated locked checkpoints should be released with:

- checkpoint filename;
- model/component name;
- software version;
- inference operating point;
- SHA-256 checksum; and
- manuscript/release version.

If checkpoint redistribution is restricted by source-model or dataset terms, the repository should instead provide the training configuration and instructions required to regenerate them where legally permitted.

---

## Reproducibility and interpretation

The notebooks are intended to reproduce the computational workflow reported in the manuscript. They should be interpreted together with the manuscript and supplementary methodological material.

In particular:

- patient/subject separation is maintained between development and locked evaluation;
- external FP/UCL evaluation is kept separate from source-domain development;
- reference annotations are used for evaluation rather than supplied to locked inference;
- CSP/LV evidence does not constitute independent confirmation of complete ISUOG plane adequacy;
- fixed inference thresholds are computational operating points, not clinical decision thresholds;
- formal probability calibration was not performed; and
- site adaptation and TIES aggregation are secondary technical analyses rather than evidence of clinical deployment readiness.

---

## Citation

If you use ATLAS-FN, please cite the associated manuscript and the archived software release.

**Manuscript citation:**  
*To be added following publication.*

**Software archive / DOI:**  
*To be added after the manuscript-associated GitHub release is archived in Zenodo.*

---

## License

*To be confirmed before the manuscript-associated release.*

The software licence applies only to code for which the authors hold redistribution rights. Third-party datasets, pretrained models, and other external resources remain subject to their original licences and terms.

---

## Contact

For questions about the computational workflow or reproducibility package, please use the repository issue tracker or contact the corresponding author listed in the manuscript d.tjondronegoro@griffith.edu.au
