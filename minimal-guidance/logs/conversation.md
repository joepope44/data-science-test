# Customer Segmentation Analysis — Conversation Log

## Analysis Workflow

### Step 1: Data Loading & Exploration
- Loaded BankChurners.csv (10,127 rows, 23 columns)
- Dropped 2 Naive Bayes classifier columns (leakage artifacts)
- No missing values found in the dataset
- Overall churn rate: ~16.1% (1,627 attrited vs 8,500 existing)

### Step 2: Exploratory Data Analysis
- Generated correlation heatmap — strong correlations between Credit_Limit and Avg_Open_To_Buy
- Attrition rates examined across Gender, Income, Education, Marital Status, and Card Category
- Churned customers show notably lower transaction counts and amounts

### Step 3: Feature Engineering & Preprocessing
- Label-encoded categorical variables (Gender, Education_Level, Marital_Status, Income_Category, Card_Category)
- Standardized all features using StandardScaler
- Excluded CLIENTNUM and Attrition_Flag from clustering features

### Step 4: K-Means Clustering
- Ran elbow method for k=2 to k=10
- Selected k=4 as optimal based on elbow curve
- PCA visualization confirms reasonably separated clusters

### Step 5: Segment Profiling
- Profiled each cluster on key behavioral and demographic metrics
- Identified segments with significantly different attrition rates
- Exported segment summary to CSV

### Step 6: Key Findings
1. **Transaction behavior** (count and amount) is the strongest differentiator between segments
2. **Inactivity** and **contact frequency** correlate with higher churn probability
3. Demographic factors show relatively uniform attrition — behavioral features are more predictive
4. High-value customers with low utilization represent an upsell opportunity
5. Segments with high contact counts and low transaction activity are at greatest churn risk

### Deliverables
- `analysis.ipynb` — Full analysis notebook
- `results/data_overview.png` — Key numeric feature distributions
- `results/correlation_matrix.png` — Correlation heatmap
- `results/attrition_by_segment.png` — Attrition rates by demographic segments
- `results/churn_distributions.png` — Churned vs existing distributions
- `results/elbow_plot.png` — Elbow method plot
- `results/cluster_visualization.png` — PCA cluster visualization
- `results/segment_profiles.png` — Segment comparison boxplots
- `results/segment_summary.csv` — Segment summary table
- `logs/conversation.md` — This conversation log
