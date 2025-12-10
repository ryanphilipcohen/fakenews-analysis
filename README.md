# Fake News Detection & Interpretability Analysis

A comprehensive machine learning project for detecting fake news with interpretable explanations using LIME (Local Interpretable Model-agnostic Explanations). This project compares TF–IDF + Logistic Regression and BERT-based transformer models for both accuracy and explainability.

## Team Members

- Ryan Cohen (ryancohen@vt.edu)
- Siddharth Jain (siddharthjain@vt.edu)

## Project Overview

### Purpose

This project develops a machine learning system to detect fake news and explain its predictions in a user-friendly way. With the rapid spread of misinformation online through social media, automatically assessing article authenticity and highlighting deceptive linguistic cues is increasingly critical.

### Key Features

- **Multiple Models**: Compares TF–IDF + Logistic Regression with domain-specific BERT models
- **Explainability**: Uses LIME to highlight influential words/phrases driving predictions
- **Domain Specialization**: Separate models for political news (PolitiFact), gossip/celebrity news, and general fake news
- **Real-time Analysis**: FastAPI backend with Chrome extension for in-browser article analysis
- **Research-Grade**: Comprehensive Jupyter notebooks with full preprocessing, training, and analysis

### Models Included

1. **TF–IDF + Logistic Regression (Combined)**: General purpose baseline model
2. **BERT Combined Specialist** (`bert_fake_news_trained_v2`): Multi-domain fake news detection
3. **BERT Political Specialist** (`bert_politifact_retrained`): Optimized for political news (PolitiFact dataset)
4. **BERT Gossip Specialist** (`bert_gossip`): Optimized for gossip/celebrity news

## Installation

### Prerequisites

- Python 3.8+
- pip or conda
- Virtual environment (recommended)

### Setup Instructions

1. Clone the repository:
   ```bash
   git clone https://github.com/ryanphilipcohen/fakenews-analysis.git
   cd fakenews-analysis
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   
   # On Windows:
   venv\Scripts\activate
   
   # On macOS/Linux:
   source venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. (Optional) Install PyTorch GPU support for faster model inference:
   ```bash
   pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
   ```

## Project Structure

```
fakenews-analysis/
├── data/
│   ├── raw/                           # Original datasets
│   │   ├── FakeNewsNet/              # PolitiFact and GossipCop datasets
│   │   │   ├── gossipcop_fake.csv
│   │   │   ├── gossipcop_real.csv
│   │   │   ├── politifact_fake.csv
│   │   │   └── politifact_real.csv
│   │   └── ISOTFakeNewsDataset/      # ISOT fake news dataset
│   │       ├── Fake.csv
│   │       └── True.csv
│   └── processed/                    # Cleaned and preprocessed data
│       ├── 00/                       # Sample and train/test splits
│       │   ├── gossipcop_sample_fake.csv      # GossipCop fake news sample
│       │   ├── gossipcop_sample_real.csv      # GossipCop real news sample
│       │   ├── politifact_sample_fake.csv     # PolitiFact fake news sample
│       │   ├── politifact_sample_real.csv     # PolitiFact real news sample
│       │   ├── politifact_test.csv            # PolitiFact test set
│       │   └── politifact_train.csv           # PolitiFact training set
│       └── 01/                       # Cleaned and consolidated datasets
│           ├── Fake_VS_Real_cleaned.csv       # Cleaned fake vs real news
│           ├── human_readable_dataset.csv     # Human-readable format dataset
│           └── reduced_dataset.csv            # Reduced/balanced dataset
├── models/                            # Pre-trained model checkpoints
│   ├── bert_fake_news_trained_v2/    # Combined specialist BERT Retrained
│   ├── bert_politifact_retrained/    # Political specialist BERT
│   └── bert_gossip/                  # Gossip specialist BERT
├── notebooks/                         # Jupyter notebooks for analysis
│   ├── 00_article_scraping.ipynb     # Data collection and scraping
│   ├── 01_preprocessing.ipynb        # Data cleaning and preprocessing
│   ├── 02_TF-IDF/
│   │   ├── 02_1_TF-IDF_training.ipynb           # TF-IDF model training
│   │   ├── 02_2_TF-IDF_investigation_1.ipynb    # TF-IDF analysis
│   │   └── experiment_log.csv                   # TF-IDF experiment results
│   └── 03_BERT/
│       ├── 03_BERT_training.ipynb               # BERT model training
│       ├── 03_BERT_Politifact.ipynb             # Political domain analysis
│       ├── 03_BERT_Gossip.ipynb                 # Gossip domain analysis
│       ├── 03_LIME_Investigation.ipynb          # LIME explainability (RECOMMENDED)
│       ├── 03_Bias_Analysis.ipynb               # Bias analysis
│       ├── Playground.ipynb                     # Quick testing and experimentation
│       ├── playground_results.txt               # Test results output
│       
├── images/                            # Repository images
│   ├── lime_comparison.png            # LIME comparison figure
│   ├── loss_curves.png                # Training loss curves
│   ├── output.png                     # Sample outputs
|   ├── lime_analysis_square.png       # LIME visualization
│   ├── lime_comparison.png            # Comparison visualization
│   ├── lime_comparison_square.png     # Square format comparison
|── README.md                          # This File
├── journal.md                         # Development journal and notes
├── requirements.txt                   # Python dependencies (pip)
└── .gitignore                         # Git ignore rules
```

## Usage

### Running Notebooks (Local Analysis)

1. Start Jupyter:
   ```bash
   jupyter notebook
   ```

2. Navigate to `notebooks/03_BERT/03_1_LIME_SHAP_Investigation.ipynb` for a comprehensive example of:
   - Loading pre-trained models
   - Making predictions
   - Generating LIME explanations
   - Analyzing semantic patterns

### Using the FastAPI Backend

1. Start the server:
   ```bash
   python app.py
   ```

2. Access the interactive API documentation:
   ```
   http://127.0.0.1:8000/docs
   ```

3. Test endpoints:
   ```bash
   curl -X POST "http://127.0.0.1:8000/analyze" \
     -H "Content-Type: application/json" \
     -d '{"text": "Your article text here"}'
   ```


## Data Sources

This project uses two publicly available fake news datasets:

1. **FakeNewsNet** - [GitHub Repository](https://github.com/KaiDMML/FakeNewsNet)
   - PolitiFact articles (fact-checked political news)
   - GossipCop articles (gossip and celebrity news)

2. **ISOT Fake News Dataset** - [Kaggle Dataset](https://www.kaggle.com/datasets/rahulogoel/isot-fake-news-dataset)
   - Real and fake news articles from various sources
   - Combined dataset for general fake news detection

### Data Preprocessing

The data preprocessing pipeline is documented in:
- `notebooks/01_preprocessing.ipynb` - Complete preprocessing steps
- `notebooks/00_article_scraping.ipynb` - Data collection methodology

## Model Performance

All models were evaluated on validation datasets from their respective training sets:

### TF–IDF + Logistic Regression
- Accuracy: 95.2%
- Precision: 94.6%
- Recall: 96.8%
- F1-Score: 95.7%
- ROC-AUC: 0.989

### BERT Models
Detailed performance metrics are available in the respective training notebooks:
- `notebooks/03_BERT/03_BERT_training.ipynb` - Political specialist results
- Comprehensive evaluation with confusion matrices and classification reports

## Example Notebooks

### 03_1_LIME_SHAP_Investigation.ipynb
A comprehensive example demonstrating:
- Loading all three BERT models
- Making predictions on sample articles
- Generating LIME explanations for word-level interpretability
- Analyzing semantic patterns (sensational language, emotional words)
- Creating publication-quality visualizations

**To run this notebook:**
1. All dependencies are in `requirements.txt`
2. Pre-trained models are in `models/`
3. No additional setup required - execute cells sequentially

## Key Findings

- **Sensational language** ("shocking," "incredible," "unbelievable") strongly correlates with fake news predictions
- **Emotional intensity** and vague claims are reliable fake news indicators
- **Real news** typically uses specific, measured language with clear attribution
- **Domain specialization** improves accuracy for news categories with distinct linguistic patterns
- **LIME explanations** reveal distinct linguistic strategies across fake vs. real news

## Citation & Academic Integrity

This project uses external code, datasets, and AI tools. All external sources and dependencies are documented in `CITATIONS.md` for academic integrity and reproducibility.

## Contact

For questions or issues, please contact:
- Ryan Cohen (ryancohen@vt.edu)
- Siddharth Jain (siddharthjain@vt.edu)
