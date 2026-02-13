# Clustering Algorithms Performance Benchmark

A comprehensive in depth performance comparison between some of the most important clustering algorithms with the goal not only to compare benchmarks but also observe each algorithm individual particularities.

The algorithms K-Means, hierarchical clustering, DBSCAN and Standard Expectation-Maximization were chosen for this project, the metric Silhouette Score was chosen for comparison across different algorithms since it can benchmark various different clustering methods, each algorithm was also tested in its respectives metrics

## 📌 Table of Contents
- [Goal](#-goal)
- [Dataset](#-dataset)
- [Preprocessing](#-Preprocessing-&-feature-engineering)
- [Algorithms](#-Algorithms)
- [Results](#-results)

## 🎯 Goal
**Business Goal:** Identify distinct customer segments within the credit card database to better understand default risk profiles and spending behaviors.

**Technical Goal:**Benchmark clustering algorithms (K-Means, DBSCAN, etc.) and preprocessing techniques (Manual Engineering vs. PCA) to determine the most computationally efficient and accurate approach.

## 📊 Dataset
**Source:** [Default of Credit Card Clients](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients)

**Features:**
- `id`: Id on each entry
- `limit_bal`: Limit balance
- `sex`: Sex
- `education`: Education level
- `marriage`: Marital status
- `age`: age in years
- `pay_0`~`pay_6`: Information about installment pay 1 through 6
- `bill_amnt1`~`bill_amnt6`: Each installment total value
- `pay_amnt1`~`pay_amnt6`: Each installment paid amount
- `default_payment_next_month`: binary column indicating next month payment

## ⚙️ Preprocessing & Feature Engineering

### 1. Data Cleaning
Initial analysis confirmed the dataset was high quality, containing no missing values or significant outliers. Therefore, no imputation or row deletion was required.

![](/images/null_values.png "Null values")

### 2. Feature Scaling
Since clustering algorithms (like K-Means) rely on distance metrics (e.g., Euclidean distance), features with larger magnitudes can disproportionately influence the model.
* **Action:** All data was scaled to ensure every feature contributes equally to the distance calculations.

### 3. Dimensionality Reduction Strategies
To reduce noise and computational cost, two distinct strategies were tested:

#### **Method A: Manual Feature Engineering (Domain Knowledge)**
We manually analyzed the features to capture financial patterns and reduce redundancy.
* **Consolidation:** The dataset originally split financial data across 6 months (features `BILL_AMT` and `PAY_AMT`).
* **Transformation:** We calculated the "Net Debt" for each month (Bill - Pay) and aggregated these into a single `Total_Debt` feature.
* **Result:** This allowed us to drop the raw monthly columns, significantly reducing dimensionality while preserving the *financial narrative* of the data (Debt vs. Payment status).

#### **Method B: Principal Component Analysis (PCA)**
We used PCA to automatically identify orthogonal components that explain the maximum variance in the data.
* **The Challenge:** Implementing PCA introduced a dual-optimization problem: finding the optimal number of *Principal Components* AND the optimal number of *Clusters*.
* **Computational Cost:** A standard nested loop (testing every component count against every cluster count) proved computationally infeasible due to exponential complexity.
* **The Solution:** Instead of a brute-force approach, we implemented a **Strategic Grid Search**. We selected representative values for component counts to balance variance retention with training time, allowing us to map performance patterns without excessive computational overhead.

- [Preprocessing](/algorithms/preprocessing)

## 🤖 Algorithms
- [K-Means](/algorithms/clustering_algorithms/k_means)

## 📈 Results
**Performance Comparison:**

|         Model         | Silhouette Score | Method(A/B) |
|-----------------------|------------------|-------------|
| K-Means               |       0.55       |      A      |


