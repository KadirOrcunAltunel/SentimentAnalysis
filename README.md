# Class Imbalance in Sentiment Analysis

This repository contains the implementation and findings of **"Class Imbalance in Sentiment Analysis"**, a project conducted by **Kadir Altunel** at the New Jersey Institute of Technology. The project explores various machine learning and deep learning models for sentiment analysis with a focus on addressing class imbalance challenges.

## Overview

Sentiment analysis is an important natural language processing (NLP) task aimed at determining the emotional tone in text data. This project evaluates the performance of traditional and modern machine learning models on three financial datasets, focusing on the prevalent issue of class imbalance. In the project:

- [Abstract](Abstract.md): A summary of the project and its key findings.
- [Introduction](Introduction.md): Background and context of the project, including its goals and significance.



## Approaches and Models

The project employs the following methods. For a detailed breakdown, see [Approach](Approach.md). Below is a summary:


1. **Logistic Regression and XGBoost**  
   - Feature extraction using TF-IDF.
   - Class-weighting and sample-weighting techniques to address class imbalance.

2. **BiLSTM with GloVe Word Embeddings**  
   - Leveraging pre-trained GloVe embeddings for contextual insights.
   - Use of focal loss to enhance minority class performance.

3. **Transformer Architectures: BERT and RoBERTa**  
   - Pre-trained BERT and optimized RoBERTa models for bidirectional contextual understanding.
   - Integration of dynamic masking and focal loss for improved performance.

## Datasets

Three datasets were used for evaluation:
1. **Financial Data Analysis Dataset**: Sentiment-labeled sentences from financial articles.
2. **Stock-Market Sentiment Dataset**: Stock-related news from Twitter.
3. **Sentiment-Labeled Financial News Dataset**: Expert-annotated financial news snippets.

## Key Findings

- Handling class imbalance significantly improved model performance on minority classes.
- RoBERTa achieved the highest overall accuracy and F1-scores across all datasets.
- Metrics like F1-score were shown to provide a more balanced evaluation compared to accuracy, especially in imbalanced datasets.

For detailed information, see:
- [Experiments](Experiments.md)

## Techniques for Class Imbalance

- **Class weights**: Applied in logistic regression and XGBoost to assign higher importance to minority classes.
- **Sample weights**: Fine-grained instance weighting in XGBoost.
- **Focal loss**: Adjusts the loss function to prioritize misclassified examples, effective for BiLSTM, BERT, and RoBERTa.

For more information, see:
- [Experiments](Experiments.md)

## Results

Detailed performance metrics (accuracy and F1-scores) for all models across datasets are available in the project.
For more details, see:
- [Experiments](Experiments.md)
- [Conclusion](Conclusion.md)

## Future Work

- Data augmentation techniques such as back-translation and word insertion.
- Domain-specific fine-tuning of BERT and RoBERTa for enhanced contextual understanding.

## References

The full list of references can be found in the accompanying paper. Please refer to [References](References.md)

## Code and Experiments


