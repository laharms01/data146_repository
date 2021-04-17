# Project 5, Part 1

> Download the anonymized dataset describing persons.csv from a West African county and import it into your PyCharm project workspace. First set the variable wealthC as your target. It is not necessary to set a seed.

I first imported the required libraries and set up my DoKFold function, then I read in the persons.csv file and set up my targets and features:

```
pns = pd.read_csv('persons.csv')

check_nan = pns['age'].isnull().values.any()
pns.dropna(inplace=True)

pns['age'] = pns['age'].astype(int)
pns['edu'] = pns['edu'].astype(int)

X = pns.drop(["wealthC", "wealthI"], axis=1)
y = pns.wealthC
```

> Perform a linear regression and compute the MSE. Standardize the features and again computer the MSE. Compare the coefficients from each of the two models and describe how they have changed.


