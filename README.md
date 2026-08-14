# An Explainable Customer Segmentation and Prediction Framework

## 📌 Overview

This project presents an **explainable customer segmentation and prediction framework** for real-time customer engagement in the food delivery industry. The framework combines unsupervised learning, explainability, and supervised machine learning to identify customer segments and predict the segment of new customers using their behavioral information.

The proposed approach consists of three main stages:

**Customer Segmentation → Cluster Explanation → Segment Prediction**

The framework first applies **RFM (Recency, Frequency, Monetary) analysis** with K-Means clustering to identify meaningful customer segments. **Formal Concept Analysis (FCA)** is then used to interpret and explain the characteristics of each segment. Finally, machine learning models are trained to predict the appropriate customer segment for new customers using behavioral features that can be collected during the ordering process.

---

## 🎯 Objectives

* Identify meaningful customer segments using transactional behavior.
* Evaluate the effectiveness of adaptive recency for customer segmentation.
* Improve the interpretability of discovered customer segments.
* Predict the segment of new customers before sufficient RFM history is available.
* Support personalized and timely customer engagement strategies.

---

## 🗂️ Dataset

The study uses the **Careem Foods Dubai dataset** containing historical customer information spanning multiple years.

For the experimental analysis, a **54-day transactional window from 1 March 2024 to 24 April 2024** was used.

The dataset contains transactional and behavioral attributes such as:

* Customer ID
* Order timestamps
* Delivery time
* Basket amount
* GMV
* Distance travelled
* Payment type
* Food categories
* Customer zones
* First and last order information

After preprocessing and feature engineering, the final dataset contained **314,786 unique customers** and **22 selected features**.

> The original dataset is not included in this repository due to data availability and size considerations.

---

## 🔬 Methodology

### 1. Data Preprocessing

The raw transactional data was cleaned and transformed through:

* Duplicate removal
* Data cleaning and normalization
* Category processing
* Handling of categorical variables
* Feature engineering
* Customer-level aggregation

### 2. Customer Segmentation

RFM features were calculated for each customer:

* **Recency** – How recently the customer placed an order
* **Frequency** – How frequently the customer ordered
* **Monetary** – How much the customer spent

Several clustering approaches were investigated, including:

* K-Means
* HDBSCAN
* DBSCAN
* Agglomerative Clustering
* BIRCH
* UMAP + HDBSCAN

K-Means with the standard **RFM features** provided the strongest clustering performance.

### 3. Adaptive Recency

An adaptive recency measure based on customers' inter-order intervals was also investigated:

[
Adaptive\ Recency = e^{-d/\mu}
]

where `d` represents the time since the customer's previous order and `μ` represents the average inter-order interval.

The experiments showed that adding adaptive recency did **not improve** the clustering performance compared with standard RFM features.

### 4. Explainability using FCA

**Formal Concept Analysis (FCA)** was applied to explain the discovered customer clusters.

FCA was used to:

* Identify characteristic behavioral patterns
* Generate interpretable cluster rules
* Describe the distinguishing properties of customer segments
* Support meaningful business-oriented segment interpretation

Examples of interpreted segments include:

* Loyal Customers
* Frequent Buyers
* Premium Customers
* At-Risk Customers

### 5. Customer Segment Prediction

After clustering, supervised learning models were trained to predict customer segments using behavioral features rather than relying directly on RFM scores.

The following models were evaluated:

* Random Forest
* XGBoost
* Multi-Layer Perceptron (MLP)

**XGBoost achieved the best predictive performance.**

---

## 📊 Results

### Clustering Performance

The best-performing RFM-based K-Means model achieved:

| Metric                  |          Score |
| ----------------------- | -------------: |
| Silhouette Score        |     **0.5036** |
| Calinski-Harabasz Index | **333,622.55** |
| Davies-Bouldin Index    |     **0.7539** |

The RFM-only configuration performed better than the configuration incorporating adaptive recency.

### Prediction Performance

| Model         |   Accuracy |
| ------------- | ---------: |
| Random Forest |     55.13% |
| XGBoost       | **57.23%** |
| MLP           |     55.30% |
| Tuned MLP     |     55.32% |

**XGBoost was selected as the final prediction model with an accuracy of 57.23%.**

---

## 🧩 Framework

```text
                    Transactional Data
                           │
                           ▼
                  Data Preprocessing
                           │
                           ▼
                    Feature Engineering
                           │
                           ▼
                    RFM Feature Creation
                           │
                           ▼
                    K-Means Clustering
                           │
                           ▼
                 Customer Segmentation
                           │
                           ▼
              Formal Concept Analysis (FCA)
                           │
                           ▼
                 Explainable Segments
                           │
                           ▼
              Behavioral Feature Extraction
                           │
                           ▼
                 Segment Prediction Models
                           │
                           ▼
                       XGBoost
                           │
                           ▼
             Predicted Customer Segment
```

---

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* RAPIDS
* cuDF
* cuML
* CuPy
* HDBSCAN
* UMAP
* FCAPY
* Jupyter Notebook
* Google Colab / Kaggle GPU

---

## 📁 Project Structure

```text
Expanatory-Customer-segmentation-and-Prediction/
│
├── README.md
├── notebooks/
│   └── customer_segmentation_prediction.ipynb
│
├── results/
│   └── ...
│
├── src/
│   └── ...
│
├── requirements.txt
└── .gitignore
```

---

## 🔑 Key Contributions

* Developed an **explainable customer segmentation framework** combining clustering and Formal Concept Analysis.
* Investigated **adaptive recency** as an alternative RFM component.
* Compared multiple clustering algorithms for customer segmentation.
* Developed a predictive layer for assigning **new customers to existing customer segments**.
* Evaluated Random Forest, XGBoost, and MLP for segment prediction.
* Achieved the best prediction accuracy of **57.23% using XGBoost**.

---

## 🚀 Future Work

Future extensions of this work may include:

* Continuous/online learning for changing customer behavior.
* Improved prediction performance through additional behavioral and contextual features.
* Real-time deployment of the prediction framework.
* Integration of customer-segment knowledge into a knowledge graph.
* Further investigation of adaptive temporal features.

---

## 👩‍💻 Author

**Komal Wahid**

MS Data Science
National University of Sciences and Technology (NUST)

---

## 📄 Research

This repository contains the implementation and experimental work associated with the research project:

**"An Explainable Customer Segmentation and Prediction Framework for Real-Time Customer Engagement"**
