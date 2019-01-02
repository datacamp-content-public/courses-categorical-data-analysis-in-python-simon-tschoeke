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
In this lesson we are going to explore ways to measure the association between variables. Many measures of correlation have been developed, each tailored for a specific type of data or use case. Earlier we have learned what a contingency table is and how it can be used to simplify the analysis of categorical data. These tables come in handy again now for calculating measures of correlation. A word of caution here: if we find that variables are associated to one another we cannot automatically conclude, that these variables also have a causal relationship, meaning that a change of one variable doesn't cause another variable to change. In fact, the correlation may just be coincidental. This is known as "correlation is not causation".


---
## Phi Coefficient

```yaml
type: "TwoColumns"
key: "f49ee1a91b"
```

`@part1`
measures correlation between two binary variables

can take one of two possible values

Two ways to calculate _**Phi**_

1. directly from frequency counts in a **2x2 contingency table**

2. using **_Chi2_ statistic**


`@part2`
![2x2contingency](https://assets.datacamp.com/production/repositories/4337/datasets/c6f49e0ac1c5735c4d00d1f4c3c776351c0c7c27/2x2contingency.png)


`@script`
Let's first consider binary variables. Binary variables can take only one of two possible values. For example a person can have a certain disease or not. At the same time this person could have been either exposed to a specific environmental condition or not. For this scenario we would like to know, if having the disease and having been exposed to a specific environment are associated to one another. We can do so by using the Phi coefficient. Phi can only be used with two binary variables but it's easy to calculate and is similar in its interpretation to the well-known Pearson's r correlation coefficient. Note however, that the value of Phi does not simply range from -1 to +1 like Pearson's r. Instead, the range depends on how the data points are distributed over the two variables. Phi ranges from -1 to +1 if each variable has 50% of the data points. Otherwise the value will be less.

Phi can be calculated by either using a 2x2 contingency table or by using the Chi2 statistic. We will focus on the first way, since we already know about contingency tables. Chi2 will be introduced in the next chapter.


---
## Phi Coefficient - example

```yaml
type: "TwoRows"
key: "cd989b611a"
center_content: false
```

`@part1`
![Phi method 1](https://assets.datacamp.com/production/repositories/4337/datasets/8fe219badc022004235fab8e2b063f0fabf2dfec/phi1.png)


`@part2`
```python
import pandas as pd

def phi(ct: pd.DataFrame) -> float:
    assert ct.shape == (3,3)
    import math
    a, b, c, d = [ct.iloc[(i,j)] for i in range(2) for j in range(2)]
    NA0, NA1 = [ct.iloc[(i, 2)] for i in range(2)]
    NB0, NB1 = [ct.iloc[(2, i)] for i in range(2)]
    return (a*d - b*c) / math.sqrt(NA0*NA1*NB0*NB1)
```


`@script`
Now, the formula for calculating Phi using a 2x2 contingency table is show here. It sets the difference of the values found on the diagonals in the table into relation with the marginals. Phi is a symmetric measure, meaning that we can reorder the rows and columns and still get the same result, with the exception of the sign. The analyst has to decide whether reordering columns should be allowed, as the sign may be relevant for the interpretation of the association.

The code example implements Phi as a function, that takes a 3x3 pandas dataframe representing the 2x2 contingency table with one additional row and column for the marginals. The python code shown here requires python 3.5 onwards as it uses type hints for clarity.


---
## Phi Coefficient - example

```yaml
type: "TwoRows"
key: "871d4a10ff"
```

`@part1`
```python
data = read_csv('data.csv')

tab = pd.crosstab(data.A, data.B, marginals=True)

phi(tab)
```


`@part2`



`@script`
In this example we read in a data file and create the contingency table, like we learned in the previous lesson. Finally we call phi.


---
## Leaving Correlation

```yaml
type: "FinalSlide"
key: "3426ee630f"
```

`@script`
We have seen how to calculate a measure of correlation. There are many more and during your work as analyst or similar role you will have to be conscious about the type of data and select the appropriate measure based on the type of data and question to be answered.

On a side note: Phi is also a special case of the Matthews Correlation Coefficient which is used to validate machine learning classifiers. For this we are using a confusion matrix, which is similar to the contingency table. The details are beyond the scope of this course but you can check the implementation in the scikit-learn package sklearn.metrics.

See you in the next lesson.

