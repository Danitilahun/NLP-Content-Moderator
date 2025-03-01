# Amharic Text Moderation Datasets

This repository contains a curated list of datasets for various Natural Language Processing (NLP) tasks, including:

- **Named Entity Recognition (NER)**
- **Text Classification**
- **Sentiment Analysis**
- **Topic Classification** *(Upcoming)*

All resource links will be added or updated as new datasets are included.

---

## Table of Contents

- [Named Entity Recognition (NER)](#named-entity-recognition-ner)
- [Text Classification](#text-classification)
- [Sentiment Analysis](#sentiment-analysis)
- [Topic Classification](#topic-classification)

---

## Named Entity Recognition (NER)

Below is a list of datasets available for Named Entity Recognition:

1. **Amharic Named Entity Recognition Dataset (Hugging Face)**  
   **Description:** A dataset for Amharic Named Entity Recognition available on Hugging Face. This dataset includes annotated Amharic texts suitable for NER tasks.  
   **Link:** [Amharic NER Dataset](https://huggingface.co/datasets/rasyosef/amharic-named-entity-recognition)

2. **Masakhane NER Amharic Train Data**  
   **Description:** The training data for Amharic NER from the Masakhane NER project. This file contains annotated text data for Named Entity Recognition tasks in Amharic.  
   **Link:** [Masakhane NER Amharic Train Data](https://github.com/masakhane-io/masakhane-ner/blob/main/data/amh/train.txt)

3. **ANEC: An Amharic Named Entity Corpus**  
   **Description:** An Amharic Named Entity Corpus provided by Ebrahimc on GitHub, containing annotated Amharic named entities for NER tasks.  
   **Link:** [ANEC: An Amharic Named Entity Corpus](https://github.com/Ebrahimc/ANEC-An-Amharic-Named-Entity-Corpus-/blob/main/Amharic%20NER%20Corpus.txt)

*(Add more datasets as needed.)*

---

## Text Classification

Below is the updated list of datasets available for Text Classification in Amharic:

1. **Amharic Hate Speech Classification Dataset**  
	**Description:** A dataset available on Hugging Face for the classification of Amharic text into hate speech categories, including ethnic, religious, and gender-based hate speech.  
	**Link:** [Amharic Hate Speech Classification Dataset](https://huggingface.co/datasets/uhhlt/amharichatespeechranlp)

2. **Hate Speech Detection in Amharic Dataset**  
	**Description:** A dataset for hate speech detection in Amharic, containing labeled data for identifying harmful content.  
	**Link:** [Hate Speech Detection in Amharic Dataset](https://github.com/nathyBekele/Hate-Speech-Detection-in-Amharic-Language/tree/main/DataSet)

3. **Amharic Offensive/Hate Speech Detection (Zenodo)**  
	**Description:** This dataset, hosted on Zenodo, provides labeled Amharic text for offensive or hate speech detection tasks.  
	**Link:** [Zenodo Record 5036437](https://zenodo.org/records/5036437)

4. **Amharic Offensive/Hate Speech Detection (Mendeley)**  
	**Description:** This Mendeley dataset contains labeled Amharic text for offensive or hate speech detection.  
	**Link:** [Mendeley Dataset](https://data.mendeley.com/datasets/gw3fdtw5v7/2)

5. **Amharic Hate Speech Data (RANLP 2023)**  
	**Description:** A dataset from the RANLP 2023 conference, containing Amharic hate speech data for text classification tasks.  
	**Link:** [RANLP 2023 Dataset](https://github.com/uhh-lt/AmharicHateSpeech/blob/main/Data/RANLP2023/train.csv)
   
*(Add more datasets as needed.)*

---
Here is the updated list of available datasets for Sentiment Analysis in Amharic:

1. **Amharic Sentiment Dataset**  
	**Description:** A sentiment analysis dataset for the Amharic language, containing labeled sentiment data for various text samples.  
	**Link:** [Amharic Sentiment Dataset](https://huggingface.co/datasets/rasyosef/amharic-sentiment)

2. **Afrisent Semeval 2023 Amharic Dataset**  
	**Description:** A dataset provided as part of the Afrisent Semeval 2023 challenge, containing Amharic language data for sentiment analysis tasks.  
	**Link:** [Afrisent Semeval 2023 Amharic Dataset](https://github.com/afrisenti-semeval/afrisent-semeval-2023/tree/main/data/amh)

3. **Masakhane AfriSenti**  
	**Description:** A Twitter sentiment analysis benchmark for multiple African languages (including Amharic), curated by the Masakhane community.  
	**Link:** [Masakhane AfriSenti](https://huggingface.co/datasets/masakhane/afrisenti)

4. **Amharic Word-Level Sentiment Dataset (Kaggle)**  
	**Description:** A dataset for word-level sentiment analysis in Amharic available on Kaggle.  
	**Link:** [Amharic Word-Level Sentiment Dataset](https://www.kaggle.com/datasets/seidissamohamed/amharic-word-level-sentiment-dataset/code)

5. **Amharic YouTube Comments Sentiment**  
	**Description:** This dataset focuses on Amharic comments extracted from YouTube, labeled for sentiment analysis tasks (positive, negative, neutral).  
	**Link:** [Amharic YouTube Comments Sentiment Dataset](https://www.kaggle.com/datasets/mulukensholaye/amharic-youtube-comments-sentiment)
   
*(Add more datasets as needed.)*

---

## Topic Classification

**Objective**: Automatically assign categories such as Religion, Ethnicity, Politics, etc., to a given text.

**Dataset Requirements**:
- Currently, no datasets are available for topic classification in Amharic.
- We plan to create our own dataset for topic classification, which will cover the following categories:
  - **Religion** (e.g., discussions on faith, doctrine, inter-religious relations).
  - **Ethnicity** (e.g., historical narratives, ethnic identity topics).
  - **Politics** (e.g., government, elections, party affiliations).
  - Other relevant categories (e.g., social issues, gender discussions).

We will prepare the necessary datasets and make them available once they are collected and annotated.

*(Add more datasets as needed.)*

---

## Data Collection Strategy

To create comprehensive datasets, we will use the following strategies:

- **Transliteration Tool**: We will use the [**Amharic Transliteration Tool**](https://accentgenerator.com/transliteration/english-to-amharic-typing/?utm_source=chatgpt.com#google_vignette) to convert English-written Amharic into proper Amharic text. This tool helps standardize the transcription of Amharic content when it is written in Roman script.
  
- **Data Collection from Social Media Platforms**: We will gather data from popular social media platforms where Amharic content is prevalent:
  - **TikTok**
  - **Facebook**
  - **Twitter**
  - **Telegram**

These platforms provide a wealth of publicly available user-generated content, which will be used to create datasets that are rich in real-world, diverse, and conversational text.

## Final Notes

- This repository will continue to be updated with new datasets as they become available.
- The inclusion of high-quality datasets for each NLP task is crucial for building effective and fair Amharic text moderation models.
- We encourage contributions from the community, including the creation of new datasets or improvements to existing datasets.

---