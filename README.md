# Phishing URL Detection using Machine Learning

This repository contains a machine learning project designed to detect phishing URLs using only their textual structure.  
The system applies lexical analysis, keyword detection, and character-level n-grams to classify URLs as benign or malicious.  
Two models were implemented: **Random Forest** and **Logistic Regression**, both evaluated with domain-grouped cross-validation.

---

## Project Overview

Phishing websites often attempt to imitate trusted services by using misleading URLs, unusual patterns, or suspicious keywords.  
This project explores how machine learning can identify these patterns without relying on webpage content or external metadata.

The full pipeline includes:

- Dataset preparation  
- Feature extraction (lexical + keyword flags + TF-IDF n-grams)  
- Model training and cross-validation  
- Performance evaluation and confusion matrices  

---

## Dataset

The dataset was obtained from Kaggle:

**Malicious and Benign URLs Dataset**  
https://www.kaggle.com/datasets/siddharthkumar25/malicious-and-benign-urls

From the original ~300k URLs, a subset of **50,000 samples** was used:

- **25,000 benign**
- **25,000 phishing**

Each URL has:
- The raw URL string  
- A binary label (0 = benign, 1 = phishing)

Grouping by domain ensures no leakage between training and testing.

---

## Feature Extraction

### **1. Lexical Features**
- URL length  
- Number of digits, dots, and symbols (`-`, `/`, `@`, `=`)  
- Number of subdomains  
- URL depth  
- Presence of HTTPS  
- Presence of IP address in the hostname  

### **2. Keyword Flags**
Binary indicators for phishing-related tokens such as:
`login`, `account`, `verify`, `secure`, `update`, `password`.

### **3. Character-level TF-IDF n-grams**
Using n-grams of size 3–5 to capture patterns like:
- `"log"`, `"gin"`, `"acc"`, `"sec"`

These help represent the structure and intent of the URL.

---

## Models

Two classic machine learning models were implemented:

- **Random Forest**  
- **Logistic Regression (SAGA)**

Both models were evaluated using **GroupKFold** by domain.
