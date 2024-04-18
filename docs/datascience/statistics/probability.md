## Cumulative probability
The probability of several scenarios to take place. E.g. What are the chances that at least 8 people have uploaded a video online, out of 100 people, over a range of 20 experiments/trials. See binomial.

```python
import numpy as np
import scipy.stats as stats

# estimate probability of distribution of people who posted a video online. 
n = 15 # number of trials
p = 0.8 # probability of one person to have posted a video online ever
k = np.arrange (0, 11) # 10 people

# calculate the pmf - probability mass function. Use binom package from scipy stats
from scipy.stats import binom

# this returns an array with the probability for each value in the k array. E.g. the first value will be the probability of only one person to have posted a video, after the 15 trials. Last will be the probability of 10 people (all the people) to have posted a video after 15 trials.
binomial = binom.pmf(k=k, n=n, p=p) 

# cumulative probability. What is the change/probability that at least 7 people have ever posted a video online
binom.cdf(k=7, n=n, p=p) # note in this case k is the max (inclusive) number of people.
 ```