# NLP Scraper – NLP Enriched News Intelligence Platform

## Project Overview

This project builds an **NLP-enriched news intelligence platform** capable of scraping news articles and analyzing them using Natural Language Processing techniques.

The platform collects news articles from a news website and processes them with an NLP pipeline to extract useful insights such as:

- Organizations mentioned in the articles
- Article topic classification
- Sentiment analysis
- Environmental scandal detection related to companies

The goal is to help analysts **identify relevant information quickly from large volumes of news data**.

---

# Project Structure

The project follows the structure required in the subject:

```
project
.
├── data
│   └── ...
├── scraper_news.py
├── nlp_enriched_news.py
├── requirements.txt
├── README.md
├── results
│   ├── training_model.py
│   ├── enhanced_news.csv
│   └── learning_curves.png
```

Description:

| File | Purpose |
|-----|--------|
| scraper_news.py | Scrapes news articles and stores them |
| nlp_enriched_news.py | Runs the NLP pipeline on scraped articles |
| training_model.py | Trains the topic classifier |
| enhanced_news.csv | Final enriched dataset |
| learning_curves.png | Model learning curves |
| requirements.txt | Python dependencies |

---

# Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/nlp-scraper.git
cd nlp-scraper
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Download SpaCy model:

```bash
python -m spacy download en_core_web_sm
```

Download NLTK resources:

```python
import nltk
nltk.download('vader_lexicon')
```

---

# Step 1 — Scraping News Articles

Run the scraper:

```bash
python scraper_news.py
```

The scraper collects **at least 300 news articles from the last week**.

For each article, the following information is stored:

- Unique ID
- URL
- Date
- Headline
- Body text

Example console output:

```
1. scraping <URL>
requesting ...
parsing ...
saved in data/articles.json

2. scraping <URL>
requesting ...
parsing ...
saved in data/articles.json
```

---

# Step 2 — Topic Classification Model

The project includes a **topic classifier** trained to detect the category of each news article.

Possible topics:

- Tech
- Sport
- Business
- Entertainment
- Politics

## Methodology

The model training pipeline includes:

1. Text preprocessing
2. Tokenization
3. Stop word removal
4. Bag-of-Words representation using **CountVectorizer**
5. Model training using **scikit-learn**
6. Evaluation using training and test datasets

The trained model is saved as:

```
topic_classifier.pkl
```

The learning curves are saved as:

```
results/learning_curves.png
```

---

# Overfitting Explanation

**Overfitting** occurs when a model learns the training data too well, including noise or irrelevant patterns, which causes poor performance on new unseen data.

In this project, overfitting is avoided by:

- Splitting data into **training and test datasets**
- Monitoring **learning curves**
- Using proper preprocessing and feature selection
- Evaluating performance on unseen test data

The model achieves **more than 95% accuracy on the test dataset**, confirming good generalization.

---

# Step 3 — NLP Engine

Run the NLP pipeline:

```bash
python nlp_enriched_news.py
```

The NLP engine processes the scraped articles and performs several analyses.

Example output:

```
Enriching <URL>

Cleaning document ...

---------- Detect entities ----------
Detected 2 companies which are Apple and Microsoft

---------- Topic detection ----------
Text preprocessing ...
The topic of the article is: Tech

---------- Sentiment analysis ----------
The article has a Positive sentiment

---------- Scandal detection ----------
Computing embeddings and distance ...
Environmental scandal detected for company
```

---

# Named Entity Recognition

Companies and organizations are detected using **SpaCy Named Entity Recognition (NER)**.

Only entities labeled **ORG** are extracted.

Example detected organizations:

```
Apple
Microsoft
Google
Amazon
```

---

# Sentiment Analysis

Sentiment analysis is performed using **NLTK VADER**, a pre-trained sentiment model.

Possible sentiment outputs:

- Positive
- Negative
- Neutral

Advantages of using a pre-trained model:

- No labeled training data required
- Fast and efficient
- Widely used in NLP applications

---

# Environmental Scandal Detection

The goal is to detect potential **environmental scandals involving companies** mentioned in news articles.

## Keywords

Environmental disaster keywords include:

```
pollution
deforestation
oil spill
toxic waste
contamination
environmental damage
industrial waste
```

## Embeddings Choice

This project uses **word embeddings** to represent words as vectors in a semantic space.

Embeddings capture relationships between words, allowing similar concepts to have similar vector representations.

Embeddings allow us to detect semantic similarity between sentences and environmental disaster keywords.

## Distance Metric

We use **cosine similarity** between embeddings.

Cosine similarity is commonly used in NLP because it measures the angle between vectors, capturing semantic similarity regardless of magnitude.

Steps:

1. Compute embeddings for disaster keywords
2. Extract sentences containing detected companies
3. Compute cosine similarity between sentence embeddings and keyword embeddings
4. Aggregate similarities to compute a **scandal score per article**

Each article receives a value:

```
scandal_distance
```

Higher similarity indicates higher likelihood of environmental scandal.

The **top 10 articles with highest scores** are flagged.

```
top_10 = True
```

---

# Output Dataset

The final enriched dataset is stored as:

```
results/enhanced_news.csv
```

Dataset structure:

| Column | Description |
|------|-------------|
| id | Unique identifier |
| url | Article URL |
| date_scraped | Scraping date |
| headline | Article title |
| body | Article content |
| org | Detected organizations |
| topic | Predicted topic |
| sentiment | Sentiment score |
| scandal_distance | Environmental scandal score |
| top_10 | Top scandal flag |

The dataset contains **300 rows corresponding to 300 articles**.

---

# Technologies Used

- Python
- BeautifulSoup
- Requests
- SpaCy
- NLTK
- Scikit-learn
- Pandas
- NumPy
- Matplotlib

---

# Future Improvements

Possible improvements include:

- Real-time streaming news processing
- Transformer-based NLP models (BERT)
- Multi-language news analysis
- Visualization dashboard for news intelligence

---

# Author

NLP Scraper Project  
AI / NLP Learning Project
