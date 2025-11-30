# Machine Learning and Deep Learning Patterns

## Learning Paradigms
- **Supervised:** Labeled data (Regression, Classification).
- **Unsupervised:** Unlabeled data (Clustering, Dimensionality Reduction).
- **Reinforcement:** Agent learns via rewards/penalties.

## Deep Learning Architectures

### CNN (Convolutional Neural Networks)
**Use Case:** Image processing, Computer Vision.
**Key Layers:** Convolution, Pooling, Fully Connected.

### RNN / LSTM / GRU
**Use Case:** Sequential data (Time series, NLP).
**Key Concept:** Memory of previous inputs.

### Transformers (Attention Mechanism)
**Use Case:** NLP (BERT, GPT), Vision (ViT).
**Key Concept:** Self-attention allows parallel processing of sequences.

## Design Patterns in ML Code

### Pipeline Pattern (Scikit-Learn)
Chaining preprocessing and modeling steps.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('clf', LogisticRegression())
])

pipe.fit(X_train, y_train)
```

### Transfer Learning
**Concept:** Using a pre-trained model (e.g., ResNet, BERT) and fine-tuning it on a smaller, specific dataset.
**Pros:** Faster training, less data required.
