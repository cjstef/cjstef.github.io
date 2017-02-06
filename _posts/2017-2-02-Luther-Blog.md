#Project Luther

The second and third weeks at Metis introduced linear regression and various related techniques as a means for predictive modeling. The lectures culminated with project Luther, a multiphase project which involved scraping data from the web, cleaning, and analyzing the data to develop a predictive model.

##Part I - Defining the Problem and Acquiring Data

For my project, I chose to examine end of season statistics for NFL teams as a means for projecting playoff success. Due to the massive popularity of football, relevant stats were abundant, and the main challenge for this aspect of the project was selecting which stats to scrape and defining the time period to acquire data from.

Data was scraped from the sports stat website [Football Outsiders](https://www.footballoutsiders.com) and the initial set of statistics (features) included were selected on a subjective basis based on my own familiarity with the sport.

The timeframe for training data was selected as the 2002 through 2015 seasons, with the 2016 season being using for prediction. This is because of the divisonal realignment that took place in 2002, and the resulting 12 team/2 wild card playoff format that has been in effect since.

The target variable was defined as "playoff round", with values from 0 through 5 possible. A 0 would indicate a team missed the playoffs entirely, with each successive round increasing by one with the eventual super bowl champion being a 5. In practice, and in training, this target variable will be a discrete value, however the actual predictive model will output a continuous variable.

-add chart with 0-5 explained-

##Part II - Data Cleaning, Visualization, and Analysis

-include mostly graphs/charts-

After the target data was acquired, it was manipulated and cleaned with the help of the pandas library in python. Working with dataframes proved to be an effective way to organize the relevant information in a meaningful way which simplified the model generation process. Excess and meaningless statistics were stripped away, and the condensed dataframe fed into the inital model included 16 features.

##Part III - Fine Tuning the Model

After the initial linear regression model was generated, the process became an iterative one of marginal improvements. In the end, 16 features were reduced to six which the model showed had the strongest predictive power with respect to the target variable.

-include picture with features here-

An important aspect of refining the model was feature transformation. However, given the time constraints of the project, this unfortunately could not be carried out in its entirety. A box-cox transformation was tested on one feature, and yielded no discernible improvement, so the model was left as it was.

##Part IV - Prediction

-include picture/go back and make better graph of prediction-

While the final model only boasted an adjusted R squared value of slightly over .5, the predictions turned out very well. The model correctly projected 10 of the 12 teams to reach the playoffs in 2016, and also the super bowl champion, the New England Patriots, had the highest projected playoff round of any team.

The discrepancy between the statistical accuracy of the model and the accuracy of the predictions was likely due to the underlying predictive power of the statistics chosen. And though it was quite rudimentary, the model shows lots of potential and I may return to refine it in the future.

##Part V - Conclusion

Project Luther was a great first taste of the big picture of what it means to be a data scientist. From the data acquisition all the way to refining a technical model, I enjoyed the exposure to all aspects of the process. Additionally, it was incredibly fun to apply the skills I have learned in bootcamp to a lifelong passion of mine and obtain meaningful results.
