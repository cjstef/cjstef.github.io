### In this post: 
* supervised machine learning classification
* understanding feature types and feature engineering
* metrics for model scoring

For my third project at Metis, dubbed "McNulty", I decided to take a bit of a different approach, as I wanted to focus on expanding my understanding of the various classification algorithms. I selected a clean dataset from the [UCI machine learning repository](http://archive.ics.uci.edu/ml/) composed of economic and demographic information for individuals collected by the US Census in the mid nineties. The target variable was binary, denoted “income class” and defined as being either high income (> $50,000) or low income (<$50,000).

The dataset contained a mixed bag of features, with some quantitative variables (ie age, hours worked per week), but was largely categorical-ordinal (ie-education level) and strictly categorical (ie - marital status, race). <sup>[1]</sup>

The first approach I tried to convert the categorical variables into something useful for classification purposes was to apply the built in [get_dummies](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.get_dummies.html) method in pandas, which involves creating artificial “bit” variables that are all set to 0 except for the one that corresponds to the value the observation takes, which is set to 1.

#### Dummy Variable Example:

![alt text](https://github.com/cjstef/cjstef.github.io/blob/master/images/blog3get_dummies.png?raw=true)

Note that, as is the case in observation 3, if all of the “dummy” variables are set to off, it is assumed to be the base case, typically the most common value of the categorical value set. In this example, this would imply the person’s race is “white”. This is convention to eliminate redundancy in information, since the state of all dummy variables being 0 can be considered a unique state, and thus is chosen to represent the remaining case.

After creating some dummy variables, I also binned the state spaces of certain categorical variables into smaller subsets to reduce the total number of features. For example, the variable **education_status** initially had 16 possible categories, which I reduced to five through binning.

Following these transformations, I had approximately 50 features (x-variables) compared with roughly 40,000 observations. I quickly realized that, while this was an adequete feature/observations ratio, it resulted in lengthy computation times for several of the distance based algorithms. This is due to a phenomenon known as [the curse of dimensionality](https://en.wikipedia.org/wiki/Curse_of_dimensionality) whereby relative distances between points become irrelevant with respect to the average distance as the number of dimensions increases. 

After further reducing the feature space, I had the model simplified to a point where I was ready to begin training and adjusting the parameters. Two things to note here: I applied a train-test split with 10 fold [cross validation](https://en.wikipedia.org/wiki/Cross-validation_(statistics)) to verify the accuracy of my model on a subset of data which was withheld during training. This avoids overfitting to the training data and ensures the model will generalize well to data it has not seen. I also standardized my data with Sklearn’s [preprocessing library](http://scikit-learn.org/stable/modules/preprocessing.html) to ensure features with higher absolute magnitudes did not dominate the model. 

Finally, it was time to test the models. I elected to try five different classifiers: Logistic Regression, Guassian Naive Bayes <sup>[2]</sup>, K-Nearest-Neighbors, LinearSVC, and Random Forest. The resulting Accuracy, Recall, Precision, and F-1 Scores are detailed in the table below, along with the Receiver Operating Characteristic Curves for the applicable classifiers.

![alt text](https://github.com/cjstef/cjstef.github.io/blob/master/images/proj3_model_scores.png?raw=true)

![alt text](https://github.com/cjstef/cjstef.github.io/blob/master/images/roc_curve.png?raw=true)

The random forest classifier performed slightly better than the other four during testing. The resulting confusion matrix for the RF is below. For comparison purposes, the benchmark naive classifier (defined as simply predicting “low income” for every data point) had a roughly 75% accuracy given that approximately 3 out of 4 observations were classified as “low income”. Thus, our model achieves a significant advantage over the baseline, and we can infer that there is a degree of predictive power in our features.

![alt text](https://github.com/cjstef/cjstef.github.io/blob/master/images/conf_matrix.png?raw=true)

Finally, I decided to try the model on a new data point: my own demographic information. Given my current unemployed status (or as we prefer to say here at Metis, ‘fun-employed’), I was pleasntly surprised that the model predicted my income status to be “high income”. A misclassification for sure, given that my current income is exactly $0, but perhaps a promising sign for the future!

![alt text](https://github.com/cjstef/cjstef.github.io/blob/master/images/proj3_connor_model_predict.png?raw=true)

### Summary
Project McNulty proved a great way to get my hands dirty with the various algorithms for classification. It also allowed me to gain a better understanding of the processes of evaluating features for a model and scoring the resulting model effectively.

I hope this post was likewise informative. You can find the jupyter notebook with my code [here](https://github.com/cjstef/MetisProjects/blob/master/Project3/mcnulty.ipynb).

Feel free to contact me with any additional questions or feedback!

#### Notes

<sup>[1]</sup> For more information about variable types, check out this [link](https://statistics.laerd.com/statistical-guides/types-of-variable.php).

<sup>[2]</sup> It is worth noting that while I was not aware of this at the time, Bernouli NB would have been a better choice here, given that the target variable was binary.
