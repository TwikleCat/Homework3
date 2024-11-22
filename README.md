# Homework3
Data collection and preparation
```
import numpy as np # linear algebra
import pandas as pd# data processing, CSV file I/O (e.g. pd.read_csv)
import matplotlib.pyplot as plt
import seaborn as sns
# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))
```
```
df = pd.read_csv("/kaggle/input/e-commerce-dataset/realistic_e_commerce_sales_data.csv")
df.head(3)
```
```
df.info()
```

```
df.describe()
```

```
df.isnull().sum()
```


```
total_revenue = df['Total Price'].sum()
print(f"Total Revenue: ${total_revenue:,.2f}")
```

```
aver = df.groupby('Customer ID')['Total Price'].sum().mean()
print(f"Average order value: ${aver:,.2f}")
```

```
unique_customers = df['Customer ID'].nunique()
print(f"Number of Unique Customers: {unique_customers}")
```

```
orders_per_customer = df.groupby('Customer ID')['Total Price'].count().mean()
print(f"Average Orders per Customer: {orders_per_customer:.2f}")
```
```
avg_ship = df['Shipping Fee'].mean()
print(f"Average Shipping Fee: ${avg_ship:,.2f}")
```
```

customer_revenue = df.groupby('Customer ID')['Total Price'].sum().sort_values(ascending=False)
top_customers_ids = customer_revenue.head(10).index
top_customers_info = df[df['Customer ID'].isin(top_customers_ids)]

top_customers_info = top_customers_info.drop_duplicates(subset=['Customer ID'])

print("Top Customers by Revenue:")
print(top_customers_info[['Customer ID', 'Gender', 'Region', 'Age', 'Total Price']].sort_values(by='Total Price', ascending=False))
```

```
bins = [0, 20, 40, 60, 80]
labels = ['Under 20', '20-40', '40-60', '60-80']
df['Age Group'] = pd.cut(df['Age'], bins=bins, labels=labels, right=False)

age_group_spending = df.groupby('Age Group')['Total Price'].sum()
print("Revenue by Age Group:")
print(age_group_spending)
```

```
category_spending = df.groupby('Category')['Total Price'].sum().sort_values(ascending=False)
print("Revenue by Product Category:")
print(category_spending)
```

```
category_spending = df.groupby('Category')['Total Price'].sum().sort_values(ascending=False)

print("Revenue by Product Category:")
print(category_spending)

plt.figure(figsize=(12,6))
sns.barplot(x=category_spending.index, y=category_spending.values, palette='YlOrBr')  
plt.title('Total Revenue by Product Category', fontsize=16)
plt.xlabel('Product Category', fontsize=12)
plt.ylabel('Total Revenue ($)', fontsize=12)
plt.xticks(rotation=45) 
plt.show()
```


```
plt.figure(figsize=(10,6))
sns.histplot(df['Total Price'], bins=25, kde=True, color='red')
plt.title('Distribution of Total Price (Revenue per Transaction)', fontsize=16)
plt.xlabel('Total Price ($)', fontsize=12)
plt.ylabel('Frequency', fontsize=12)
plt.show()
```

```
gender_revenue = df.groupby('Gender')['Total Price'].sum().reset_index()

plt.figure(figsize=(8,6))
sns.barplot(x='Gender', y='Total Price', data=gender_revenue, palette='viridis')
plt.title('Total Revenue by Gender', fontsize=16)
plt.xlabel('Gender', fontsize=12)
plt.ylabel('Total Revenue ($)', fontsize=12)
plt.show()
```

```
region_revenue = df.groupby('Region')['Total Price'].sum().reset_index()

plt.figure(figsize=(10,6))
sns.barplot(x='Region', y='Total Price', data=region_revenue, palette='muted')
plt.title('Total Revenue by Region', fontsize=16)
plt.xlabel('Region', fontsize=12)
plt.ylabel('Total Revenue ($)', fontsize=12)
plt.xticks(rotation=45)
plt.show()
```
