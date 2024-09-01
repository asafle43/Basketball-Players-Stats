<iframe src="https://giphy.com/embed/7NAQ6qRoa61vCYU9Pa" width="480" height="480" style="" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/nba-cavs-cleveland-cavaliers-donovan-mitchell-7NAQ6qRoa61vCYU9Pa">via GIPHY</a></p>
# Basketball Players Stats-Predicting the #Blocks per Player
An Exploratory Data Analysis and Machine Learning Approach

## 1. Intro
This project focused building a predictive ML model for who want to find and prodict 'How may blocks each player accumulate during a specific season?'.Blocks are a critical defensive metric in basketball, reflecting a player's ability to prevent the opposing team from scoring by deflecting or stopping their shots.
The project relied on a data set from Kaggle and included about 11k players who played in the top 49 leagues and their details.
The details were divided into two - dry details about the player and details about his statistics. 

## Blocks
A block occurs when a defensive player legally deflects or stops a shot attempt from an opposing player, preventing the ball from reaching the basket. Blocks are a key statistic in evaluating a player's defensive abilities.
## Data Insights and Features
*Historical Player Data:*<br>
This includes a player's past performance in terms of blocks, minutes played, games started, and other relevant statistics like rebounds, steals, and fouls.<br>
*Player Attributes:* <br> Physical characteristics such as height, weight, and age and position played (e.g., center, forward).

## 2. Data Preparation: 
### Data Extraction- 
The data set was provided in excel file and i worked on with Python for operations menthos and some EDA(Explanatory Data Analysis).
This file conteind data about the Player and scraped from the https://basketball.realgm.com/ website. <br>
In addition, during the EDA an important need for data on the position of the player emerged.
In basketball every player has a position and the assumption is that the taller the player and in the appropriate position, he will make more blocks.
In the selected data set there was no mention on a position, so I went back to step 1(Data Preparation), turned to the data frame developer, asked him for the code and made adjustments so that each player would have the relevant position for him.

### Variables Translation

This section provides a translation of the key variables used in the model, explaining each basketball statistic and player attribute.

| **Variable**      | **Description**                             |
|-------------------|---------------------------------------------|
| **League**        | The league in which the player competes     |
| **Season**        | The specific season (year)                  |
| **Stage**         | The stage of the season (e.g., Regular, Playoffs) |
| **Player**        | Player's name                               |
| **Team**          | The team for which the player competes      |
| **GP**            | Games Played                                |
| **MIN**           | Minutes Played                              |
| **FGM**           | Field Goals Made                            |
| **FGA**           | Field Goals Attempted                       |
| **FG%**           | Field Goal Percentage                       |
| **3PM**           | Three-Point Shots Made                      |
| **3PA**           | Three-Point Shots Attempted                 |
| **3P%**           | Three-Point Percentage                      |
| **FTM**           | Free Throws Made                            |
| **FTA**           | Free Throws Attempted                       |
| **FT%**           | Free Throw Percentage                       |
| **TOV**           | Turnovers                                   |
| **PF**            | Personal Fouls                              |
| **ORB**           | Offensive Rebounds                          |
| **DRB**           | Defensive Rebounds                          |
| **REB**           | Total Rebounds                              |
| **AST**           | Assists                                     |
| **STL**           | Steals                                      |
| **BLK**           | Blocks                                      |
| **PTS**           | Points                                      |
| **birth_year**    | Year of Birth                               |
| **birth_month**   | Month of Birth                              |
| **birth_date**    | Date of Birth                               |
| **height**        | Height (in feet and inches)                 |
| **height_cm**     | Height (in centimeters)                     |
| **weight**        | Weight (in pounds)                          |
| **weight_kg**     | Weight (in kilograms)                       |
| **nationality**   | Player's nationality                        |
| **high_school**   | High school attended                        |
| **draft_round**   | Round in which the player was drafted       |
| **draft_pick**    | Draft pick number                           |
| **draft_team**    | Team that drafted the player                |

Following this step and accordnig to the time frame of this project, we decided to ignore the Time-Series features.Followitg that i collapsed the stats per Player and the chosen season was '2019-2020' (for hose who played in more than one League/team- we created a calulated column). 

## 3.EDA-Exploratory Data Analysis-
An initial exploratory data analysis was conducted to identify patterns, distributions, and potential correlations between features and the target variable.

1. **Data Cleaning**: Removing duplicates and irrelevant columns, players with two nationalities tagged as 'Two Nationalities'

2. **Data Imputation**: Missing values were addressed using the KNN imputer, which utilizes the nearest neighbors to estimate missing values based on similarity in feature space.
3. **Feature Engineering and Feature selection**: It involves creating new features or modifying existing ones to improve the model’s performance like Minutes per game/FG%- %Field goals/FT%- %Free Throws and Assist:Turnover Ratio per player.Feature selection was conducted using multiple models, including Lasso Regression, Random Forest, and Gradient Boosting, to identify the most predictive variables.

**Plots charts** 
Distribution of Numeric Features:

![image.png](attachment:46b1d21f-6476-485c-9641-1d97ccce09a0.png)

**Numeric Features to identify Outliers:**

![image.png](attachment:39149457-1b86-467c-96fb-d17744dad429.png)
![image.png](attachment:28ff285a-f8ea-44a4-9a33-648d24cbdc59.png)

**Distribution of target value(BLK) Vs. Position:**
![image.png](attachment:c1424a52-77d3-4677-b800-4ffed3f0547a.png)


**Correlation Matrix Heatmap:**
<br>
![image.png](attachment:fcfb4bbe-5d74-4f69-8e8f-e937dd7bcd46.png)

## 4.Model Selection
In this phase the main goal is to select a model that best captures the underlying patterns in the data while generalizing well to unseen data.We chose regression models, were selected due the target variable.
The df was split into Training set size: 69.99%, Validation (Dev) set size: 15.00% and Testing set size: 15.00%.

Multiple models were selected and traind- 
- Linear Regression
- Decision Tree Regressor
- Random Forest Regressor
- AdaBoost Regressor
- Gradient Boosting Regressor (GBM)
- Support Vector Regressor (SVR)
- XGBoost Regressor
- Random Forest Fine Tuning using GridSearchCV
- XGBoost Regressor w Fine Tuning using GridSearchCV

Model Results using the Metrics
- MSE - Mean Squared Error
- RMSE Root Mean Squared Error
- MAE Mean Absolute Error Calculates the average of the absolute differences between predicted and actual values.
- RMSLE Root Mean Squared Logarithmic Error

- Train Results-

![image.png](attachment:e0285741-c83d-4346-8501-f58113b634d7.png)
<br>

- Dev Results- 

![image.png](attachment:b63b8c70-7ac5-4e55-86cf-7311d909eae8.png)
<br>
# 5.Implementation

Following those metrics, the XGBoost Regressor and Random Forest were identified as the top-performing models.
I tested XGBoost model on the test data and we can see good results. <br>
![image.png](attachment:b54d3e20-679c-4e4f-bda4-ab8f6f2d1285.png) <br><br>
![image.png](attachment:9d84e005-5ed3-4c1a-91f4-b41cb7b43045.png)
<br>
