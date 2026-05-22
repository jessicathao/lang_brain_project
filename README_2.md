# Emotional Language fMRI Decoding

> Decoding emotional valence from brain activity during naturalistic language comprehension — bridging linguistics, neuroimaging, and machine learning.

**Status:** In active development (Brainhack School 2026 final project)
**Author:** Thach Thao Le (Jessica) — PhD candidate, Linguistics, National Taiwan University

---

## Project Overview

This project investigates how the brain processes emotional content during naturalistic language comprehension by building an end-to-end fMRI brain-decoding pipeline. The core question: **can we predict the emotional valence of language stimuli from brain activity patterns alone?**

The pipeline combines three components:

1. **NLP-driven label generation** — A transformer-based sentiment classifier (BERT) automatically labels naturalistic language stimuli (sentences from open fMRI corpora) with emotional valence.
2. **fMRI feature extraction** — Brain activity patterns are extracted from open neuroimaging datasets using `nilearn`, focusing on language and emotion-relevant regions.
3. **Machine learning decoder** — SVM and MLP classifiers are trained to predict emotional valence from voxel-level brain activity, evaluated with cross-validation.

---

## Why This Matters

This work sits at the intersection of computational linguistics, cognitive neuroscience, and brain-computer interface (BCI) research:

- **Non-invasive brain decoding** — Demonstrates that meaningful affective brain states can be decoded from non-invasive fMRI signals, with direct conceptual relevance to BCI systems (e.g. Neuralink-style applications) which face the same fundamental problem at a different scale and resolution.
- **Addresses a data gap** — Most open fMRI datasets lack emotion labels, limiting their use in affective neuroscience research. Automated NLP labeling offers a scalable solution.
- **Linguistic representation** — Most neurolinguistic decoding research focuses on English. This project lays groundwork for extending to under-represented languages such as Vietnamese.

---

## Technical Stack

| Component | Tool |
|---|---|
| fMRI data handling | `nilearn`, `nibabel` |
| Sentiment labels | Hugging Face Transformers (BERT) |
| Machine learning | `scikit-learn` (SVM, logistic regression) |
| Deep learning | PyTorch (MLP) |
| Environment | Conda (Python 3.11), macOS Apple Silicon |
| Version control | Git / GitHub |

---

## Methodology

```
Open fMRI dataset
       │
       ▼
┌────────────────┐      ┌─────────────────────┐
│ Brain activity │      │ Linguistic stimuli  │
│  (voxel data)  │      │  (sentences/text)   │
└────────┬───────┘      └──────────┬──────────┘
         │                         │
         │                         ▼
         │              ┌─────────────────────┐
         │              │ BERT sentiment      │
         │              │ classifier          │
         │              └──────────┬──────────┘
         │                         │
         │                         ▼
         │              ┌─────────────────────┐
         │              │ Emotional valence   │
         │              │ labels              │
         │              └──────────┬──────────┘
         │                         │
         ▼                         ▼
       ┌─────────────────────────────┐
       │  SVM / MLP decoder          │
       │  (cross-validated)          │
       └──────────────┬──────────────┘
                      │
                      ▼
       Decoded emotional state from brain activity
```

---

## Roadmap

- [x] Project proposal and design
- [x] Tool selection (BERT for sentiment, SVM/MLP for decoding)
- [ ] Open fMRI dataset selection (candidates: LPPC-fMRI, Narratives, MOUS)
- [ ] BERT sentiment label generation on stimulus text
- [ ] Label validation on small annotated subset
- [ ] fMRI preprocessing and masking
- [ ] Decoder training and cross-validation
- [ ] Results visualization and statistical analysis
- [ ] Final report and Singapore symposium presentation
- [ ] Extension to multilingual / Vietnamese stimuli (future work)

---

## Background

This project builds on skills developed during **Brainhack School 2026** (NTU Taiwan):

- fMRI brain decoding with SVM (Haxby dataset — 84.5% test accuracy)
- MLP implementation in PyTorch and Keras (82.8% test accuracy on Haxby)
- Open neuroimaging data handling (ADHD 200, ABIDE II)
- Reproducible research practices (Git, FAIR principles, OSF)

---

## Acknowledgments

- **Brainhack School 2026** organizers and TAs across Taipei and Singapore hubs

---

## Contact

- GitHub: [@jessicathao](https://github.com/jessicathao)
- Affiliation: Linguistics PhD program, National Taiwan University
- Research interests: Sociolinguistics, corpus linguistics, computational language processing, brain decoding

---

*Code and analysis notebooks will be added to this repository as the project progresses.*
