# Earthquake Damage Prediction and Rental Prices in Istanbul
Term Project for DSA210: Introduction to Data Science

## Project Overview 
Istanbul is a highly populated city with a large number of buildings and a well-known high earthquake risk due to its location near active fault lines. This project aims to analyze the relationship between earthquake damage risk and rental housing prices across Istanbul's different districts and neighborhoods. By considering the predicted building damage and casualty rates at the district and neighborhood level under a potential 7.5 magnitude earthquake, rental prices will be examined together with building-related features such as age, floor level, apartment size, and number of rooms to determine which factors most strongly influence rent values. The main goal is to understand the overall pattern of Istanbul's housing market and urban planning, and to guide safer housing decisions. 

## Motivation
Recently, while searching for a new apartment in Istanbul with my family, the main factor we considered was the earthquake damage risk of the buildings and districts. This experience led me to wonder how and to what extent this factor affects rental prices across the city, and whether people's housing decisions reflect earthquake risk awareness. 

## Objectives
- Analyze how rental prices across Istanbul differ according to earthquake damage and casualty risk levels at the district and neighborhood scale.
- Examine how property characteristics — such as building age, floor level, apartment size, and number of rooms — influence rental values.
- Identify which of these factors have the biggest overall impact on housing prices and how they interact with earthquake risk.
- Compare the relative impact of seismic risk and property features to identify which plays a more dominant role in shaping rent variation.

## Data Sources

**Istanbul Rental Apartments Dataset (2025) on Kaggle**
- This dataset contains rental apartment listings from Istanbul. It includes detailed information about rental properties such as: 
   - district: The district (e.g., Beşiktaş, Kadıköy)
   - neighborhood: The neighborhood name
   - room: Number of rooms
   - living_room: Number of living rooms
   - area_m2: Apartment size in square meters (m²)
   - age: Age of the building
   - floor: Floor number (Negative values indicate basement floors)
   - price_per_m2: Rental price per square meter in Turkish Lira (TRY)
   - total_rent: Total rental price of apartment
     
**Earthquake Risk Data — “District-Level Earthquake Loss Estimation Reports” (İBB)**
- Published by the Istanbul Metropolitan Municipality (İBB) Earthquake and Ground Investigation Department under the "Olası Deprem Kayıp Tahminleri İlçe Kitapçıkları" project (2020–2025).
- Provides district and neighborhood-level numerical estimates for a potential 7.5 magnitude earthquake scenario. Includes variables such as:
   - Predicted building damage counts: number of lightly, moderately, heavily, and very heavily damaged buildings
   - Estimated human impact values: number of fatalities, severe injuries, hospital-treated injuries, and minor injuries
 
## Analysis Plan 
  - Extract building damage and casualty estimation tables from İBB’s District-Level Earthquake Loss Estimation Reports and convert them into a clean CSV format
  - Clean and standardize district and neighborhood names to ensure consistency across both datasets
  - Merge the rental housing dataset and the earthquake loss dataset using district and neighborhood as common keys
  - Create new variables to represent earthquake vulnerability, such as:
    - Damage Ratio: proportion of damaged buildings (light, moderate, heavy, very heavy) relative to total buildings
    - Casualty Ratio: proportion of predicted minor injuries, hospitalizations, severe injuries, and fatalities relative to the neighborhood population
 - Conduct exploratory data analysis (EDA) to observe trends and outliers
 - Perform statistical tests and correlation analysis to see how rent relates to risk and property factors
 - Visualize results using charts to highlight patterns
  
## Hypotheses
  - **H1 - Earthquake Risk vs Rent:**
       - **Null Hypothesis(H0):** District and neighborhood-level earthquake risk indicators (damage ratio, casualty ratio) have no relationship with rental prices.
       - **Alternative Hypothesis(H1):** Districts and neighborhoods with higher earthquake risk have lower rental prices on average.
  - **H2 - Building Age vs Earthquake Risk Interaction:**
       - **Null Hypothesis(H0):** The relationship between building age and rental price does not depend on the level of neighborhood earthquake risk.
       - **Alternative Hypothesis(H2):** The negative effect of building age on rental prices is stronger in high-risk neighborhoods, indicating that older buildings are discounted              more heavily where earthquake risk is elevated.
  - **H3 - Floor Level vs Earthquake Risk Interaction:** 
      - **Null Hypothesis(H0):** Floor level has the same impact on rental prices across low-risk and high-risk neighborhoods.
      - **Alternative Hypothesis(H3):** Higher-floor apartments become cheaper in high-risk neighborhoods compared to low-risk ones, showing that people are more worried about living on upper floors when the earthquake risk is higher.
   
## Methodology Overview

The analysis follows a three-stage pipeline. First, exploratory data analysis (EDA) is conducted on the merged rental and earthquake datasets to understand distributions, detect outliers, and identify preliminary relationships. Second, formal hypothesis testing is performed to quantify the statistical significance and magnitude of the relationships between earthquake risk, property characteristics, and rental prices. Finally, multiple machine learning models are trained to evaluate predictive performance and to compare the relative importance of earthquake risk indicators versus structural apartment features.

## Methodology

This project follows a three-stage workflow: (1) data preparation and exploratory analysis, (2) statistical hypothesis testing, and (3) predictive modeling with machine learning. The objective is to assess whether neighborhood-level earthquake risk is reflected in rental prices and how its influence compares with structural apartment characteristics.

### 1) Data Preparation & Feature Engineering
Rental apartment listings are merged with neighborhood-level earthquake loss estimates published by the Istanbul Metropolitan Municipality using standardized district and neighborhood identifiers. Location names are normalized (case, Turkish characters, and spelling variants) to minimize merge mismatches, and duplicate or clearly invalid observations are removed based on consistent filtering rules.

The primary outcome variable is **price per square meter**, with log-transformations applied where appropriate to reduce skewness and support statistical assumptions. Earthquake-related variables—including building damage counts and casualty estimates—are converted into **ratio-based indicators** to enable fair comparisons across neighborhoods of different sizes. These indicators are further combined into a **unified earthquake risk index** that summarizes multiple risk dimensions in a single comparable measure.

The resulting analysis-ready dataset includes structural apartment features (size, number of rooms, building age, and floor level), engineered earthquake risk indicators, and location identifiers used for grouping and robustness checks.

### 2) Exploratory Data Analysis (EDA)
Exploratory data analysis is conducted to understand distributions, detect outliers, and identify preliminary relationships prior to formal inference. Rental price variables are inspected for heavy right-skewness, motivating the use of log-transformed outcomes in subsequent analyses.

Bivariate relationships between rental prices and key predictors—apartment size, room count, building age, floor level, and earthquake risk—are visualized and summarized to guide model and test selection. Neighborhoods are classified into **low-risk and high-risk groups using a median split of the unified earthquake risk index**, ensuring balanced and interpretable comparisons. Insights from EDA are used to refine hypotheses and motivate the structure of subsequent statistical tests.

### 3) Hypothesis Testing & Predictive Modeling
This stage combines statistical inference, which focuses on significance and interpretability, with machine learning, which emphasizes predictive performance and relative feature importance.

For hypothesis testing, statistical significance is evaluated at **α = 0.05**, with test choices guided by distributional properties and heteroskedasticity considerations.  
- **H1 (Earthquake Risk vs Rent):** The relationship between earthquake risk and log(price per m²) is examined using correlation analysis and mean comparisons between low-risk and high-risk neighborhoods.  
- **H2 (Building Age × Risk):** Separate regressions are estimated for low-risk and high-risk groups to directly compare the magnitude of age-related price penalties across risk levels.  
- **H3 (Floor Level × Risk):** A similar group-wise regression approach is used to assess whether the price premium associated with higher floors weakens under higher earthquake risk.

For predictive modeling, a linear regression baseline is compared with non-linear models to evaluate how well rental prices can be predicted and to assess the relative contribution of earthquake risk indicators versus structural apartment characteristics. Model performance is evaluated using **5-fold cross-validation**, with comparisons focusing on both predictive accuracy and stability across folds. Evaluation metrics include **R² and error-based measures**, capturing both explanatory power and prediction quality. Machine learning results are interpreted as complementary evidence, providing insight into complex, non-linear relationships that extend beyond isolated statistical tests.
   
## Results and Interpretation

### Exploratory Data Analysis (EDA)

The merged dataset successfully integrates rental listings with detailed neighborhood-level earthquake indicators. Earthquake-related variables are transformed into normalized ratios and a unified earthquake risk index, enabling consistent comparisons across districts and neighborhoods.

Rental prices are heavily right-skewed and show substantial spatial variation across Istanbul. Property characteristics such as apartment size, number of rooms, building age, and floor level exhibit clear and interpretable relationships with price per square meter. In comparison, earthquake risk shows a negative but moderate association with rental prices: higher-risk neighborhoods tend to have lower average prices per m², although this effect is weaker than that of core property features.

These findings motivate formal hypothesis testing to assess the statistical significance and magnitude of these relationships.

---

### Hypothesis Testing Results

**H1 – Earthquake Risk vs Rental Prices**

Both Pearson correlation analysis and group-based comparisons indicate a statistically significant relationship between earthquake risk and rental prices. The correlation between the earthquake risk index and log(price per m²) is moderate and negative (r ≈ –0.25), with a p-value far below the 0.05 significance level. Similarly, low-risk neighborhoods exhibit substantially higher mean rental prices per m² than high-risk neighborhoods.

These results suggest that earthquake risk is reflected in rental prices in Istanbul, leading to rejection of the null hypothesis for H1.

---

**H2 – Building Age × Earthquake Risk Interaction**

Regression results confirm that building age has a statistically significant negative effect on rental prices per m² across all neighborhoods. However, the magnitude of this effect differs by risk group. Contrary to expectations, the negative impact of age is stronger in low-risk neighborhoods than in high-risk ones.

Because older buildings are not discounted more heavily in high-risk areas, the evidence does not support H2. Therefore, the null hypothesis cannot be rejected.

---

**H3 – Floor Level × Earthquake Risk Interaction**

Floor level has a statistically significant positive effect on rental prices in both low-risk and high-risk neighborhoods. However, this positive effect is substantially weaker in high-risk areas. While higher floors command strong price premiums in low-risk neighborhoods, this premium is noticeably reduced where earthquake risk is elevated.

This asymmetric effect supports the alternative hypothesis, leading to rejection of the null hypothesis for H3.

---

### Machine Learning Results

Across all tested models, non-linear approaches outperform the linear baseline, indicating that rental price formation in Istanbul is not well described by simple linear relationships. Among these models, Random Forest achieves the strongest and most stable performance under cross-validation.

Feature importance analysis shows that structural apartment characteristics remain the dominant drivers of rental prices. Nevertheless, earthquake risk indicators contribute meaningful predictive signal, complementing the statistical findings from the hypothesis testing stage. Moderate R² values across models suggest that important explanatory factors—such as neighborhood amenities, construction quality, and broader market conditions—are not fully captured in the dataset.

## Conclusion

This project examines whether neighborhood-level earthquake loss estimates are reflected in Istanbul’s rental housing market when controlling for property characteristics. The results indicate that while structural apartment features and location dominate rental price formation, earthquake risk is statistically associated with lower rents and influences how certain features—such as floor level—are priced.

Overall, the findings suggest that earthquake risk is partially incorporated into rental prices, though its effect is smaller than that of traditional housing attributes. This highlights a gap between objective seismic risk and market valuation, with important implications for urban planning and safer housing decisions.

## Limitations and Future Work

This study relies on online rental listings, which may not fully represent the entire housing market and may contain listing bias. The analysis is observational, so causal interpretations cannot be made. Additionally, the earthquake risk data and rental listings are not perfectly aligned in time, and neighborhood-level aggregation may mask building-specific risk differences.

Future work could incorporate spatial variables such as proximity to fault lines, public transportation, and amenities, as well as building quality indicators and temporal price dynamics. More advanced spatial or hedonic pricing models could further improve explanatory power and policy relevance.
