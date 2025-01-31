[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

```python
from __future__ import print_function, division

import numpy as np

import nsfg

preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d

print(CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb))
print(CohenEffectSize(firsts.prglngth, others.prglngth))
```

Cohen's D between firsts' and others' total weight(lb) is -0.089 while the D for their pregnancy length is 0.029.  This means that first babies are lighter than others by a larger margin than the difference in pregnancy lengths.
