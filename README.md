# 🛍️ Shopper Spectrum – Customer Segmentation & Product Recommendation

[![Streamlit App](https://img.shields.io/badge/Live%20App-Streamlit-FF4B4B?logo=streamlit&logoColor=white)](https://project-4-shopperspectrum-segmentation-2ptwvgivtsdfuyqgxqmxwr.streamlit.app/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> A data-driven web application that segments customers using RFM analysis + KMeans clustering, and recommends similar products using cosine similarity — all wrapped in an interactive Streamlit UI.

---

## 📌 Table of Contents

1. [Project Overview](#-project-overview)
2. [Live Demo](#-live-demo)
3. [Features](#-features)
4. [Project Structure](#-project-structure)
5. [Dataset](#-dataset)
6. [Methodology](#-methodology)
   - [EDA](#exploratory-data-analysis-eda)
   - [RFM Feature Engineering](#rfm-feature-engineering)
   - [KMeans Clustering](#kmeans-clustering)
   - [Product Recommendation](#product-recommendation)
7. [Customer Segments](#-customer-segments)
8. [App Screenshots](#-app-screenshots)
9. [Getting Started](#-getting-started)
10. [Tech Stack](#-tech-stack)
11. [Author](#-author)

---

## 📖 Project Overview

**Shopper Spectrum** analyzes transactional data from an online retail store to answer two key business questions:

1. **Who are our customers?** — Identify behavioral groups using the RFM (Recency, Frequency, Monetary) model and KMeans clustering.
2. **What else might a customer want to buy?** — Surface related products using item-based collaborative filtering with cosine similarity.

The end product is a fully interactive **Streamlit web app** where users can input customer metrics or a product name and get instant predictions/recommendations.

---

## 🌐 Live Demo

👉 **[Launch the App](https://project-4-shopperspectrum-segmentation-2ptwvgivtsdfuyqgxqmxwr.streamlit.app/)**

---

## ✨ Features

| Feature | Description |
|---|---|
| 🎯 **Customer Segmentation** | Classify customers into 4 behavioral groups based on RFM values |
| 🤖 **Segment Prediction** | Enter Recency, Frequency & Monetary values to predict the customer segment |
| 🧠 **Product Recommendation** | Enter a product name to get 5 similar product recommendations |
| 🔍 **Fuzzy Matching** | Handles approximate product name inputs using fuzzy string matching |
| 📊 **EDA Notebook** | Full exploratory analysis with visualizations in Jupyter |

---

## 📁 Project Structure

```
Project-4-Shopper_spectrum-segmentation/
│
├── data/
│   └── online_retail.csv          # Raw transactional dataset
│
├── models/
│   ├── rfm_kmeans_model.pkl        # Trained KMeans model (k=4)
│   ├── rfm_scaler.pkl              # StandardScaler for RFM features
│   └── product_similarity.pkl     # Cosine similarity matrix for products
│
├── output_images/
│   ├── Screenshot 2025-08-03 191455.png
│   └── Screenshot 2025-08-03 191508.png
│
├── Shopper_Spectrum.ipynb          # EDA, feature engineering & model training notebook
├── app.py                          # Streamlit web application
├── requirements.txt                # Python dependencies
└── README.md
```

---

## 📦 Dataset

- **Source:** [UCI Online Retail Dataset](https://archive.ics.uci.edu/ml/datasets/Online+Retail)
- **File:** `data/online_retail.csv`
- **Description:** Transactional data for a UK-based online retail store (2010–2011)

| Column | Description |
|---|---|
| `InvoiceNo` | Unique invoice number (prefix `C` = cancelled) |
| `StockCode` | Product code |
| `Description` | Product name |
| `Quantity` | Units purchased per transaction |
| `InvoiceDate` | Date and time of the transaction |
| `UnitPrice` | Price per unit (£) |
| `CustomerID` | Unique customer identifier |
| `Country` | Customer's country |

**Preprocessing steps:**
- Removed rows with missing `CustomerID`
- Removed cancelled transactions (`InvoiceNo` starting with `C`)
- Filtered out negative or zero `Quantity` and `UnitPrice`
- Added `TotalPrice = Quantity × UnitPrice`
- Dropped duplicate records

---

## 🧪 Methodology

### Exploratory Data Analysis (EDA)

The notebook covers several key visualizations:

- 📅 **Transactions Over Time** — Monthly transaction trend to identify seasonality
- 🌍 **Sales by Country** — Top 10 countries by transaction volume
- 🏆 **Top 10 Best-Selling Products** — By total quantity sold
- 💵 **Invoice Amount Distribution** — Spread of order values
- 👤 **Customer Monetary Value Distribution** — Total spend per customer
- 📦 **Quantity & Price Distributions** — Understanding purchase behavior

---

### RFM Feature Engineering

Each customer is described by three metrics computed from their transaction history:

| Metric | Definition |
|---|---|
| **Recency (R)** | Days since the customer's last purchase |
| **Frequency (F)** | Number of unique invoices (purchases) |
| **Monetary (M)** | Total amount spent |

Features are standardized using `StandardScaler` before clustering.

---

### KMeans Clustering

- The optimal number of clusters (**k = 4**) was selected using the **Elbow Method** and **Silhouette Score**.
- The trained model and scaler are saved as `.pkl` files for use in the app.

---

### Product Recommendation

- A **customer-product pivot table** is built (rows = customers, columns = product descriptions, values = quantity purchased).
- **Cosine similarity** is computed between all product vectors (item-based collaborative filtering).
- Given a product name, the top 5 most similar products are returned.
- **Fuzzy matching** (`fuzzywuzzy`) is used as a fallback when an exact product name is not found.

---

## 👥 Customer Segments

| Cluster | Segment | Description |
|---|---|---|
| 0 | 🟢 **Regular Buyer** | Purchases consistently with moderate RFM values |
| 1 | 🔴 **At-Risk Customer** | High recency (hasn't purchased recently), low engagement |
| 2 | 🌟 **High-Value Customer** | Low recency, high frequency and monetary value |
| 3 | 🟡 **Occasional Shopper** | Infrequent purchases, lower spend |

---

## 📸 App Screenshots

| Home Page | Clustering Page |
|---|---|
| ![Home](output_images/Screenshot%202025-08-03%20191455.png) | ![Clustering](output_images/Screenshot%202025-08-03%20191508.png) |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- pip

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/Tharunkunamalla/Project-4-Shopper_spectrum-segmentation.git
cd Project-4-Shopper_spectrum-segmentation

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the Streamlit app
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`.

> **Note:** The dataset and pre-trained model files (`data/` and `models/`) must be present in the project root before running the app.

---

## 🛠️ Tech Stack

| Tool / Library | Purpose |
|---|---|
| **Python** | Core programming language |
| **Streamlit** | Interactive web application UI |
| **pandas** | Data manipulation and analysis |
| **NumPy** | Numerical computations |
| **scikit-learn** | KMeans clustering, StandardScaler, cosine similarity |
| **Matplotlib** | Data visualization |
| **Seaborn** | Statistical data visualization |
| **fuzzywuzzy** | Fuzzy string matching for product search |
| **pickle** | Model serialization |

---

## 👤 Author

**Tharun Kunamalla**

- 🔗 GitHub: [@Tharunkunamalla](https://github.com/Tharunkunamalla)
- 📁 Project Repo: [Project-4-Shopper_spectrum-segmentation](https://github.com/Tharunkunamalla/Project-4-Shopper_spectrum-segmentation)
