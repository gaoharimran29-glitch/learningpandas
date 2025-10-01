# Pandas Practice Questions (Dataset1)

## Q1. Load the dataset into Pandas and display the first 10 rows.
```python
import pandas as pd

df = pd.read_csv(r"dataset1.csv")
print(df.head(10))
```
## Q2. How many passengers are there in total?
```python
print(len(df))
# OR
print(df.shape[0])
```

## Q3. What are the column names and data types?
```python
print(df.dtypes)
```

## Q4. Count the number of missing values in each column.
```python
print(df.isnull().sum())
```

## Q5. Get summary statistics for numeric columns.
```python
print(df.describe())
```

## Q6. Show all passengers in Pclass = 1.
```python
print(df[df["Pclass"] == 1])
```

## Q7. How many male vs female passengers are there?
```python
print(df["Sex"].value_counts())
```

## Q8. Display passengers younger than 18.
```python
print(df[df["Age"] < 18])
```

## Q9. Find passengers who paid fare greater than 100.
```python
print(df[df["Fare"] > 100])
```

## Q10. Show all passengers who embarked from 'C' port.
```python
print(df[df["Embarked"] == "C"])
```

## Q11. What was the average age of passengers (ignore missing values)?
```python
print(df["Age"].mean(skipna=True))
```

## Q12. What is the average fare paid by each passenger class (Pclass)?
```python
print(df.groupby("Pclass")["Fare"].mean())
```

## Q13. Find survival rate by gender.
```python
print(df.groupby("Sex")["Survived"].mean())
```

## Q14. Group passengers by Embarked and find the average fare.
```python
print(df.groupby("Embarked")["Fare"].mean())
```

## Q15. Find the maximum number of siblings/spouses onboard.
```python
print(df["Siblings/Spouses"].max())
```

## Q16. Fill missing Age values with the median age.
```python
df["Age"].fillna(df["Age"].median(), inplace=True)
```

## Q17. Fill missing Fare values with the average fare of that passenger’s Pclass.
```python
df["Fare"] = df.groupby("Pclass")["Fare"].transform(lambda x: x.fillna(x.mean()))
```

## Q18. Create a new column “FamilySize” = Siblings/Spouses + Parents/Children + 1.
```python
df["FamilySize"] = df["Siblings/Spouses"] + df["Parents/Children"] + 1
```

## Q19. Find the top 5 oldest passengers and their survival status.
```python
print(df.sort_values("Age", ascending=False)[["Name", "Age", "Survived"]].head(5))
```

## Q20. What percentage of passengers survived?
```python
survival_rate = df["Survived"].mean() * 100
print(f"Survival Rate: {survival_rate:.2f}%")
```
