# Pandas Sampling

### 1) Simple Random Sampling:
**Concept:** This is the most basic form of sampling. Every individual in the dataset has an equal chance of being selected.

**Example:** Imagine you have a bowl of 100 different colored marbles and you want to get a sense of the colors. If you close your eyes and pick 10 marbles at random, that's simple random sampling.

**Pandas Implementation:**
```python
import pandas as pd

df = pd.read_csv('bike.csv')

# This will pick 10 random sample from the data frame
simple_random_sample = df.sample(n = 10)

simple_random_sample
```

### 2) Stratified Random Sampling:
**Concept:** In this method, the population is divided into smaller groups called strata based on certain shared characteristics (like age, gender, etc.). Then, a random sample is taken from each stratum.

**Example:** Let's say you have a class of 50 male and 50 female students and you want to survey 20 students. If you pick 10 males and 10 females randomly, ensuring the gender ratio is maintained, that's stratified random sampling.

**Pandas Implementation:**
```python
import pandas as pd
import numpy as np

# Create a sample dataset
np.random.seed(42)  # for reproducibility
data = {
    'ID': range(1, 101),
    'Age': np.random.randint(18, 30, 100),
    'Gender': np.random.choice(['Male', 'Female'], 100),
    'State': np.random.choice(['StateA', 'StateB', 'StateC', 'StateD', 'StateE'], 100)
}
df1 = pd.DataFrame(data)
df1.head()
```

```python
from sklearn.model_selection import train_test_split

training_data, sample_data = train_test_split(df1, test_size=0.1, stratify=df1['Gender'])

print(training_data)
print(sample_data)
```

### 3) Systematic Sampling:
**Concept:** Instead of random selection, you pick every kth item from your dataset.

**Example:** From a list of 100 students, if you decide to pick every 10th student, starting from the 1st, you'd pick the 1st, 11th, 21st,... and so on.

**Pandas Implementation:**
```python
k = 10

#systematic_sample_data = df1.iloc[::k, :]
systematic_sample_data = df1.iloc[0:100:k, :]

systematic_sample_data
```

### 4) Cluster Sampling:
**Concept:** The population is divided into clusters (groups) and a few clusters are selected at random. All observations from these selected clusters are included in the sample.

**Example:** Imagine a country with 50 states, and you want to survey the population. Instead of surveying people from all 50 states, you randomly select 5 states and survey everyone from those 5 states.

**Pandas Implementation:** This is a bit more involved since you'd first group your data into clusters and then sample from those clusters.
```python
# Sample 2 states randomly
selected_states = np.random.choice(df1['State'].unique(), 2, replace=False)

# Select all rows that belong to the 2 randomly selected states
sampled_data = df1[df1['State'].isin(selected_states)]

sampled_data.head()
```

