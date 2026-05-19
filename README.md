# FQM Zambia — Copper Production Forecast 2025–2031
### Sentinel FQM & Kansanshi Mine | Scenario Modelling, Tableau Visualisation & Machine Learning

---

## Dashboard.

![Dashboard](Tableau%20Screenshots/Copper%20Production%20Scenario%20Dashboard%20Screenshot.png)

The dashboard shows the FQM copper prodution predictions starting from the actual at 2024 all the way to 2031. The bar chart shows the three 2031 scenario totals for both mines combined. There is the Best Case at 485,416 tonnes, Optimistic at 624,315 tonnes, and Pessimistic at 350,347 tonnes. The pie chart on the right shows how Kansanshi's Optimistic 2031 output is divided based on the type of ore of which mixed ore contributes more at 184,275 tonnes. The line chart at the bottom shows how each scenario trends from the  2024 actual value of 401,721 tonnes all the way up to 2031. The dip on the Best Case line at 2028 is a data entry error in the original excel file which was corrected using three dfferent machine learning algorithms for validation purposes.

---

## 2031 Scenario Comparison

![Scenario Comparison](Tableau%20Screenshots/Copper%20production%20by%20scenario%20Screenshot.png)

Three scenarios were modelled for the combined FQM Zambia operations across Sentinel and Kansanshi. The  difference between optimistic and pessimistic scenario is 274,000 tonnes. The reason for this is because of the mixed ore at Kansanshi. Under the pessimistic case, mixed ore contributes 41,652 tonnes. Under the optimistic case it contributes 184,275 tonnes. That is a difference of 142,000 tonnes. Therefore mixed ore is the most important contributing factor in this prediction.

---

## Production Trajectory 2024–2031

![Production Trajectory](screenshots/Production_trajectory_Screenshot.png)

All three scenarios start from the same 2024 actual baseline of 401,721 tonnes and diverge over seven years. The Optimistic trajectory assumes the mine achieves recovery rates, ore grades, and throughput volumes it has never historically reached — which is why the machine learning models later predict more conservatively on this scenario than the formula-based Excel forecast does. The Best Case line dips sharply at 2028 — this is the data anomaly identified during analysis where a missing zero in the Kansanshi mixed ore summary table recorded 10,620 tonnes instead of 106,260 tonnes. The corrected figure is used in all ML predictions.

---

## Kansanshi Ore Circuit Breakdown — Optimistic 2031

![Kansanshi Ore Circuits](screenshots/Kansanshi_Mixed_ore_Screenshot.png)

Kansanshi operates three ore circuits simultaneously — oxide, mixed, and sulphide — each with completely different grade, recovery, and throughput characteristics. Under the optimistic 2031 scenario, mixed ore accounts for 184,275 tonnes (52% of total Kansanshi output), sulphide for 119,784 tonnes (34%), and oxide for 50,503 tonnes (14%). This breakdown is the reason Kansanshi was modelled circuit by circuit in the machine learning section rather than as a single entity. Each circuit required its own model.

---

## Machine Learning — Sentinel FQM

Three models were applied to Sentinel's historical production data (2015–2024): Random Forest, Ridge Regression, and Gaussian Process Regression. Sentinel was chosen as the primary modelling target because it is a single-ore open pit with clean, consistent inputs — making it the most suitable candidate for regression-based ML on a small dataset of 10 years.

### Random Forest

![Sentinel RF](ml-screenshots/sentinel_rf_chart.png)

Random Forest builds 200 decision trees independently and averages their predictions. The feature importance panel reveals that throughput drives 43.8% of Sentinel's production variance, recovery rate 33.4%, and ore grade 22.8%. From an operational standpoint this means mill utilisation is the single biggest lever available to the operations team — more so than grade improvement or reagent optimisation. The 2031 prediction panel exposes a key limitation of tree-based models on small datasets: the Best Case and Optimistic predictions are identical at 239,450 tonnes, meaning the model has hit a ceiling. It cannot predict values outside the range it was trained on. This is addressed by Ridge Regression and GPR below.

### Ridge Regression

![Sentinel Ridge](ml-screenshots/sentinel_ridge_chart.png)

Ridge Regression is a regularised linear model that prevents overfitting on small datasets by penalising large coefficients. It achieved the strongest cross-validated R² of the three models at 0.4359, and a test R² of 0.9584. The coefficients panel shows that throughput and recovery both push production upward as expected. Ore grade shows a negative coefficient which at first appears counterintuitive — higher grade should mean more production. This is a known artefact of multicollinearity on small datasets: grade and recovery are correlated in the historical data, causing Ridge to partially offset one against the other. Unlike Random Forest, Ridge extrapolates properly — the Optimistic prediction of 242,533 tonnes is distinct from the Best Case at 238,715 tonnes.

### Gaussian Process Regression

![Sentinel GPR](ml-screenshots/sentinel_gpr_chart.png)

Gaussian Process Regression is specifically designed for small datasets and uniquely provides a confidence interval alongside each prediction rather than a single point estimate. The confidence band chart shows the 95% interval narrowing tightly at Pessimistic (±9,333 tonnes, 3.8% of the prediction) and widening dramatically at Optimistic (±33,545 tonnes, 12.1%). This widening is not a weakness — it is an honest quantification of uncertainty. The Optimistic scenario requires recovery rates and throughput volumes Sentinel has never historically achieved. GPR is acknowledging that it cannot be as certain about that prediction. The Excel forecast of 269,753 tonnes sits comfortably within GPR's Optimistic confidence interval of 243,913 to 311,004.

---

## Machine Learning — Kansanshi

Kansanshi was modelled circuit by circuit. Three separate models were trained for each circuit — oxide, mixed, and sulphide — using the same three algorithms. The circuit-level predictions were then summed to produce the total Kansanshi forecast.

### Oxide Circuit

![Kansanshi Oxide](ml-screenshots/kansanshi_oxide_chart.png)

The oxide circuit is the most stable and predictable of the three. All three models produce tight predictions close to the Excel forecast across all scenarios — GPR's confidence intervals are the narrowest in the entire project (±2,331 pessimistic, ±1,593 best case, ±3,665 optimistic). Ridge achieves the only positive cross-validated R² at 0.1323. The oxide circuit is in structural long-term decline as the oxide cap depletes, which is reflected in the relatively modest range between scenarios compared to mixed ore.

### Mixed Ore Circuit

![Kansanshi Mixed](ml-screenshots/kansanshi_mixed_chart.png)

The mixed ore circuit is the most analytically interesting and operationally critical circuit in the entire project. It drives the largest spread between scenarios — from 41,652 tonnes pessimistic to 184,275 tonnes optimistic — a 142,000 tonne range from a single circuit. Ridge achieves a cross-validated R² of 0.8890 on mixed ore, the strongest performance of any model on any circuit in this project. The RF ceiling effect is clearly visible on the RF panel — Optimistic and Best Case predictions are identical at 79,409 tonnes. Ridge and GPR both extrapolate beyond the training range, though more conservatively than the Excel formula. The Optimistic GPR confidence interval of ±23,250 tonnes is the widest of any circuit, reflecting genuine uncertainty about mixed ore behaviour at input levels the mine has not historically operated at.

### Sulphide Circuit

![Kansanshi Sulphide](ml-screenshots/kansanshi_sulphide_chart.png)

The sulphide circuit tells the most important geological story in the project. Sulphide ore grade has declined from 0.88% in 2021 to 0.60% in 2024 — a structural deterioration driven by the mine progressing into lower-grade zones of the ore body. The RF feature importance panel quantifies this operationally: throughput drives 55.9% of sulphide production variance and grade drives 37.0%. The dominance of throughput over grade reveals that the mine has been compensating for falling grade by pushing more ore through the mill. This strategy has physical limits — which is why the pessimistic sulphide scenario assumes this compensation eventually fails. GPR's Best Case confidence interval of just ±716 tonnes is the tightest prediction in the entire project.

---

## Slope Analysis & Best Case Correction

![Slope Analysis](ml-screenshots/slope_analysis.png)

The slope analysis quantifies the rate of production change in tonnes per year between 2024 and 2031. The top panel shows the corrected Best Case Excel line — the 2028 dip caused by the data entry error has been removed and replaced with the correct value of 106,260 tonnes. The bottom left chart shows absolute slopes across all models and scenarios. The bottom right chart shows ML model divergence from Excel's assumed growth rate — on Pessimistic the divergence is small, all models broadly agree. On Optimistic the divergence is large, with RF at -20,883 t/yr. The pessimistic scenario is statistically the most defensible forecast. The optimistic scenario requires operating conditions no model has seen before.

---

## All Models — 2031 Final Comparison

![Predictions Comparison](ml-screenshots/predictions_comparison.png)

The final comparison shows Excel, Ridge, and GPR side by side for both mines. For Sentinel, Ridge and GPR closely bracket the Excel forecast on Pessimistic and Best Case within 5%. For Kansanshi the models are more conservative on Optimistic due to the mixed ore extrapolation challenge. The overall picture validates the Excel regression forecasts for Pessimistic and Best Case with high confidence. The Optimistic scenario should be treated as an aspirational target with ML models providing a conservative lower bound.

---

## Scenario Forecast Lines

![Scenario Forecast Lines](ml-screenshots/scenario_forecast_lines.png)

Three line charts show the full 2024 to 2031 trajectory for each scenario. The Pessimistic chart shows all lines declining from the 2024 baseline. The Best Case chart shows the corrected smooth Excel trajectory with Ridge and GPR tracking closely. The Optimistic chart is where the story is clearest — the Excel line climbs steeply to 624,315 tonnes while RF flatlines and Ridge and GPR rise more gradually. The gap between Excel and the ML models on Optimistic is not a failure of the models. It is an honest reflection of the fact that the Optimistic inputs require the mine to operate beyond anything it has historically achieved.

---

## Data Quality — Anomaly Detection

During exploratory analysis a data entry error was identified in the Kansanshi Best Case 2028 mixed ore summary figure. The recorded value of 10,620 tonnes is inconsistent with surrounding years which range between 86,000 and 113,000 tonnes. The formula inputs for that row produce a calculated value of 106,260 tonnes. All three ML models were independently applied to those same inputs:

| Method | Prediction |
|---|---|
| Formula | 106,260 t |
| Random Forest | 79,389 t |
| Ridge Regression | 97,635 t |
| GPR | 95,038 t |
| Recorded in Excel | 10,620 t ← error |

Four independent methods all predict a value in the 79,000 to 106,000 tonne range. The recorded figure is an order of magnitude below all of them. The conclusion is a missing zero in the summary table. The corrected value of 106,260 tonnes is used in all ML predictions.

---

## Repository Structure

```
zambia-copper-forecast/
├── README.md
├── data/
│   ├── Zambia_Copper_production_project.xlsx
│   ├── Zambia_Copper_Tableau_Ready.xlsx
│   └── Kansanshi_Circuits.xlsx
├── report/
│   └── FQM_Copper_Forecast_Report.docx
├── notebook/
│   ├── FQM_Copper_Production_ML.ipynb
│   ├── sentinel_rf_clean.py
│   ├── sentinel_ridge.py
│   ├── sentinel_gpr.py
│   ├── kansanshi_oxide.py
│   ├── kansanshi_mixed.py
│   ├── kansanshi_sulphide.py
│   ├── kansanshi_total.py
│   ├── fqm_total.py
│   ├── scenario_lines.py
│   └── slope_analysis_v2.py
├── screenshots/
│   ├── Copper_Production_Scenario_Dashboard_Screenshot.png
│   ├── Copper_production_by_scenario_Screenshot.png
│   ├── Production_trajectory_Screenshot.png
│   └── Kansanshi_Mixed_ore_Screenshot.png
└── ml-screenshots/
    ├── sentinel_rf_chart.png
    ├── sentinel_ridge_chart.png
    ├── sentinel_gpr_chart.png
    ├── kansanshi_oxide_chart.png
    ├── kansanshi_mixed_chart.png
    ├── kansanshi_sulphide_chart.png
    ├── slope_analysis.png
    ├── predictions_comparison.png
    └── scenario_forecast_lines.png
```

---

## Tools Used

- **Microsoft Excel** — source data, scenario modelling, regression analysis (R² = 0.993)
- **Tableau** — interactive dashboard and scenario visualisation
- **Python — scikit-learn** — Random Forest, Ridge Regression, Gaussian Process Regression
- **Python — pandas, matplotlib, numpy** — data preparation and visualisation

---

*Data covers FQM Zambia operations 2015–2024 (historical) and 2025–2031 (forecast). All production figures in metric tonnes of copper. Ore processed in thousands of tonnes (000t).*
