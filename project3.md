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
