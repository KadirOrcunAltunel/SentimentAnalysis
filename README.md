# Class Imbalance in Sentiment Analysis

Sentiment analysis is an important domain of natural language processing (NLP) that focuses on detecting the emotional tone or sentiment within the text data. This paper evaluated and compared the performance of logistic regression, XGBoost, BiLSTM, BERT and RoBERTa individually in sentiment analysis using three different financial datasets. Although a powerful task for identifying emotional tone, sentiment analysis suffers from class imbalance. 

Lango (2019) highlighted the negative effects of class imbalance on model performance, especially in minority classes. In cases where class imbalance draws issues, using metrics like accuracy can be misleading, as it disproportionately reflects the performance of majority classes. Lango (2019) emphasized the need for metrics such as F1- score to better evaluate model effectiveness on both majority and minority classes. 

The three datasets I used in this paper varied significantly in their class distribution. On the first dataset, the minority class made up 15% of the dataset while in the second dataset the minority class was at 36%. On the third dataset, the minority class made up 46%. In this study, to assess model performance, I used class-level F1-scores for each sentiment class individually. 

The results of this study showed that applying techniques such as *class weights*, *sample weights*, and *focal loss* to address class imbalances significantly improved the F1-scores of the models. This underscores the importance of aligning evaluation metrics with task-specific needs. However, these findings are specific to the datasets used in this study and may vary with other datasets or domains.
