---
title: Insert title here
key: f0d972138e8911bea6c58ca8a219ecae

---
## Correlation

```yaml
type: "TitleSlide"
key: "cfbf90fa31"
```

`@lower_third`

name: Simon Tschöke
title: Data Scientist


`@script`
Hi, welcome back. In this lesson we are going to explore ways to measure the association between variables. Many measures of correlation have been developed, each tailored for a specific type of data or use case. Earlier we have learned what a contingency table is and how it can be used to simplify the analysis of categorical data. These tables come in handy again now for calculating measures of correlation.


---
## Phi Coefficient

```yaml
type: "TwoColumns"
key: "f49ee1a91b"
```

`@part1`
1. using **_Chi2_ statistic**{{1}}

2. directly from frequency counts in a **2x2 contingency table**{{2}}


`@part2`
![2x2contingency](https://assets.datacamp.com/production/repositories/4337/datasets/c6f49e0ac1c5735c4d00d1f4c3c776351c0c7c27/2x2contingency.png){{2}}


`@script`
We can do so by using the Phi coefficient for example. Phi can only be used with two binary variables but it's easy to calculate and is similar in its interpretation to the well-known Pearson's r correlation coefficient.

Phi can be calculated by either using the Chi2 statistic or by using a 2x2 contingency table. We will focus on the second way, since we already know about contingency tables. Chi2 will be introduced in the next chapter.


---
## Phi Coefficient - example

```yaml
type: "TwoRows"
key: "cd989b611a"
center_content: false
```

`@part1`
![Phi method 1](https://assets.datacamp.com/production/repositories/4337/datasets/8fe219badc022004235fab8e2b063f0fabf2dfec/phi1.png){{1}}


`@part2`
```python
import pandas as pd

def phi(ct: pd.DataFrame) -> float:
    assert ct.shape == (3,3)
    import math
    a, b, NA0 = ct.iloc[0,:]
    c, d, NA1 = ct.iloc[1,:]
    NB0, NB1 = ct.iloc[2,:2]
    return (a*d - b*c) / math.sqrt(NA0*NA1*NB0*NB1)
```{{2}}


`@script`
Now, the formula for calculating Phi using a 2x2 contingency table is shown here. Phi is a symmetric measure, meaning that we can reorder the rows and columns and still get the same result, with the exception of the sign.

The code example implements Phi as a function, which takes a 3x3 pandas dataframe representing the 2x2 contingency table with one additional row and column for the marginals. The python code shown here requires python 3.5 onwards as it uses type hints for clarity.
Inside the function we first check that the dataframe has indeed the required 3x3 shape and then proceed to extract the components used in the formula. Python's unpacking feature can help here to write readable code. We use iloc to access every line of the dataframe by index, which return a 1-dimensional pandas series. Conveniently a pandas series can be unpacked straight away. Finally we simply calculate Phi as given by the formula above.


---
## Phi Coefficient - example

```yaml
type: "TwoRows"
key: "871d4a10ff"
```

`@part1`
```python
tab1 = pd.DataFrame(data=[[10, 0, 10], [0, 10, 10], [10, 10, 20]], columns=[0,1,'All'], index=[0,1,'All'])
tab2 = pd.DataFrame(data=[[0, 10, 10], [10, 0, 10], [10, 10, 20]], columns=[0,1,'All'], index=[0,1,'All'])
tab3 = pd.DataFrame(data=[[5, 5, 10], [5, 5, 10], [10, 10, 20]], columns=[0,1,'All'], index=[0,1,'All'])
tab4 = pd.DataFrame(data=[[7, 1, 8], [9, 3, 12], [16, 4, 20]], columns=[0,1,'All'], index=[0,1,'All'])
```{{1}}


`@part2`
```python
phi(tab1)  # 1.0
phi(tab2)  # -1.0
phi(tab3)  # 0.0
phi(tab4)  # 0.15309310892394865
```{{2}}


`@script`
Let's look at some examples. First we create a couple of contingency tables, simply by calling pd.DataFrame and passing 2-dimensional lists to the data argument. The format of the generated dataframes should look familiar, as they resemble the output from pd.crosstab which we explored earlier.

Now it is time to use our function to calculate the Phi coefficient. The first 2 examples illustrate cases for which Phi has its maximum values of +1 and -1 respectively. For the third case 0 is returned, which signifies that no relevant association is present. The last case indicates that there is a slightly positive association between the variables.


---
## Leaving Correlation

```yaml
type: "FinalSlide"
key: "3426ee630f"
```

`@script`
We have seen how to calculate a measure of correlation. There are many more and during your work as analyst or similar role you will have to be conscious about the type of data and select the appropriate measure based on the type of data and question to be answered.

A word of caution here: if we find that variables are associated to one another we cannot automatically conclude, that these variables also have a causal relationship, meaning that a change of one variable doesn't cause another variable to change. In fact, the correlation may just be coincidental. This is known as "correlation is not causation".

On a side note: Phi is also a special case of the Matthews Correlation Coefficient which is used to validate machine learning classifiers. For this we are using a confusion matrix, which is similar to the contingency table. The details are beyond the scope of this course but you can check the implementation in the scikit-learn package sklearn.metrics.

See you in the next lesson.

