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
The ATLAS code release provides the model checkpoints and an executable Python inference notebook for generating evidence-linked fetal-head biometry outputs. The notebook documents preprocessing, checkpoint loading, inference settings, input requirements, and output schema. The model-development, training, cohort-construction, and data-integrity pipelines are not included in the public release.

### Inference

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

## Data availability

The repository does not redistribute third-party fetal-ultrasound datasets.

The HC18 source-domain benchmark and the external FP/UCL resources should be obtained from their original public repositories and used according to their respective terms and licences. Dataset-specific preparation instructions and expected directory structures should be documented separately in `data/README.md`.

Users are responsible for complying with the original dataset licences and terms of use.


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
