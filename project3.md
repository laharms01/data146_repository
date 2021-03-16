> Download the dataset charleston_ask.csv and import it into your PyCharm project workspace. Specify and train a model the designates the asking price as your target variable and beds, baths and area (in square feet) as your features. Train and test your target and features using a linear regression model. Describe how your model performed. What were the training and testing scores you produced? How many folds did you assign when partitioning your training and testing data? Interpret and assess your output.

For this first question, in order to create a linear regression of our data and train / test it we will want to setup our workspace like this:
```
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import KFold
import numpy as np
import pandas as pd
```

Next, we will use pandas to read in the csv that contains our desired data, designate our Y (target) and X (features) variables, and define our linear regression:
```
data = pd.read_csv('charleston_ask.csv')

X = data[['beds', 'baths', 'sqft']]
Y = data['prices']

lin_reg = LinearRegression()
```

Now that we have our model, we should perform K-Fold cross validation to start the process of ascertaining the train and test scores of the data. In order to determine these scores, the dataset is split into a number of folds (specified by n_splits) and subsequently tested. We can define our K-Folds like this:
```
kf = KFold(n_splits=10, shuffle=True)
```
I personally chose to have 10 folds in the cross validation. This is because, in general, the higher the amount of folds, the more accurate our resulting train and test scores will be.

We can find the train and test scores like this:
```
train_scores = []
test_scores = []

for idxTrain, idxTest in kf.split(X):
    Xtrain = X.iloc[idxTrain, :]
    Xtest = X.iloc[idxTest, :]
    ytrain = Y.iloc[idxTrain]
    ytest = Y.iloc[idxTest]

    lin_reg.fit(Xtrain, ytrain)

    train_scores.append(lin_reg.score(Xtrain, ytrain))
    test_scores.append(lin_reg.score(Xtest, ytest))

print('Training: ' + format(np.mean(train_scores), '.3f'))
print('Testing: ' + format(np.mean(test_scores), '.3f'))
```

By running this code, the resulting values were output:
```
Training: 0.019
Testing: -0.004
```

These values tell us quite a lot about the shape of our regression and the strength of the relationship between our variables. The higher the score is, the better our model is at explaining the variance we see in our data, with a score of 1 indicating perfect explanatory power.

Unfortunately, it seems that our model is not super useful in explaining all the variation present. Our training score is positive but very low, and thus not very useful. The testing score actually turned out to be slightly negative, which is even worse. This is an indication that our current features (beds, baths, sqft) are not very useful in determining the price of a given house. In order to better adpat our model to the dataset, there are a few extra steps that should be taken.


> Now standardize your features (again beds, baths and area) prior to training and testing with a linear regression model (also again with asking price as your target). Now how did your model perform? What were the training and testing scores you produced? How many folds did you assign when partitioning your training and testing data? Interpret and assess your output.

In order to better optimize our model to interpret the data, it will be useful to standardize our features. This can be achieved by importing the standard scaler from sklearn like this:
```
from sklearn.preprocessing import StandardScaler as SS
```

With this new  function, we can run our train / test score code again with the addition of a few new lines of code which standardize our data:
```
train_scores = []
test_scores = []

for idxTrain, idxTest in kf.split(X):
    Xtrain = X.iloc[idxTrain, :]
    Xtest = X.iloc[idxTest, :]
    ytrain = Y.iloc[idxTrain]
    ytest = Y.iloc[idxTest]
    
    ss = SS()
    Xtrain = SS.fit_transform(Xtrain)
    Xtest = SS.transform(Xtest)

    lin_reg.fit(Xtrain, ytrain)

    train_scores.append(lin_reg.score(Xtrain, ytrain))
    test_scores.append(lin_reg.score(Xtest, ytest))

print('Training: ' + format(np.mean(train_scores), '.3f'))
print('Testing: ' + format(np.mean(test_scores), '.3f'))
```

Note that, like the last question, the amount of folds used in this code is still 10.
The resulting outputs are:
```
Training: 0.020
Testing: -0.000
```

Hmm... it seems that standardizing our data has improved the efficacy of our model, but no where near the extent we would like. The training score is still very low and the testing score is now just zero. Thus, even after standardizing our features, they are still not good determinants of the price of a given house.


> Then train your dataset with the asking price as your target using a ridge regression model. Now how did your model perform? What were the training and testing scores you produced? Did you standardize the data? Interpret and assess your output.

Our next step in trying to improve our model will be to try ridge regression instead of linear regression. We can do this by first importing the ridge function into our code:
```
from sklearn.linear_model import Ridge
```

All we need to find now is the optimal alpha value to run our ridge regression, which was determined to be 100 (from a range of 0 to 100). With this value, we can run our ridge model:
```
rid_reg = Ridge(alpha=100)

train_scores = []
test_scores = []

for idxTrain, idxTest in kf.split(X):
  Xtrain = X.iloc[idxTrain, :]
  Xtest = X.iloc[idxTest, :]
  ytrain = Y.iloc[idxTrain]
  ytest = Y.iloc[idxTest]

  ss = SS()
  Xtrain = ss.fit_transform(Xtrain)
  Xtest = ss.transform(Xtest)

  rid_reg.fit(Xtrain, ytrain)

  train_scores.append(rid_reg.score(Xtrain, ytrain))
  test_scores.append(rid_reg.score(Xtest, ytest))

print('Training: ' + format(np.mean(train_scores), '.3f'))
print('Testing: ' + format(np.mean(test_scores), '.3f'))
```
Note that the amount of folds used in this code is still 10 and our data is still standardized.
The resulting outputs are:
```
Training: 0.019
Testing: 0.012
```

There is some significant (at least compared to the last few questions) change in the testing score, which is now a positive number. However, the training score has remained pretty much unchanged and both testing and training are still very low values. So even with ridge regression our model is not as efficient as we would like.


> Next, go back, train and test each of the three previous model types/specifications, but this time use the dataset charleston_act.csv (actual sale prices). How did each of these three models perform after using the dataset that replaced asking price with the actual sale price? What were the training and testing scores you produced? Interpret and assess your output.

Let's first read in our new csv:
```
data = pd.read_csv('charleston_act.csv')
```

All models still use 10 folds.

### Training and Testing Scores:

Unstandardized Linear Model:
```
Training: 0.006
Testing: -0.028
```

Standardized Linear Model:
```
Training: 0.004
Testing: -0.012
```

Standardized Ridge Model:
```
Training: 0.004
Testing: -0.008
```

It seems, even when using the actual price data, our models are still not very efficient. In fact, from the tests I ran, this dataset seemed to prodce models that were slightly less useful in explaining our data. We can conclude that even when considering actual price, our current features are insufficient in determining the price of a given house.


> Go back and also add the variables that indicate the zip code where each individual home is located within Charleston County, South Carolina. Train and test each of the three previous model types/specifications. What was the predictive power of each model? Interpret and assess your output.

After inclding the remaining zipcode columns in our features list, I ran the three models again and got the following scores:

Unstandardized Linear Model:
```
Training: 0.339
Testing: 0.236
```

Standardized Linear Model:
```
Training: 0.346
Testing: -304448750933676656689152.000
```

Standardized Ridge Model:
```
Training: 0.342
Testing: 0.270
```

With the addition of zip codes in our features list, the efficiency of our models improved by a very large amount when compared to past changes. This is an indication that zip codes are very pertinent values to consider when determining the price of a given house and are much more useful as features than beds, baths, and sqft. The unstandardized linear and standardized ridge models both improved significantly by adding the zip codes. The training score for the standardized linear model also improved. However, the testing score of this model is now a very (very) large negative number, which could be due to a number of reasons. I would imagine it has something to do with the binary nature of the zip code data and the process of standardizing it.

> Finally, consider the model that produced the best results. Would you estimate this model as being overfit or underfit? If you were working for Zillow as their chief data scientist, what action would you recommend in order to improve the predictive power of the model that produced your best results from the approximately 700 observations (716 asking / 660 actual)?

The model which produced the best predictive results is our standardized ridge model. From the testing and training scores we can estimate that the model is a little overfit, because training score is higher than testing score. 
Our next step to improve this model would be to find more pertinent variables that we can include in our regression. While zipcodes were found to be great predictors of our target (price), there is still a lot of room for our model to improve in explanatory power. Right now our model only explains ~30% of the variation in our data. These additional variables could include local geographic factors, more information about the house such as age or ..., or dynamic space variables like distance from certain desirable locations (grocery store, downtown, etc.).





