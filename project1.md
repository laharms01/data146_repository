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
To determine the total amount of new outcomes that will be added, I must first figure out how many countries are present in the data frame. There are a total of 1704 rows. Each country has 12 rows representing every 5 years between 1952 - 2007. 1704 / 12 = 142. So there are 142 countries in our data frame and to make the data current we are adding two new rows (2012, 2017) to each of these. Thus the total number would be 142 * 2 = 284.
