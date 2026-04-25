# TF-IDF Document Ranking

## Overview

This project implements a simple document ranking system using **TF-IDF** and **cosine similarity**.

The goal is to compare a query with a small corpus and rank the documents from the most relevant to the least relevant.

---

## Corpus

```python
corpus = [
    "the sky is blue",
    "the sun is bright",
    "the sun in the sky"
]
```

---

## Method

The project follows these steps:

1. Preprocess the documents:
   - tokenization
   - lowercasing
   - stopword removal

2. Compute **TF** to measure how often a word appears in a document.

3. Compute **IDF** to measure how rare a word is in the corpus.

4. Compute **TF-IDF** to give an importance score to each word.

5. Convert documents and query into vectors.

6. Use **cosine similarity** to compare the query with each document.

7. Rank the documents based on similarity.

---

## Query

```text
The bright sun
```

After preprocessing:

```python
["bright", "sun"]
```

---

## Result

The final ranking is:

1. `the sun is bright`
2. `the sun in the sky`
3. `the sky is blue`

The first document is ranked highest because it contains both important query words: `bright` and `sun`.

---

## Conclusion

This homework shows how TF-IDF can represent text as numerical vectors and how cosine similarity can be used to find the most relevant documents for a query.
