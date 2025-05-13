#  Formula 1 Through Data: Uncovering What Drives Success on the Track

## Introduction 

Formula 1 (F1) widely regarded as the pinnacle of motorsport, where cutting-edge technology, driver expertise, and strategic decision-making converge to create one the most competitive sports globally. Spanning diverse circuits worldwide, each Grand Prix epitomizes engineering excellence, precise strategy execution, and split-second decisions that often determine success or failure.

The ultimate goal for teams and drivers each season is to secure the World Drivers' Championship (WDC) and World Constructors' Championship (WCC). where fractions of  second can be the difference between winning and losing. A team or driver's success is influenced by several independent factors:

- Driver skill and adaptability: A driver’s ability to adjust to changing race conditions, car dynamics, and strategic demands is vital.
- Constructor performance: The technical prowess of the car, including aerodynamics, power unit optimization, and tire management, plays a significant role.
- Circuit features: Track characteristics like length, corner count, straights, and throttle zones all impact strategy.
- Pit stop strategy : Fast and efficient pit stops are critical for maintaining or gaining track position.

This project leverages exploratory data analysis (EA) and machine learning techniques to uncover relationships in F1 racing data. By analyzing driver performance, constructor success, pit stop efficiency, and circuit characteristics, the project seeks to explain how strategy, engineering decisions, and team execution shape race outcomes. 

## Research Questions

1. How does a driver's performance evolve when they switch teams, and what role fo constructors play in shaping their success?
2. Can patterns or trends in pit stop data reveal insights into team strategies and race outcomes?
3. Can data-driven models predict race outcomes, such as point finishes, podium placements, or race wins, based on race and pit stop data?
4. What influence do pit stop duration, frequency, and timing have on overall race success for drivers and teams?

## Data Collection

Data was collected from a combination of APIs and web scrapping:

**ERGGASRT API** 
- Race information: Season, round, location, date, driver, and constructor details.
- Driver standings: Contains total points earned by each driver from 2000 to 2023. 
- Circuit information: Circuit name, city, country, coordinates. 
- Pit stop data: Duration and frequency of pit stops per race. 

**NEWS API**

Articles were gathered for the top 10 drivers as of Round 22 (Las Vegas) of the 2024 season to analyze media coverage and potential career moves. 

**fastf1** 
Circuit Features: Around the F1 season, circuits vary widely in their features—some are known for tight, technical corners, others for long, high-speed straights, and a few for their narrow and challenging layouts. These unique characteristics influence car and driver performance significantly, with certain drivers or car designs excelling on specific track types. Analyzing racetrack features is crucial for understanding how different teams and drivers perform under varying conditions. This information can be used to classify tracks, which can further be studied to identify patterns and trends in race results.

**Web Scraping (Wikipedia)**
Weather Data: Collected for each Grand Prix, as race-day conditions impact tire choice, race strategy and driver performance. 

## Data Cleaning

Standard data cleaning methods were applied on the text data and tabular data. 

## Exploratory Data Analysis

- News Data: The analysis of news articles centered in select drivers who dominated media attention during the 2024 season, including Max Verstappen, Carlos Sainz, Lando Norris, Daniel Riccardo, and Lewis Hamilton. These drivers were closely followed due to contract negotiations, mid-season performance shifts, and transfer rumors ahead of the 2025 season. Word clouds of article mentions helped visualize how media focus evolved throughout the season. This added a valuable off-track dimension to the understanding of driver dynamics and public perception.

- Driver Performance: Driver performance was evaluated by analyzing cumulative points accumulated across their careers. This longitudinal view allowed patterns of driver development, consistency, and peak seasons to emerge. Additionally, the proportion of points earned under each constructor was calculated to understand the role of team changes on driver success, and highlighted key moments when drivers switched teams and if the driver's ability improved or struggled to adapt. 

- Constructor Performance: Constructors were studied based on key operational metrics including race completion rates, mechanical failure rates, and frequency of lapped races. These indicators were essential in assessing the overall reliability and competitiveness of each team.

## Feature Selection

Feature selection was used to identify the most relevant features that contribute significantly to predicting if a driver will score points or not in the grand prix. 

Methods used: 
- Correlatiion Analysis
- Recursive Feature Elimination (RFE) 
- Mutual Information

## Unsupervised Learning

Dimensionality Reduction and Clustering techniques were used to uncover hidden structures within the F! dataset, particularly focusing on pit stop data and circuit characteristics. First, dimensionality reduction techniques such as PCA and t-SNE were applied to the high-dimensional pit stop dataset to simplify it and visualize relationships between variables in two dimensions. This made subsequent clustering more interpretable. 

Clustering algorithms like KMeans, DBSCAN, and Hierarchical Clustering were then used to analyze race strategies and circuit groupings. Clustering pit stop data helped identify patterns in stop frequency, duration, and timing across teams and races. For circuit analysis, clustering based on track features (e.g., number of corners, straight lengths, average speeds) revealed natural groupings of similar circuits such as high-speed power tracks versus tight, technical street circuits. These groupings offered valuable insights into how drivers and teams adapt strategies across different racing conditions.

## Supervised Learning 

A series of supervised learning models were applied to predict race outcomes and pit stop durations. For race outcome predictions, the primary task was to classify whether a driver would finish in the points or not. Decision Tree and Random Forest Classifiers were tuned to address this binary classification problem, producing reliable results in predicting points finishes based on pit stop data.

|Model| Accuracy|
|:-:|:-:|
|Decision Tree |0.80|
|Random Forest | 0.81|

To further explore the predictive power of pit stop data, the race outcome variable was binned into 4 categories. Models like Random Forest Classifier and KNN were applied to this multiclass problem. While the first 5 finishes were predicted with higher accuracy, the results confirmed that prediction performance decreased as the number of classes increased, illustrating the complexity of predicting exact finishing positions solely based on pit stop behavior.

|Model| Accuracy|
|:-:|:-:|
|Random forest| 0.51|
|KNN| 0.51|

For regression, Linear Regression, Polynomial Regression, Support Vector Regression, and Random Forest Regressors were used to predict pit stop durations.

|Model| MSE |
|:-:|:-:|
|Linear regression | 0.0118|
| Polynomial regression | 0.0116|
|SVR | 0.0104|
| Random forest | 0.0043|




