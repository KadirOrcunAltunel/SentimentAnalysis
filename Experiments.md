**Datasets**: For the project, I used 3 datasets. My first dataset consists of FiQA and Financial PhraseBank and provides financial sentences with sentiment labels for over 5K financial articles. My second dataset is a compilation of approximately 6K pieces of stock news gathered from multiple Twitter handles. The dataset also includes the sentiment for each piece of news. Finally, my last dataset is a snippet of 400 financial news articles that have the sentiment annotated by experts.
To address class imbalance in the datasets, I introduced *class weights* for logistic regression and XGBoost models, and *focal loss* for BiLSTM, BERT and RoBERTa models.

The ***class_weight=balanced*** parameter in logistic regression assigns a weight to each class based on its frequency.


$$
\text{class weight for class } i = \frac{\text{total number of samples}}{\text{(number of classes} \times \text{number of samples in class } i)}
$$

The minority class receives a higher weight whereas the majority class receives a lower weight. This helps the model to become more sensitive to recall, thus improving F1-score.

The ***sample_weight*** parameter in XGBoost also achieves the same result. However, it is more flexible allowing different weights for each instance.

$$
\text{weight}_c = \frac{\text{Total Number of Samples}}{\text{Number of Samples in Class } c}
$$

***Focal loss*** is a loss function that helps with class imbalance issues. Although it is usually used in object detection, it can also be effective in NLP tasks where class imbalance can be problematic. Focal loss down-weights the loss assigned to well classified examples, focusing on the harder, misclassified examples. For binary classification, the focal loss formula is:

$$
\text{Focal Loss}(p_t) = -\alpha \cdot (1 - p_t)^\gamma \cdot \log(p_t)
$$

And for multiclass classification, the formula is:

$$
\text{Focal Loss} = -\alpha_t \cdot (1 - p_t)^\gamma \cdot \log(p_t)
$$

Where:
- $$p_t$$: the predicted probability for true class
- $$\alpha$$: thescaling factor that helps balance the importance of positive vs. negative classes
- $$\gamma$$: the focusing parameter that adjusts the rate at which easy examples are down-weighted

Here are the performances of all 3 datasets on various models:

### Dataset 1 – Accuracy & F1-Score Performance

| Model                                | Accuracy | F1-Score                                          |
|--------------------------------------|----------|---------------------------------------------------|
| Logistic Regression                  | 0.72     | Negative: 0.21, Neutral: 0.80, Positive: 0.72     |
| Logistic Regression (*class weights*)| 0.72     | Negative: 0.53, Neutral: 0.78, Positive: 0.73     |
| XGBoost                              | 0.68     | Negative: 0.19, Neutral: 0.76, Positive: 0.70     |
| XGBoost (*sample weights*)           | 0.68     | Negative: 0.42, Neutral: 0.75, Positive: 0.69     |
| BiLSTM                               | 0.75     | Negative: 0.41, Neutral: 0.82, Positive: 0.77     |
| BiLSTM (*focal loss*)                | 0.71     | Negative: 0.57, Neutral: 0.75, Positive: 0.75     |
| BERT                                 | 0.80     | Negative: 0.37, Neutral: 0.86, Positive: 0.85     |
| BERT (*focal loss*)                  | 0.79     | Negative: 0.44, Neutral: 0.83, Positive: 0.86     |
| RoBERTa                              | 0.82     | Negative: 0.50, Neutral: 0.86, Positive: 0.88     |
| RoBERTa (*focal loss*)               | 0.81     | Negative: **0.63**, Neutral: 0.83, Positive: 0.88 |



### Dataset 2 – Accuracy & F1-Score Performance

| Model                                 | Accuracy | F1-Score                              |
|-------------------------------------  |----------|---------------------------------------|
| Logistic Regression                   | 0.77     | Negative: 0.63, Positive: 0.84        |
| Logistic Regression (*class weights*) | 0.79     | Negative: 0.73, Positive: 0.83        |
| XGBoost                               | 0.76     | Negative: 0.60, Positive: 0.83        |
| XGBoost (*sample weights*)            | 0.76     | Negative: 0.67, Positive: 0.81        |
| BiLSTM                                | 0.75     | Negative: 0.63, Positive: 0.82        |
| BiLSTM (*focal loss*)                 | 0.73     | Negative: 0.66, Positive: 0.77        |
| BERT                                  | 0.78     | Negative: 0.72, Positive: 0.82        |
| BERT (*focal loss*)                   | 0.81     | Negative: 0.72, Positive: 0.86        |
| RoBERTa                               | 0.84     | Negative: 0.77, Positive: 0.87        |
| RoBERTa (*focal loss*)                | 0.84     | Negative: **0.77**, Positive: 0.87    |



### Dataset 3 – Accuracy & F1-Score Performance

| Model                | Accuracy | F1-Score                              |
|----------------------|----------|---------------------------------------|
| Logistic Regression  | 0.65     | Negative: 0.60, Positive: 0.69        |
| XGBoost              | 0.65     | Negative: 0.60, Positive: 0.69        |
| BiLSTM               | 0.46     | Negative: 0.47, Positive: 0.47        |
| BERT                 | 0.65     | Negative: 0.62, Positive: 0.67        |
| RoBERTa              | 0.88     | Negative: 0.87, Positive: 0.88        |


Based on the charts above, the base RoBERTa model reached the highest accuracy and class-level F1-scores across all models, even in the presence of class imbalance. However, in sentiment analysis, identifying all instances of a target sentiment is critical, making F1-score a more important metric than accuracy in many cases. On the first dataset, which retained significant classimbalance, all models showed improvements when class imbalance techniques were applied. Remarkably, RoBERTa with *focal loss* emerged as the strongest performer for minority class F1-scores, despite a slight decline in accuracy.

On the other hand, for dataset 2 where class imbalance was less notable, RoBERTa outperformed the other models and emerged as the best overall performer. Interestingly, logistic regression with *class weights* also performed very well, coming very close to RoBERTa, underscoring the importance of handling class imbalance effectively. On dataset 3, where classes are balanced RoBERTa was once again the winner. These findings highlight the importance of aligning model evaluation metrics with the specific goals of a sentiment analysis task and adapting strategies to handle varying levels of class imbalance.


