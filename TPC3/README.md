# Character and Relationship Extraction in Harry Potter

This project aims to identify characters in the book *Harry Potter and the Philosopher’s Stone* and extract potential relationships between them using Natural Language Processing techniques.

## Dataset

The analysis is performed on the file `Harry_Potter.txt`, which contains the full text of the book in Portuguese.

## Tools and Libraries

The project is implemented in Python using the **spaCy** library and the **pt_core_news_sm** language model for Portuguese.

The following components are used:

- Named Entity Recognition (NER)
- Part-of-Speech tagging (POS tagging)
- spaCy `Matcher` for custom pattern detection

## Methodology

The approach is divided into two main steps.

### 1. Character Extraction

The text is processed and split into sentences.  
For each sentence, a pattern is applied to detect entities of type `PER` (person) composed of one or more proper nouns (`PROPN`).

The extracted names are then filtered to remove noise, such as:

- strings starting with lowercase letters;
- elements containing invalid characters or unwanted tokens;
- artifacts from the raw text.

This filtering step is necessary because the `pt_core_news_sm` model is not specifically trained on literary texts, which may lead to inaccurate detections.

### 2. Relationship Extraction

A relationship between two characters is assumed when both appear in the same sentence.

For each sentence, all possible pairs of detected characters are generated using `combinations` from the `itertools` module.

Each pair is stored in a set to avoid duplicates.

## Output

The program produces two main outputs:

1. A list of all detected characters
2. A list of character pairs representing co-occurrence within the same sentence

## Limitations

This approach has some limitations:

- Co-occurrence in the same sentence does not necessarily imply a real relationship (e.g., friendship);
- Some names may be incorrectly extracted;
- The performance depends on the accuracy of the language model, which is not optimized for narrative texts.

Despite these limitations, the method provides a simple and effective way to explore character interactions in the text.
