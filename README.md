# README for team "No-Burn Buddies: Straw Edition"

# This README is served as the final report for our mini project.

# Authors: Wen Lu, Xiaoyu Fang, Run Wang, Zijun Xu and Mingyuan Chi

(PS: The "CHN_County.shp" is in the provided dataset, but it is too big (57M) for upload. So we don't upload it in this repository. We did use it for analysis, and sorry for any inconvenience caused.)
# Task 4: Comparison of Agricultural and Other Fires  
## Research objective
This task aims to systematically compare the spatiotemporal and radiative characteristics between **agricultural fires** and **other fires** in Heilongjiang Province.  
The analysis focuses on:  
- Fire Radiative Power (FRP) differences  
- Event duration estimation using DBSCAN  
- Seasonal (DOY) and diurnal (Hour) distribution differences
## Data and Preprocessing
Input file ：modis_heilongjiang_classified_fires.csv
Basic Pretreatment steps :
1. Identify the time column and convert it to the 'datetime' type.
2. Derived time features: 'year', 'month', 'doy' (day-of-year), 'hour', 'week'.
3. Identify 'fire_type' (map to 'fire_type' if there is only 'type') Use 'agri_list = ['Maize_Straw_Burning', 'Wheat_Straw_Burning', 'Cropland_Fire_Other']' to determine whether it is an agricultural fire.
4. Parse the 'geometry' or use 'longitude/latitude' to build a 'GeoDataFrame' and project it to EPSG:3857 (metric) for distance calculation.
5. Prioritize the use of the 'FRP' column. If not available, use 'frp' and convert it to a numerical value. Perform a 'log1p' transformation on FRP for visualization and box plot (retain the original FRP for statistical tests or reverse calculations).
## Methods and Processes
1. Calculation of event duration
- Take the difference between the earliest and latest observation times of each fire event (unit: days).
- Events with a duration that is too short (such as less than 0.1 days) are classified as "hot within one day".

2. Characteristics of Fire Radiant Power (FRP)
- Use the 'log1p(FRP)' transformation to make the distribution smoother and reduce the influence of extreme values.
- Compare the energy release intensity and dispersion of agricultural fires with those of other types of fires.

3. Time Distribution Analysis
- **Annual Distribution (DOY)** : On which day of the year the fire point occurs (1-365), reflecting the seasonality.
- **Intraday distribution (Hour)** : The hour when the ignition point occurs (0-23), reflecting the intraday pattern.

4. Statistical test
To verify whether the differences between the two types of fire are significant, the following non-parametric tests are adopted:
- **Mann-Whitney U test** testing the median difference between the distributions of the two groups
- **Kolmogorov-Smirnov (KS) test** to test the overall difference in distribution between the two groups
## Results and Analysis
### 1. Distribution of Event Duration
! [Event Duration](task4_duration_comparison.png)

** Result Summary: **
- The duration of both types of fire incidents was highly concentrated within one day.
- The tail of the "Other Fires" distribution is slightly longer, and some events last for 2 to 5 days, indicating possible forest fires or grassland fires.
- The box plot shows that the median of agricultural fires is lower and there are fewer outliers, indicating that their burning time is shorter and their controllability is stronger.

### 2. Fire radiation Power Distribution (FRP, log1p transformation)

! [FRP Distribution](task4_frp_comparison.png)

**Result Summary:**
- The FRP peak of agricultural fire is slightly to the left.
- The distribution of other fires is more gentle, with a longer right tail, and there are a few high-intensity events.
- The box plot shows that the distribution of agricultural fires is more concentrated and fluctuates less.

### 3. Time Distribution Characteristics (DOY and Hour)

! [Temporal Distribution](task4_time_distribution.png)

**Annual Distribution (DOY)** :
- Both types of fire show a bimodal distribution.
- Spring (DOY 90-120) and autumn (DOY 270-300) correspond to the seasons of crop harvest and straw burning.
- The peak of agricultural fires is more acute, indicating that their occurrence has a stronger seasonal regularity.
- Other fires have a relatively smooth distribution throughout the year, indicating non-agricultural factors.
**Intraday distribution (Hour)** :
- Agricultural fires are concentrated from 10:00 to 15:00 during the day.
- Other fires are more widely distributed, with a few night-time fire events.
- This indicates that agricultural fires are mostly artificially controlled burning activities and are significantly influenced by human schedules and safe periods.
## Conclusions
1. Agricultural fires show obvious characteristics of human control:
- Concentrated occurrence time (spring and autumn)
- Short duration and low intensity
- Intraday distribution pattern (mainly during the day)
It reflects the concentrated burning characteristics of agricultural activities such as straw burning.
2. **Other fires** exhibit **higher uncertainty** :
- It lasts longer.
- The intensity fluctuates more greatly.
- The distribution of seasons and time periods is relatively scattered.
It may include natural ignition, improper management or non-agricultural use of fire.
# Challenge 1:
To investigate whether significant difference exists between the intensity of agricultural fire and wildfire,vwe categorize Maize_Straw_Burning and Wheat_Straw_Burning as agricultural fires, Cropland_Fire_Other and Non_Cropland fires as wildfires based on the classified fire data in HeiLongjiang Province(modis_heilongjiang_classified_fires.csv). Then,  we first draw a box plots and probability density graph of each group's intensity, to preliminarily observe the distribution of the two groups of data. We find that there are 2890 agricultural fires, while the number of wildfires is 132622, which is much higher. And the max FRP of wildfire is 1824, also much higher than agricultural fire(315). For mean intensuty,  wildfire's FRP is  slightly higher than agricultural fire's FRP. We than carry statistic test to find whether significant difference between the two types of fire's FRP exist. After exmain the distribution of FRP for both type, we find that both of them are not normal distribution, so we use Mann-Whitney U test. The result shows that the fire intensity between the two group has significant difference. In conclusion, we find that agricultural may be not the source of major intense buring events, and wildfires can cause much larger damage compared to agriculture fires.
