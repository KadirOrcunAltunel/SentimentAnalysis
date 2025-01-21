This project follows 3 approaches:
1. Logistic regression and XGBoost with TF-IDF Feature Extraction
2. BiLSTM with GloVe Word Embeddings
3. Transformer Architectures: BERT and RoBERTa

#### Logistic Regression and XGBoost with TF- IDF Feature Extraction

I used logistic regression and XGBoost as my base models. To transform textual data into numerical features, I applied TF-IDF. Then, I trained logistic regression and XGBoost on these TF-IDF features.TF-IDF is an established technique that captures the importance of terms in relation to their frequency within documents and entire dataset.

The formula for calculating the TF-IDF value is as follows:

\[
w_{x, y} = tf_{x, y} \times \log\left(\frac{N}{df_x}\right)
\]

Where:
- \( w_{x, y} \): TF-IDF weight for term \( x \) in document \( y \).
- \( tf_{x, y} \): Frequency of term \( x \) in document \( y \).
- \( df_x \): Number of documents containing term \( x \).
- \( N \): Total number of documents.
