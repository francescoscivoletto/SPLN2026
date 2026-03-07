# SPLN2026
First homework for SPLN course
# Medical Dictionary Extraction

This Homework consists in extracting information from a medical dictionary in XML format and converting it into a structured JSON dictionary.

The objective of the assignment was to process the XML file and obtain a clean and usable dictionary containing the main information for each medical concept.

## Project description

The XML dictionary contains different medical concepts.  
Each concept includes:

- an identifier
- the term in Galician
- the domain of the term
- possible synonyms
- variants
- notes
- translations into other languages (Spanish, English, Portuguese and Latin)

The goal of the project was to automatically extract this information and organize it in a Python dictionary.

## Method

The XML file is first read using Python.  
Then the file is divided into different concept entries.

Each entry is processed by the function `processar_conceito`, which uses regular expressions to extract the relevant parts of the text.

The function identifies:

- the concept ID
- the Galician term
- the domain
- synonyms (SIN)
- variants (VAR)
- notes (Nota)
- translations in other languages

All the extracted information is stored in a Python dictionary.

Finally, the dictionary is exported as a JSON file.

## Output

The final result is a JSON dictionary where each concept ID corresponds to an entry with the extracted information.

Example:

```json
{
  "1": {
    "galego": "ala",
    "dom": "Anatomía",
    "es": "ala",
    "en": "wing",
    "pt": "asa",
    "la": "ala"
  }
}
