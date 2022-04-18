import numpy as np
import pandas as pd
import scipy.stats as stats
import statsmodels.stats.api as sms
import matplotlib as mpl
import matplotlib.pyplot as plt

#The aproximate probability distribution between the test group and the control group
testsample = pd.read_csv('testSamples.csv')

testsample.info()

test = testsample.groupby('test_group').count()
test.columns = ['count']
display(test)

test.hist(column='count', by='test_group')

contral_rate = 44886 / 59721
test_rate = 14835 / 59721
print(contral_rate)
print(test_rate)


df = pd.read_csv('transdata.csv')

df.info()

join = pd.merge(df, testsample, on='sample_id')
print(join)

#Is a user that must call-in to cancel more likely to generate at least 1 addition REBILL?
#No, web from to cancel more likely to generate more REBILLS
rebill = join.groupby(['test_group','transaction_type']).count()
display(rebill)

#Is a user that must call-in to cancel more likely to generate more revenues? 
#Yes, Test group generate more revenues
revenues = join.groupby('test_group')['transaction_amount'].sum()
display(revenues)

#Is a user that must call-in more likely to produce a higher chargeback rate(CHARGEBACKs/REBILLs)?
#No, web form more likely to produce a higher chargeback rate

chargeback_rate_0 = 106 / 3756 #Use the number from the calculation above to find the rate
chargeback_rate_1 = 57 / 3205
print(chargeback_rate_0)
print(chargeback_rate_1)


```python

```
