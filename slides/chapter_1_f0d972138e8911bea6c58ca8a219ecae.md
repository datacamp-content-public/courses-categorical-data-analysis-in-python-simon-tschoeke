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
In this lesson we are going to explore ways to measure, if categorical variables are correlated. Many measures of correlation have been developed, each tailored for a specific type of data or use case. Earlier we have learned what a contingency table is and how it can be used to simplify the analysis of categorical data. we will use these tables here again to measure if categorical variables are associated to one another. A word of caution here: if we find that variables are associated to one another we cannot automatically conclude, that one variable causes the other variable to change. In fact the correlation may just be coincidental. This is known as "correlation is not causation".


---
## Binary Variables

```yaml
type: "TwoColumns"
key: "f49ee1a91b"
```

`@part1`
- can take one of two possible values
- represented as 2x2 contingency table


`@part2`
![](image-url)


`@script`
Let's first consider binary variables. Binary variables can take only one of two possible values. For example a person can have a certain disease or not. At the same time this person was either exposed to an environmental condition or not. We will be using a 2x2 contingency table to represent categorical, binary variables.


---
## Phi Coefficient

```yaml
type: "FullCodeSlide"
key: "590e98b9ad"
```

`@part1`
```python
import pandas as pd
import numpy as np
```


`@script`
One common measure in this context is the **Phi** statistic.


---
## Final Slide

```yaml
type: "FinalSlide"
key: "3426ee630f"
```

`@script`


