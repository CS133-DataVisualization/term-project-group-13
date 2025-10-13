Team-Project-Group-13
# Video Game Analytics Dataset v1.0

## Overview

This dataset contains synthetic but realistic video game sales and streaming analytics data designed for educational and analytical purposes. The data includes comprehensive game information, sales metrics, critic/user scores, and Twitch streaming statistics.

**Intended Use Cases:**
- Categorical data analysis and visualization
- Correlation analysis between sales and streaming metrics
- Platform and genre trend analysis
- Data merging and join operations
- Feature engineering with apply/map functions

## Dataset Files

### 1. vg_sales_v1.csv (2,500 rows)
Main dataset containing video game sales and metadata.

### 2. twitch_stats_v1.csv (2,500 rows)
Complementary dataset with Twitch streaming metrics for the same games.

### 3. README_v1.md
This documentation file.

## Schema Documentation

### vg_sales_v1.csv Schema

| Column | Type | Description | Allowed Values |
|--------|------|-------------|----------------|
| Game | string | Unique game title | Synthetic game names |
| Platform | category | Gaming platform | NES, SNES, N64, PS1, PS2, PS3, PS4, PS5, X360, XOne, XSX, GC, Wii, WiiU, Switch, PC |
| Genre | category | Game genre | Action, Adventure, Platform, Role-Playing, Shooter, Sports, Racing, Strategy, Simulation, Fighting, Party, Puzzle, Indie |
| Publisher | category | Game publisher | 50 synthetic company names |
| Year | integer | Release year | 1985-2025 (skewed to 2005-2020) |
| Global_Sales_M | float | Global sales in millions | 0.01-50.0 (right-skewed) |
| Critic_Score | integer | Metacritic critic score | 30-98 (normal distribution, μ=73, σ=11) |
| User_Score | float | User rating | 3.5-9.8 (correlated with critic score) |
| ESRB_Rating | category | Age rating | E (28%), E10+ (17%), T (27%), M (25%), RP (3%) |
| Dev_Team_Size | integer | Development team size | 3-400 (correlated with platform/genre) |
| Budget_MUSD | float | Development budget in millions USD | 0.1-200 (correlated with team size) |
| Region | category | Primary market region | NA, EU, JP, Other |
| Franchise | boolean | Part of a franchise | True (35%), False (65%) |
| Metascore_Bucket | category | Derived from Critic_Score | Low (<65), Mid (65-79), High (80-89), Top (90+) |

### twitch_stats_v1.csv Schema

| Column | Type | Description | Range |
|--------|------|-------------|-------|
| Game | string | Game title (join key) | Matches vg_sales_v1.csv |
| Avg_Concurrent_Viewers | integer | Average concurrent viewers | 0-350,000 (heavy tail) |
| Peak_Concurrent_Viewers | integer | Peak concurrent viewers | 0-2,000,000 (≥ Avg * 1.2) |
| Monthly_Hours_Watched_M | float | Monthly hours watched in millions | 0-120 (correlated with viewers) |
| Streamer_Count | integer | Number of active streamers | 10-120,000 (weak correlation with viewers) |
| Streaming_Popularity_Bucket | category | Streaming popularity tier | Low, Mid, High, Top (by quantiles) |

## Data Generation Methodology

### Distributions and Correlations

**Sales Distribution:**
- Right-skewed exponential distribution
- Median ~0.3M, 95th percentile ~8M
- Outliers up to 25-40M copies
- Positive correlation with critic scores (~0.25-0.35)

**Genre Effects:**
- High-selling genres: Shooter, Sports, Action, Role-Playing
- Lower-selling genres: Strategy, Indie, Puzzle
- Nintendo platforms favor family-friendly genres

**Platform Trends:**
- Recent years (2017+) favor PS4/PS5/Switch/PC
- Platform-year compatibility enforced
- Budget correlates with platform capabilities

**Streaming Correlations:**
- Moderate correlation between sales and streaming (~0.25-0.4)
- Shooter/Action games have higher streaming metrics
- Puzzle/Strategy games have lower streaming despite some sales
- Includes counterexamples (cult classics vs. big sellers)

### Noise and Randomness

- All correlations include realistic noise
- 5% chance of streaming outliers
- Budget includes platform/genre multipliers with noise
- User scores have moderate correlation with critic scores

## Data Merging Instructions

### Using Pandas

```python
import pandas as pd

# Load datasets
vg_sales = pd.read_csv('vg_sales_v1.csv')
twitch_stats = pd.read_csv('twitch_stats_v1.csv')

# Merge on Game column
merged_df = pd.merge(vg_sales, twitch_stats, on='Game', how='inner')

# Verify merge
print(f"Original games: {len(vg_sales)}")
print(f"Twitch stats: {len(twitch_stats)}")
print(f"Merged dataset: {len(merged_df)}")
```

### Expected Results
- Perfect 1:1 join (2,500 rows each)
- No missing values after merge
- All games have both sales and streaming data

## Ethical Considerations

**Synthetic Data Disclaimer:**
- All data is artificially generated
- No real intellectual property or trademarks used
- Game titles are algorithmically generated
- Publishers are fictional companies
- No data scraping or real-world data collection involved

## Example Analysis Code

### Data Loading and Basic Checks

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load data
vg_sales = pd.read_csv('vg_sales_v1.csv')
twitch_stats = pd.read_csv('twitch_stats_v1.csv')

# Basic data quality checks
print("Missing values:")
print(vg_sales.isna().sum())
print(twitch_stats.isna().sum())

print("\nUnique counts:")
print(f"Games: {vg_sales['Game'].nunique()}")
print(f"Platforms: {vg_sales['Platform'].nunique()}")
print(f"Genres: {vg_sales['Genre'].nunique()}")
```

### Categorical Visualizations

```python
# Platform distribution
plt.figure(figsize=(12, 6))
sns.countplot(data=vg_sales, y='Platform', order=vg_sales['Platform'].value_counts().index)
plt.title('Game Distribution by Platform')
plt.show()

# Genre vs Sales
plt.figure(figsize=(12, 8))
sns.boxplot(data=vg_sales, x='Genre', y='Global_Sales_M')
plt.xticks(rotation=45)
plt.title('Sales Distribution by Genre')
plt.show()

# ESRB Rating distribution
plt.figure(figsize=(8, 6))
vg_sales['ESRB_Rating'].value_counts().plot(kind='pie', autopct='%1.1f%%')
plt.title('ESRB Rating Distribution')
plt.show()
```

### Interactive Plotly Example

```python
import plotly.express as px
import plotly.graph_objects as go

# Merge datasets
merged_df = pd.merge(vg_sales, twitch_stats, on='Game')

# Interactive scatter plot
fig = px.scatter(merged_df, 
                 x='Global_Sales_M', 
                 y='Avg_Concurrent_Viewers',
                 color='Genre',
                 size='Critic_Score',
                 hover_data=['Game', 'Platform', 'Publisher'],
                 title='Sales vs Streaming Popularity by Genre')

fig.show()

# Correlation heatmap
correlation_data = merged_df[['Global_Sales_M', 'Critic_Score', 'User_Score', 
                             'Avg_Concurrent_Viewers', 'Monthly_Hours_Watched_M']].corr()

fig = px.imshow(correlation_data, 
                text_auto=True, 
                aspect="auto",
                title='Correlation Matrix')
fig.show()
```

### Feature Engineering with Apply

```python
# Create generation buckets from Year
def get_generation(year):
    if year < 1990:
        return '8-bit Era'
    elif year < 2000:
        return '16-bit Era'
    elif year < 2010:
        return 'Early 3D Era'
    elif year < 2020:
        return 'HD Era'
    else:
        return 'Modern Era'

vg_sales['Generation'] = vg_sales['Year'].apply(get_generation)

# Analyze by generation
generation_analysis = vg_sales.groupby('Generation').agg({
    'Global_Sales_M': ['mean', 'median', 'count'],
    'Critic_Score': 'mean',
    'Budget_MUSD': 'mean'
}).round(2)

print("Analysis by Gaming Generation:")
print(generation_analysis)
```

### Advanced Analytics

```python
# Platform performance analysis
platform_performance = vg_sales.groupby('Platform').agg({
    'Global_Sales_M': ['mean', 'median', 'sum'],
    'Critic_Score': 'mean',
    'Budget_MUSD': 'mean',
    'Game': 'count'
}).round(2)

platform_performance.columns = ['Avg_Sales', 'Median_Sales', 'Total_Sales', 
                               'Avg_Critic_Score', 'Avg_Budget', 'Game_Count']
platform_performance = platform_performance.sort_values('Total_Sales', ascending=False)

print("Platform Performance Analysis:")
print(platform_performance.head(10))

# Genre profitability analysis
genre_profitability = vg_sales.groupby('Genre').agg({
    'Global_Sales_M': 'mean',
    'Budget_MUSD': 'mean',
    'Critic_Score': 'mean'
}).round(2)

genre_profitability['ROI'] = (genre_profitability['Global_Sales_M'] * 50 - 
                              genre_profitability['Budget_MUSD']) / genre_profitability['Budget_MUSD']
genre_profitability = genre_profitability.sort_values('ROI', ascending=False)

print("\nGenre Profitability Analysis:")
print(genre_profitability)
```

## Data Quality Assurance

### Validation Checks

```python
# Shape validation
assert len(vg_sales) == len(twitch_stats) == 2500, "Row count mismatch"

# Key uniqueness
assert vg_sales['Game'].nunique() == len(vg_sales), "Duplicate games in sales data"
assert twitch_stats['Game'].nunique() == len(twitch_stats), "Duplicate games in twitch data"

# No null values
assert vg_sales.isna().sum().sum() == 0, "Null values found in sales data"
assert twitch_stats.isna().sum().sum() == 0, "Null values found in twitch data"

# Categorical validation
valid_platforms = {'NES', 'SNES', 'N64', 'PS1', 'PS2', 'PS3', 'PS4', 'PS5', 
                   'X360', 'XOne', 'XSX', 'GC', 'Wii', 'WiiU', 'Switch', 'PC'}
assert set(vg_sales['Platform'].unique()).issubset(valid_platforms), "Invalid platforms"

valid_genres = {'Action', 'Adventure', 'Platform', 'Role-Playing', 'Shooter', 
               'Sports', 'Racing', 'Strategy', 'Simulation', 'Fighting', 
               'Party', 'Puzzle', 'Indie'}
assert set(vg_sales['Genre'].unique()).issubset(valid_genres), "Invalid genres"

# Logical constraints
assert all(twitch_stats['Peak_Concurrent_Viewers'] >= 
          twitch_stats['Avg_Concurrent_Viewers'] * 1.2), "Peak < Avg * 1.2"

# Correlation checks
merged_df = pd.merge(vg_sales, twitch_stats, on='Game')
sales_critic_corr = merged_df['Global_Sales_M'].corr(merged_df['Critic_Score'])
sales_streaming_corr = merged_df['Global_Sales_M'].corr(merged_df['Monthly_Hours_Watched_M'])

assert 0.2 <= sales_critic_corr <= 0.5, f"Sales-Critic correlation out of range: {sales_critic_corr}"
assert 0.2 <= sales_streaming_corr <= 0.5, f"Sales-Streaming correlation out of range: {sales_streaming_corr}"

print("All validation checks passed!")
print(f"Sales-Critic correlation: {sales_critic_corr:.3f}")
print(f"Sales-Streaming correlation: {sales_streaming_corr:.3f}")
```

## File Format Specifications

- **Encoding:** UTF-8
- **Delimiter:** Comma (,)
- **Header:** First row contains column names
- **Quotes:** No quoted numbers, strings may be quoted if they contain commas
- **Line Endings:** Unix-style (LF) or Windows-style (CRLF)
- **File Size:** ~200KB each (2,500 rows)
