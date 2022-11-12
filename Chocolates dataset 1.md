
# Chocolate Data Analysis

Using Numpy, Pandas, and Seaborn

In this article series, we perform beginner-friendly data manipulation, data calculation, and visualization on a given dataset.

Data analysis on the chocolate dataset is 3 parts tutorial to keep it on point and short, here is the first part.

# Introduction

Chocolate is considered to be one of the most popular candies in the world.

> _As of 2022, the global chocolate industry is worth $127.9 billion USD_

When we look at chocolate consumption by country, gender, and even time of year, the amount of data to wade through can be overwhelming.

We read fun facts regarding chocolate such as,

> _Switzerland is the biggest consumer of chocolate in the world,_ as stated in the [global chocolate consumption](https://damecacao.com/chocolate-statistics/) report.
> 
> Halloween is the most popular time of year to buy chocolate, shown in the [Halloween time state](https://damecacao.com/chocolate-statistics/#Halloween_Time).
> 
> _The average cost of a chocolate bar in 2022 is up 8%, mentioned in_ [_chocolate stats_](https://damecacao.com/chocolate-statistics/#4)_._

Assuming we have the dataset, how to reach these conclusions? in other words, how to derive meaning from the raw data.

We work on the dataset that contains expert ratings of over 1,795 individual chocolate bars, along with information on their regional origin, percentage of cocoa, the variety of chocolate beans used, and where the beans were grown. This dataset can be accessed from this [GitHub repo](https://github.com/hardbucket/Datasets_repository/blob/main/chocolate.csv).

![](https://miro.medium.com/max/875/1*DI3KKOygiIpS5226aBQwuw.png)

delicious chocolates

So let’s start working on the dataset:

# Import Libraries

```
import numpy as np  
import pandas as pd
```

# Read File

We use `read_csv(‘path_to_file’)` to read `.csv` files. In a simple explanation, we store data in a column and comma-separated values called CSV.  
There are other types like `.tsv` which you guessed it is tab-separated values and can be read by `read_csv` as well as given the parameter of `sep` `read_csv(‘path_to_file’, sep=’\t’)`

```
df = pd.read_csv('chocolate.csv')   
df.head()
```
# Data Preparation

First, we get to know our dataset.  
* The number of rows and columns is called the number of observations and features, respectively.  
* The names of columns by `df.columns`.

```
s = df.shape  
cols = df.columns  
print(s)  
print(cols)
```

Ok, now we can see, our columns are separated with`\n` , that is used to make the new line. we don’t need the column in the same format therefore, we modify them by the cell below.

```
df.columns = [c.replace("\n", " ") for c in cols]  
df.columns
```

In the below cell, we have a look at the column’s type.

```
df.info()
```

It shows that the columns are consistent with the string types and are cast as objects, it is better to convert them to string for better calculations and manipulations.  
note: this dataset is meant to have no nan values, so the explanation and data preparation is more straightforward however, it’s rare to find a dataset without nan values, and dealing with nan values is one significant part of data preparation.

```
df = df.convert_dtypes()  
df.info()
```

The next problem we face is the `Cocoa Percent` column. The data in this column is the number that we want as a percentage of cocoa. First, we need to remove the percentage sign and cast the column’s type from `string` to `float`, to perform calculations on the column easier.

```
df['Cocoa Percent'] = df['Cocoa Percent'].str.replace("%", "")  
df[["Cocoa Percent"]] = df[["Cocoa Percent"]].astype("float")
```

We check our dataset.

```
df.info()
```

Ok, now we have our preferred dataset.

Since on the doorstep the data visualization can reveal some significance from our data, we are inclined to perform the histogram plot with the help of seaborn.

```
import seaborn as sns  
sns.displot(df, x = 'Cocoa Percent', bins = 30)
```

![](https://miro.medium.com/max/440/1*JAQ03U9XaaqDdPdTUYcqkw.png)

Histogram of Dataset

The histogram shows that most chocolate bars contain 70% cocoa, which might be hard to see from tabular data.

We are off to a good start. Now, we can save our data`.csv` as `chocolate_preprocessed.csv` and leave out the index by setting the `index=False`.

```
df.to_csv("./chocolate_preprocessed.csv", index=False)
```

After you are done with part one, you can go to part two and perform calculations on prices, plot prices to understand the elements that price is depending on, and so on.