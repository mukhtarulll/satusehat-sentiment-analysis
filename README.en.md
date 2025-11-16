[![id](https://img.shields.io/badge/lang-id-blue.svg)](https://github.com/ilovetahugimbal/satusehat-sentiment-analysis/blob/main/README.md)

# SatuSehat App Sentiment Analysis with IndoBERT
## Project: Data Mining & NLP

This project analyzes sentiment from 1,048 user reviews of Indonesia's SatuSehat health app on Google Play Store using IndoBERT model (mdhugol/indonesia-bert-sentiment-classification). The main objective is to identify user complaint and praise patterns to provide data-driven product improvement recommendations.

---

## Quick Summary

![Sentiment Analysis Results](HASIL_ANALISIS.png)

Analysis results show:
- **87.3% negative reviews** — Dominated by technical complaints (login/OTP, barcode scan, vaccine certificate)
- **8.4% neutral reviews** — Mixed experience or unclear feedback
- **4.3% positive reviews** — Appreciation for specific health monitoring features

---

## Dataset

**Source:** Google Play Store (Web Scraping)  
**App:** SatuSehat — Official Health App by Indonesian Ministry of Health  
**Scraping Period:** January 2024  

| Attribute | Detail |
|-----------|--------|
| Total Reviews | 1,048 reviews |
| Rating Range | 1-5 stars |
| Content | Indonesian language text reviews |
| Preprocessing | Cleaning, casefolding, tokenization, stopword removal |

---

## Methodology

### 1. Data Collection
- Scraping reviews using Google Play API and Python script
- Fields extracted: content (review text), score (star rating)

### 2. Text Preprocessing
![Methodology Flowchart](Metode%20Miniriset%20UAS.drawio.png)

Preprocessing pipeline:
- **Cleaning**: Remove non-alphabetic characters, emojis, URLs
- **Casefolding**: Convert to lowercase for consistency
- **Tokenization**: Split sentences into word tokens
- **Stopword Removal**: Filter common words (except negations: "tidak"/"not", "bukan"/"no", "gagal"/"failed", "error")

### 3. Sentiment Classification
- **Model**: IndoBERT (`mdhugol/indonesia-bert-sentiment-classification`)
- **Pre-trained**: Fine-tuned for Indonesian language context
- **Framework**: HuggingFace Transformers
- **Output**: Sentiment label (positive/neutral/negative) + confidence score

### 4. Analysis & Visualization
- Sentiment distribution (bar chart)
- Dominant keyword wordcloud (positive vs negative)
- N-gram analysis (bigram, trigram) for complaint patterns
- Confidence score histogram for model validation

---

## Key Findings

### Top 5 Complaints (Negative Sentiment)
1. **"tolong diperbaiki" / "please fix"** (105 occurrences) — Generic bug fix requests
2. **"sertifikat vaksin" / "vaccine certificate"** (94 occurrences) — Issues downloading/accessing vaccination certificates
3. **"peduli lindungi"** (65 occurrences) — Data migration problems from PeduliLindungi app
4. **"scan barcode"** (49 occurrences) — QR/barcode scanning feature not working
5. **"kode OTP" / "OTP code"** (not explicitly counted, but dominant in reviews) — OTP verification issues during login

### Top 3 Praises (Positive Sentiment)
1. **"terima kasih" / "thank you"** (4 occurrences) — General appreciation
2. **"sertifikat vaksin" / "vaccine certificate"** (4 occurrences, positive context) — Successfully downloaded certificate
3. **Blood pressure monitoring feature** — Appreciation for health tracking integration

### Confidence Score Insights
- **Negative**: Average confidence 0.96 (model very confident in negative classification)
- **Positive**: Average confidence 0.87 (lower due to small sample size)
- **Neutral**: Average confidence 0.78 (highest ambiguity)

---

## Recommendations for SatuSehat Developers

### Priority 1 (High Impact, Quick Win)
1. **Fix login/OTP flow** — Most consistent complaint; review SMS gateway implementation & error handling
2. **Fix barcode scanning feature** — Test across various devices & OS versions for compatibility
3. **Simplify vaccine certificate download** — Reduce steps, add offline mode if possible

### Priority 2 (Medium Term)
4. **In-app FAQ & troubleshooting** — Reduce support load with self-service guides
5. **Improve onboarding UX** — "Hard to use" complaints indicate friction in first-time use
6. **Optimize app performance** — "Slow" & "long loading" complaints need profiling & optimization

### Priority 3 (Long Term)
7. **Expand health monitoring features** — Leverage positive sentiment on BP monitoring to add more features (glucose, heart rate, etc.)
8. **Sentiment monitoring dashboard** — Automate review tracking for early detection of new issues

---

## How to Run

### Prerequisites
- Python 3.8+
- GPU recommended (for faster IndoBERT inference, but CPU works too)

### Installation
```bash
# Clone repository
git clone https://github.com/yourusername/satusehat-sentiment-analysis.git
cd satusehat-sentiment-analysis

# Install dependencies
pip install -r requirements.txt
```

### Requirements
```
transformers>=4.30.0
torch>=2.0.0
pandas>=2.0.0
matplotlib>=3.7.0
seaborn>=0.12.0
wordcloud>=1.9.0
nltk>=3.8.0
Sastrawi>=1.0.1
```

### Run Analysis
```bash
# Open Jupyter Notebook
jupyter notebook Miniriset-UAS_Mukhtarul-Hadi_2304140066.ipynb

# Or run Python script (if standalone script exists)
python sentiment_analysis.py
```

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| **Scraping** | Python, Google Play Store API/Selenium |
| **Preprocessing** | NLTK, Sastrawi (Indonesian stemmer), Pandas |
| **Model** | IndoBERT (HuggingFace Transformers) |
| **Visualization** | Matplotlib, Seaborn, WordCloud |
| **Notebook** | Jupyter Notebook |
| **Environment** | Google Colab (for GPU access) |

---

## Model Evaluation Results

| Metric | Score |
|--------|-------|
| **Accuracy** | ~92% (based on manual validation of 100 samples) |
| **Precision (Negative)** | 0.94 |
| **Recall (Negative)** | 0.97 |
| **F1-Score (Negative)** | 0.95 |

*Note: Model performs very well for negative sentiment detection due to heavily skewed data (87.3% negative class).*

---

## Limitations & Future Work

### Limitations
1. **Class imbalance** — Only 4.3% positive, may bias model
2. **No sentiment intensity** — Model only classifies 3 classes, doesn't measure "how negative"
3. **Context loss** — Some sarcastic/ironic reviews may be misclassified
4. **Single app focus** — Model trained generally, may need fine-tuning for health domain

### Future Work
1. **Multi-label classification** — Detect specific complaint categories (login, barcode, certificate, etc.)
2. **Aspect-based sentiment** — Identify sentiment per app feature
3. **Time-series analysis** — Track sentiment changes across app updates
4. **Cross-app comparison** — Compare SatuSehat vs competitors (e.g., Halodoc, Alodokter)

---

## License & Citation

- **Dataset**: Scraped from Google Play Store (public reviews)
- **Model**: IndoBERT by mdhugol (HuggingFace, MIT License)
- **Project**: Open for educational & portfolio purposes

If using this project, please cite:
```
@misc{satusehat_sentiment_2024,
  author = {Mukhtarul Hadi},
  title = {Sentiment Analysis of SatuSehat App Reviews Using IndoBERT},
  year = {2024},
  publisher = {GitHub},
  url = {https://github.com/yourusername/satusehat-sentiment-analysis}
}
```
