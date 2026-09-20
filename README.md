# ECE 2112: Advanced Computer Programming and Algorithms
## Experiment 4: Data Wrangling and Data Visualization

**Name:** [Your Name]  
**Section:** 2ECE-[Section]  
**Date Submitted:** September 20, 2026  

---

## A. Overview of the Assignment

This repository contains the Python implementation for **Experiment 4**, focusing on data wrangling, multi-condition filtering, feature selection, categorical aggregations, and data visualization using `pandas`, `matplotlib`, and `seaborn` on the ECE Board Exam dataset (`board2.csv`).

The experiment demonstrates how to:
1. **Derive calculated features** by computing `Average` board exam scores from individual subject grades (`Math`, `GEAS`, `Electronics`).
2. **Isolate student demographics** using explicit multi-condition Boolean indexing.
3. **Construct focused DataFrames** with specified column ordering without mutating the source dataset.
4. **Summarize performance metrics** across categorical features and communicate comparative findings using consistently scaled plots and non-causal statistical interpretations.

---

## B. Discussion of Each Problem

### Problem A: Visayas Communication DataFrame (`VisComm`)
* **Objective:** Filter for students whose `Hometown` is **Visayas** AND whose `Track` is **Communication**, retaining only `Name`, `Gender`, `Math`, `Electronics`, and `Average`.
* **Implementation & Logic:**
  * **Derived Column Setup:** Calculates overall average grades using `df['Average'] = df[['Math', 'GEAS', 'Electronics']].mean(axis=1)` to ensure the feature exists prior to indexing.
  * **Explicit Filtering:** Applies `(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')` to isolate records meeting both criteria simultaneously.
  * **Feature Selection:** Subsets the target columns in the required order and displays the resulting `VisComm` DataFrame along with its total row count (`len(VisComm)`).

### Problem B: Visayas Female DataFrame (`VisFemale`)
* **Objective:** Create a DataFrame of female students from Visayas containing `Name`, `Track`, `GEAS`, `Electronics`, and `Average`, then display a sub-filtered view of students with an `Average >= 60`.
* **Implementation & Logic:**
  * **Primary DataFrame Creation:** Applies `(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')` to generate the core `VisFemale` DataFrame with requested column ordering.
  * **Non-Destructive Slicing:** Passes `VisFemale[VisFemale['Average'] >= 60]` directly into `display()` to show students meeting the passing mark. This preserves the underlying `VisFemale` DataFrame without overwriting or mutating it.

### Problem C: Category-Average Visualization & Interpretation
* **Objective:** Calculate mean `Average` scores across `Track`, `Gender`, and `Hometown`, display summary tables, generate a 1x3 comparative bar chart figure, and identify peak-performing categories.
* **Implementation & Logic:**
  * **Categorical Aggregation:** Computes category means using `df.groupby('Feature')['Average'].mean()` to construct three clean summary tables.
  * **Visual Encoding:** Uses `plt.subplots(1, 3, sharey=True)` to create three side-by-side bar charts. Enforcing a shared y-axis scale ensures accurate visual comparison across categories. Category annotations and clean axis labels are included for clarity.
  * **Empirical Analysis:** Programmatically retrieves top-performing categories using `.idxmax()`. Output statements strictly describe sample mean differences without attributing causal links between demographic traits and exam scores.
