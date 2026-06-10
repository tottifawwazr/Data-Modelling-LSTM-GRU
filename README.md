# Gold Return Forecasting Using Stacking GRU–LSTM and Macroeconomic Indicators

https://doi.org/10.5281/zenodo.20631198

## 1. Title

**Project Name:** Gold Return Forecasting Using Stacking GRU–LSTM and Macroeconomic Indicators
**Research Domain:** Financial Time-Series Forecasting
**Forecasting Target:** One-Day-Ahead Gold Return / Gold Price Movement
**Period Covered:** 1990–2025
**Final Model:** Stacking GRU–LSTM

---

## 2. Project Description

This project develops machine learning and deep learning models for forecasting one-day-ahead gold returns using historical gold price data and macroeconomic indicators. Gold return forecasting is challenging due to nonlinear price behavior, volatility, and changing market conditions.

Several baseline, tuned, and ensemble forecasting models were evaluated, including:

* XGBoost
* Random Forest
* GRU
* LSTM
* CNN
* Adjusted LSTM
* Stacking GRU–CNN
* Stacking CNN–LSTM
* Stacking GRU–LSTM

The final selected model is **Stacking GRU–LSTM**, which combines the temporal learning ability of GRU with the sequential memory capability of the Adjusted LSTM model. The stacking model uses a linear regression meta-learner to combine predictions from the base models.

This project includes:

* Data preprocessing
* Feature engineering
* Baseline modelling
* Hyperparameter tuning
* Adjusted LSTM development
* Stacking ensemble learning
* Rolling walk-forward validation
* Diebold-Mariano statistical testing
* Explainability analysis
* Residual diagnostics

---

## 3. Dataset Information

The dataset combines daily gold prices with financial market and macroeconomic indicators from 1990 to 2025. The dataset was compiled from publicly available financial sources, including Kaggle and Investing.com.

## Financial Market Variables

* `GOLD_CLOSE`
* `SILVER_CLOSE`
* `SP500`
* `VIX`
* `WTI`
* `COPPER`

## Macroeconomic Variables

* `FED_FUNDS`
* `CPI_ACTUAL`
* `TREASURY_10Y`
* `REAL_YIELD`
* `REAL_INTEREST_RATE`
* `M2`

## Engineered Features

* `RET_PAST_1`
* `RET_PAST_3`
* `RET_PAST_5`
* `VOL_5`
* `VOL_20`
* `MONTH`
* `DAY`
* `DAY_OF_WEEK`
* `IS_WEEKEND`

The main forecasting target is **one-day-ahead gold return**, derived from historical gold price movements.

---

## 4. Methodology

## Data Gathering

Financial and macroeconomic data were collected and combined into a single time-series dataset covering the period from 1990 to 2025.

## Data Preprocessing

The preprocessing stage includes:

* Sorting data by date
* Setting the date column as the time-series index
* Selecting relevant financial and macroeconomic variables
* Handling missing values
* Creating return-based target variables
* Generating lag features
* Creating rolling volatility features
* Adding calendar-based features
* Removing highly correlated features
* Applying chronological train-validation-test splitting
* Applying robust scaling to numerical features

## Feature Engineering

Several temporal and statistical features were generated to improve forecasting performance:

* Lagged return features
* Rolling volatility features
* Calendar-based variables
* One-day-ahead target return
* Target price reconstruction for evaluation

## Forecasting Models

### Baseline Models

The baseline models used in this study include:

* XGBoost
* Random Forest
* GRU
* LSTM
* CNN

### Tuned Models

Hyperparameter optimization was applied to improve model performance. The LSTM model was further adjusted by refining the sequence length, applying target scaling, and improving the training strategy. This produced the **Adjusted LSTM** model.

### Stacking Ensemble Models

Several stacking variants were evaluated:

* Stacking GRU–CNN
* Stacking CNN–LSTM
* Stacking GRU–LSTM

The final selected model is **Stacking GRU–LSTM**, based on test performance.

---

## 5. Evaluation Metrics

The forecasting models were evaluated using:

* RMSE: Root Mean Squared Error
* MAE: Mean Absolute Error
* MAPE: Mean Absolute Percentage Error
* Rolling walk-forward validation
* Diebold-Mariano statistical test
* Residual diagnostics
* Explainability analysis

---

## 6. Final Model Performance

The final **Stacking GRU–LSTM** model achieved the best test performance among the evaluated models.

| Model              | Test RMSE | Test MAE | Test MAPE |
| ------------------ | --------: | -------: | --------: |
| Stacking GRU–LSTM  |   18.0822 |  10.9840 |    0.0051 |
| Stacking CNN–LSTM  |   18.0927 |  11.0298 |    0.0051 |
| LSTM Improved Best |   18.1299 |  10.9904 |    0.0051 |
| Stacking GRU–CNN   |   18.1584 |  11.0907 |    0.0052 |
| GRU Tuned          |   18.2146 |  11.5898 |    0.0054 |
| CNN Tuned          |   18.6201 |  12.0611 |    0.0056 |

The final model improved RMSE by approximately **0.4195%** compared with the previous Stacking GRU–CNN model.

---

## 7. Rolling Walk-Forward Validation

Rolling walk-forward validation was used to evaluate the robustness of the model under realistic forecasting conditions.

| Model             | Rolling RMSE | Rolling MAE | Rolling MAPE |
| ----------------- | -----------: | ----------: | -----------: |
| Stacking GRU–LSTM |      14.4112 |      8.4740 |       0.0048 |

This validation approach reduces look-ahead bias and better reflects real-world financial forecasting conditions.

---

## 8. Diebold-Mariano Statistical Test

The Diebold-Mariano test was used to compare the predictive accuracy of the final Stacking GRU–LSTM model against the previous Stacking GRU–CNN model.

| Comparison          | Loss Function  | p-value | Conclusion      |
| ------------------- | -------------- | ------: | --------------- |
| GRU–LSTM vs GRU–CNN | Squared Error  |  0.1674 | Not Significant |
| GRU–LSTM vs GRU–CNN | Absolute Error |  0.0063 | Significant     |

The results indicate that GRU–LSTM significantly improves forecasting performance under absolute error loss, although the improvement is not statistically significant under squared error loss.

---

## 9. Explainability Analysis

Model interpretability was analyzed using meta-learner contribution and feature-level importance.

## Meta-Learner Contribution

| Component     | Relative Contribution |
| ------------- | --------------------: |
| GRU Tuned     |                19.48% |
| Adjusted LSTM |                80.52% |

The Adjusted LSTM component contributed the largest proportion to the final stacking model, indicating that LSTM-based temporal memory plays a dominant role in the final prediction.

## Important Features

Feature-level analysis identified several important predictors:

* `GOLD_CLOSE`
* `SP500`
* `RET_PAST_1`
* `FED_FUNDS`
* `CPI_ACTUAL`
* `WTI`
* `VOL_20`
* `TREASURY_10Y`
* `VIX`

These results suggest that gold price persistence, equity market movement, short-term return memory, monetary policy, and inflation-related indicators are important in short-term gold return forecasting.

---

## 10. Residual Diagnostics

Residual diagnostics were conducted to evaluate the adequacy of the final model. The residuals were centered close to zero, indicating limited prediction bias. However, the residual distribution showed heavy-tailed behavior, which is common in financial time-series data due to volatility and extreme market movements.

| Metric          |     Value |
| --------------- | --------: |
| Mean Residual   |    0.2927 |
| Median Residual |   -0.5033 |
| Std Residual    |   18.0845 |
| Min Residual    | -116.8057 |
| Max Residual    |  114.8228 |
| Skewness        |   -0.0958 |
| Kurtosis        |    6.6781 |
| RMSE            |   18.0822 |
| MAE             |   10.9840 |
| MAPE            |    0.0051 |

---

## 11. Requirements

Install the required Python libraries:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow xgboost shap statsmodels scipy openpyxl
```

---

## 12. Usage Instructions

## Step 1 — Clone Repository

```bash
git clone https://github.com/tottifawwazr/Data-Modelling-LSTM-GRU.git
cd Data-Modelling-LSTM-GRU
```

## Step 2 — Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow xgboost shap statsmodels scipy openpyxl
```

## Step 3 — Open Notebook

Open the Jupyter Notebook file:

```text
DATMOD_GRU_LSTM_FINAL_CLEAN (1).ipynb
```

## Step 4 — Load Dataset

Make sure the dataset file is located in the same folder as the notebook:

```text
Gold_Silver_Forecasting - New.xlsx
```

## Step 5 — Run the Notebook

Run all cells sequentially to reproduce:

* Data preprocessing
* Feature engineering
* Baseline model training
* Tuned model training
* Adjusted LSTM experiment
* Stacking GRU–LSTM model
* Rolling validation
* Diebold-Mariano testing
* Explainability analysis
* Residual diagnostics

---

## 13. Research Contribution

This project demonstrates that combining recurrent deep learning architectures through a stacking ensemble framework can improve gold return forecasting performance. The final Stacking GRU–LSTM model achieved the best test performance among the evaluated models and provides interpretable forecasting results through meta-learner contribution, feature importance analysis, and residual diagnostics.

The study contributes to financial time-series forecasting by integrating:

* Macroeconomic indicators
* Deep learning models
* Adjusted LSTM optimization
* Stacking ensemble learning
* Rolling validation
* Statistical significance testing
* Explainable model interpretation

---

## 14. DOI and Repository

## DOI

https://doi.org/10.5281/zenodo.20631198

## Zenodo Badge

[![DOI](https://zenodo.org/badge/1265322073.svg)](https://doi.org/10.5281/zenodo.20631198)

## Repository

https://github.com/tottifawwazr/Data-Modelling-LSTM-GRU

---

## 15. Citation

If you use this project, please cite the Zenodo archive:

```text
Totti Fawwaz Reda. (2026). Gold Return Forecasting Using Stacking GRU–LSTM and Macroeconomic Indicators. Zenodo. https://doi.org/10.5281/zenodo.20631198
```

---

## 16. License

This project is released under the MIT License and is intended for academic and research purposes.
