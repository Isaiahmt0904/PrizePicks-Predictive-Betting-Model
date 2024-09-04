This model represents one of my first independent projects, designed to apply and reinforce my data science skills in a real-world context. It integrates a variety of data-mining and analytical techniques in JupyterLab, allowing me to explore and reinforce key concepts in a practical, impactful way that is related to a personal interest: Sports.

**Project Structure**
1. Web Scraping
The web scraping module is responsible for collecting raw data from various sources. It gathers:
Player Data: Individual statistics for players, including game-by-game performance.
Betting Data: Over 300 instances of historical betting outcomes, focusing on accuracy and deviations from 2023 NBA data [slight discrepancy since the project bets on WNBA players].
Last 5 Games & Yearly Averages Tables: Summarized statistics that capture a player's most recent form and overall seasonal performance, providing context for more nuanced predictions.

2. Predictor Section
This section of the model initializes multiple predictors, each responsible for analyzing different aspects of the collected data. The predictors generate recommendations on betting decisions, assigning weights based on their confidence level:
- Rolling Average Predictor (Lower Weight)
This predictor calculates the rolling average of the player's last five games for a given statistic. It compares this average to a baseline statistic to make a prediction of "Over" or "Under." The confidence weight for this predictor is static and does not adjust based on model effectiveness.
-Optimized Threshold Calculator 
A function that takes in the betting data acquired before and uses Threshold Optimization via computing the maximized F1 Score (Precision-Recall Metric), to later be compared to the standard deviation of a particular player. 
- Consistency Predictor 
This predictor assesses the consistency of the player's performance over time by calculating the standard deviation of a player from the inputted base stat and compares it to the optimal betting threshold obtained prior,  all via a simple linear regression. The R-squared value from the regression determines the confidence weight, which reflects the model's confidence in its prediction.     
- Trend Predictor
This predictor analyzes long-term trends in the player's performance over years by performing linear regression on time-series data. It accounts for missing data due to injuries by interpolating values. The confidence weight is also adjusted based on the R-squared value, reflecting how well the trend fits the data.
- Minutes Played (MP) Predictor
This predictor evaluates the relationship between the player's minutes played (MP) and the target statistic using linear regression. It splits the data into training and test sets, scales the features, and once again uses the R-squared value to adjust the confidence weight.

3. ObtainDecision Function
This function takes in a player and base stat and synthesizes the outputs and confidence weights from each predictor to make the final data-driven betting decision (over or under). By accounting for the varying degrees of confidence in the predictors, the function ensures that the model's overall recommendation is well-grounded in the analyzed data.


