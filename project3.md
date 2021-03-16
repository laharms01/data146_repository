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
