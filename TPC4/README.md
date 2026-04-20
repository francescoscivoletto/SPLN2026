# Word2Vec Analysis of Harry Potter Texts

This project explores semantic relationships in two Portuguese Harry Potter novels using a Word2Vec model trained on the book texts.

## Objective

The aim of this homework is to apply distributional semantics to literary data and analyze how word embeddings capture characters, locations, objects, and narrative relationships in the Harry Potter universe.

The project focuses on:

- preparing and cleaning a textual corpus;
- tokenizing Portuguese text into sentences and words;
- training a Word2Vec model;
- exploring semantic similarity, analogy, and clustering;
- visualizing embeddings with PCA;
- testing semantic group queries.

## Dataset

The corpus is built from two Portuguese Harry Potter books:

- `harrypotter.txt`
- `Harry_Potter_Camara_Secreta-br.txt`

Both books are preprocessed and merged into a single corpus before training. The notebook reports 6314 sentences for the first book, 6757 for the second, and 13071 sentences in total. :contentReference[oaicite:2]{index=2}

## Libraries Used

The project is implemented in Python and uses the following libraries:

- `gensim` for Word2Vec
- `nltk` for NLP utilities
- `numpy` for numerical operations
- `matplotlib` for visualization
- `scikit-learn` for PCA
- `re` for text cleaning and tokenization rules

These dependencies are explicitly installed and imported in the notebook. :contentReference[oaicite:3]{index=3}

## Methodology

### 1. Corpus Preparation

The first step consists of loading the raw text files and cleaning them.

The cleaning function removes:

- BOM markers;
- form feed characters;
- carriage returns;
- typographic quotation marks;
- repeated newlines and extra spaces.

This normalization makes the corpus more consistent before tokenization. :contentReference[oaicite:4]{index=4}

### 2. Tokenization

The text is split into sentences using a regular expression based on punctuation.  
Each sentence is then lowercased and tokenized with a regex pattern designed to keep alphabetic words, including accented Portuguese characters and internal hyphens or apostrophes.

Only sentences with at least three tokens are kept in the final corpus. :contentReference[oaicite:5]{index=5}

A manual inspection of the first tokenized sentences shows that the tokenization works correctly, although some copyright and editorial material is still present in the corpus. The notebook also notes that the cleaning stage is only partially effective and could be improved with a more specific filtering function. :contentReference[oaicite:6]{index=6}

### 3. Word2Vec Training

After preprocessing, a Word2Vec model is trained on the merged sentence list with the following main parameters:

- `vector_size = 100`
- `window = 5`
- `min_count = 3`
- `sg = 0` (CBOW architecture)
- `epochs = 10`
- `workers = 4`

The resulting vocabulary size is 4870 words. :contentReference[oaicite:7]{index=7}

### 4. Embedding Exploration

Several analyses are carried out on the trained model:

#### Word vectors
The notebook retrieves the embedding of a specific token such as `"harry"` to show how words are represented as dense vectors. :contentReference[oaicite:8]{index=8}

#### Most similar words
The `most_similar()` function is used to inspect the semantic neighborhood of words such as:

- `harry`
- `rony`
- `hermione`
- `hogwarts`

The results are particularly coherent for central characters, since their closest neighbors are often other major characters that appear in similar narrative contexts. :contentReference[oaicite:9]{index=9}

#### Word similarity
Pairwise cosine similarity is measured between important characters such as Harry, Rony, Hermione, and Voldemort.  
The model shows stronger similarity between Harry, Rony, and Hermione than between Harry and Voldemort, which reflects their different contextual roles in the story. :contentReference[oaicite:10]{index=10}

#### Odd-one-out task
The notebook uses `doesnt_match()` to identify the semantic outsider in small sets of words.  
For example, the model correctly separates places or objects from character names in several cases. :contentReference[oaicite:11]{index=11}

#### Analogy task
An analogy query is also tested with the pattern:

`harry : hermione = rony : ?`

The returned result is `"jorge"`, which is not a strict analogy but still suggests that the model captures a shared social and narrative environment around the main trio. :contentReference[oaicite:12]{index=12}

### 5. PCA Visualization

To visualize the learned embeddings, the notebook reduces selected word vectors to two dimensions using PCA and plots them in a scatterplot.

The selected terms include:

- major characters (`harry`, `rony`, `hermione`, `snape`, `hagrid`, `draco`, `voldemort`, `dumbledore`)
- places and concepts (`hogwarts`, `magia`, `varinha`, `quadribol`)

The plot suggests a partial semantic separation between characters, locations, and magical concepts. :contentReference[oaicite:13]{index=13}

### 6. Semantic Group Queries

The notebook also defines a `semantic_query()` function to inspect broader semantic fields using positive and negative seed words.

The explored groups are:

- main trio semantic field;
- magical school environment;
- antagonistic context;
- friendship vs conflict.

These results suggest that the model performs better on central characters and recurring relationships than on broader or more abstract semantic domains. :contentReference[oaicite:14]{index=14}

## Output

The project produces several types of outputs:

- corpus statistics;
- tokenized sentence samples;
- vocabulary inspection;
- nearest-neighbor lists for selected words;
- similarity scores;
- odd-one-out results;
- analogy results;
- PCA plot of selected embeddings;
- semantic query outputs.

## Main Findings

The notebook highlights a few important observations:

- the model captures meaningful relations among the main characters;
- Harry, Rony, and Hermione appear strongly connected in embedding space;
- antagonistic characters tend to form a different contextual group;
- some noisy or irrelevant words still appear among the nearest neighbors;
- corpus cleaning could be improved, especially to remove editorial front matter and copyright material. :contentReference[oaicite:15]{index=15} :contentReference[oaicite:16]{index=16} :contentReference[oaicite:17]{index=17}

## Limitations

This approach has some limitations:

- the corpus still contains non-narrative noise;
- Word2Vec relies on context co-occurrence and does not provide deep semantic understanding;
- analogy and semantic-field queries are not always precise;
- PCA offers only a simplified two-dimensional projection of a higher-dimensional space.

## Conclusion

This project shows how Word2Vec can be applied to literary texts to explore semantic similarity and narrative structure.  
Even with some preprocessing noise, the model is able to identify relevant relationships between central characters and distinguish, at least partially, between characters, locations, and magical concepts.

## How to Run

1. Install the required libraries:
   - `gensim`
   - `nltk`
   - `scikit-learn`
   - `matplotlib`
   - `numpy`

2. Make sure the following text files are available in the working directory:
   - `harrypotter.txt`
   - `Harry_Potter_Camara_Secreta-br.txt`

3. Run the notebook or script step by step:
   - corpus preparation
   - tokenization
   - Word2Vec training
   - semantic analysis
   - PCA visualization
