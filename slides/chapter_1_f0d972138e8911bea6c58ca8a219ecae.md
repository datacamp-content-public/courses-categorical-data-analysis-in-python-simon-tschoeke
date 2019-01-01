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
In this lesson we are going to explore ways to measure the association between variables. Many measures of correlation have been developed, each tailored for a specific type of data or use case. Earlier we have learned what a contingency table is and how it can be used to simplify the analysis of categorical data. These tables come in handy again now for calculating measures of correlation. A word of caution here: if we find that variables are associated to one another we cannot automatically conclude, that one variable causes the other variable to change. In fact, the correlation may just be coincidental. This is known as "correlation is not causation".


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
![2x2contingency](https://assets.datacamp.com/production/repositories/4337/datasets/4aba9a40e1a6e566ba7da4a4f06b3db124ba9f05/2x2contingency.png)


`@script`
Let's first consider binary variables. Binary variables can take only one of two possible values. For example a person can have a certain disease or not. At the same time this person was either exposed to a specific environmental condition or not. We can check, if these two variables are associated by using the Phi coefficient. Phi can only be used with two binary variables but it's easy to calculate and is similar in its interpretation to the well-known Pearson's r. Note however, that the value of Phi does not simply range from -1 and +1. Instead it depends on how the data points are distributed over the two variables. Phi ranges from -1 to +1 if each variable has 50% of the data points. Otherwise the value will be less.

Phi can be calculated by either using a 2x2 contingency table or by using the Chi2 statistic. We will focus on the first way, since we already know about contingency tables. Chi2 will be introduced in the next chapter.


---
## Phi Coefficient - example

```yaml
type: "TwoRows"
key: "cd989b611a"
```

`@part1`
```python
import pandas as pd

def phi(ct: pd.DataFrame) -> float:
    assert ct.shape == (3,3)
    import math
    a, b, c, d = [ct.iloc[(i,j)] for i in range(2) for j in range(2)]
    NAn, NAp = [ct.iloc[(i, 2)] for i in range(2)]
    NBn, NBp = [ct.iloc[(2, i)] for i in range(2)]
    return (a*d - b*c) / math.sqrt(NAn*NAp*NBn*NBp)
```


`@part2`
```python
data = pd.read_csv('data.csv', sep=';')

tab = pd.crosstab(data.y, data.yhat, margins=True)

phi(tab)
```


`@script`



---
## Leaving Correlation

```yaml
type: "FinalSlide"
key: "3426ee630f"
```

`@script`
We have seen how 

Phi is also known as Matthews Correlation Coefficient and is used to validate machine learning classifiers.

