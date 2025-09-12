# 📊 Pandas Notes – Beginner to Intermediate

This repository contains beginner-friendly notes and examples for **Pandas**, one of the most powerful data manipulation libraries in Python.  
These notes include reading/writing data, creating DataFrames, selection, filtering, updating, handling missing values, merging, concatenation, and more.  
At the end, you’ll also learn about the important parameter `ignore_index` with examples.

---

## 📑 Table of Contents
1. Installation & Setup  
2. Reading Files  
3. Creating DataFrames  
4. Viewing Data  
5. Saving DataFrames  
6. Selecting Data  
7. Updating & Inserting Data  
8. Handling Missing Data  
9. Sorting & Grouping  
10. Interpolation  
11. Merging DataFrames  
12. Concatenation  
13. Understanding `ignore_index`  
14. Conclusion  

---

## 🔧 Installation & Setup

```
# Install pandas
pip install pandas

# Install openpyxl for Excel support
pip install openpyxl
```

CSV and JSON support works out-of-the-box.

---

## 📥 Reading Files into Pandas

```
import pandas as pd

# Reading Excel file
df = pd.read_excel(r"C:\Users\hp\Desktop\IRFAN DATA.xlsx")

# Reading CSV file
df_csv = pd.read_csv("filename.csv")

# Reading JSON file
df_json = pd.read_json("filename.json")

# Display the data
print(df)

# Show column names, null values count, data types
print(df.info())

# Show basic statistics (mean, std, min, percentiles, etc.)
print(df.describe())

# Notes:
# object → string/text
# int64 → integers
# float64 → decimals
```

---

## 🏗 Creating a DataFrame

```
import pandas as pd

data = {
    "Name": ["RAM", "SHYAM", "HUSSAIN", "KHAN"],
    "ID": [0, 1, 2, 3],
    "AGE": [25, 53, 56, 79],
    "PERFORMANCE SCORE": [80, 90, 20, 30]
}

df = pd.DataFrame(data)
print(df)

# Output:
#      Name  ID  AGE  PERFORMANCE SCORE
# 0     RAM   0   25                 80
# 1   SHYAM   1   53                 90
# 2 HUSSAIN   2   56                 20
# 3    KHAN   3   79                 30
```

---

## 📖 Viewing Data

```
print(df.head(1))  # First row
print(df.tail(1))  # Last row
print("Shape:", df.shape)  # (rows, columns)
print("Columns:", df.columns)

# Output:
#   Name  ID  AGE  PERFORMANCE SCORE
# 0  RAM   0   25                 80
# Shape: (4, 4)
# Columns: Index(['Name','ID','AGE','PERFORMANCE SCORE'], dtype='object')
```

---

## 💾 Saving DataFrames

```
df.to_excel("output.xlsx", index=False)  # Save Excel
df.to_csv("output.csv")                  # Save CSV
df.to_json("output.json")                # Save JSON
```

---

## 🎯 Selecting Data

```
# Selecting one column (returns Series)
print(df["Name"])

# Selecting multiple columns (returns DataFrame)
print(df[["Name","AGE"]])

# Selecting rows with conditions
aged = df[(df['AGE'] > 50) & (df['PERFORMANCE SCORE'] > 50)]
print(aged)

aged2 = df[(df['AGE'] > 50) | (df['PERFORMANCE SCORE'] > 50)]
print(aged2)
```

---

## ✏️ Updating & Inserting Data

```
# Update value
df.loc[0, "AGE"] = 30
print(df)

# Update entire column
df['PERFORMANCE SCORE'] = df['PERFORMANCE SCORE'] * 1.05
print(df)

# Insert a new column
df['Bonus'] = df['PERFORMANCE SCORE'] * 0.1
print(df)

# Insert at specific position
df.insert(0, "Emp-ID", [10, 20, 30, 40])
print(df)
```

---

## 🚫 Handling Missing Data

```
import pandas as pd
import numpy as np

data = {
    "Name":["RAM", None, "SHYAM", "HUSSAIN", "KHAN"],
    "ID":[0, None, 1, 2, 3],
    "AGE":[25, 53, 53, None, 53],
    "PERFORMANCE SCORE":[80,90,20,30, None],
    "Salary":[30000,50000,40000,70000,None]
}

df = pd.DataFrame(data)

# Detect missing values
print(df.isnull())
print(df.isnull().sum())

# Fill missing values
df["AGE"].fillna(df["AGE"].mean(), inplace=True)
df.fillna(0, inplace=True)

# Drop rows with any missing values
df.dropna(inplace=True)

# Drop columns
df.drop(columns=["ID","AGE"], inplace=True)
print(df)
```

---

## 🔄 Sorting & Grouping

```
# Sort values by AGE descending
df.sort_values(by="AGE", ascending=False, inplace=True)
print(df)

# Group by AGE and sum Salary
grouped = df.groupby("AGE")["Salary"].sum()
print(grouped)
```

---

## 📈 Interpolation

```
data = {
    "Time":[1,2,3,4,5],
    "Value":[10, None, 30, 40,50]
}
df = pd.DataFrame(data)
df['Value'] = df['Value'].interpolate(method='linear')
print(df)
```

---

## 🔗 Merging DataFrames

```
df_customers = pd.DataFrame({
    'CustomerId':[1,2,3],
    'Name':['Ramesh','Suresh','Kalpesh']
})

df_orders = pd.DataFrame({
    'CustomerId':[1,2,4],
    'OrderAmount':[250,450,350]
})

# Merge examples
df_merged = pd.merge(df_customers, df_orders, on='CustomerId', how='right')
print(df_merged)

df_merged = pd.merge(df_customers, df_orders, on='CustomerId', how='left')
print(df_merged)

df_merged = pd.merge(df_customers, df_orders, on='CustomerId', how='outer')
print(df_merged)

df_merged = pd.merge(df_customers, df_orders, on='CustomerId', how='inner')
print(df_merged)
```

---

## ➕ Concatenation

```
df_Region1 = pd.DataFrame({
    'CustomerId':[1,2,3],
    'Name':['Ramesh','Suresh','Kalpesh']
})

df_Region2 = pd.DataFrame({
    'CustomerId':[4,5,6],
    'Name':['Imran','Khan','Hero']
})

# Concatenate vertically
df_concat = pd.concat([df_Region1, df_Region2], axis=0, ignore_index=True)
print(df_concat)
```

---

## 📝 Understanding ignore_index

```
# ignore_index=True resets the index after concatenation
df_a = pd.DataFrame({"X":[1,2,3]})
df_b = pd.DataFrame({"X":[4,5,6]})

# Without ignore_index
print(pd.concat([df_a, df_b], ignore_index=False))

# With ignore_index
print(pd.concat([df_a, df_b], ignore_index=True))
```

Output:  

```
ignore_index=False:
   X
0  1
1  2
2  3
0  4
1  5
2  6

ignore_index=True:
   X
0  1
1  2
2  3
3  4
4  5
5  6
```

---

## 🎯 Conclusion

- Pandas is a powerful tool for data analysis.  
- You can easily handle files (Excel, CSV, JSON).  
- Perform filtering, grouping, merging, concatenation.  
- Understand `ignore_index` carefully when concatenating.  
- With practice, Pandas will make your data manipulation super easy.
