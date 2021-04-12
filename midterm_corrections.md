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
X_df = data.frame
X_df.corr()
```
This code will return us a table with the correlation coefficients of each variable. From this table I determined that MedInc was the variable most correlated to our target.

## 16
To determine if standardization will affect our correlations we must first take our data from question 15 and standardize it likewise:
```
ss = StandardScaler()
ss_X = ss.fit_transform(X)

ss_X_df = pd.DataFrame(ss_X, columns= data.feature_names)
ss_Xy_df = ss_X_df.copy()
ss_Xy_df['y'] = y
ss_Xy_df.corr()
```
The resulting correlation table indicated that standardization had no affect on correlation values.

## 17
To answer this question, we must perform a regression of just the MedInc variable on our y.
```
np.corrcoef(X_df['MedInc'], y)[0][1]**2, 2
```
This returned a coefficient of determination of ~0.47

## 18
For this question, I ran a linear regression on our data frame to calculate the training and testing scores:
```
k = 20
train_scores, test_scores, train_mse, test_mse = DoKFold(LR(), X, y, k, True)
print(np.mean(train_scores), np.mean(test_scores))
```
The train and test scores resulting from this regression are as follows,

Training: 0.6063
Testing: 0.60198

## 19
Next we ran the same data through a ridge regression:
```
rid_a_range = np.linspace(20, 30, 101)
k = 20

rid_tr = []
rid_te = []
rid_tr_mse = []
rid_te_mse = []

for a in rid_a_range:
    reg_a = Ridge(alpha=a)
    train, test, train_mse, test_mse = DoKFold(reg_a, X, y, k, True, random_state=146)

    rid_tr.append(np.mean(train))
    rid_te.append(np.mean(test))
    rid_tr_mse.append(np.mean(train_mse))
    rid_te_mse.append(np.mean(test_mse))
    
idx = np.argmax(rid_te)

print('Optimal alpha value: ' + format(rid_a_range[idx], '.5f'))
print('Training score for this value: ' + format(rid_tr[idx], '.5f'))
print('Testing score for this value: ' + format(rid_te[idx], '.5f'))
```
Running this code gave us the following scores,

Optimal alpha value: 25.80000
Training score: 0.60627
Testing score: 0.60201

## 20
Next we ran a lasso regression:
```
las_a_range = np.linspace(0.001, 0.003, 101)
k = 20

las_tr = []
las_te = []
las_tr_mse = []
las_te_mse = []

for a in las_a_range:
    reg_a_l = Lasso(alpha=a)
    train, test, train_mse, test_mse = DoKFold(reg_a_l, X, y, 20, True, 146)

    las_tr.append(np.mean(train))
    las_te.append(np.mean(test))
    las_tr_mse.append(np.mean(train_mse))
    las_te_mse.append(np.mean(train_mse))


idx = np.argmax(las_te)
print('Optimal alpha value: ' + format(las_a_range[idx], '.5f'))
print('Training score for this value: ' + format(las_tr[idx], '.5f'))
print('Testing score for this value: ' + format(las_te[idx], '.5f'))
```
Running this code gave the following scores,
Optimal alpha value: 0.00186
Training score: 0.60616
Testing score: 0.60213

## 21
From the correlation table we found in question 15, I determined that the least correlated variable was AveOccup. Next I had to find which regression resulted in the smallest coefficient for this variable.
```
lin = LR(); rid = Ridge(alpha=25.8); las = Lasso(alpha=0.00186)
lin.fit(Xs, y); rid.fit(Xs, y); las.fit(Xs, y);
lin.coef_[5], rid.coef_[5], las.coef_[5]
```
The returned values were:
(-0.039326266978148866, -0.039412573728940366, -0.03761823364553458)

This indicates that lasso regression led to the lowest coefficient for the AveOccup variable.

## 22

## 23

## 24

## 25
