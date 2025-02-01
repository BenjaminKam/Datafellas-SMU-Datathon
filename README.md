# README: Dataset Cleaning and Processing

## Overview

This script performs text preprocessing, named entity recognition (NER), and relationship extraction on a dataset containing unstructured text. The primary goal is to clean the text, extract meaningful entities, and establish relationships between them for further analysis.

## Prerequisites

Before running the script, ensure that the following dependencies are installed:

```sh
pip install spacy pandas nltk contractions stanza openai transformers networkx matplotlib scipy
```

Additionally, you need to download the required NLTK and SpaCy resources:

```python
import nltk
nltk.download('stopwords')
nltk.download('punkt')
nltk.download('wordnet')

import spacy
spacy.cli.download("en_core_web_sm")
```

## Dataset

- **Input File:** `wikileaks_parsed.xlsx`
- **Output Files:**
  - `preprocessed_text.xlsx` – Contains cleaned and tokenized text
  - `entities.xlsx` – Extracted named entities
  - `relationships_extracted_separated.xlsx` – Extracted relationships between entities

## Processing Steps

### 1. Text Preprocessing

- Expands contractions (e.g., "don't" → "do not").
- Converts text to lowercase.
- Replaces abbreviations based on a predefined mapping.
- Removes punctuation and standalone numbers.
- Normalizes currency formats (e.g., "€4278" → "4278 euros").
- Removes common stopwords and domain-specific stopwords.
- Performs lemmatization to normalize words to their base forms.

### 2. Tokenization & Sentence Segmentation

- Tokenizes the processed text into individual words.
- Segments the text into meaningful sentences.

### 3. Named Entity Recognition (NER)

- Identifies and extracts entities (e.g., organizations, people, locations) using SpaCy.
- Formats the extracted entities for better readability.

### 4. Relationship Extraction

- Uses Stanford CoreNLP’s OpenIE model to extract relationships between entities.
- Outputs relationships in the format `{entity1, relation, entity2}`.
- Saves the extracted relationships to an Excel file.

## Running the Script

1. Place the input dataset (`wikileaks_parsed.xlsx`) in the script directory.
2. Run the script using:

```sh
python dataset_cleaning.py
```

3. The processed outputs will be saved as Excel files in the same directory.

## Notes

- Ensure that the Stanford CoreNLP server is running before executing relationship extraction.
- Modify `abbreviation_map` and `domain_stopwords` as needed for domain-specific use cases.

## Troubleshooting

- If `scipy` or other dependencies are missing, manually install them using:
  ```sh
  pip install scipy
  ```
- If the CoreNLP client fails, ensure the server is running with:
  ```sh
  stanza.install_corenlp()
  ```
- If SpaCy’s model is not found, manually download it:
  ```sh
  python -m spacy download en_core_web_sm
  ```

## Author

This script was developed for extracting insights from unstructured text in the context of legal documents, privacy policies, and investigative reports.
