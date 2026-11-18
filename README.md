# Complaint Triage Intelligence
### Turning Turkish Customer Feedback into Actionable Insights

**95.15% Accuracy · 94.86% Macro F1 · 49% Fewer Missed Complaints**

[English](README.md) | [Türkçe](README_TR.md)

Customer feedback is one of the clearest signals of product and service quality. The challenge is identifying the feedback that needs attention when comments arrive at scale, in different writing styles, and often with mixed sentiment.

**Complaint Triage Intelligence** is an NLP and machine learning project that identifies complaints in Turkish customer feedback and evaluates which text representation and classification strategy works best. The focus is not simply predicting a label: it is **improving complaint detection while keeping the results measurable and interpretable**.

## Results at a glance

| Metric | Optimized model |
|---|---:|
| Classification accuracy | **95.15%** |
| Macro F1-score | **94.86%** |
| Complaint recall | **94.82%** |
| Missed complaints | **53 → 27** |
| Reduction in missed complaints | **~49%** |

The final model is **character-level TF-IDF (3–5 grams) + balanced Linear SVM**, selected through cross-validation and evaluated on a held-out test set of 1,382 comments.

## Why this matters

In customer experience operations, an overlooked complaint can mean a delayed response and a missed opportunity to improve a service. This project explores how automated text analysis can help teams:

- **Spot complaints sooner** across large volumes of written feedback.
- **Support customer support triage** by separating potentially actionable complaints from other comments.
- **Track recurring customer pain points** through language patterns and exploratory analysis.
- **Make model decisions easier to inspect** with feature-level interpretation and error analysis.

These are potential business applications of the classification approach; the repository presents an experimental model, not a deployed production service.

## What I built

**1. Data preparation and exploration**  
Worked with a public Turkish customer-feedback dataset, resolved conflicting duplicate labels, and prepared **6,906 comments** for analysis. Examined class distribution, comment length, and language patterns.

**2. Turkish-language NLP pipeline**  
Applied Turkish-aware normalization and tokenization, stopword handling, n-gram analysis, part-of-speech tagging, named entity recognition, and dependency parsing.

**3. Representation and model benchmarking**  
Compared **Bag of Words, word-level TF-IDF, Word2Vec, and BERTurk embeddings**. Benchmarked **Naive Bayes, Logistic Regression, and Linear SVM** across traditional text classification experiments.

**4. Targeted model optimization**  
Investigated classification errors and ran **18 optimization experiments** across word and character n-grams, regularization, and class weighting. Character-level TF-IDF with Linear SVM delivered the strongest result in the main evaluation.

**5. Explainability and deeper validation**  
Analyzed influential text features, confusion matrices, error patterns, and the effect of comment length. Evaluated pretrained BERTurk representations in a separate controlled comparison.

## How the approach evolved

| Stage | Macro F1 | Accuracy |
|---|---:|---:|
| Baseline: word TF-IDF + Logistic Regression | 93.10% | 93.56% |
| Optimized: character TF-IDF + Linear SVM | **94.86%** | **95.15%** |

The key improvement was not just a higher overall score: **the number of actual complaints missed by the classifier dropped from 53 to 27** on the same held-out test set.

## Tech stack

`Python` · `pandas` · `NumPy` · `scikit-learn` · `NLTK` · `Stanza` · `gensim` · `Transformers / BERTurk` · `Matplotlib` · `Seaborn` · `Jupyter Notebook`

## Explore the project

The notebook documents the workflow from raw data to model evaluation, including visual analysis, model comparisons, optimization experiments, and BERTurk-based representation analysis.

**[Open the analysis notebook](notebooks/)**

To reproduce the experiments, install the dependencies listed in `requirements.txt` and run the notebook in order. Some NLP model downloads may require an internet connection.

## Dataset and evaluation

- **Dataset:** Complaint Classification Dataset, published by nanelimon on Hugging Face (source and license are documented in the notebook).
- **Main evaluation:** 5,524 training and 1,382 test samples; stratified split and three-fold cross-validation for model selection.
- **Transformer comparison:** A separate 1,000-comment subset was used to compare frozen BERTurk embeddings against TF-IDF approaches.

## About the project

I developed this project to explore how NLP can turn unstructured Turkish customer feedback into a measurable classification workflow. It brings together data exploration, feature engineering, model benchmarking, targeted optimization, and interpretable evaluation—skills directly relevant to customer analytics, applied machine learning, and data science.

**Author:** [Ceren Sinmec](https://github.com/cerensinmec)
