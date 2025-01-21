# Diamonds Dataset Analysis

This project involves analyzing the Diamonds dataset from Kaggle to gain insights into various factors affecting diamond prices. The analysis includes data exploration, visualization, and correlation studies.

---

## Prerequisites

Install the required libraries:

```bash
pip install kaggle pandas matplotlib seaborn
```

---

## Steps to Run the Project

### Step 1: Set Up Kaggle API Key

1. Download your Kaggle API key (`kaggle.json`) from [Kaggle](https://www.kaggle.com/account).
2. Upload the `kaggle.json` file to your environment:

```python
from google.colab import files
files.upload()
```

### Step 2: Configure Kaggle

Set up the Kaggle API credentials:

```bash
!mkdir -p ~/.kaggle
!mv kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json
```

### Step 3: Download the Diamonds Dataset

Search and download the dataset:

```bash
!kaggle datasets list -s diamonds
!kaggle datasets download -d shivam2503/diamonds
```

Unzip the dataset:

```bash
!unzip diamonds.zip
```

### Step 4: Load and Explore the Dataset

Load the dataset into a Pandas DataFrame:

```python
import pandas as pd

df = pd.read_csv('diamonds.csv')

print("First few rows of the dataset:")
print(df.head())

print("\nDataset Info:")
print(df.info())

print("\nSummary Statistics:")
print(df.describe())

print("\nMissing Values:")
print(df.isnull().sum())
```

---

## Data Visualization

### Distribution of Diamond Prices

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(8, 5))
sns.histplot(df['price'], kde=True, color='blue', bins=30)
plt.title('Distribution of Diamond Prices')
plt.xlabel('Price')
plt.ylabel('Frequency')
plt.show()
```

### Correlation Matrix

```python
numerical_df = df.select_dtypes(include=['number'])

plt.figure(figsize=(10, 6))
sns.heatmap(numerical_df.corr(), annot=True, cmap='coolwarm', fmt=".2f")
plt.title('Correlation Matrix')
plt.show()
```

### Boxplots for Price by Cut and Color

```python
plt.figure(figsize=(8, 5))
sns.boxplot(x='cut', y='price', data=df, palette='Set2')
plt.title('Price by Cut')
plt.xlabel('Cut')
plt.ylabel('Price')
plt.show()

plt.figure(figsize=(8, 5))
sns.boxplot(x='color', y='price', data=df, palette='Set3')
plt.title('Price by Color')
plt.xlabel('Color')
plt.ylabel('Price')
plt.show()
```

### Scatterplot of Price vs Carat

```python
plt.figure(figsize=(8, 5))
sns.scatterplot(x='carat', y='price', data=df, hue='cut', palette='viridis', alpha=0.7)
plt.title('Price vs Carat')
plt.xlabel('Carat')
plt.ylabel('Price')
plt.legend(title='Cut')
plt.show()
```

### Pairplot of Selected Features

```python
selected_features = ['carat', 'price', 'depth', 'table', 'x', 'y', 'z']
sns.pairplot(df[selected_features], diag_kind='kde', plot_kws={'alpha': 0.5})
plt.show()
```

### Heatmap of Average Price by Cut and Color

```python
avg_price_cut_color = df.groupby(['cut', 'color'])['price'].mean().unstack()

plt.figure(figsize=(10, 6))
sns.heatmap(avg_price_cut_color, annot=True, fmt=".2f", cmap='YlGnBu')
plt.title('Average Price by Cut and Color')
plt.xlabel('Color')
plt.ylabel('Cut')
plt.show()
```

---

## Key Insights

1. **Price Distribution**: Diamond prices exhibit a right-skewed distribution.
2. **Correlation Analysis**: Carat weight has a strong positive correlation with price.
3. **Cut and Color Impact**: Diamonds with better cuts and colors generally fetch higher prices.
4. **Interactive Features**: Visualizations highlight trends and outliers effectively.

---

## Dataset Details

- **Source**: [Kaggle - Diamonds Dataset](https://www.kaggle.com/shivam2503/diamonds)
- **Columns**:
  - `carat`: Weight of the diamond
  - `cut`: Quality of the cut (Fair, Good, Very Good, Premium, Ideal)
  - `color`: Color grading (from J (worst) to D (best))
  - `clarity`: Clarity grading
  - `depth`: Total depth percentage
  - `table`: Width of the diamond's top as a percentage of the widest point
  - `price`: Price in US dollars
  - `x`, `y`, `z`: Length, width, and depth in mm

---

## License

This project is open-source and available under the MIT License.

