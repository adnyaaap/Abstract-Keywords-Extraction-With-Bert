Keyword Extraction using Bert and DistilBERT to Enhance Understanding of Articles Abstracts
---
This repository contains the inplementation of models for keyword extraction from article abstracts in the fields of Artificial Intelligences (AI) and Computer Science. The goal is to facilitate efficient indexing, search, and summarization of academic literature.

## Table of Contents
1. Dataset
2. Best Model
3. Model Evaluation
4. API

## Endpoint Description

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
