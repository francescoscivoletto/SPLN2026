# TPC 5 - Named Entity Recognition with BERT and spaCy


## Overview

This assignment explores the task of **Named Entity Recognition (NER)** in Portuguese using two different approaches:

1. a **Transformer-based classroom model** from `aula9.ipynb`, based on **BERT**
2. a **spaCy NER model** trained on the provided `.iob` files

The main goal of this work is to compare the results obtained by the two approaches and analyze their performance on the same task.

---

## Part 1 - Classroom model (BERT)

The first part of the assignment is based on the notebook developed in class, `aula9.ipynb`.  
This notebook uses a **BERT model** for token classification and applies it to the Portuguese NER task.

The classroom model follows the typical Transformer workflow:

- dataset loading
- tokenization with a BERT tokenizer
- label alignment with subword tokens
- fine-tuning for token classification
- evaluation using standard NER metrics

This approach is directly related to the theory presented in class about **Transformers**, **BERT**, and **fine-tuning for Named Entity Recognition**.

### Classroom model results

The classroom BERT-based model obtained the following results:

| Model | Precision | Recall | F1 |
|-------|-----------|--------|----|
| BERT (classroom model) | 93.91 | 96.68 | 95.27 |

---

## Part 2 - spaCy model

The second part of the assignment consists of training a **spaCy NER model** using the provided `.iob` files.

The workflow was the following:

1. convert the `.iob` files into `.spacy` format
2. initialize a spaCy configuration file for Portuguese NER
3. train the model using the training split
4. evaluate the best saved model on the validation split
5. compare the results with the classroom model

### Files used

- `arquivo_ner_train.iob` - training data
- `arquivo_ner_test.iob` - validation data
- `aula9.ipynb` - classroom baseline model
- `spacy_model.ipynb` - notebook for the spaCy model

### Commands used

    python -m spacy convert -c iob arquivo_ner_train.iob ./datasets
    python -m spacy convert -c iob arquivo_ner_test.iob ./datasets
    python -m spacy init config config.cfg --lang pt --pipeline ner --optimize accuracy
    python -m spacy train config.cfg --output ./output --paths.train ./datasets/arquivo_ner_train.spacy --paths.dev ./datasets/arquivo_ner_test.spacy
    python -m spacy evaluate output/model-best ./datasets/arquivo_ner_test.spacy

### spaCy evaluation results

The spaCy model obtained the following evaluation scores:

| Metric | Value |
|--------|-------|
| Precision | 93.31 |
| Recall | 92.78 |
| F1-score | 93.05 |

### spaCy results by entity type

| Entity type | Precision | Recall | F1 |
|-------------|-----------|--------|----|
| Data | 98.06 | 97.02 | 97.54 |
| Pessoa | 94.40 | 95.16 | 94.78 |
| Local | 93.03 | 96.73 | 94.85 |
| Organizacao | 81.97 | 50.51 | 62.50 |
| Profissao | 69.23 | 54.00 | 60.67 |

These results show that the spaCy model performs well overall, especially for **Date**, **Person**, and **Location** entities, while **Organization** and **Profession** remain more difficult categories.

---

## Final comparison

The final comparison between the two approaches is shown below:

| Model | Precision | Recall | F1 |
|-------|-----------|--------|----|
| BERT (classroom model) | 93.91 | 96.68 | 95.27 |
| spaCy | 93.31 | 92.78 | 93.05 |

From this comparison, the **BERT-based classroom model achieved better overall results** than the spaCy model in this experiment.

In particular:

- the BERT model achieved higher **recall**
- the BERT model also achieved a higher **F1-score**
- the spaCy model still produced solid results, but its performance dropped more strongly on some entity categories, especially **Organization** and **Profession**

---


