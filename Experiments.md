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
