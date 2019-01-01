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
In previous sessions we have learned what a contingency table is and how to use it for measuring agreement. In this lesson we are going to explore ways to measure, if categorical variables are correlated. In other words we would like to know, if the variables are associated in any way.


---
## Binary Variables

```yaml
type: "FullSlide"
key: "86af209bed"
```

`@part1`



`@script`
Let's first consider binary variables. Binary variables can take only one of two possible values. For example a person can have a certain disease or not. At the same time this person was either exposed to an environmental condition or not. Here we are interested in analyzing whether the two binary variables are associated to each other in any way.


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


