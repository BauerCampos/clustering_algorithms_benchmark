# Agglomerative Clustering

## Dependencies
- matplotlib
- scipy
- sklearn
- pickle
- pandas

## Overview

Agglomerative clustering is a hierarchical machine learning method that builds nested clusters by iteratively merging data points or groups. Initially, each data point is treated as its own cluster. The algorithm then repeatedly merges the two closest clusters (based on a distance metric in Euclidean space) into a single cluster, reducing the total number of clusters by one each step. This process continues until only one cluster remains, and the hierarchy of merges is typically visualized using a dendrogram.
For this algorithm, performance was evaluated using the silhouette score, as it is the only metric used to compare algorithms in this project. The dendrogram suggested that two clusters would be optimal. Initial tests revealed that training the model on the full dataset was infeasible due to the high computational cost of agglomerative clustering on large datasets. Therefore, the model was trained on a sample of 20,000 data points.

## Performance Analysis
**Silhouette Score**

- *Dendrogram:*

![Dendrogram](../../../images/hierarchical_clustering/dendrogram.png)

Observation: The dendrogram suggests that for agglomerative clustering two clusters would achieve optimal results

- *Manual Engineering (Method A):*

![Silhouette Score Metric 1](../../../images/hierarchical_clustering/m1_s_score.png)

Observation: Peak score 0.490 with 2 clusters

- *PCA (Method B):*

![Silhouette Score Metric 2](../../../images/hierarchical_clustering/m2_s_score.png)

Observation: Peak score 0.446 with 2 components

## Key Takeaways

**Dendrogram Observation**
Building a dendogram is computationally expensive but useful to observe how the database behave under hierarchical bottom up clustering models and decide the optimal number of clusters.

**Manual vs PCA:**
- **Manual Engineering:** Manual Feature Engineering consistently yielded higher Silhouette scores. This suggests that our domain‑driven feature aggregation preserved the natural cluster structure more effectively than linear dimensionality reduction.
- **PCA Performance:** PCA Performance improved with fewer components. This trend can be attributed to two factors: 
Variance ordering: PCA prioritizes components with the highest explained variance. The initial components capture the dominant data structure, while later components often represent noise or negligible variance, which can obscure true clusters.
Curse of dimensionality: As dimensions increase, distance metrics in Euclidean space become less discerning—a phenomenon known as distance concentration. This reduces the contrast between intra‑cluster and inter‑cluster distances, lowering the Silhouette score.
