# Week 15, Lecture 02 CodeAlong: Hypothesis Testing

- xx/xx/xx

Today, we will be analyzing data from the Crowdfunding website Kiva and answering several questions about the data.

- Use your hypothesis testing skills and the  ["Guide: Choosing the Right Hypothesis Test"](https://login.codingdojo.com/m/376/12533/88117) lesson from the LP.
    

- Kiva Crowdfunding Data Set:
    -  https://www.kaggle.com/datasets/kiva/data-science-for-good-kiva-crowdfunding 



### Questions to Answer

- Q1: Do all-male teams get more funding vs teams that include at least 1 female?
- Q2: Do different sectors get more/less funding?

# Hypothesis Testing


```python
import json
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns

from scipy import stats
import scipy
scipy.__version__
```


```python
## load the kiva_loans.csv. display info and head
df = pd.read_csv('Data/kiva_loans.csv')
df.info()
df.head()
```


```python
## Drop null values from related columns
df = df.dropna(subset=['borrower_genders','funded_amount'])

# Setting the id as the index
df = df.set_index('id')
df.info()
df.head()
```

# Q1:  Do all-male teams get more funding vs teams that include at least 1 female?

## 1. State the Hypothesis & Null Hypothesis 

- $H_0$ (Null Hypothesis):
- $H_A$ (Alternative Hypothesis):  

## 2. Determine the correct test to perform.
- Type of Data?
- How many groups/samples?
- Therefore, which test is appropriate?

### Visualize and separate data for hypothesis

- What column is our target?
- What column determines our groups?


```python
## check the col that contains the measurement

```


```python
## check the col that contains info on gender

```


```python
## create a column that easily separates our groups

```


```python
## save list of columns needed for each group
needed_cols = None
```


```python
## save male team in separate variable
male_df = None
male_df
```


```python
## save female team in separate variables
female_df = None
female_df
```


```python
## Make a df just for visualization by concat the groups 
plot_df =  None
plot_df
```


```python
## visualize the group means

```

## 3. Testing Assumptions

- No significant outliers
- Normality
- Equal Variance

### Checking Assumption of No Sig. Outliers


```python
## Saving JUST the numeric col as final group variables
male_group = None
female_group = None

```


```python
## Check female group for outliers
female_outliers = None

## how many outliers?

```


```python
## remove outliers from female_group

```


```python
## Check male group for outliers
male_outliers = None

## how many outliers?

```


```python
## remove outliers from male_group

```

### Test for Normality


```python
## Check female group for normality

```


```python
## Check n for female group

```


```python
## Check male group for normality

```


```python
## Check n for male group

```

- Did we meet the assumption?

### Test for Equal Variances


```python
## Use Levene's test for equal variance

```


```python
## Use an if-else to help interpret the p-value

```

- Did we meet the assumptions?

## Final Hypothesis Test

- Did we meet our test's assumptions? 
    - If not, what is the alternative test?


```python
## run final hypothess test

```


```python
## make a plot or calcualte group means to know which group had more/less.

```

- Final Conclusion:
    - ...

# Q2: Do different sectors get more/less funding?

## 1. State the Hypothesis & Null Hypothesis 

- $H_0$ (Null Hypothesis): 
- $H_A$ (Alternative Hypothesis):  

## 2. Determine the correct test to perform.

- Type of Data?
- How many groups/samples?
- Therefore, which test is appropriate?


```python
## how many sectors?

```

### Visualize and separate data for hypothesis

- What column is our target?
- What column determines our groups?


```python
## barplot

```


```python
## Create a dictionary with each group as key and funded_amount as values

```


```python
## check one of the sectors in the dict

```

## 3. Testing Assumptions

- No significant outliers
- Normality
- Equal Variance

### Checking Assumption of No Sig. Outliers


```python
## Loop through groups dict

    ## determine if there are any outliers
    
    ## print a statement about how many outliers for which group name

    ## Remove the outiers from data and overwrite the sector data in the dict

```

### Test for Normality


```python
## Running normal test on each group and confirming there are >20 in each group

## Save a list with an inner list of column names
norm_results = [['group','n','pval','sig?']]


## loop through group dict

    ## calculate normaltest results
    
    
    ## Append the right info into norm_resutls (as a list)
    
    
    
## Make norm_results a dataframe (first row is columns, everything else data)

```

- Did we meet the assumption?

### Test for Equal Variances


```python
## DEMO: using the * operator to unpack lists
a_list = ['a','b','c']
b_list = [1,2,3]
new_list= [*a_list, *b_list]
new_list
```


```python
## Use Levene's test for equal variance

```


```python
## Use an if-else to help interpret the p-value

```

- Did we meet the assumption?


## Final Hypothesis Test

- Did we meet our test's assumptions? 
    - If not, what is the alternative test?


```python
## Run final test and get p-value

```

- Interpret Results. Did we have a significant result?
- Is a post-hoc test needed?

### Post-Hoc Multiple Comparison Test


```python
## Post Hoc
from statsmodels.stats.multicomp import pairwise_tukeyhsd
```

- Tukey's test requires a list of group names and a list of measured values. 
- Easiest way to produce and visualize this is to make our groups dict into a dataframe 

#### Testing Converting our Dictionary to a DataFrame


```python
## slice a test sector
temp = None

```


```python
## test making a dataframe from the test sector and filling in the sector name

```

#### Preparing the new dataframe for Tukey's test in a looop


```python
## make a list for saving the dataframes to


## Loop through groups dict's items


    ## make a temp_df with the data and the sector name
    
    ## append to tukeys_dfs
    
## concatenate them into 1 dataframe    

```


```python
## save the values as kg_lost and the labels to the Diet
values = None
labels = None

## perform tukey's multiple comparison test and display the summary
tukeys_results = None

```


```python
## optional -slicing out dataframe from results
```


```python
## make a barplot of final data to go with results

```


```python
## also can use built-in plot tukeys_reuslts.plot_simultaneous

```

- Final summary of group differences
