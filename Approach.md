This project follows 3 approaches:
1. Logistic regression and XGBoost with TF-IDF Feature Extraction
2. BiLSTM with GloVe Word Embeddings
3. Transformer Architectures: BERT and RoBERTa

#### Logistic Regression and XGBoost with TF- IDF Feature Extraction

I used logistic regression and XGBoost as my base models. To transform textual data into numerical features, I applied TF-IDF. Then, I trained logistic regression and XGBoost on these TF-IDF features.TF-IDF is an established technique that captures the importance of terms in relation to their frequency within documents and entire dataset.

The formula for calculating the TF-IDF value is as follows:

$$
w_{x, y} = tf_{x, y} \times \log \left( \frac{N}{df_x} \right)
$$

Where:
- $w_{x, y}$: TF-IDF weight for term $x$ in document $y$.
- $tf_{x, y}$: Frequency of term $x$ in document $y$.
- $df_x$: Number of documents containing term $x$.
- $N$: Total number of documents.

TF-IDF works by assigning higher weights to the terms that are frequent in a document but rare across corpus.
As a linear classifier, logistic regression performs a probability prediction based on a sentiment class. It is highly effective on high dimensional data like TF-IDF matrices.

In contrast, XGBoost is an ensemble method. It is designed for building gradient boosted decision trees. It has especially shown high performance in datasets where complex patterns are observed.

#### BiLSTM with GloVe Word Embeddings

Next, I used a deep learning approach using BiLSTM with GloVe word embeddings. GloVe is a pre-trained word embedding model that transforms textual data into numerical features. GloVe provides dense vector representations that are the co- occurrence patterns in large text corpora. GloVe vectors are loaded into BiLSTM model as an embedding layer.
BiLSTM differs from traditional LSTM model by processing the input sequence in both directions at the same time. In BiLSTM, one LSTM process reads input in forward direction and the other one reads the input in backward direction. As a result, the model can gain contextual insights from past and future words within a sequence.

![LSTM vs. BiLSTM](https://github.com/KadirOrcunAltunel/SentimentAnalysis/blob/main/images/LSTM%20and%20BiLSTM.png)

I also introduced regularization by applying a dropout layer to prevent overfitting. Depending on the sentiment classification (binary vs. multiclass), I used a fully connected dense output layer with sigmoid or softmax activation.

#### Transformer Architectures: BERT and RoBERTa

For the final approach for my sentiment analysis task, I utilized transformer architectures. BERT is one of the most popular transformer architectures used in sentiment analysis. Its ability to capture bidirectional context makes it well suited for comprehending complex language patterns. For this paper, I utilized BERT-base architecture. BERT-base architecture consists of 12 transformer layers with 768 hidden units in each layer, and each layer has 12 self-attention heads. The architecture contains approximately 110 million parameters, which balance performance and computational efficiency.

![BERT](https://github.com/KadirOrcunAltunel/SentimentAnalysis/blob/main/images/BERT.png)

I also compared the performance of BERT- base with another transformer-based architecture, RoBERTa. RoBERTa is an optimized variant of BERT. RoBERTa introduces dynamic masking to improve the training process of BERT. In dynamic masking, different masked tokens are created for the same input sequence during each epoch of training. This allows model to generalize better by learning various contexts for each word.

In BERT, a model is introduced to pairs of sentences, and it is tasked with determining whether the second sentence logically follows the first in the original context. This is referred to as **Next Sentence Prediction (NSP)**. RoBERTa does not use NSP for the pretraining process. Instead, it relies on larger datasets and longer training sequences which improves overall performance of the model.
