# CS133 – Term Project (Group 13)
## Video Game Sales Data Analysis and Classification

**Course:** CS133 – Data Visualization  
**Instructor:** [Instructor Name]  

**Group 13 Members:**
- Haitham Assaf  
- Shruthi Raghavachary  
- Kaulan Serzhanuly  

---

## Project Overview

This project uses the **Video_Games_Sales_as_at_22_Dec_2016.csv** dataset to:

1. Clean and prepare the data.
2. Answer at least five data-driven questions using different types of visualizations.
3. Build a machine learning pipeline that predicts whether a game is a **“Hit”**
   (Global_Sales > 0.5 million units) based on its platform, genre, and year.
4. Evaluate at least three ML models using N-fold cross-validation and a held-out test set.
5. Visualize the performance of the best model using a confusion matrix and classification report.

All final project code lives in **`Final (1).ipynb`**.  
The written report is in **`cs133report.pdf`** .

---

## Repository Structure

- `Final (1).ipynb`  
  Main Jupyter notebook. Includes:
  - Data loading and cleaning
  - Five+ static visualizations (seaborn / matplotlib)
  - One interactive Plotly visualization
  - Train/test split and preprocessing with `ColumnTransformer`
  - Three ML models: Logistic Regression, Decision Tree, Random Forest
  - 5-fold cross-validation, accuracy comparison, confusion matrix, and classification report

- `Video_Games_Sales_as_at_22_Dec_2016.csv`  
  Primary dataset used in the notebook.

- `PS4_GamesSales.csv`, `XboxOne_GameSales.csv`  
  Additional console-specific datasets provided with the starter materials.

- `CS133_F25_P1_relplot_scatter_(2).ipynb`  
  Earlier practice notebook (relplot / scatter examples).

- `CS133_F25_P2_categorical_interactive_transform_(1).ipynb`  
  Earlier practice notebook (categorical plots + basic interactive plots).

- `cs133report.pdf`  
  Written report summarizing the project, visualizations, ML pipeline, and results.

---

## How to Run the Project in Google Colab

1. Open **Google Colab**.
2. Upload the following files to Colab or your Google Drive:
   - `Final (1).ipynb`
   - `Video_Games_Sales_as_at_22_Dec_2016.csv`
3. Open **`Final (1).ipynb`** in Colab.
4. Run the **imports cell**. If any library is missing, install it inside Colab with:
   ```python
   !pip install pandas numpy matplotlib seaborn plotly scikit-learn

5. Run all remaining cells in order:

Data loading and cleaning

Exploratory visualizations (Figures 1–6)

Interactive Plotly visualization

ML pipeline (train/test split, preprocessing)

Cross-validation and model comparison

Confusion matrix + classification report

All plots and metrics used in the PDF report are generated directly from this notebook.

Required Python Libraries

The notebook uses only libraries covered in CS133 lectures:

pandas

numpy

matplotlib

seaborn

plotly

scikit-learn

When running in Colab, these can be installed with:
!pip install pandas numpy matplotlib seaborn plotly scikit-learn
Project Output

The notebook produces:

Histograms, boxplots, scatter plots, line plots, and a hexbin joint plot for initial data exploration.

An interactive Plotly line chart showing genre trends over time.

A bar chart comparing accuracy of Logistic Regression, Decision Tree, and Random Forest.

A confusion matrix heatmap for the best model (Logistic Regression).

A full classification report (precision, recall, F1-score, support) for the best model.

These outputs are discussed and interpreted in the written report in the report pdf. 
