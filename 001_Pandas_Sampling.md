# Pandas Sampling

### 1) Simple Random Sampling:
**Concept:** This is the most basic form of sampling. Every individual in the dataset has an equal chance of being selected.

**Example:** Imagine you have a bowl of 100 different colored marbles and you want to get a sense of the colors. If you close your eyes and pick 10 marbles at random, that's simple random sampling.

**Pandas Implementation:**
```python
import pandas as pd

# Assuming df is your DataFrame
df = pd.read_csv('bike.csv')
sampled_data = df.sample(n=10)  # This will pick 10 random rows from the DataFrame df
```

### 2) Stratified Random Sampling:
**Concept:** In this method, the population is divided into smaller groups called strata based on certain shared characteristics (like age, gender, etc.). Then, a random sample is taken from each stratum.

**Example:** Let's say you have a class of 50 male and 50 female students and you want to survey 20 students. If you pick 10 males and 10 females randomly, ensuring the gender ratio is maintained, that's stratified random sampling.

**Pandas Implementation:**
```python
from sklearn.model_selection import train_test_split

# Assuming df is your DataFrame and 'gender' is the column you want to stratify on
train, sampled_data = train_test_split(df, test_size=0.2, stratify=df['gender'])
```

### 3) Systematic Sampling:
**Concept:** Instead of random selection, you pick every kth item from your dataset.

**Example:** From a list of 100 students, if you decide to pick every 10th student, starting from the 1st, you'd pick the 1st, 11th, 21st,... and so on.

**Pandas Implementation:**
```python
k = 10
sampled_data = df.iloc[::k, :]
```

### 4) Cluster Sampling:
**Concept:** The population is divided into clusters (groups) and a few clusters are selected at random. All observations from these selected clusters are included in the sample.

**Example:** Imagine a country with 50 states, and you want to survey the population. Instead of surveying people from all 50 states, you randomly select 5 states and survey everyone from those 5 states.

**Pandas Implementation:** This is a bit more involved since you'd first group your data into clusters and then sample from those clusters.
```python
# Assuming df is your DataFrame and 'state' is your clustering column
clusters = df.groupby('state')
selected_clusters = clusters.sample(n=5)
sampled_data = df[df['state'].isin(selected_clusters.index)]
```

