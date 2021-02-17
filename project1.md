Project 1

Describe what is a package? Also, describe what is a library? What are the two steps you need to execute in order to install a package and then make that library of functions accessible to your workspace and current python work session? Provide examples of how you would execute these two steps using two of the packages we have used in class thus far.

A programming package is a bundle of functions that can be utilized in a certain programming language. Different packages may have bundles of functions that are useful for different purposes. These packages must be installed on your computer to access them. 

In contrast, a library is simply a set of similar functions that are paired togehter and can be used in your program. Libraries are often a collection of packages whose functions serve similar purposes.

The two steps which must be taken in order to access a packages functions are downloading and importing to the workspace. In order to download packages in the software we will be using (PyCharm), first go to preferences. Next, under the project dropdown on the python interpreter page there will be a list of the accessible programming packages. In the bottom left of the page, there is a plus sign that once clicked on, will allow you to search for and download a large number of packages. Finally, once the package is downloaded and visible on the python interpretor page, you may access it in any workspace in the future by typing the import function and then the name of the package. This will grant access to all functions present in the imported package.

Example:
Assume I am attempting to download the pandas and numpy packages, both very useful in the acquisition and visualization of data. In preferences, under the project dropdown, on the python interpretor page, I would first click the plus sign on the bottom left. Next, I type the names of the packages in the search bar I want and download them. Once back in my workspace I would make the first line of my code 'import numpy', for example, to gain access to the numpy functions in my specific workspace. When importing, it may be useful to use an alias to label the package in order to make your coding easier. This can be done likewise: 'import pandas as pd'. By doing this we can call the pandas funtions using pd instead of pandas, which will save us time longterm.
