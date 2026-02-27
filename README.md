mcPHASES-ML

Multimodal Temporal Representation Learning for Personalized Menstrual Cycle Modeling

Overview

This project investigates whether multimodal physiological time-series signals can be used to learn meaningful and personalized representations of menstrual cycle dynamics.

Using the mcPHASES dataset, we study:

Representation learning from wearable and hormonal signals

Menstrual phase classification

Ovulation detection

Personalized modeling vs global modeling

The goal is to move beyond simple classification and explore whether latent physiological state embeddings improve predictive performance and generalization.

Research Questions
RQ1 – Representation Learning

Can self-supervised temporal models learn meaningful physiological embeddings from multimodal wearable and hormonal time-series data?

RQ2 – Downstream Prediction

Do learned embeddings improve:

Phase classification accuracy

Ovulation detection performance

compared to raw-feature baselines?

RQ3 – Personalization

Does individualized fine-tuning outperform global models in modeling menstrual cycle dynamics?

Dataset

We use the mcPHASES dataset, which includes:

HRV

Resting heart rate

Skin temperature

Sleep metrics

Activity

Hormone levels (e.g., LH, estrogen)

Menstrual phase labels

Data is processed into sliding windows (default: 7-day windows).

Project Structure
mcphases-ml/
│
├── data/
│   ├── raw/
│   ├── interim/
│   ├── processed/
│   └── splits/
│
├── configs/
│
├── src/
│   ├── data/
│   ├── models/
│   ├── losses/
│   ├── training/
│   ├── visualization/
│   ├── utils/
│   └── main.py
│
├── experiments/
├── notebooks/
├── requirements.txt
└── README.md
Installation
1. Create virtual environment
python3 -m venv venv
source venv/bin/activate
2. Install dependencies
pip install -r requirements.txt
Required packages
torch
numpy
pandas
scikit-learn
xgboost
matplotlib
seaborn
pyyaml
tqdm
einops
Experimental Pipeline
Step 1 — Data Preprocessing
python src/data/preprocess.py

Includes:

Missing value handling

Normalization

Sliding window segmentation

User-level split

Output stored in:

data/processed/
Step 2 — Baseline Models (Raw Features)
python src/training/train_classifier.py --config configs/baseline.yaml

Models:

Logistic Regression

XGBoost

LSTM

Transformer

Step 3 — Self-Supervised Encoder (RQ1)
python src/training/train_encoder.py --config configs/encoder.yaml

Training objectives:

Contrastive learning

Masked time-step prediction

Reconstruction

Output:

Physiological embeddings

Encoder checkpoints

Step 4 — Embedding-Based Prediction (RQ2)
python src/training/train_classifier.py --config configs/classification.yaml

Compare:

Raw features vs Embedding features

Metrics:

Accuracy

F1-score

AUROC

Step 5 — Personalization (RQ3)
python src/training/fine_tune_user.py --config configs/personalization.yaml

Compare:

Global model

Per-user fine-tuning

Few-shot adaptation

Evaluation Strategy

User-level data split

Leave-one-user-out validation

Cross-user generalization

Metrics:

Accuracy

F1-score

AUROC

Per-user performance

Embedding Analysis

We analyze learned representations via:

t-SNE visualization

Clustering separability

Phase separability

Notebook:

notebooks/embedding_analysis.ipynb
Expected Contributions

A multimodal temporal representation learning framework for female health modeling

Empirical evaluation of embedding utility in downstream tasks

Quantitative analysis of personalization benefits

A reproducible pipeline for menstrual cycle modeling

Ethical Considerations

Data privacy protection

Bias across demographic groups

Clinical interpretation limitations

This project is intended for research purposes only and does not provide medical advice.

Future Work

Survival modeling for phase transition prediction

Generative modeling of physiological trajectories

Causal analysis between hormones and wearable signals

Domain adaptation across datasets

Author

Annie Luo
Computer Science
Wake Forest University