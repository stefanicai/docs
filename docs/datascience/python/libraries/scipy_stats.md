# scipy.stats
Library used to calculate probabilities

```python
import scipy.stats as stats
```

## Binomial
```python
from scipy.stats import binomial

# probability mass function
binomial.pmf()

# corelated distribution function. Pass a value, returns probability to happen
binomial.cdf()

# percentile point given probability - oposite of cdf, pass a probability, returns value having that probability to happen.
binomial.ppf()
```

## Uniform

```python
from scipy.stats import uniform

# probability mass function - for discrete
uniform.pmf()

# probability density function - for continuous
uniform.pdf(x, loc=1, scale=4) # starts at 1 and has 4 steps, thus 1-5. x is the data

# corelated distribution function. Pass a value, returns probability to happen
binomial.cdf(x=2, loc=1, scale=4) # probability that x is 2, for a uniform distribution from 1-5.

# percentile point given probability - oposite of cdf, pass a probability, returns value having that probability to happen.
binomial.ppf(q=0.2, loc=1, scale=4) # value that has the probability of 20%, for a uniform distr from 1-5
```
