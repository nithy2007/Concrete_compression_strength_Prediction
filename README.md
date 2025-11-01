## Concrete Compressive Strength Prediction
## Overview

This project predicts concrete compressive strength (MPa) based on its composition and curing age.
Accurately modeling concrete strength helps optimize material usage, reduce costs, and improve structural safety.

The dataset is obtained from the UCI Machine Learning Repository and contains 1,030 concrete mixtures with 8 input variables describing ingredient proportions and curing age.

## Dataset Description
| **Variable**                      | **Type**     | **Unit**     | **Description**            |
| :-------------------------------- | :----------- | :----------- | :------------------------- |
| Cement                            | Quantitative | kg/m³        | Cement content             |
| Blast Furnace Slag                | Quantitative | kg/m³        | Slag content               |
| Fly Ash                           | Quantitative | kg/m³        | Fly ash content            |
| Water                             | Quantitative | kg/m³        | Water content              |
| Superplasticizer                  | Quantitative | kg/m³        | Superplasticizer content   |
| Coarse Aggregate                  | Quantitative | kg/m³        | Coarse aggregate content   |
| Fine Aggregate                    | Quantitative | kg/m³        | Fine aggregate content     |
| Age                               | Quantitative | days (1–365) | Age of the sample          |
| **Concrete Compressive Strength** | Quantitative | MPa          | Target variable (strength) |


## Objective

The goal of this project is to build and compare regression models to predict the compressive strength of concrete based on its ingredients and curing age.

Steps:

Perform exploratory data analysis (EDA) to understand distributions and correlations.

Fit and compare the following regression models:

Polynomial Regression

Polynomial Ridge Regression

Orthogonal Polynomial Regression

Spline Regression (PyGAM)

Regression Tree & Pruned Tree

Random Forest

Used a 70–30 train-test split.

Evaluate models using Mean Squared Error (MSE) and R².

Use cross-validation for hyperparameter tuning.

Compare models on accuracy, interpretability, and complexity.

## Models and Results
| **Model**                              | **Train MSE** | **Test MSE** | **Train R²** | **Test R²** | **Remarks**                                                              |
| :------------------------------------- | ------------: | -----------: | -----------: | ----------: | :----------------------------------------------------------------------- |
| **Polynomial Regression (Degree = 2)** |         49.61 |        63.14 |        0.820 |       0.779 | Explains ~78% variance; suffers from multicollinearity and overfitting.  |
| **Polynomial Ridge Regression**        |         49.79 |        63.20 |        0.820 |       0.778 | Ridge regularization did not improve results (alpha → smallest value).   |
| **Orthogonal Polynomial Regression**   |         30.30 |        48.55 |        0.890 |       0.830 | Better generalization than standard polynomial; moderate complexity.     |
| **Spline Regression (PyGAM)**          |         21.56 |        32.25 |    **0.922** |   **0.887** | Captures nonlinearities smoothly; best generalization among regressions. |
| **Full Regression Tree**               |         31.54 |        72.08 |        0.996 |       0.747 | Overfitting observed; key predictors: age, cement, water.                |
| **Pruned Regression Tree**             |          1.37 |        58.49 |        0.995 |       0.795 | Reduced overfitting; slightly better generalization than full tree.      |
| **Random Forest (GridSearchCV)**       |         14.47 |        38.02 |    **0.948** |   **0.867** | Strong performance, robust and less overfitting, but less interpretable. |


## Key Insights

Linearity insufficient: Ramsey RESET test confirmed the need for nonlinear modeling.

Polynomial models: Captured nonlinearity but suffered from multicollinearity.

Splines (PyGAM): Best balance of interpretability and predictive accuracy.

Tree-based models: Capture interactions well; Random Forest showed high robustness.

Important predictors: Cement, water, and age most strongly influence strength.

## Tools & Libraries

Python 3.11

pandas, numpy, matplotlib, seaborn

statsmodels, scikit-learn, pygam

Jupyter Notebook / nbconvert

## Conclusion

The Spline GAM achieved the best overall performance (R² ≈ 0.89 on test data) with smooth, interpretable relationships.

The Random Forest achieved robust predictive accuracy (R² ≈ 0.87) and identified key variables driving strength.

Linear and polynomial models performed moderately well but lacked flexibility to model nonlinear effects.

## Best Models: 
      Spline GAM & Random Forest
## Best Predictors: 
      Cement, Water, Age
