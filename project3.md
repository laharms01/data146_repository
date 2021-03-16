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

These values tell us quite a lot about the shape of our regression and the strength of the relationship between our variables. The higher the score is, the better our model is at explaining the variance we see in our data.

Unfortunately, it seems that our model is not super useful in explaining all the variation present. Our training score is positive but very low, and thus not very useful. The testing score actually turned out to be slightly negative, which is even worse. In order to better adpat our model to the dataset, there are a few extra steps that should be taken.


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

Hmm... it seems that standardizing our data has improved the efficacy of our model, but no where near the extent we would like. The training score is still very low and the testing score is now just zero.


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
Note that the amount of folds used in this code is still 10 and our data is still standardized in our code.
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


















