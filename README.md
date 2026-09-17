# Lincolnshire Crop Prediction

## Project overview

This project explores how agricultural land use changed within a selected area of Lincolnshire between 2024 and 2025.

The longer-term aim is to build a machine-learning model that predicts the following year’s land-use classification using previous classifications, location and confidence scores.

## Data

The project uses the UK Government’s [Crop Map of England (CROME) datasets](https://www.gov.uk/government/statistical-data-sets/agriculture-in-the-united-kingdom-data-sets).

CROME divides England into small geographical cells and assigns each cell a land-use category, such as Winter Wheat, Grass or Maize.

A sample of 4,868 matching cells was selected from the Lincolnshire datasets for 2024 and 2025.

## Initial analysis

The first stage examined the structure and quality of the data. It included:

* Matching the same geographical cells across both years.
* Checking for missing or duplicate records.
* Translating land-use codes into understandable descriptions.
* Comparing land-use patterns between 2024 and 2025.
* Reviewing the confidence of the classifications.

All 4,868 cells matched successfully across the two years, with no missing or invalid geographical data.

Approximately 76% received a different land-use classification in 2025. Winter Wheat increased from 29% to 46% of the selected area and became the most common classification.

Some classifications had relatively low confidence scores. Therefore, the observed changes may reflect both genuine agricultural changes and uncertainty within the source data.

## Next steps

The next stages will:

* Prepare the data for modelling.
* Create useful geographical and historical features.
* Build and compare classification models.
* Test the model on geographically separate data.
* Explore groups of similar land-use patterns.

## Repository structure

```text
data/          Data folders
notebooks/     Analysis and modelling notebooks
README.md      Project summary
requirements.txt
```

## Tools

Python, pandas, GeoPandas, Requests, Matplotlib, Seaborn, scikit-learn and JupyterLab.
