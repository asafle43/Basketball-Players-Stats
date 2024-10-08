![](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExOWthcXVyZ3h3eWhoY2Mwc3hrMTNhdnJnY3ZhNmFocDFuanNkOWp3OCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/7NAQ6qRoa61vCYU9Pa/giphy.gif)

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

![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.14.55.png)
![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.15.06.png)


**Numeric Features to identify Outliers:**

![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.16.01.png)

**Distribution of target value(BLK) Vs. Position-Chart A**

![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.16.43.png)

**Distribution of target value(BLK) Vs. Position-Chart B**
![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.16.50.png)


**Correlation Matrix Heatmap:**
![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.16.36.png)
<br>


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

![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.34.19.png)
<br>

- Dev Results- 
![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.34.22.png)
<br>

## 5.Implementation

Following those metrics, the XGBoost Regressor and Random Forest were identified as the top-performing models.
I tested XGBoost model on the test data and we can see good results. <br>
![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2018.34.31.png) <br><br>
![Screenshot_2](https://github.com/asafle43/Basketball-Players-Stats/blob/main/Screenshot%202024-09-01%20at%2016.08.41.png)

<br>

## 6.Conclusion
In this project, I developed a machine learning model to predict the number of blocks for each basketball player in a specific season. After thorough data preparation and exploratory data analysis (EDA), I experimented with several models, evaluating them based on error metrics such as RMSE and MAE. The XGBoost model emerged as the best-performing model, achieving an impressive RMSE of 0.108 and an MAE of 0.07, indicating strong predictive accuracy. This model can potentially be used to gain valuable insights into player performance and inform strategic decisions in basketball analytics.
