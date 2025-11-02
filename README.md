# README for team "No-Burn Buddies: Straw Edition"

# This README is served as the final report for our mini project.

# Authors: Wen Lu, Xiaoyu Fang, Run Wang, Zijun Xu and Mingyuan Chi

(PS: The "CHN_County.shp" is in the provided dataset, but it is too big (57M) for upload. So we don't upload it in this repository. We did use it for analysis, and sorry for any inconvenience caused.)
# Challenge 1:
To investigate whether significant difference exists between the intensity of agricultural fire and wildfire,vwe categorize Maize_Straw_Burning and Wheat_Straw_Burning as agricultural fires, Cropland_Fire_Other and Non_Cropland fires as wildfires based on the classified fire data in HeiLongjiang Province(modis_heilongjiang_classified_fires.csv). Then,  we first draw a box plots and probability density graph of each group's intensity, to preliminarily observe the distribution of the two groups of data. We find that there are 2890 agricultural fires, while the number of wildfires is 132622, which is much higher. And the max FRP of wildfire is 1824, also much higher than agricultural fire(315). For mean intensuty,  wildfire's FRP is  slightly higher than agricultural fire's FRP. We than carry statistic test to find whether significant difference between the two types of fire's FRP exist. After exmain the distribution of FRP for both type, we find that both of them are not normal distribution, so we use Mann-Whitney U test. The result shows that the fire intensity between the two group has significant difference. In conclusion, we find that agricultural may be not the source of major intense buring events, and wildfires can cause much larger damage compared to agriculture fires.
