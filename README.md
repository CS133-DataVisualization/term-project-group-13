# Video Game Sales Data Analysis Project

**Group 13**: Kaulan Serzhanuly, Shruthi Raghavan, Haitham Assaf (018226910)  
**Course**: CS-133  
**Project**: Data Exploration and Visualization

## 📊 Dataset Overview

This project analyzes two comprehensive video game sales datasets to explore relationships between game features, sales performance, and critical reception.

### Dataset 1: Video Games Sales (Primary Dataset)
- **File**: `Video_Games_Sales_as_at_22_Dec_2016.csv`
- **Size**: 16,720 records
- **Source**: Historical video game sales data up to December 2016
- **Focus**: Global video game market analysis

### Dataset 2: Xbox One Game Sales
- **File**: `XboxOne_GameSales.csv`
- **Size**: 614 records
- **Source**: Xbox One platform-specific sales data
- **Focus**: Microsoft Xbox One console performance

## 🎮 Dataset Features

### Video Games Sales Dataset Columns:
- **Name**: Game title
- **Platform**: Gaming platform (PS4, Xbox One, PC, etc.)
- **Year_of_Release**: Release year
- **Genre**: Game category (Action, Sports, RPG, etc.)
- **Publisher**: Publishing company
- **NA_Sales**: North American sales (millions)
- **EU_Sales**: European sales (millions)
- **JP_Sales**: Japanese sales (millions)
- **Other_Sales**: Other regions sales (millions)
- **Global_Sales**: Total worldwide sales (millions)
- **Critic_Score**: Professional critic rating (0-100)
- **Critic_Count**: Number of critic reviews
- **User_Score**: User rating (0-10)
- **User_Count**: Number of user reviews
- **Developer**: Game development studio
- **Rating**: ESRB content rating

### Xbox One Dataset Columns:
- **Pos**: Ranking position
- **Game**: Game title
- **Year**: Release year
- **Genre**: Game category
- **Publisher**: Publishing company
- **North America**: NA sales (millions)
- **Europe**: EU sales (millions)
- **Japan**: JP sales (millions)
- **Rest of World**: Other regions sales (millions)
- **Global**: Total worldwide sales (millions)

## 🔍 Analysis Questions

This project addresses six key data exploration questions:

### Q1: Missing Data Analysis
- **Objective**: Identify data quality issues
- **Method**: Count missing values per column
- **Visualization**: Bar chart of missing data

### Q2: Data Types Summary
- **Objective**: Understand dataset structure
- **Method**: Analyze column data types
- **Output**: Data type distribution visualization

### Q3: Pairwise Relationships
- **Objective**: Explore feature correlations
- **Method**: Pair plot with polynomial regression
- **Visualization**: Scatter matrix with regression lines

### Q4: Linear Regression Analysis
- **Objective**: Quantify relationships between features
- **Method**: Linear regression with confidence intervals
- **Focus**: Sales vs. Critical reception correlation

### Q5: Multi-dimensional Visualization
- **Objective**: Show complex relationships
- **Method**: Relplot with hue and size encoding
- **Features**: Sales, scores, platforms, and temporal data

### Q6: Small Multiples Analysis
- **Objective**: Compare across categories
- **Method**: Faceted plots (3 per row)
- **Focus**: Platform and genre comparisons

## 🛠️ Technical Requirements

### Python Libraries:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
```

### Key Features:
- **Encoding Handling**: Robust UTF-8/Latin-1/CP1252 support
- **Missing Data**: Comprehensive null value analysis
- **Visualization**: Professional plots with proper styling
- **Adaptive Analysis**: Automatically selects appropriate features

## 📈 Expected Insights

### Sales Patterns:
- **Regional Preferences**: NA vs EU vs JP market differences
- **Platform Performance**: Console vs PC vs Mobile trends
- **Genre Popularity**: Most successful game categories

### Critical Reception:
- **Score Correlations**: Critic vs User rating relationships
- **Sales Impact**: How scores affect commercial success
- **Temporal Trends**: Evolution of game quality over time

### Market Analysis:
- **Publisher Performance**: Top-performing game studios
- **Release Timing**: Optimal release periods
- **Platform Strategy**: Cross-platform vs exclusive titles

## 🚀 Usage Instructions

### 1. Environment Setup:
```bash
# Install required packages
pip install pandas numpy matplotlib seaborn scipy jupyter
```

### 2. Run Analysis:
```bash
# Start Jupyter Notebook
jupyter notebook

# Open video_game_data_exploration.ipynb
# Run all cells sequentially
```

### 3. File Structure:
```
CS-133-project-1/
├── README.md
├── video_game_data_exploration.ipynb
├── Video_Games_Sales_as_at_22_Dec_2016.csv
└── XboxOne_GameSales.csv
```

## 📊 Output Visualizations

### 1. Data Quality Assessment
- Missing data bar chart
- Data type distribution
- Dataset summary statistics

### 2. Correlation Analysis
- Pairwise scatter plots with regression lines
- Correlation heatmaps
- Feature relationship matrices

### 3. Sales Performance
- Regional sales comparisons
- Platform performance analysis
- Genre popularity rankings

### 4. Critical Reception
- Score distribution analysis
- Critic vs User rating comparisons
- Quality trends over time

### 5. Market Segmentation
- Platform-specific analysis
- Publisher performance rankings
- Genre market share

## 🎯 Key Findings Preview

### Sales Insights:
- **Top Performing Genres**: Action, Sports, and Shooter games dominate
- **Regional Preferences**: NA favors shooters, JP prefers RPGs
- **Platform Trends**: Console vs PC market dynamics

### Quality Metrics:
- **Score Correlations**: Strong relationship between critic and user scores
- **Sales Impact**: Higher scores generally correlate with better sales
- **Temporal Quality**: Game quality has improved over time

### Market Dynamics:
- **Publisher Dominance**: Major publishers control market share
- **Platform Strategy**: Cross-platform releases perform better
- **Release Timing**: Holiday seasons show peak performance

## 📚 Data Sources

- **Video Games Sales**: Historical gaming industry data
- **Xbox One Sales**: Microsoft platform-specific metrics
- **Critical Scores**: Professional and user review aggregations
- **Sales Data**: Regional and global market performance

## 🔧 Troubleshooting

### Common Issues:
1. **Encoding Errors**: Fixed with multiple encoding fallbacks
2. **Missing Data**: Handled with appropriate null value analysis
3. **Memory Issues**: Optimized for large dataset processing
4. **Visualization**: Professional styling and clear labeling

### Performance Notes:
- **Large Dataset**: 16K+ records require efficient processing
- **Memory Usage**: Optimized pandas operations
- **Visualization**: High-quality plots with proper sizing

## 📝 Project Deliverables

1. **Jupyter Notebook**: Complete analysis with all 6 questions
2. **Visualizations**: Professional plots with proper titles
3. **Data Quality Report**: Missing data and type analysis
4. **Correlation Analysis**: Feature relationship insights
5. **Market Analysis**: Sales and performance trends

## 🎓 Learning Objectives

This project demonstrates:
- **Data Exploration**: Comprehensive dataset analysis
- **Visualization**: Professional plotting techniques
- **Statistical Analysis**: Correlation and regression methods
- **Data Quality**: Missing data and encoding handling
- **Market Research**: Gaming industry insights

---

**Note**: This analysis provides insights into the video game industry's sales patterns, critical reception, and market dynamics. The findings can inform business decisions, market strategies, and academic research in the gaming sector.
