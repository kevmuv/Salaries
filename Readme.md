# Salaries By Region
## Visualization By Kevin Muvunyi

I used a dataset from Kaggle entitled "salaries by region". This dataset is comprised of a list of American Universities 
which are categorized by region, as well as a list of salaries from graduating students on a period of ten years from their graduation date.
As part of this project, I used a bar graph and pie chart to illustrate both the average starting median salary and the overall average 
salaries by region. 

## Getting Started

First we import pandas,numpy and matplot lib in order to read in the csv file, but also perform different visualizations:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
```
The we proceed to read in the csv file.

```
#The function pd.read_csv reads in the csv file, which was saved on the computer as "Salariesandregion.csv".
#We save the csv file in the variable salaries
#We use the function dropna, in order to drop all the NA values
salaries=pd.read_csv("Salariesandregion.csv")
salaries.head()
salaries.dropna()
```
![GitHub Logo](/png0.PNG)

Then we use the function dtypes to establish the data types of our values.

```
#Since the values are floats it is easier to visualize
salaries.dtypes
School Name                           object
Region                                object
Starting Median Salary               float64
Mid-Career Median Salary             float64
Mid-Career 10th Percentile Salary    float64
Mid-Career 25th Percentile Salary    float64
Mid-Career 75th Percentile Salary    float64
Mid-Career 90th Percentile Salary    float64
dtype: object
```
Then we use the describe function to do a quick analysis of the data. In this particular instance we 
analyze the 'Mid-Career Median Salary' column.

```
salaries['Mid-Career Median Salary'].describe()
count       320.000000
mean      83934.375000
std       15191.443091
min       43900.000000
25%       73725.000000
50%       82700.000000
75%       93250.000000
max      134000.000000
Name: Mid-Career Median Salary, dtype: float64
```

Moving on we create a small table as we seek to examine the relationship between region & Starting Median Salary.

```
schools = salaries[['School Name','Region','Starting Median Salary'
]]
schools.head()
```
![GitHub Logo](/png5.PNG)

We then call the function mean in order to get the regional averages we want for the 'Starting Median Salary' column.

```
Salaryreg = salbyregion.mean()
Salaryreg

Starting Median Salary
Region

California
51032.142857
Midwestern
44225.352113
Northeastern
48496.000000
Southern
44521.518987
Western
44414.285714
```
## Plotting

Now we can plot a bar graph using the code below.

```
#We call in the function plot to visualize our averages
#We set kind to "bar", because we want a bar graph
my_plot = Salaryreg.plot(kind='bar')
```
![GitHub Logo](/png1.PNG)

To make a more comprehensive graph we add new lines of code.

```
#In order to make the chart more insightful we can add other things
#For example we can remove the legend by setting it to none
#We can give a title to the graph by using "title="
#We can also label the two axis by using .set_xlable & .set_ylabel
my_plot = Salaryreg.plot(kind='bar',legend=None,title="Average Starting Salary By Region")
my_plot.set_xlabel("Region")
my_plot.set_ylabel("Salaries ($)")
```
![GitHub Logo](/png2.PNG)

Now let us look at the overall average salaries for the 10 year period by region.

```
#Now let us get the overall salaries for the five regions
#Therefore, we create new variable Unis
#We still group by region
Unis = salaries[['Region','Starting Median Salary','Mid-Career Median Salary','Mid-Career 10th Percentile Salary',
                 'Mid-Career 25th Percentile Salary', 'Mid-Career 75th Percentile Salary','Mid-Career 90th Percentile Salary']]
Salbyregion = Unis.groupby('Region')
#We repeat the same process as the previous graph
salaryreg = Salbyregion.mean()
my_plot = salaryreg.plot(kind='bar',title="Overall Average Salary By Region")
my_plot.set_xlabel("Region")
my_plot.set_ylabel("Salaries ($)")
```

![GitHub Logo](/png3.PNG)

Finally we create a pie chart representing the average Starting Median Salary by region.

```
#To create the pie chart it is important to note that we assigned sizes based on the first bar graph
#Sizes represent avg Starting Median Salary by region
#For the labels we use the regions


labels = ['California', 'Midwestern', 'Northeastern', 'Southern','Western']
sizes = [51032.1, 44225.4, 48496.0, 44521.5,44414.3]
colors = ['maroon','green', 'red', 'blue', 'orange','purple']
patches, texts = plt.pie(sizes, colors=colors, shadow=True, startangle=90)
plt.legend(patches, labels, loc="best")
plt.axis('equal')
plt.tight_layout()
plt.show()
```
![GitHub Logo](/png4.PNG)






