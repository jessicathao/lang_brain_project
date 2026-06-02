# lang_brain_project

**Validating transformer-generated emotion labels against human consensus in naturalistic film fMRI**

Status: In active development (Brainhack School 2026 final project)
Author: Thach Thao Le (Jessica) — PhD student, Linguistics, National Taiwan University

## Project overview

This project tests whether emotion labels generated automatically by a transformer
language model (BERT) agree with human consensus annotations, using the **Emo-FilM**
dataset — fMRI and emotion ratings collected while participants watched short films.

The central question: **can an automatic NLP method label the emotional valence of
film dialogue well enough to substitute for slow, costly human annotation?**

### Two research questions
1. **Agreement (committed):** Do BERT-generated valence labels, derived from film
   transcripts, correlate with the human consensus annotations?
2. **Brain decoding (stretch):** Can those labels decode emotional valence from the
   fMRI BOLD signal as well as human labels can?

## Why it matters
- **Label provenance:** any decoder is only as good as its labels; knowing where
  automatic labels fail is understudied.
- **Scale:** if automatic labels prove reliable, many unlabeled naturalistic datasets
  become usable for affective neuroscience.
- **Extensible:** the same method can later move to cross-linguistic data, including
  under-represented languages such as Vietnamese.

This measures emotion in film *via language* (spoken dialogue), not language
processing in isolation — a deliberate, scoped first test.

## Data

**Emo-FilM** (Morgenroth et al., 2025, *Scientific Data* 12:684), on OpenNeuro:
- fMRI: [ds004892](https://openneuro.org/datasets/ds004892) (CC0)
- Annotations: [ds004872](https://openneuro.org/datasets/ds004872) (CC0)
- 14 short films, 30 participants (3 Tesla), 44 annotators, 50 emotion items.
- TR = 1.3 s. Preprocessed BOLD available in MNI space.

The **human valence signal** is taken from the appraisal item *PleasantOther* (the
highest-agreement item in the dataset), with a positive-minus-negative emotion
contrast as a backup.

## Method

```
Film transcript  ──►  BERT sentiment  ──►  valence (1 Hz)  ──┐
(.srt or Whisper)     (per segment)        NaN if silent     │
                                                             ▼
                            Pearson correlation  ◄──  Human consensus
                            (per film, vs ~0.40        (PleasantOther, 1 Hz)
                             human–human ceiling)
                                                             │
                                            (stretch) ───────┘
                            Train SVM to decode valence from BOLD,
                            human labels vs BERT labels, compare accuracy
```

- **Committed deliverable:** BERT labels + valence proxy + per-film correlation
  against the human consensus. Pure NLP + statistics; no fMRI preprocessing on the
  critical path.
- **Stretch goal:** brain decoding with a linear SVM (leave-one-film-out CV),
  comparing human vs BERT labels.

## Technical stack

| Component | Tool |
|---|---|
| fMRI data handling | nilearn, nibabel |
| Sentiment labels | Hugging Face Transformers (`phanerozoic/BERT-Sentiment-Classifier`) |
| Machine learning | scikit-learn (SVM) |
| Transcription | OpenAI Whisper (for films without subtitles) |
| Environment | Conda (Python 3.11), macOS Apple Silicon |
| Version control | Git / GitHub |

## Repository layout
```
src/          analysis and pipeline scripts
data/
  subs/         film subtitle files (.srt)
  transcripts/  processed transcripts (.json)
docs/         notes and documentation
notebooks/    Jupyter notebooks
results/      figures and outputs
```
Large data (brain images, film media) is gitignored and not stored here.

## Progress
- [x] Project proposal and design (pitched June 2026)
- [x] Tool selection (BERT for sentiment, SVM for decoding)
- [x] Dataset selection: Emo-FilM (ds004892 / ds004872)
- [x] fMRI structure explored; preprocessing confirmed available in MNI space
- [x] BERT model validated on SST-2 (86.3% accuracy)
- [x] First transcript produced (Sintel, from official subtitles)
- [ ] Extract PleasantOther human valence signal from ds004872
- [ ] Resolve subtitle/film-time alignment
- [ ] BERT valence vs human consensus — first correlation
- [ ] Remaining transcripts (Tears of Steel via .srt; rest via Whisper)
- [ ] Brain decoding (stretch)
- [ ] Final report and Singapore symposium presentation

## Background
Builds on Brainhack School 2026 (NTU Taiwan): fMRI decoding with SVM (Haxby,
84.5%), MLP in PyTorch (82.8%), open neuroimaging data handling (ADHD 200,
ABIDE II), and reproducible-research practices (Git, FAIR, OSF).

## References
- Morgenroth, E., et al. (2025). Emo-FilM: A multimodal dataset for affective
  neuroscience using naturalistic stimuli. *Scientific Data, 12*, 684.

## Acknowledgments
Brainhack School 2026 organizers and TAs across the Taipei and Singapore hubs.

## Contact
GitHub: [@jessicathao](https://github.com/jessicathao)
