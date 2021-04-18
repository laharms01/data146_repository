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

After running a linear regression on the data I calculated the raw and standardized MSE and R^2 values. The resulting scores are as follows:

Unstandardized MSE: 0.44281008
Standardized MSE:   0.44281333

Unstandardized R^2: 0.735825
Standardized R^2:   0.735833

Next, I compared the coefficients of each of the two models. It seems although standardization only minutely affects the MSE and R^2 values, it does change the coefficients by a large amount.

Unstandardized Coefficients:
```
[ 3.01812923e-02  1.07882853e-02 -5.57603897e-04  8.37880684e-02
  4.04701739e-02  6.37198352e-02 -1.40023112e-01  9.99896825e-02
  1.85515805e-01 -2.49517259e-01 -2.47122665e-01 -7.30324831e-02
  3.09612080e-01 -1.29375995e-01  3.53607318e-01  2.33225714e-01
 -1.34364084e-01 -1.92558301e-01 -1.20146711e-01  3.59279100e-02
  1.46004504e-01 -1.81932414e-01  1.05944573e-01  4.00186663e-01
  1.72822325e-01  2.29943453e-02  1.03043774e-01 -1.15888783e-01
 -2.18966624e-01 -2.90949455e-01 -3.83672661e-01 -3.84737293e-01
  3.07519898e-01  2.55401258e-02  2.56163113e-01  3.95033383e-01
  3.60442298e-01  1.90435535e-01  3.86891012e-01  1.53405264e-01
 -2.09042764e-02  5.43122461e-02 -1.27172669e-01 -5.40268677e-01
 -5.63637093e-01 -1.58355761e-01 -1.08923385e-01 -2.12578757e-02
 -3.26132080e-01  3.26132080e-01 -6.44297719e-02  6.44297719e-02
 -2.76390443e-01  4.32693258e-01  6.03439291e-02  4.07576086e-01
 -6.37787977e-01  1.35651470e-02 -2.47897601e-01  2.47897601e-01]
 ```

Standardized Coefficients:
```
[ 1.12548658e-01  5.24358116e-03 -1.08884589e-02  6.92579735e-02
  7.36951509e+10  8.66257201e+10  7.69209583e+10  7.91372426e+10
  8.45473781e+10  7.89854838e+10  7.88333540e+10  8.76583681e+10
  8.66134726e+10  8.54267349e+10  1.16140874e+11  1.01070442e+11
  7.65053798e+10  7.51091695e+10  8.19133567e+10  4.80000747e+10
  7.26531241e+10  7.87003037e+10 -6.56609287e+09 -6.60161265e+09
 -1.20447035e+10 -1.40140921e+10 -7.23238899e+10 -3.56557715e+10
 -1.50138208e+10 -2.23537221e+10 -6.34833466e+10 -4.69533271e+09
 -7.80211026e+09 -1.23673099e+10 -1.59629508e+10  5.30991560e+10
  2.31813714e+11  8.95044996e+10  4.32553262e+10  1.67206073e+10
  3.49539754e+11  2.11161816e+11  2.27988135e+11  4.41825617e+11
  1.81354767e+10  2.62747629e+10  1.66594092e+11  3.43909538e+10
 -2.42890031e+11 -2.42890031e+11  1.82248582e+10  1.82248582e+10
  1.21238081e+10  5.65381739e+09  1.10197079e+10  2.38345511e+11
  2.39952072e+11  3.49669495e+10 -4.32651302e+10 -4.32651302e+10]
```


> Run a ridge regression and report your best results.

Next I ran a ridge regression on the data, with an alpha range of 74 - 76, and compared the R^2 values to those from the linear regression to determine the relative effectiveness of the ridge regression results.

```
Unstandardized R^2: 0.7349521607
Standardized R^2:   0.7351239419
```

Based on the results, it seems The ridge regression ended up performing well, having R^2 values similar to those from the linear regression. This indicates our ridge regression is about as effective in analyzing our data. Standardizing our data led to a very slight increase in the effectivenss of the model.


> Run a lasso regression and report your best results.

For the lasso regression I used an alpha range of 85 - 95. After runnning through the data, the lasso regression results were as follows:

```
Unstandardized R^2: 0.7344910812
Standardized R^2:   0.7351637846
```

Again, it seems the lasso was around as effective in explaining our data as both the linear and ridge regressions. Standardization seemed to benefit the model very slightly.


> Repeat the previous steps using the variable wealthI as your target.

For this part I ran the data through linear, ridge, and lasso regressions just like I did above. However, this time I changed my target variable from WealthC to WealthI:
```
y = pns.wealthI
```

Linear Regression:

```
Unstandardized MSE: 1750276834.930474
Standardized MSE:   1750174405.288178

Unstandardized R^2: 0.825836
Standardized R^2:   0.825826
```

Although setting WealthI as the target seems to increase the R^2 and thus effectiveness of our model, the values for MSE have shot up to very large numbers indicating that something may be problematic to our analysis.

The correlations also changed by a large amount, similar to the linear model when WealthC was our target.


Ridge Regression:

```
Unstandardized R^2: 0.8248920211
Standardized R^2:   0.8251763126
```

Again, the ridge regression is shown to be quite similar to the linear in terms of R^2 values. Standardized and unstandardized values are also very close.

Lasso Regression:

```
Unstandardized R^2: 0.82518588232
Standardized R^2:   0.82477660702
```

The results followed precedent. All three models share a similar R^2 value when WealthI is the target. Whereas all the models had an R^2 around 0.75 when WealthC was the target, now the value seems to be higher at around 0.825. This would indicate that setting WealthI as the target generates a better model to approximate the data, although the large values of MSE must be considered to fully claim this.




> Which of the models produced the best results in predicting wealth of all persons throughout the smaller West African country being described? Support your results with plots, graphs and descriptions of your code and its implementation. You are welcome to incorporate snippets to illustrate an important step, but please do not paste verbose amounts of code within your project report. Alternatively, you are welcome to provide a link in your references at the end of your (part 1) Project 5 report.


When determining which model produced the best predictive results, we should first eliminate a target that is less effective. Based on what we've seen, across the board, having WealthI as target generates models with larger R^2 values and thus more accurate predictive results. On average, those models with a target of WealthI are about 7.5% more effective than those with a target of WealthC.

As all R^2 values among the remaining three models in consideration are nearly identical, it is hard to precisely decide which model is the best. Based on the data I got during this lab, it seems that the linear model barely beats out the ridge and lasso models as the most effective.















