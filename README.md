# Lincolnshire Crop Prediction

A machine-learning project using Crop Map of England (CROME) data to examine land-use patterns in a selected area of Lincolnshire.

The project combines:

- supervised learning to predict 2025 land-use classifications;
- unsupervised learning to identify geographical and agricultural clusters.

## Data

The analysis uses official CROME data for 2024 and 2025 from the UK government environmental data service.

A geographical sample containing 4,868 matching grid cells was selected from southern Lincolnshire.

Each cell includes:

- a unique CROME identifier;
- land-use classification;
- classification confidence;
- geographical geometry.

The raw and generated data files are excluded from GitHub because they can be downloaded or recreated from the original sources.

[UK government agriculture datasets](https://www.gov.uk/government/statistical-data-sets/agriculture-in-the-united-kingdom-data-sets)

## Project structure

### 1. CROME schema audit

`notebooks/01_crome_schema_audit.ipynb`

- examines the 2024 and 2025 API schemas;
- checks identifiers, geometry and missing values;
- compares annual land-use distributions;
- reviews classification confidence;
- confirms that all 4,868 cell identifiers and geometries match.

### 2. Data preparation

`notebooks/02_data_preparation.ipynb`

- joins 2024 predictors to 2025 outcomes;
- translates land-use codes into readable descriptions;
- calculates British National Grid coordinates;
- combines rare 2025 classes into an `OTHER` category;
- prepares 13 target classes for modelling.

The selected predictors are:

- 2024 land-use code;
- 2024 classification confidence;
- easting;
- northing.

### 3. Supervised classification

`notebooks/03_baseline_classification.ipynb`

Four classification models were tested using a geographical train-test split.

| Model | Accuracy | Balanced accuracy | Macro F1 |
|---|---:|---:|---:|
| Dummy classifier | 47.8% | 7.7% | 5.0% |
| Logistic regression | 39.4% | 28.5% | 25.1% |
| K-nearest neighbours | 64.8% | 24.8% | 24.5% |
| Random forest | 59.9% | 35.5% | 30.7% |

K-nearest neighbours achieved the highest overall accuracy. Random forest provided the strongest balanced accuracy and Macro F1, making it more effective across the unevenly represented classes.

The models performed well for several common classes but struggled with rare crops.

### 4. Unsupervised clustering

`notebooks/04_unsupervised_clustering.ipynb`

K-means clustering was used to identify groups based only on 2024 information.

Four clusters were selected. The silhouette score was 0.215, indicating that the clusters overlap and represent broad patterns rather than completely separate groups.

The clusters differed in:

- geographical location;
- dominant crops;
- classification confidence;
- year-to-year classification-change rates.

Cluster 2 was dominated by winter crops, had the highest average classification confidence and had the lowest relative classification-change rate.

The 2025 data was used only to interpret the completed clusters and did not influence their creation.

## Main findings

- Winter Wheat increased from 29.2% of cells in 2024 to 46.3% in 2025.
- Approximately 75.9% of sampled cells received a different annual classification.
- K-nearest neighbours achieved the highest test accuracy at 64.8%.
- Random forest achieved the best balanced accuracy at 35.5%.
- Location was highly influential in the classification models.
- K-means identified four overlapping geographical and agricultural groups.
- Classification changes may reflect crop rotation, genuine land-use change or differences in annual satellite classification.

## Limitations

- The analysis covers a small selected area rather than all of Lincolnshire.
- Only two annual CROME datasets were used.
- The target classes are imbalanced.
- Rare classes were combined into an `OTHER` category.
- CROME confidence scores may not represent calibrated probabilities.
- Strong geographical effects may limit performance in other locations.
- Observed classification changes cannot automatically be treated as genuine land-use changes.

## Tools

- Python
- pandas
- GeoPandas
- scikit-learn
- Matplotlib
- Seaborn
- JupyterLab

## Running the project

Clone the repository and install the required packages:

```bash
git clone git@github.com:DafyddFuture/lincolnshire-crop-prediction.git
cd lincolnshire-crop-prediction
pip install -r requirements.txt
jupyter lab
```

The CROME lookup workbooks should be placed in `data/raw` using these filenames:

```text
crome_lucode_lookup_2024.xlsx
crome_lucode_lookup_2025.xlsx
```

Run the notebooks in numerical order. Notebook 2 creates the interim geographical dataset required by Notebooks 3 and 4.

## Data note

Raw and processed datasets are intentionally excluded from version control. This keeps the repository lightweight and avoids publishing generated data files.
