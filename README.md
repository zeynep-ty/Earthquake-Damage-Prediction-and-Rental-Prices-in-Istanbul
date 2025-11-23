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
   - price: Rental price per square meter in Turkish Lira (TRY)
     
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
 - Visualize results using charts and maps to highlight spatial patterns
  
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
  - **H4 - Dominant Factor Comparison:**
      - **Null Hypothesis(H0):** Earthquake risk indicators and property features(size, building age, room count, floor level, etc.) have equal predictive power for rental prices.
      - **Alternative Hypothesis(H4):** The influence of property characteristics on rental prices is stronger than the effect of earthquake risk indicators, suggesting that market             dynamics prioritize structural factors over risk perception.

