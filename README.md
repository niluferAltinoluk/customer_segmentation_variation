# Project Summary: 
## Customer Segmentation & Category Prediction
This project focuses on analyzing customer demographics to predict their market segmentation and category types. By employing multi-class classification algorithms like K-Nearest Neighbors (KNN) and Random Forest, the project aims to identify patterns in customer behavior and profiles.

# Dataset
* Source: Customer training dataset (Train-customer.csv).

* Data Type: Structured tabular data (8068 rows, 11 columns).

#### Target Variables:

* Segmentation: Customer groups (A, B, C, D).

* Var_1: Anonymized customer categories (Cat_1 to Cat_7).

* Key Features: Gender, Ever Married, Age (Categorized), Profession, Work Experience, Spending Score, and Family Size.

# Project Steps

### 1. Data Cleaning and Initialization
* Initial Checks: The ID column is dropped as it lacks predictive value. Missing values are identified and handled by dropping rows with null entries to maintain data integrity.

* Age Categorization: The continuous Age variable is transformed into categorical groups (e.g., '18-24', '25-34', etc.) using pd.cut. bu sayede modelin yaş grupları arasındaki farkları daha iyi anlaması sağlanmıştır.

* Type Management: Numeric-looking categorical features like Family_Size and Work_Experience are converted to strings to ensure correct encoding.

### 2. Manual Encoding and Mapping
* Dictionary Mapping: Instead of automated encoders, custom dictionaries are created for all categorical variables:

* Gender, Graduation, Marriage: Binary/Ordinal mapping.

* Profession: 9 distinct professional categories mapped to integers.

* Segmentation & Var_1: Target labels converted to numeric scales for model compatibility.

* Data Synthesis: The text-based values in the DataFrame are replaced with these numeric mappings to prepare the mathematical input for the models.

### 3. Feature Scaling & Data Splitting
* Normalization: Since KNN is a distance-based algorithm, MinMaxScaler is applied to all features to scale them between 0 and 1.

* Splitting: Data is partitioned into 80% training and 20% testing sets using train_test_split.

### 4. Model Training & Hyperparameter Analysis
#### K-Nearest Neighbors (KNN):

* The model was tested with various n_neighbors values (1 to 10).

* Analysis: A line plot was generated to visualize the "Elbow" point, showing how training accuracy decreases while test accuracy stabilizes as n increases.

#### Random Forest Classifier:

* A forest-based ensemble model was trained to capture non-linear relationships.

* Compared to KNN, Random Forest showed higher training accuracy, indicating a strong fit on the complex customer features.

### Results
* Predictive Power: The models performed significantly better at predicting the Var_1 category compared to the Segmentation labels.

* Model Choice: Random Forest consistently outperformed KNN in test accuracy across both tasks.

* Optimization: The gap between training and test accuracy suggests that further hyperparameter tuning (like depth control in Random Forest) could reduce overfitting.

| Target Variable | Model | Train Accuracy | Test Accuracy |
| :--- | :--- | :---: | :---: |
| **Segmentation** (Groups A-D) | KNN (n=10) | 0.5769 | 0.4876 |
| **Segmentation** (Groups A-D) | Random Forest | 0.8665 | 0.4929 |
| **Var_1** (Anonymized Category) | KNN (n=4) | 0.7125 | 0.6189 |
| **Var_1** (Anonymized Category) | Random Forest | 0.8938 | 0.6309 |

### Visual Analysis


### Key Libraries Used
* Data Processing: pandas, numpy, scipy

* Machine Learning: scikit-learn (KNN, Random Forest, LocalOutlierFactor, Scalers)

* Visualization: seaborn, matplotlib, graphviz


Note: The use of MinMaxScaler was crucial for the KNN model, ensuring that features with larger ranges (like encoded Profession IDs) did not disproportionately influence the distance calculations.
