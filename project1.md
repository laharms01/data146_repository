# Project 1

> Describe what is a package? Also, describe what is a library? What are the two steps you need to execute in order to install a package and then make that library of functions accessible to your workspace and current python work session? Provide examples of how you would execute these two steps using two of the packages we have used in class thus far.

A programming package is a bundle of functions that can be utilized in a certain programming language. Different packages may have bundles of functions that are useful for different purposes. These packages must be installed on your computer to access them. 

In contrast, a library is simply a set of similar functions that are paired togehter and can be used in your program. Libraries are often a collection of packages whose functions serve similar purposes.

The two steps which must be taken in order to access a packages functions are downloading and importing to the workspace. In order to download packages in the software we will be using (PyCharm), first go to preferences. Next, under the project dropdown on the python interpreter page there will be a list of the accessible programming packages. In the bottom left of the page, there is a plus sign that once clicked on, will allow you to search for and download a large number of packages. Finally, once the package is downloaded and visible on the python interpretor page, you may access it in any workspace in the future by typing the import function and then the name of the package. This will grant access to all functions present in the imported package.

Example:
Assume I am attempting to download the pandas and numpy packages, both very useful in the acquisition and visualization of data. In preferences, under the project dropdown, on the python interpretor page, I would first click the plus sign on the bottom left. Next, I type the names of the packages in the search bar I want and download them. Once back in my workspace I would make the first line of my code 'import numpy', for example, to gain access to the numpy functions in my specific workspace. When importing, it may be useful to use an alias to label the package in order to make your coding easier. This can be done likewise: 'import pandas as pd'. By doing this we can call the pandas funtions using pd instead of pandas, which will save us time longterm.


> Describe what is a data frame? Identify a library of functions that is particularly useful for working with data frames. In order to read a file in its remote location within the file system of your operating system, which command would you use? Provide an example of how to read a file and import it into your work session in order to create a new data frame. Also, describe why specifying an argument within a read_() function can be significant. Does data that is saved as a file in a different type of format require a particular argument in order for a data frame to be successfully imported? Also, provide an example that describes a data frame you created. How do you determine how many rows and columns are in a data frame? Is there an alternate terminology for describing rows and columns?

A data frame is a table, made of columns and rows, which represent data values of a certain type. Each column is a separate variable while each row contains a set of values for each column. Data frames allow for the visualization and easy calculation of data sets. 

Pandas is one of the most useful library of functions when working with data frames as it allows us to quickly locate data points or subset our whole data frame.

In order to read a file from the file system into our workspace, we must use the read_csv function in pandas. For example, suppose we have a file we want to read into our workspace, 'exfile.tsv'. To do this, assuming we have imported pandas as pd, we can type pd.read_csv('exfile.tsv'). This goes into pandas and uses the read_csv function to read in the file we typed between the parentheses. Within the read_csv function you must specify at least one argument which is the filename. Without doing this the function does not know which file to read in. By inputting the filename, the function locates this file in your file system and reads it into your workspace. There is a second optional argument that can be used when data is saved in a file under a different format. In order to successfully import data frames from reading in files, the data must be able to be separated and parsed through based on the separation format. Thus a second argument, sep = ' ', can be used to specify the file's data format. If data in a file is separated with tabs use sep = '\t', if separated with spaces use sep = '\s', and so on.

An example of a data frame I created in past exercises is as shown:
  dataf = pd.read_csv(path_to_data, sep='\t')
This creates a data frame, called dataf, by reading in data from the path_to_data file, specifying that data is delimited by tabs.

In order to determine the number of rows and columns in a given data frame, you must use the .shape function. If I were trying to do so with my dataf data frame in the above example I would type print(dataf.shape).

Another way to describe the rows and columns of a data frame is through series. A series is a one-dimensional array that contains any type of data (pretty much the same thing as a column). Data frames are made through the combination of numerous series.


> Import the gapminder.tsv data set and create a new data frame. Interrogate and describe the year variable within the data frame you created. Does this variable exhibit regular intervals? If you were to add new outcomes to the raw data in order to update and make it more current, which years would you add to each subset of observations? Stretch goal: can you identify how many new outcomes in total you would be adding to your data frame?

It seems the year variable within the gapminder.tsv data set exhibits regular intervals of 5 years. The max year in each subset of data observations is 2007. In order to make this data more current I would include the years 2012 and 2017, adhering to the 5 year intervals present in the data before. 

Stretch Goal:
To determine the total amount of new outcomes that will be added, I must first figure out how many countries are present in the data frame. There are a total of 1704 rows. Each country has 12 rows representing every 5 years between 1952 - 2007. 1704 / 12 = 142. So there are 142 countries in our data frame and to make the data current we are adding two new rows (2012, 2017) to each of these. Thus the total number would be 142 * 2 = 284 new outcomes.


> Using the data frame you created by importing the gapminder.tsv data set, determine which country at what point in time had the lowest life expectancy. Conduct a cursory level investigation as to why this was the case and provide a brief explanation in support of your explanation.

The country with the lowest life expectancy in the data was Rwanda in the year 1992 (23.6 years). My theory as to why this is the case was the ethnic conflicts culminating in the Rwandan civil war and genocide which occurred around the same time in the country.


> Using the data frame you created by importing the gapminder.tsv data set, multiply the variable pop by the variable gdpPercap and assign the results to a newly created variable. Then subset and order from highest to lowest the results for Germany, France, Italy and Spain in 2007. Create a table that illustrates your results (you are welcome to either create a table in markdown or plot/save in PyCharm and upload the image). Stretch goal: which of the four European countries exhibited the most significant increase in total gross domestic product during the previous 5-year period (to 2007)?

| Country       | GDP                    |
| ------------- |:-------------:         |
| Germany       | 2,650,870,893,900.9224 |
| France        | 1,861,227,940,621.3972 |
| Italy         | 1,661,264,433,000.4402 |
| Spain         | 1,165,759,889,360.7666 |

Stretch Goal:
Increase in total GDP:
Germany -  177402446825
France  -  127834440236
Italy   -   41156438274.9
Spain   -  168553191330

Germany experienced the most significant increase in total GDP in the 5-year period up to 2007.


> You have been introduced to four logical operators thus far: &, ==, | and ^. Describe each one including its purpose and function. Provide an example of how each might be used in the context of programming.

&

& is a bitwise operator. This means when used to compare two values (x & y), it goes through each bit by bit. If the first bit of both x and y are 1, the corresponding bit in the output will also be 1. If the bit value of x or y is 0 however, even if the other is 1, the output bit will be 0.
The & operator is useful when subsetting a data frame to select data which fulfill multiple parameters. For example, suppose I have a data frame with economic data of countries over time. In order to select only those data points from Africa in the past year I could sebset my data likewise: new_frame = old_frame[old_frame['continent'] == 'Africa'] & old_frame[old_frame['year'] == '2020']

==

Whereas a single = is used to assign values (for example to new variables, pie = 3.14), the == operator is used to check for equality between two values / variables. 
If I were attempting to subset a data frame into a smaller data frame with certain parameters I could use the == operator. Suppose I have a number of data points on precipitation in the williamsburg area for the past 20 years in my data frame. If I was only interested in data for the past year, in order to clean up my table I could select only data points in the year 2020 like this: prec_data_2020 = prec_data[prec_data['year'] == '2020']

|

| is a bitwise operator, and functions similar to the & operator. When used to compare two values (x | y) bit by bit, only one bit has to be 1 for the output to be 1. The output will be 0 only if the corresponding bit in both x and y are 0. 
The | operator is useful when subsetting data frames to select data which fulfill either of a set of parameters. For example, suppose I have a data frame with economic data of countries over time. If I were attempting to select data points that are either from the most recent year or from the year 2000 to compare rates of change over 20 years I could do so likewise: new_frame = old_frame[old_frame['year'] == '2020'] | old_frame[old_frame['year'] == '2000']

^

^ is an exclusive or bitwise operator. This means when used to compare two values (x ^ y) bit by bit, each output bit is set to 1 if and only if one of the two corresponding bit values is 1. If the bit in both x and y is 1, the output is 0.
This operator can be useful when selecting those data points in a set that fulfills only one of a set of parameters. For example, if I had a data set of earthquakes in US states and only wanted those points that affected California and Nevada but not both I could write:
new_frame = old_frame[old_frame['state'] == 'California'] ^ old_frame[old_frame['state'] == 'Nevada']

> Describe the difference between .loc and .iloc. Provide an example of how to extract a series of consecutive observations from a data frame. Stretch goal: provide an example of how to extract all observations from a series of consecutive columns.

.loc and .iloc are two useful tools in the pandas library for the selection of certain data points. When using .iloc, you pass in the integer position of the desired data rows to be selected. For example, if I wanted to select only the 3rd row in my data I would input data_f.iloc[2]. In contrast, when using .loc, you pass in the label of the rows to be selected. If I wanted to select only that same 3rd row in my data I would input data_f.loc['France'], assuming my data points are indexed by country.

In order to extract a series of consecutive observations from a data frame I would use .iloc. Lets say I want the first 10 rows of my data to be selected. I could do so by inputting data_f.iloc[0:10]
This starts selecting row 0 and selects up to just before the last number, 10. This results in rows 0 - 9 being selected, the first 10 in the data frame.

Stretch Goal:
.iloc can also be used to select whole columns of the data frame which may be useful for a number of purposes. If I wanted to select the first two columns of my data frame I would input data_f.iloc[:, 0:2]


> Describe how an api works. Provide an example of how to construct a request to a remote server in order to pull data, write it to a local file and then import it to your current work session.

APIs, or application programming interfaces, are servers that allow for the retrieval of certain data through the input of code requests. It works pretty simply, code is inputted that sends a data retrieval request to the api server. The server then processes this request and outputs the desired data to be used.

In order to utilize api requests in python, we must first download the requests library which grants access to a number of ways to request and access data from apis. Once the requests library is installed you must type 'import requests' in your workspace to be able to utilize this library. When attempting to retrieve data, the get request function is often used. This is a simple function with only one required input, the api URL that the request is being made to. An example of a get request would look like this:
new_data = requests.get(http://api.somethingsomething.org)
Running this line sends a request to the specified api and creates a response variable, in this case named new_data, with the information from the api. With this response variable, you now have access to the desired data in your workspace and can use it for further analysis.

 
> Describe the apply() function from the pandas library. What is its purpose? Using apply) to various class objects is an alternative (potentially preferable approach) to writing what other type of command? Why do you think apply() could be a preferred approach?

The apply() function in pandas is a usefull tool that applies an inputted function onto an entire set of data in a data frame. It then outputs a data frame with the new data points after the inputted function has been applied. For example, if I have a data frame and want to create a new frame with the square root of each data point I can quickly do this by using the apply() function. In this case I would pass the numpy.sqrt function into the apply(). 
data_f.apply(numpy.sqrt)

Using the apply() function is an alternative to writing a loop that iterates over a data frame. The apply() function is often preferable to writing loops as it is a more succinct method of achieving the same end goal. Using apply() takes up a lot less space and makes your code easier to read through.


> Also describe an alternative approach to filtering the number of columns in a data frame. Instead of using .iloc, what other approach might be used to select, filter and assign a subset number of variables to a new data frame?

An alternative to using the .iloc function to select a series of columns from a data frame is selecting based on column labels. For example, suppose I have 5 columns in my data frame but am only interested in the 'Date' and 'Location' columns. To select these I can simply write data_frame['Date', 'Location'] and assign this to a new object. The resulting data frame will only comprise these two specified columns. 



