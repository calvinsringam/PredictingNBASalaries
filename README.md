# NBA Salary Predictions

## Introduction/Background
<p>The NBA, National Basketball Association, is one of the four major sports leagues in the United States. With this, comes a high level of competition between each team, with each team constantly looking for ways to improve. One such method that has gained popularity in the league in free agency, which allows a team to create a contract with a player who is not currently on a team due to the end of their previous contract or any other reason. This project aims to predict the salary of players as they enter free agency based on their performance with statistics such as points, 3-point percentage, and other metrics.</p>

## Problem Definition
<p>The issue with contracts in the NBA is cap space, which prevents larger market teams from offering large sums to the best player, which would suffocate smaller market teams [1]. Cap space puts a limit on the amount that a team can pay all of its players in total [1]. Predicting contracts would aid in correctly assessing a player's worth to a team, and if the contract is viable for a certain team. Additionally, larger contracts are a point of interest for fans of the NBA, which provides another avenue of discussion with contracts.</p>

## Methods
<p>
Previous research in predicting salaries, which was published in 2016, uses a Random Forest model to determine a salary range for students with a variety of input features, for example gender and GPA [2]. This, informally, makes logical sense: an employer may have certain thresholds for applicant traits that they think are important, and they may base hiring policies and salaries on if these thresholds are met by applicants. There is evidence that this model has parallels in NBA salary prediction, a Decision Tree or Random Forest Regressor will be a good start for predicting player salaries (and we can also try classifying over ranges of salaries) [3]. </p>
<p>
Because of the use of a Random Forest Regression, it is not necessary to perform feature reduction or selection. In stead, the regression applies importance to each eafture, which can be seen later, and calculates salaries based on those factors. Below is a heatmap which illustrates the relation of the features to each other using this idea. </p>

![heatmap](https://github.gatech.edu/storage/user/47366/files/f8626e0e-1841-444e-853f-038924c01278)


## Results and Discussion
<p> By analyzing different features and their impact on player salaries, the model should present which statistics teams value in creating a player contract, the worth of that player to the franchise, and the player's attribution to the success of the team. These features would present a viable prediction for a contract range for the player.</p>

<img width="412" alt="Screen Shot 2022-04-04 at 1 09 02 PM" src="https://github.gatech.edu/storage/user/45892/files/7cb73927-5c2b-466d-8d73-52909c2fd8de">

<p> The pi chart above shows the six top features that have the largest impact on player salary (PTS, FTM, FTA, FGM, +/-, and DREB). The other eighteen features only account for 26.8% combined, with little impact on player salary when considered individually. The most important features being PTS, FTA, and FTM makes logical sense when considering the correlation of the features with player salary. These three features take up over 50% of the feature importance, making them prime candidates for further analysis. </p>

![image](https://github.gatech.edu/storage/user/60314/files/ac35f99e-ad03-489a-b2e7-25efdda7fbdb)

<p>The above chart shows the percentage contribution on player salary by feature. The top three features (PTS, FTM, and FTA) contribute the most significantly to the salary, and the next two (FGM and +/-) are the next most significant. All other features contribute less than 5% to the player salary.</p>

![image](https://github.gatech.edu/storage/user/60314/files/a5b7c4e8-cd76-4ead-a4a6-8e512ee39389)<br/>
![r2](https://github.gatech.edu/storage/user/47366/files/187f4239-e64b-483e-a305-2814a34ec53b)

<p>Above are various metrics we tested our model on. The standard for explained variance is that is should not be below 0.6, and our model exceeds that value.
However, our MAPE score is not within the standard for a typical acceptable amount.</p>

![image](https://github.gatech.edu/storage/user/60314/files/47a47c52-deed-4bfd-a1d4-523519d05526)
<p>One interesting point of data was the difference in salary for Brook Lopez. This was the highest difference between actual and predicted salary (meaning our model indicats he was overpaid). After researching into the situation, Lopez was injured in 2013, meaning he wasn't able to play and had less data points to contribute, particulary in the points feature which our model showed as the most important predictor. Going forward, it would be interesting to introduce an 'Injured' feature into the data that indicates whether a player was injured during the season and for how long to make the model more accurate.</p>

<p>Another improvement going forward could be not looking at the salary amount, but rather the percentage of the salary cap that a team has. Since the cap has increased, it is inevitable that players will be paid more and comparisons across years wont be as indicative as to actual values. Using the percetange of salary cap would help to standardize this more across different years.</p>

![image](https://github.gatech.edu/storage/user/60314/files/3d96df86-228b-47b6-aa92-cdee874cf891)

<p>One final area for improvement would be adjusting the hyper parameters for the model, specifically the number of estimators, maximum features, and maximum depth. For number of estimators, setting that at six would likely maximize the accuracy of the model since six features as shown in the above sections account for the majority of the contribution in the model. A randomizedsearchCV package was implemented, but gave poor results in terms of accuracy, so ideal implementation was not reached. A slightly lower accuracy was reached after adjusting some parameters, but the difference was not significant. We weren't able to fully tune the hyper parameters, but the ideal situation would be looping through many (hundredss or thousands) of iterations of the three mentioned parameters, printing out the accuracy of the model given the train and test data, and going with the hyper parameters that provided the highest accuracy. It is important to note that while the model can be adjusted to make better predictions, the limitations of the model will still persist.</p>

<p> Contrary to our results, experts analysis say that Three point %, Assist to Turnover Ratio and Offensive Rebounds and assists are some of the most valuable stats. But our analysis with the data we have extracted says otherwise. This maybe because our dataset is not exactly whole or maybe we can't perfectly deduce contract values by just looking at statistics. This is probably one of the limitations of what data can accurately show, we may use additional methods to test our hypothesis.  </p>

#### Linear Regression

![image](https://github.gatech.edu/storage/user/47366/files/6efa7737-ecb9-4526-a710-d0c7aaba8b36)

<p>After using Random Forest, we wanted to confirm our results with different machine learning models so we tried using Linear Regression. In Linear Regression we used the same dataset we used for Random Forest and got a similar Root Mean Squared Error (RMSE). We got a RMSE value of 4330957.16 and a Rsquared value of 0.63 using the Random Forest Model and a RMSE value of 4711974.11 and a R-squared value of 0.6204 using the Linear Regression Model. While the relative value of the RMSE in both models is close to the other, Random Forest edges out the linear regression model, meaning that the Random Forest Model is better suited for salary predictions than linear regression.</p>

#### Decision Tree

![image](https://github.gatech.edu/storage/user/47366/files/9509108b-656d-40a7-9ac4-3571214765a4)

<p>For a final comparison, a single decision tree model was implemented, and the performance metrics of this model can be seen above. In comparison to the random forest model, the decision tree has a much higher RMSE value and a lower R-squared value (under the expected 0.6 variance). This implies that the model is not adequate for predicting NBA player salaries, which is expected compared to random forest. Since a random forest is comprised of many decision trees which are utilized to make a final decision, a random forest will naturally produce better results.</p>

## Conclusion
<p>After implementing the feature selection methods and prediction model, it can be seen that points, free throws made/attempted, and field goals are the most important factors when it comes to predicting salaries in the NBA. However, these models are not able to account for injuries players may sustain, which would lower the value of that player during the season. Additionally, a salary cap consideration can be made to better analyze the worth teams see in a player's contribution to the team. Finally, after comparison with linear regression and decision tree models, it can be concluded that a random forest model is the most effective in predicting NBA salaries. </p>

## References
<ol>
  
  <li> S. Mincev, "Analysing Data Mining Methods in Sports Analytics: A Case Study in NHL Player Salary Prediction." Order No. 28727378, Universidade NOVA de Lisboa (Portugal), Ann Arbor, 2021. </li>
  <li>P. Khongchai and P. Songmuang, "Random Forest for Salary Prediction System to Improve Students' Motivation," 2016 12th International Conference on Signal-Image Technology & Internet-Based Systems (SITIS), 2016, pp. 637-642, doi: 10.1109/SITIS.2016.106.
 </li>
  <li>J. Brownlee, “How to calculate feature importance with python,” Machine Learning Mastery, 20-Aug-2020. [Online]. Available: https://machinelearningmastery.com/calculate-feature-importance-with-python/. [Accessed: 23-Feb-2022].  </li>
  <li> Hagness, M. (2022, March 3). The most important stats to track for your basketball team. BREAKTHROUGH BASKETBALL. Retrieved April 5, 2022, from https://www.breakthroughbasketball.com/stats/how-we-use-stats-Hagness.html  </li>
</ol>

