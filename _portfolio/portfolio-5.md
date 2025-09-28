---
title: "Sarcasm detection in news headlines"
excerpt: "Tackles sarcasm detection on news headlines using deep NLP methods (LSTM, BERT) and also evaluates performance changes with varying embedding models"
collection: portfolio
---
**Stack:** Python | Keras | TensorFlow | NLTK | pandas | Word2Vec | BERT | LSTMs  
## Overview  

This project tackles sarcasm detection on news headlines using deep NLP methods. I used the *“News Headlines Dataset for Sarcasm Prediction”* and experimented with embeddings (Word2Vec, BERT) and recurrent models (LSTM) to distinguish sarcastic vs non-sarcastic headlines.

## Data & Approach  

- **Dataset:** Headlines labeled with `is_sarcastic` (0 or 1) along with their article link. :contentReference[oaicite:0]{index=0}  
- **Preprocessing & features:**  
  - Tokenization, lowercasing, stop-word removal via NLTK  
  - Embedding strategies: Word2Vec pretrained vectors, fine-tuned BERT embeddings  
- **Models evaluated:**  
  - LSTM (baseline)  
  - BERT-based classifier  
  - Hybrid architectures combining embeddings + LSTM layers  


## Results & Learnings  

- The models achieved competitive classification accuracy and F1 scores (detailed in the report).  
- Word2Vec + LSTM baseline provided a strong starting point; BERT embeddings improved robustness on edge cases.  
- Observed challenges included class imbalance, subtle lexical cues, and sarcasm’s dependency on context beyond a headline.


## Links to Code & Report  

- **Repository (code & notebooks):**  
  [prasadboi/Sarcasm-detection-in-news-headlines](https://github.com/prasadboi/Sarcasm-detection-in-news-headlines/)  
- **Detailed write-up / report:**  
  (Should be available in the same repo—check for a `report.md`, `report.pdf`, or `docs/` folder)


## Representative Snippets & Examples

1. config / hyperparameters snippet

```python
EMBEDDING_DIM = 300
LSTM_UNITS = 128
DROPOUT_RATE = 0.3
BATCH_SIZE = 64
EPOCHS = 10
LEARNING_RATE = 2e-5
MAX_SEQ_LEN = 40
```

2. 🚀 train loop / model snippet

```python
from tensorflow.keras import Model
from tensorflow.keras.layers import Input, LSTM, Dense, Dropout, Bidirectional
from transformers import TFBertModel

# Example: BERT + LSTM
input_ids = Input(shape=(MAX_SEQ_LEN,), dtype='int32')
attention_mask = Input(shape=(MAX_SEQ_LEN,), dtype='int32')

bert_out = TFBertModel.from_pretrained('bert-base-uncased')(input_ids, attention_mask=attention_mask)[0]
lstm_out = Bidirectional(LSTM(LSTM_UNITS, return_sequences=False))(bert_out)
drop = Dropout(DROPOUT_RATE)(lstm_out)
out = Dense(1, activation='sigmoid')(drop)

model = Model(inputs=[input_ids, attention_mask], outputs=out)
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
```
