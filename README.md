# Text Preprocessing with NLTK and pandas

![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&logoColor=white)
![NLTK](https://img.shields.io/badge/NLTK-3.8%2B-154F5B)
![pandas](https://img.shields.io/badge/pandas-1.5%2B-150458?logo=pandas&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

A hands-on walkthrough of the standard **text-preprocessing pipeline** every NLP project starts with, applied to real TripAdvisor hotel reviews: cleaning, tokenization, stemming vs. lemmatization, and n-gram frequency analysis.

## Overview

Raw review text is messy — mixed case, punctuation, filler words. This notebook takes 109 TripAdvisor hotel reviews (with 1–5 star ratings) and transforms them step by step into analysis-ready tokens:

| Step | Technique | Notes |
|---|---|---|
| 1. Normalize | Lowercasing | `str.lower()` on the raw review column |
| 2. Stop-word removal | NLTK English stop words | **`not` is deliberately kept** — negation carries sentiment ("not clean" ≠ "clean") |
| 3. Punctuation removal | Regex `([^\w\s])` | Strips all non-word, non-space characters |
| 4. Tokenization | `nltk.word_tokenize` | Splits reviews into word tokens |
| 5. Stemming | `PorterStemmer` | Fast but crude: *expensive → expens*, *anniversary → anniversari* |
| 6. Lemmatization | `WordNetLemmatizer` | Dictionary-based: *parking → parking*, *arrived → arrived* |
| 7. N-grams | `nltk.ngrams` | Unigram and bigram frequency counts |

Each intermediate result is stored as a new DataFrame column, so you can compare every stage side by side.

## Key results

Frequency analysis over the cleaned, lemmatized corpus:

- **Top unigrams:** hotel (292), room (275), great (126), **not (122)**, stay (95) — keeping the negation token pays off; it's the 4th most frequent word.
- **Top bigrams:** *great location* (24), *space needle* (21), *hotel monaco* (16), *great hotel* (12), *staff friendly* (12) — the bigrams instantly reveal these are Seattle hotel reviews and surface what guests praise most.
- **Stemming vs. lemmatization:** the side-by-side columns show why lemmatization is usually preferred for readability (*expens/expensive*, *anniversari/anniversary*).

## Project structure

```
├── Pratical_27_01.ipynb            # Step-by-step preprocessing pipeline
├── tripadvisor_hotel_reviews.csv   # 109 hotel reviews with star ratings
├── requirements.txt                # Python dependencies
└── README.md
```

## Getting started

```bash
git clone https://github.com/adityashroff06-code/TEXT-PREPROCESSING-WITH-NLTK-AND-PANDAS.git
cd TEXT-PREPROCESSING-WITH-NLTK-AND-PANDAS

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# one-time NLTK corpus downloads
python -c "import nltk; [nltk.download(p) for p in ('punkt', 'stopwords', 'wordnet')]"

jupyter notebook Pratical_27_01.ipynb
```

## Dataset

`tripadvisor_hotel_reviews.csv` is a 109-review sample from the public TripAdvisor Hotel Reviews dataset (columns: `Review`, `Rating`). Included for reproducibility; used for educational purposes only.

## License

Released under the [MIT License](LICENSE).

## Author

**Aditya Shroff** — [GitHub](https://github.com/adityashroff06-code) · [LinkedIn](https://www.linkedin.com/in/aditya-shroff-8033a31b0)
