# Fake News Detection & Interpretability Analysis

A comprehensive machine learning project for detecting fake news with interpretable explanations using LIME (Local Interpretable Model-agnostic Explanations). This project compares TF–IDF + Logistic Regression and BERT-based transformer models for both accuracy and explainability.

## Team Members

- Ryan Cohen (ryancohen@vt.edu)
- Siddharth Jain (siddharthjain@vt.edu)

## Project Overview

### Purpose

This project develops a machine learning system to detect fake news and explain its predictions in a user-friendly way. With the rapid spread of misinformation online through social media, automatically assessing article authenticity and highlighting deceptive linguistic cues is increasingly critical.

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
│   ├── raw/                          
│   │   ├── FakeNewsNet/              # PolitiFact and GossipCop datasets
│   │   │   ├── gossipcop_fake.csv
│   │   │   ├── gossipcop_real.csv
│   │   │   ├── politifact_fake.csv
│   │   │   └── politifact_real.csv
│   │   └── ISOTFakeNewsDataset/      # ISOT fake news dataset
│   │       ├── Fake.csv
│   │       └── True.csv
│   └── processed/                    # Cleaned and preprocessed data
│       ├── 00/                       
│       │   ├── gossipcop_sample_fake.csv      
│       │   ├── gossipcop_sample_real.csv      
│       │   ├── politifact_sample_fake.csv     
│       │   ├── politifact_sample_real.csv     
│       │   ├── politifact_test.csv           
│       │   └── politifact_train.csv           
│       └── 01/                       
│           ├── Fake_VS_Real_cleaned.csv       
│           ├── human_readable_dataset.csv     
│           └── reduced_dataset.csv           
├── models/                            
│   ├── bert_fake_news_trained_v2/    
│   ├── bert_politifact_retrained/    
│   └── bert_gossip/                 
├── notebooks/                         # Jupyter notebooks 
│   ├── 00_article_scraping.ipynb     
│   ├── 01_preprocessing.ipynb        
│   ├── 02_TF-IDF/                               # TF-IDF model training / analysis
│   │   ├── 02_1_TF-IDF_training.ipynb           
│   │   ├── 02_2_TF-IDF_investigation_1.ipynb    
│   │   └── experiment_log.csv                   
│   └── 03_BERT/                                 # BERT model training / analysis
│       ├── 03_BERT_training.ipynb               
│       ├── 03_BERT_Politifact.ipynb             
│       ├── 03_BERT_Gossip.ipynb                 
│       ├── 03_LIME_Investigation.ipynb          
│       ├── 03_Bias_Analysis.ipynb               
│       ├── Playground.ipynb                    
│       ├── playground_results.txt               
│       
├── images/                           
│   ├── lime_comparison.png           
│   ├── loss_curves.png                
│   ├── output.png                    
|   ├── lime_analysis_square.png       
│   ├── lime_comparison.png           
│   ├── lime_comparison_square.png     
|── README.md                          
├── journal.md                         
├── requirements.txt                   
└── .gitignore                        
```

