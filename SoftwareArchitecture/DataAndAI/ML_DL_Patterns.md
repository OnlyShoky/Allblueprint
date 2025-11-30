# Machine Learning and Deep Learning Patterns

#machine-learning #deep-learning #ml-patterns #ai

> [!important] ML System Design
> Machine learning isn't just about algorithms—it's about building reliable systems that serve predictions at scale. Design patterns help structure ML code for production.

**Related:** [[MLOps|MLOps]] · [[DataEngineering|Data Engineering]] · [[DataModeling|Data Modeling]] · [[../BestPractices/Testing_TDD_BDD|Testing]]

---

## Learning Paradigms

| Paradigm | Data Type | Examples |
|----------|-----------|----------|
| **Supervised** | Labeled (X, y) | Regression, Classification |
| **Unsupervised** | Unlabeled (X only) | Clustering, Dimensionality Reduction |
| **Reinforcement** | Agent + Environment | Game AI, Robotics |
| **Semi-Supervised** | Mostly unlabeled + some labeled | Self-training, Co-training |

---

## Deep Learning Architectures

### CNN (Convolutional Neural Networks)

**Use Case:** Image processing, Computer Vision  
**Key Layers:** Convolution, Pooling, Fully Connected

> [!success] Vision Tasks
> CNNs are the foundation of image classification, object detection, and segmentation.

**Applications:** Face recognition, medical imaging,  autonomous vehicles

---

### RNN / LSTM / GRU

**Use Case:** Sequential data (Time series, NLP)  
**Key Concept:** Memory of previous inputs

> [!note] Sequential Processing
> Recurrent networks maintain hidden state, making them perfect for sequences.

**Applications:** Stock prediction, language translation, speech recognition

---

### Transformers (Attention Mechanism)

**Use Case:** NLP (BERT, GPT), Vision (ViT), Multi-modal  
**Key Concept:** Self-attention allows parallel processing of sequences

> [!success] Current State-of-the-Art
> Transformers have revolutionized NLP and are now expanding to vision and beyond.

**Applications:** ChatGPT, BERT, image generation (DALL-E), code completion

**Related:** See [[../TrendsAndInnovations/GenAI_LLM|Generative AI integration]].

---

## Design Patterns in ML Code

### Pipeline Pattern (Scikit-Learn)

**Concept:** Chain preprocessing and modeling steps for reproducibility.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('pca', PCA(n_components=10)),
    ('clf', LogisticRegression())
])

pipe.fit(X_train, y_train)
predictions = pipe.predict(X_test)
```

> [!tip] Reproducibility
> Pipelines ensure preprocessing and modeling steps are applied consistently during training and inference.

**Related:** Essential for [[MLOps#Model Deployment|production deployment]].

---

### Transfer Learning

**Concept:** Use pre-trained model (ResNet, BERT) and fine-tune on smaller, specific dataset.

> [!success] Less Data, Faster Training
> Transfer learning lets you leverage knowledge from models trained on massive datasets.

```python
from transformers import BertForSequenceClassification, Trainer

# Load pre-trained BERT
model = BertForSequenceClassification.from_pretrained('bert-base-uncased', num_labels=2)

# Fine-tune on your data
trainer = Trainer(model=model, train_dataset=train_data)
trainer.train()
```

**Pros:** Faster training, less data required, better performance  
**Cons:** Domain mismatch can hurt performance

---

### Feature Store Pattern

**Concept:** Centralized repository for ML features, ensuring consistency between training and serving.

**Problem Solved:** Training/serving skew (features computed differently in training vs production).

> [!important] Eliminate Skew
> Feature stores ensure features are computed identically for training and inference.

**Tools:** Feast, Tecton, AWS SageMaker Feature Store

**Related:** Core of [[MLOps#Feature Engineering|MLOps infrastructure]].

---

### Model Registry Pattern

**Concept:** Centralized storage for trained models with versioning and metadata.

**Features:**
- Model versioning
- Experiment tracking
- Model lineage
- Deployment staging (dev/staging/prod)

**Tools:** MLflow, Weights & Biases, Neptune

**Related:** Required for [[MLOps#Model Deployment|model governance]].

---

## ML-Specific Patterns

### Ensemble Methods

**Concept:** Combine multiple models for better predictions.

**Types:**
- **Bagging:** Random Forest (reduce variance)
- **Boosting:** XGBoost, LightGBM (reduce bias)
- **Stacking:** Train meta-model on predictions

> [!success] Kaggle Winners
> Ensembles almost always win competitions by combining diverse models.

---

### Online Learning

**Concept:** Model updates incrementally as new data arrives.

**Use Case:** Streaming data, concept drift adaptation

```python
from river import linear_model

model = linear_model.LogisticRegression()

# Update model with each new sample
for x, y in stream:
    model.learn_one(x, y)
    prediction = model.predict_one(x)
```

**Related:** Complements [[../ModernArchitectures/Serverless_EventDriven#Stream Processing|stream processing]].

---

## Anti-Patterns

> [!warning] Common ML Mistakes
> - **Data leakage:** Test data  contaminating training
> - **Ignoring class imbalance:** Model predicts majority class always
> - **Not tracking experiments:** Can't reproduce results
> - **No model versioning:** Can't rollback bad deployments
> - **Training/serving skew:** Different feature computation

---

## Further Reading

- Deploy with [[MLOps|MLOps pipelines]]
- Build features from [[DataEngineering|data pipelines]]
- Model data with [[DataModeling|proper schemas]]
- Integrate [[../TrendsAndInnovations/GenAI_LLM|LLMs and generative AI]]
- Test with [[../BestPractices/Testing_TDD_BDD|ML testing frameworks]]

**Tags:** #machine-learning #deep-learning #cnn #transformers #ml-patterns
