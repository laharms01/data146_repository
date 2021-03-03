# Project 2

> Describe continuous, ordinal and nominal data. Provide examples of each. Describe a model of your own construction that incorporates variables of each type of data. You are perfectly welcome to describe your model using english rather than mathematical notation if you prefer. Include hypothetical variables that represent your features and target.

Continuous data is numerical data that can hold the value of any decimal number. For example, average temperatures in a given area are continuous data points because they can take any decimal value.
Ordinal data is a categorical data type in which data points take on the values of ordered categories. An example of ordinal data could be a survey question to citizens of a given city asking them to rank overall city sanitation on a scale from 1 - 5. Because these results are distinctly ordered, with 1 being the worst and 5 the best, this represents an ordinal data type.
Nominal data is also categorical like ordinal data, however it is not ordered in any meaningfull way. An example of this could be hair color or home nation. While these data points will fall into certain categories (brown hair, USA, etc.), the order of these categories has no meaning in the analysis of this data.

Suppose we are constructing a model in an attempt to predict a countries GDP based on a number of variables of each type. It might look like this:
Y = X0 + X1 + X2 + X3 + X4
Where Y represents our target, GDP, and X1, X2, X3, and X4 represent our features. In this case X1 is a continuous variable, life expectancy. X2 and X3 are ordinal variables represented on a scale of 1 - 10, economic development and living standards respectively. X4 is a nominal variable, continent. Of course, X0 is the intercept of our regression line.
