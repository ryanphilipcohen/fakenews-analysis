# fakenews-analysis

## Team Members

Ryan Cohen - ryancohen@vt.edu

Siddharth Jain - siddharthjain@vt.edu

## Purpose

The goal of this project is to develop a machine learning system to detect fake news and explain its predictions in a user-friendly way.
With the rapid spread of misinformation online, especially through social media, the ability to automatically assess the authenticity of news and highlight deceptive linguistic cues has become increasingly important.

This project compares a TF–IDF + Logistic Regression model and a BERT-based transformer model to determine both accuracy and interpretability in fake news detection. The system not only predicts whether an article is real or fake, but also highlights the most influential words or phrases contributing to that prediction. The results will be presented via a FastAPI backend and an accompanying Chrome extension for real-time web article analysis.

## Installation

### For Developers

1. Clone the repo:

`git clone https://github.com/ryanphilipcohen/fakenews-analysis.git`

2. Create an activate virutal environment:

`python -m venv venv`
`venv\Scripts\activate`

3. Install requirements:

`pip install -r requirements.txt`

## Data Sources and References

https://github.com/KaiDMML/FakeNewsNet/blob/master/README.md
https://www.kaggle.com/datasets/rahulogoel/isot-fake-news-dataset?resource=download
