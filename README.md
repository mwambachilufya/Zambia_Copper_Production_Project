# FQM Zambia — Copper Production Forecast 2025–2031
### Sentinel FQM & Kansanshi Mine | Scenario Modelling, Tableau Visualisation & Machine Learning

---

## Dashboard.

![Dashboard](Tableau%20Screenshots/Copper%20Production%20Scenario%20Dashboard%20Screenshot.png)

The dashboard shows the FQM copper prodution predictions starting from the actual at 2024 all the way to 2031. The bar chart shows the three 2031 scenario totals for both mines combined. There is the Best Case at 485,416 tonnes, Optimistic at 624,315 tonnes, and Pessimistic at 350,347 tonnes. The pie chart on the right shows how Kansanshi's Optimistic 2031 output is divided based on the type of ore of which mixed ore contributes more at 184,275 tonnes. The line chart at the bottom shows how each scenario trends from the  2024 actual value of 401,721 tonnes all the way up to 2031. The dip on the Best Case line at 2028 is a data entry error in the original excel file which was corrected using three dfferent machine learning algorithms for validation purposes.

---

## 2031 Scenario Comparison

![Scenario Comparison](Tableau%20Screenshots/Copper%20production%20by%20scenario%20Screenshot.png)

Three scenarios were modelled for the combined FQM Zambia operations across Sentinel and Kansanshi. The  difference between optimistic and pessimistic scenario is 274,000 tonnes. The reason for this is because of the mixed ore at Kansanshi. Under the pessimistic case, mixed ore contributes 41,652 tonnes. Under the optimistic case it contributes 184,275 tonnes. That is a difference of 142,623 tonnes. Therefore mixed ore is the most important contributing factor in this prediction thus making it a key performance indicator.

---

## Production Trajectory 2024–2031

![Production Trajectory](Tableau%20Screenshots/Production%20trajectory%20Screenshot.png)

All three scenarios start from the same 2024 actual value of 401,721 tonnes and trend over seven years. The Optimistic case assumes the mine achieves recovery rates, ore grades, and throughput volumes that are very ideal which is why the machine learning models later predict more cautiously on this scenario than the formula-based Excel forecast does because in the real word things are far from ideal. The Best Case line dips sharply at 2028 this is the data error where a missing zero in the Kansanshi mixed ore summary table recorded 10,620 tonnes instead of 106,260 tonnes. The corrected figure is used in all ML predictions.

---

## Kansanshi Ore Circuit Breakdown — Optimistic 2031

![Kansanshi Ore](Tableau%20Screenshots/Kansanshi%20Mixed%20ore%20Screenshot.png)

Kansanshi mines three types of ore. These are oxide, mixed, and sulphide. Each of these has completely different grade, recovery, and throughput characteristics. Under the optimistic 2031 scenario, mixed ore accounts for 184,275 tonnes (52% of total Kansanshi output), sulphide for 119,784 tonnes (34%), and oxide for 50,503 tonnes (14%). In the dashboard the optimistic scenario was chosen because we are trying to investigate what factors contribute to copper production as well as try to predict whether the 3 million tonnes is a viable target. So the optimistic scenario is our best chance of getting a value that high. In this case it turns out that in this particular scenario if we wanted to get a value that high then more of the mixed ore would have to be mined seeing it produces the most to kansanshi which will in turn increase the overall production of FQM. 

---

## Machine Learning — Sentinel FQM

Three models were applied to Sentinel's historical production data (2015–2024): Random Forest, Ridge Regression, and Gaussian Process Regression. Sentinel was chosen first because it is a single ore open pit.

### Random Forest

![Sentinel RF](Model%20results%20screenshots/sentinel_rf_chart.png)

Random Forest works by building 200 decision trees independently and then average their predictions. The feature importance panel reveals that throughput drives 43.8% of Sentinel's production, recovery rate 33.4%, and ore grade 22.8%. So this means that under these parameters the mine can focus on having their equipment always available such as crushers and mills and also working on making surre their blasting is high quality so that more rock may enter the mills.. The 2031 prediction panel shows that the Best Case and Optimistic predictions are identical at 239,450 tonnes, meaning the model has hit a ceiling. It cannot predict values outside the range it was trained on. This is addressed by Ridge Regression and GPR below.

### Ridge Regression

![Sentinel Ridge](Model%20results%20screenshots/sentinel_ridge_chart.png)

Ridge Regression shrinks the coefficients towards zero in order to stop overfitting which is common with small datasets like this one. It gave the strongest cross-validated R² of the three models at 0.4359, and a test R² of 0.9584. The coefficients panel shows that throughput and recovery both drive production upward as expected. So under this model the mine must focus on blasting and equipment availability to ensure maximum throughput and making the grinding finer so as to make sure the reagent chemicals can reach the finer grinded rock. Ore grade shows a negative but this is because the two values recovery and ore grade correlate in some ways in the historical data when one is positive the other is positive too and so on. So the ridge model separates these two and makes one a negative for more cautious prediction purposes so it is something that s unique to the model. Unlike Random Forest, Ridge extrapolates properly the Optimistic prediction of 242,533 tonnes is different from the Best Case at 238,715 tonnes.

### Gaussian Process Regression

![Sentinel GPR](Model%20results%20screenshots/sentinel_gpr_chart.png)

Gaussian Process Regression is specifically designed for small datasets and provides a confidence interval alongside each prediction rather than a single value. The confidence band chart shows the 95% interval becoming a bit narrow at Pessimistic (±9,333 tonnes, 3.8% of the prediction) and widening very much at Optimistic (±33,545 tonnes, 12.1%). The Optimistic scenario requires recovery rates and throughput volumes Sentinel has never had before.So in this case GPR is showing a level of uncertainty with these predictions which is healthy . The Excel forecast of 269,753 tonnes is within GPR's Optimistic confidence interval of 243,913 to 311,004.

---

## Machine Learning — Kansanshi

Kansanshi was modelled by ore type. Three separate models were trained for each type: oxide, mixed, and sulphide using the same three algorithms. The ore type predictions were then summed to produce the total Kansanshi forecast.

### Oxide Ore

![Kansanshi Oxide](Model%20results%20screenshots/kansanshi_oxide_chart.png)

The oxide circuit is the most stable and predictable of the three. All three models produce tight predictions close to the Excel forecast across all scenarios — GPR's confidence intervals are the narrowest in the entire project (±2,331 pessimistic, ±1,593 best case, ±3,665 optimistic). Ridge achieves the only positive cross-validated R² at 0.1323. The oxide ore is in long-term decline.

### Mixed Ore Circuit

![Kansanshi Mixed](Model%20results%20screenshots/kansanshi_mixed_chart.png)

The mixed ore type is the most interesting ore type in the entire project. It drives the largest spread between scenarios. it goes from 41,652 tonnes pessimistic to 184,275 tonnes optimistic which is a 142,000 tonne range from a single ore type. Ridge achieves a cross-validated R² of 0.8890 on mixed ore, the strongest performance of any model on any ore type in this project. The RF ceiling effect is clearly visible on the RF panel. The Optimistic and Best Case predictions are identical at 79,409 tonnes. Ridge and GPR both extrapolate beyond the training range, though more cautiously than the Excel formula. This is an ore type worth searching and investing in.

### Sulphide Circuit

![Kansanshi Sulphide](Model%20results%20screenshots/kansanshi_sulphide_chart.png)

Sulphide ore grade has declined from 0.88% in 2021 to 0.60% in 2024 . The RF feature importance panel tells us that: throughput drives 55.9% of sulphide production  and grade drives 37.0%. The dominance of throughput over grade reveals that the mine has been compensating for falling grade by pushing more ore through the mill. This strategy has though successful at times has its limits and can lead to the over using of mining machinery.

---

## Slope Analysis & Best Case Correction

![Slope Analysis](Model%20results%20screenshots/slope_analysis.png)

The slope analysis shows the rate of production change in tonnes per year between 2024 and 2031. The top panel shows the corrected Best Case Excel line  the 2028 dip caused by the data entry error has been removed and replaced with the correct value of 106,260 tonnes. The bottom left chart shows slopes across all models and scenarios. The bottom right chart shows how the ML models differ from the Excel growth rate. On Pessimistic scenario the difference is small, all models are more all less the same. On Optimistic the difference is large, with RF at -20,883 t/yr. Therefore, the pessimistic scenario is statistically the most likely forecast. The optimistic scenario requires operating conditions that have never been seen before at either mines. If we had to pick one scenario that would happen in 2031 the pessimistic scenario is the safest and realistic bet.

---

## All Models — 2031 Final Comparison

![Predictions Comparison](Model%20results%20screenshots/predictions_comparison.png)

The final comparison shows Excel, Ridge, and GPR side by side for both mines. For Sentinel, Ridge and GPR closely bracket the Excel forecast on Pessimistic and Best Case within 5%. For Kansanshi the models are more cautious on the Optimistic scenario. The overall picture shows that the scenarios, predicted by the models, that are more in agrrement with the  Excel predictions are for Pessimistic and Best Case. The Optimistic scenario should be treated as something that needs a lot of things to go right before it occurs which in an ideal world it does not.

---

## Scenario Forecast Lines

![Scenario Forecast Lines](Model%20results%20screenshots/scenario_forecast_lines.png)

Three line charts show the full 2024 to 2031 trajectory for each scenario. The Pessimistic chart shows all lines declining from the 2024 baseline. The Best Case chart shows the error in the  Excel trajectory. The Optimistic chart is where the story is clearest. The Excel line climbs in a very steep way up to 624,315 tonnes while RF goes flat and Ridge and GPR rise steadily. The gap between Excel and the ML models on Optimistic means that the mines need to operate in an ideal way which is rare in the real world.

---

## Conclusion

---

Can Zambia reach 3m tonnes by 2031? Yes and no. FQM contributes roughly 45 % of Zambias total copper output then the 55 is split by the other big mines which are Barrick lumwana, KCM and Mopani as well as small scale mines. For the share of 45% FQM would need to provide historical numbers of output approximately 1.3 million tonnes, by expanding into more areas with mixed ore for kansanshi and increasing the throughput and overall operations at sentinel to never before seen excellent levels. Then the rest must be compensated for by other big mines or other newer mines being set up. In this case it is possible. If however things remain as they are then the target may come too soon. 

---
