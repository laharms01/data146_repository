# Project 5, Part 2

I first set up my workspace by importing the libraries and functions and creating the commands I will need:
```
import numpy as np
import pandas as pd
import matplotlib
import matplotlib.pyplot as plt

from sklearn.datasets import load_wine as ld
from sklearn.datasets import load_breast_cancer as lbc
from sklearn.datasets import make_blobs as mb
from sklearn.cluster import KMeans
from sklearn.decomposition import PCA
from sklearn.manifold import TSNE
from sklearn.model_selection import KFold
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import StandardScaler as SS
from sklearn.model_selection import train_test_split as tts
from sklearn.neighbors import KNeighborsClassifier as KNN

def GetColors(N, map_name='rainbow'):
    cmap = matplotlib.cm.get_cmap(map_name)
    n = np.linspace(0, N, N) / N
    return cmap(n)


def GetData(scale=False):
    Xtrain, Xtest, ytrain, ytest = tts(X, y, test_size=0.4)
    ss = StandardScaler()
    if scale:
        Xtrain = ss.fit_transform(Xtrain)
        Xtest = ss.transform(Xtest)
    return Xtrain, Xtest, ytrain, ytest


def PlotGroups(points, groups, colors, ec='black', ax='None', alpha=0.5, marker=None, s=None):
    if ax == 'None':
        fig, ax = plt.subplots()
    else:
        fig = plt.gcf()

    for i in np.unique(groups):
        idx = (groups == i)
        ax.scatter(points[idx, 0], points[idx, 1],
                   color=colors[i], edgecolor=ec,
                   label='Group ' + str(i), alpha=alpha, marker=marker, s=s)
    ax.set_xlabel('$x_1$')
    ax.set_ylabel('$x_2$')
    ax.legend(bbox_to_anchor=[1, 0.5], loc='center left')
    return fig, ax


def CompareClasses(actual, predicted, names=None):
    accuracy = sum(actual == predicted) / actual.shape[0]
    classes = pd.DataFrame(columns=['Actual', 'Predicted'])
    classes['Actual'] = actual
    classes['Predicted'] = predicted
    conf_mat = pd.crosstab(classes['Predicted'], classes['Actual'])
    # Relabel the rows/columns if names was provided
    if type(names) != type(None):
        conf_mat.index = y
        conf_mat.index.name = 'Predicted'
        conf_mat.columns = X
        conf_mat.columns.name = 'Actual'
    print('Accuracy = ' + format(accuracy, '.2f'))
    return conf_mat, accuracy
```

Next, before we begin to analyze our data, I had to read the desired file into the workspace:
```
url = "https://raw.githubusercontent.com/tyler-frazier/intro_data_science/main/data/city_persons.csv"
pns = pd.read_csv(url, sep=",")

pns.dropna(inplace=True)

pns['age'] = pns['age'].astype(int)
pns['edu'] = pns['edu'].astype(int)

X = pns.drop(["wealthC"], axis=1)
y = pns.wealthC
```


> Execute a K-nearest neighbors classification method on the data. What model specification returned the most accurate results? Did adding a distance weight help?

> Execute a logistic regression method on the data. How did this model fair in terms of accuracy compared to K-nearest neighbors?

> Next execute a random forest model and produce the results. See the number of estimators (trees) to 100, 500, 1000 and 5000 and determine which specification is most likely to return the best model. Also test the minimum number of samples required to split an internal node with a range of values. Also produce results for your four different estimator values by both comparing both standardized and non-standardized (raw) results.

> Repeat the previous steps after recoding the wealth classes 2 and 3 into a single outcome. Do any of your models improve? Are you able to explain why your results have changed?

> Which of the models produced the best results in predicting wealth of all persons throughout the large West African capital city being described? Support your results with plots, graphs and descriptions of your code and its implementation. You are welcome to incorporate snippets to illustrate an important step, but please do not paste verbose amounts of code within your project report. Avoiding setting a seed essentially guarantees the authenticity of your results. You are welcome to provide a link in your references at the end of your (part 2) Project 5 report.
