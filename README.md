## Predicting traffic congestion using environmental crash data

### Background:
Most of us use the mapping software on our phones when we want to avoid traffic. Those softwares determine how to route us using historical traffic data along with real time data from road sensors and phones. The problem with this system is that, by the time sensors and phones in cars start showing traffic slowing enough to reroute other vehicles, a traffic jam has already started.

According to the US DOT, the second leading cause of traffic is crashes, accounting for upwards of 25% of all congestion. A crash during peak driving times can create traffic for hours. I wanted to see if I could make a tool that would use information available at the time of a crash to predict the severity of the traffic impact. 

### Data:
Obtained [here](https://www.kaggle.com/sobhanmoosavi/us-accidents)

Over 3 million records of crashes from across the US between 2016-2020. Variables include time, weather, location, side of the road, and severity(target variable). 

### Modeling:
As might be expected, there was a large class imbalance in my outcome variable, with one value occuring more than 100 times as often as another. To handle this I binarized my target variable and then balanced it using SMOTE. 

I compared 3 models: Gradient Boosting, Random Forest and XGBclassifier. The best results came from the XGBClassifier, although all three were fairly similar. All models performed very well on the training set, with accuracy scores in the high 90s. The test scores were significantly lower, with an average accuracy score of 64. What this shows is not so much overfitting as just different data. Where my training set was synthetically balanced, my test set was not. 

For this particular problem, accuracy was not the metric I was interested in. I was only looking for recall, not necessarily precision, since it is much worse to miss a crash that will cause traffic than it is to mistakenly say a crash will cause traffic when it will not. The recall score for my XGBClassifier model was an 84, which is a significant improvement from a dummy model.

### Continuing Work:
In the interest of dimensionality reduction, I did not include location information in this model. The existing information such as state and county don't have much explanatory power and grossly expand the size of the dataset when turned into dummy variables. Incorporating location specific information such as population or miles of road per capita could be a work around. Another interesting option is creating region based models for areas with similar weather or road conditions.

Although this model could help predict traffic impacts, it is still a reactive measure once a crash has occured. This dataset provides enough time, location and environmental information that it could potentially be used to predict crashes before they happen.
