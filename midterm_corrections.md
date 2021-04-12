# Midterm Corrections

First consider the data we imported:
```
from sklearn.datasets import fetch_california_housing
data = fetch_california_housing()
X = data.data
X_names = data.feature_names
y = data.target
```
And now our defined DoKFold:
```
def DoKFold(model, X, y, k, standardize=False, random_state=146):
    if standardize:
        from sklearn.preprocessing import StandardScaler as SS
        ss = SS()

    kf = KFold(n_splits=k, shuffle=True, random_state=random_state)
   
    train_scores = []
    test_scores = []

    train_mse = []
    test_mse = []

    for idxTrain, idxTest in kf.split(X):
        Xtrain = X[idxTrain,:]
        Xtest = X[idxTest,:]
        ytrain = y[idxTrain]
        ytest = y[idxTest]

        if standardize:
            Xtrain = ss.fit_transform(Xtrain)
            Xtest = ss.transform(Xtest)

        model.fit(Xtrain, ytrain)

        train_scores.append(model.score(Xtrain, ytrain))
        test_scores.append(model.score(Xtest, ytest))

        ytrain_pred = model.predict(Xtrain)
        ytest_pred = model.predict(Xtest)

        train_mse.append(np.mean((ytrain - ytrain_pred)**2))
        test_mse.append(np.mean((ytest - ytest_pred)**2))
        
    return train_scores, test_scores, train_mse, test_mse
```


## 15
Finding the feature with the strongest correlation to the target is quite simple. We just data into a dataframe and calculate the correlations:
```
data_f = data.frame
data_f.corr()
```
This code will return us a table with the correlation coefficients of each variable. From this table I determined that MedInc was the variable most correlated to our target.

## 16
To determine if standardization will affect our correlations we must first take our data from question 15 and standardize it likewise:
```
ss = StandardScaler()
ss_X = ss.fit_transform(X)

ss_X_df = pd.DataFrame(ss_X, columns= data.feature_names)
ss_Xy_df = st_X_df.copy()
ss_Xy_df['y'] = y
ss_Xy_df.corr()
```
The resulting correlation table indicated that standardization had no affect on correlation values.

## 17

## 18

## 19

## 20

## 21

## 22

## 23

## 24

## 25
