# Kyphosis Disease Classification using Python and Seaborn
This project analyzes clinical risk factors for kyphosis using Python, Seaborn, and statistical correlation

## 📘 Project Overview

This project analyzes and classifies Kyphosis, an abnormal curvature of the spine that may occur after corrective spinal surgery in children.
Using Python, Pandas, Seaborn, and Matplotlib, I performed data exploration, correlation analysis, and visualization to understand which features (Age, Number of vertebrae, Start position) influence the likelihood of kyphosis after surgery.

🔗 **Interactive Google Colab Notebook:**  
https://colab.research.google.com/drive/1elo33VAK5gXzu7mBObYkWT9KuNTfBQZk?usp=sharing 

## 🧬 Dataset Information

The dataset contains records from 81 pediatric patients who underwent spinal surgery.
| Feature      | Description                                            |
| ------------ | ------------------------------------------------------ |
| **Kyphosis** | Outcome variable (`present` or `absent`) after surgery |
| **Age**      | Age of the patient (in months)                         |
| **Number**   | Number of vertebrae involved in the surgery            |
| **Start**    | The number of the topmost vertebra operated on         |

📊 Source: [Kyphosis Dataset on Kaggle](https://www.kaggle.com/abbasit/kyphosis-dataset)

## ⚙️ Code Walkthrough
1️⃣ Data Import & Setup

I began by importing essential Python libraries for data analysis and visualization:

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from scipy.stats import pointbiserialr

```
The dataset was uploaded and loaded into a Pandas DataFrame.
I confirmed there were 81 rows and 4 columns and no missing values.

2️⃣ Exploratory Data Analysis (EDA)

To understand the dataset better, I explored:

- Data types

- Missing values

- Class distribution

- Basic statistics
```python
df.describe(include='all')
```
Findings:

- 79% of cases showed kyphosis absent

- 21% of cases showed kyphosis present

- Age ranged from 1 to 206 months

- The number of vertebrae involved ranged from 2 to 10

3️⃣ Correlation Analysis

To explore relationships between the target (Kyphosis) and numeric features,
I encoded Kyphosis as binary (0 = absent, 1 = present) and calculated the correlation matrix.
```python
df_corr = df.copy()
df_corr['Kyphosis_num'] = df_corr['Kyphosis'].map({'absent': 0, 'present': 1})
corr = df_corr[['Kyphosis_num', 'Age', 'Number', 'Start']].corr()
sns.heatmap(corr, annot=True, cmap='coolwarm', vmin=-1, vmax=1)
```

## 🧩 Correlation Heatmap
| Variable   | Correlation (r) | Direction           |
| ---------- | --------------- | ------------------- |
| **Number** | +0.36           | Moderately positive |
| **Age**    | +0.13           | Slightly positive   |
| **Start**  | -0.45           | Moderately negative |
- As Age and Number of vertebrae increase, kyphosis is more likely.

- As the Start vertebra number increases (meaning surgery starts lower in the spine), kyphosis is less likely.

4️⃣ Point-Biserial Correlation

To confirm the relationships statistically, I used the pointbiserialr() test for continuous–binary correlation.
```python
for col in ['Age', 'Number', 'Start']:
    r, p = pointbiserialr(df_corr['Kyphosis_num'], df_corr[col])
    print(col, "r =", r, "| p =", p)
This confirmed the same pattern seen in the heatmap.
```

5️⃣ Pairplot Visualization

A pairplot helped visualize feature distributions and interactions across classes (absent vs. present).
```python
sns.pairplot(
    data=df,
    vars=['Age', 'Number', 'Start'],
    hue='Kyphosis',
    kind='scatter',
    diag_kind='hist',
    plot_kws={'alpha':0.85, 's':40, 'edgecolor':'white'}
)
```
## 🌈 Pairplot Result

Observations:

Children with kyphosis present tend to be older.

More vertebrae involved (higher Number) increases kyphosis likelihood.

Lower Start values (closer to the top of the spine) are linked to kyphosis presence.

There is overlap between classes, suggesting nonlinear model boundaries (useful insight for Part II modeling).

## 💡 What I Learned

This project helped me gain hands-on experience with:

Cleaning and exploring real medical datasets

Using correlation analysis to identify predictive variables

Visualizing feature relationships with Seaborn

Interpreting clinical patterns from numerical data

Communicating results clearly for healthcare analytics

## Key Takeaways:

Data visualization is crucial for uncovering trends before modeling.

Even small datasets can reveal meaningful clinical insights when analyzed thoughtfully.

Negative correlation (like Start) can be as informative as positive ones.

## 🧾 Summary of Insights

Positive correlations: Age and Number → higher values increase kyphosis risk

Negative correlation: Start → lower values (closer to the top vertebra) increase risk

Overall: Older patients with more vertebrae involved and upper-level surgeries are more likely to develop kyphosis post-surgery.

## 🧩 Tools & Technologies
| Tool                     | Purpose                             |
| ------------------------ | ----------------------------------- |
| **Python (Colab)**       | Development environment             |
| **Pandas**               | Data manipulation                   |
| **Seaborn & Matplotlib** | Visualization                       |
| **SciPy**                | Statistical correlation tests       |
| **GitHub**               | Version control & portfolio hosting |

## ✨ Author

👩‍💻 Asiana Holloway
Master’s Student in Health Informatics

