# SmartCart-Clustering
Customer segmentation for a retail/e-commerce platform using unsupervised clustering (K-Means &amp; Agglomerative) on demographic and spending data, with PCA-based dimensionality reduction and visualization.

## Dataset

The dataset (`smartcart_customers.csv`) contains customer-level records including:

- **Demographics**: Year of Birth, Education, Marital Status, Income
- **Household**: Kidhome, Teenhome
- **Engagement**: Customer enrollment date (Dt_Customer), Recency, Response
- **Spending**: Amount spent on Wines, Fruits, Meat, Fish, Sweets, Gold products

## Project Workflow

### 1. Data Loading & Inspection
- Load the dataset with pandas
- Check shape, missing values, and data structure

### 2. Data Preprocessing
- **Missing values**: Filled missing `Income` values with the median

### 3. Feature Engineering
- **Age**: Derived from `Year_Birth`
- **Customer_Tenure_Days**: Days since enrollment, relative to the most recent customer
- **Total_Spending**: Sum of spending across all product categories
- **Total_Children**: Combined `Kidhome` + `Teenhome`
- **Education**: Simplified into `UnderGraduate`, `Graduate`, `PostGraduate`
- **Living_with**: Simplified `Marital_Status` into `Partner` or `Alone`

### 4. Dropping Redundant Columns
- Removed `ID`, `Year_Birth`, `Marital_Status`, `Kidhome`, `Teenhome`, `Dt_Customer`, and individual spending columns (replaced by `Total_Spending`)

### 5. Outlier Removal
- Visualized relationships using pair plots
- Removed records with `Age > 90` and `Income > 600,000`

### 6. Correlation Analysis
- Generated a correlation heatmap of numeric features

### 7. Encoding
- One-hot encoded `Education` and `Living_with`

### 8. Feature Scaling
- Standardized all features using `StandardScaler`

### 9. Dimensionality Reduction & Visualization
- Applied **PCA** to reduce features to 2D and 3D
- Visualized customer distribution in 2D and 3D PCA space
- Reviewed explained variance ratio for each component

### 10. Determining Optimal Number of Clusters
- **Elbow Method**: Computed WCSS for k = 1–10 and used `KneeLocator` to find the optimal k
- **Silhouette Score**: Computed for k = 2–10
- Combined plot of WCSS and Silhouette Scores for comparison

### 11. Clustering
- Applied **K-Means** (k=4) on PCA-transformed data
- Applied **Agglomerative Clustering** (ward linkage, 4 clusters)
- Visualized both results in 3D PCA space

### 12. Cluster Characterization
- Assigned cluster labels back to the dataset
- Visualized cluster sizes (count plot)
- Visualized clusters by `Total_Spending` vs `Income`
- Generated cluster-wise summary statistics (mean values per cluster)

## Tech Stack
- Python
- pandas
- matplotlib, seaborn
- scikit-learn (PCA, KMeans, AgglomerativeClustering, StandardScaler, OneHotEncoder)
- kneed (Elbow point detection)

## How to Run
1. Clone this repository
2. Install dependencies:
   ```bash
   pip install pandas matplotlib seaborn scikit-learn kneed jupyter
   ```
3. Place `smartcart_customers.csv` in the project directory
4. Open and run `Smartcart_clustering.ipynb`
