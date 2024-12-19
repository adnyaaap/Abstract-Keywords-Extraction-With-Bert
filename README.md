Keyword Extraction using Bert and DistilBERT to Enhance Understanding of Articles Abstracts
---
This repository contains the inplementation of models for keyword extraction from article abstracts in the fields of Artificial Intelligences (AI) and Computer Science. The goal is to facilitate efficient indexing, search, and summarization of academic literature.

## Table of Contents
1. Dataset
2. Best Model
3. Model Evaluation
4. API

## Dataset
The dataset used in this project consist of academic article abstracts primaly in the fields of Artificial Intelligence (AI) and Computer Science. Keywords were manually labeled for each abstract to capture the core concepts. The dataset contains approximately 5800 records and was collected from Institute of Advanced Engineering and Science (IAES) and Modern Education and Computer Science Press (MECS Press).

## Best Model
The best-performing model for this task was selected after evaluating multiple approaches. BERT and DistilBERT were trained and fine-tuned for keyword extraction tasks, with thei performance compared based on precision, recall, and F1-Score. The final selection was made based on their ability to generalize and extract accurate keywords from unseen abstracts.

## Model Evaluation
The model evaluation for this task was divided by two level, which are Token Level that measured the ability of the model to classify the B-I-O tokens, and Entity Level that evaluate the result of the extracted keywords from the predicted tokens.

### Token Level
| Tokenization and Model       | Loss   | Precision Micro | Precision Macro | Recall Micro | Recall Macro | F1-Score Micro | F1-Score Macro |
|------------------------------|--------|-----------------|-----------------|--------------|--------------|----------------|----------------|
| **70:30 Split**              |        |                 |                 |              |              |                |                |
| NLTK - DistilBERT            | 0.045  | 0.97            | 0.76            | 0.97         | 0.75         | 0.97           | 0.75           |
| NLTK - BERT                  | 0.049  | 0.97            | 0.77            | 0.97         | 0.75         | 0.97           | 0.76           |
| BERT - DistilBERT            | 0.88   | 0.94            | 0.77            | 0.94         | 0.74         | 0.94           | 0.75           |
| BERT - BERT                  | 0.88   | 0.97            | 0.77            | 0.97         | 0.75         | 0.97           | 0.76           |
| **80:20 Split**              |        |                 |                 |              |              |                |                |
| NLTK - DistilBERT            | 0.04   | 0.97            | 0.77            | 0.94         | 0.76         | 0.94           | 0.76           |
| NLTK - BERT                  | 0.049  | 0.97            | 0.75            | 0.97         | 0.76         | 0.97           | 0.75           |
| BERT - DistilBERT            | 0.084  | 0.94            | 0.76            | 0.94         | 0.76         | 0.94           | 0.76           |
| BERT - BERT                  | 0.07   | 0.94            | 0.76            | 0.94         | 0.76         | 0.94           | 0.76           |


### Entity Level
| Tokenisasi dan Model       | Precision Micro | Precision Macro | Recall Micro | Recall Macro | F1-Score Micro | F1-Score Macro | Mayor Match | Total Match |
|----------------------------|-----------------|-----------------|--------------|--------------|----------------|----------------|-------------|-------------|
| **70:30 Split**            |                 |                 |              |              |                |                |             |             |
| NLTK - DistilBERT          | 0.198           | 0.29           | 0.29         | 0.20         | 0.23           | 0.22           | 34.34%      | 64.64%      |
| NLTK - BERT                | 0.20            | 0.28           | 0.28         | 0.21         | 0.23           | 0.22           | 34.34%      | 66.19%      |
| BERT - DistilBERT          | 0.16            | 0.19           | 0.23         | 0.16         | 0.19           | 0.16           | 29.76%      | 45.72%      |
| BERT - BERT                | 0.19            | 0.28           | 0.16         | 0.23         | 0.24           | 0.22           | 38.72%      | 64.30%      |
| **80:20 Split**            |                 |                |              |              |                |                |             |             |
| NLTK - DistilBERT          | 0.22            | 0.30           | 0.30         | 0.22         | 0.25           | 0.23           | 34.34%      | 66.23%      |
| NLTK - BERT                | 0.21            | 0.28           | 0.28         | 0.21         | 0.24           | 0.22           | 29.76%      | 45.68%      |
| BERT - DistilBERT          | 0.20            | 0.28           | 0.28         | 0.20         | 0.24           | 0.22           | 38.71%      | 64.41%      |
| BERT - BERT                | 0.20            | 0.28           | 0.28         | 0.22         | 0.24           | 0.22           | 34.34%      | 66.23%      |

## API

### Keyword Extraction (`POST /extract_keyword`)
Predicts the keyword from article's abstract and return the keyword from the classified entitiy token.

#### Request
- **Endpoint** `/extract_keyword`
- **Method:** `POST`
- **Request Body (Form Data):**
  - `JSON` : Article Abstract (string)

#### Responses:
- **200 OK:** Keyword extracted successfully
  ```json
  {"keywords": ["sistem rekomendasi","produk perawatan wajah","model Transformer","ekstraksi kata kunci"],"message": "Ok"}
  ````
- **400 Bad Request:** Invalid or missing abstract field
  ```json
  {"error": "Field 'abstract' tidak boleh kosong"}
  ```
