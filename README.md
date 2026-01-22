# 15N_chemical_shift_of_organic_compounds_NMR

---
## This is an unfinished project due to the lack of training data
---

## Purpose of the project

## Purpose of the project

+ Develop a machine learning model that predicts chemical shifts of nitrogen atoms of nitrogen-containing organic compounds.

## Object of research

+ Nitrogen-containing organic compounds

## Data description

The target variable was collected from the SpectraBase database, which includes various spectra of compounds in different solvents, including 15N NMR spectra. As a basic model, compounds containing one nitrogen atom without taking into account the variety of solvents was used. Currently, the dataset is represented by 243 unique compounds, in which the distribution of the target variable differs from the normal one. For correct distribution into the test and training samples (ratio 0.8 - 0.2), the data were divided into quartiles.

## Model

The prediction is based on a two-stage regression model. The first stage is the prediction of a chemical shift characteristic of a functional group of a chemical compound based on fingerprints of increasing radius. Fingerprints are a categorical variable, so prediction is performed by CatBoostRegressor. Hyperparameters were selected using Optuna. OneHotEncoder was previously used.

The predictions obtained at the first stage are used as a feature for the second stage of the regression model. Embeddings from the MolFormer output have been added as features. Only those variables that show correlation with the target variable are used as features - 165, 202, 292, 312, 319, 541, 562, 725 ( R2 > 0.3). Due to the small size of the dataset and a number of drop-down target values, Ridge regression is recognized as the best model for regression.

## Results

The model greatly overpredicts on the test. A relatively small dataset and unequal distribution of training and test samples affect the final quality metrics. Therefore, the control MAE value was evaluated on a separate dataset that was collected later (MAE - 41.4 ppm, R2 - 0.38). The result of the control metric was worse than those published by another research group, which is probably due to the small amount of initial data.
