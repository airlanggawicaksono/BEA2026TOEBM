# BEA 2026 — Vocabulary Test Item Difficulty Prediction

**Mantera Studio** | BEA 2026 Shared Task Submission

## Overview

Ensemble system predicting L2 vocabulary test item difficulty (GLMM score) across Spanish, German, and Mandarin Chinese using multilingual transformers + Ridge stacking.

## Models

| Model | HF ID |
|-------|-------|
| XLM-RoBERTa | `FacebookAI/xlm-roberta-base` |
| mDeBERTa-v3 | `microsoft/mdeberta-v3-base` |
| mmBERT | `jhu-clsp/mmBERT-base` |

Trained checkpoints saved to HuggingFace repo: `wicaksonolxn/bea2026-kvl-toebm`

## Architecture

- **Encoder**: pretrained multilingual transformer
- **Regression head**: LayerNorm → Linear → ReLU → Dropout → Linear(1)
- **Projection head**: for contrastive loss (dim=128)
- **Ensemble**: Ridge stacking (RidgeCV) over per-model predictions

## Loss

```
L = L_reg + λ_imp * L_impcon + λ_soft * L_softsucon
```

- `L_reg`: MSE on GLMM score
- `L_impcon`: Implicit contrastive loss (augmented view via English context)
- `L_softsucon`: Soft supervised contrastive loss (score-weighted similarity)

## Setup

### HuggingFace Token

Set via Colab Secrets (do **not** hardcode):

```python
from google.colab import userdata
HF_TOKEN = userdata.get('HF_TOKEN')
```

Or env var:

```bash
export HF_TOKEN=hf_...
```

### Data

Loaded from Google Drive. Mount drive and set `GDRIVE_URLS` in notebook cell 1.

Dataset: KVL extended (Skidmore et al. 2025) — ES/DE/CN train/dev/test splits.

## Usage

Open `last_submission.ipynb` in Google Colab. Key flags in cell 1:

| Flag | Default | Description |
|------|---------|-------------|
| `SAVE_RESULTS` | `False` | Save test predictions to Drive |
| `MERGE_DEV_TRAIN` | `True` | Merge dev into train for final submission |
| `USE_ENSEMBLE` | `True` | Run Ridge-stacked ensemble |
| `LANGUAGES` | `["es","de","cn"]` | Languages to train |
| `EPOCHS` | `5` | Training epochs per model |

## Results

Ridge ensemble evaluated via Spearman correlation and RMSE per language.

## License

MIT License — Mantera Studio 2026. See [LICENSE](LICENSE).

Dataset: CC BY-NC 4.0 (Schmitt et al. 2024, Skidmore et al. 2025).
