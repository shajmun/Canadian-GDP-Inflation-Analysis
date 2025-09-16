# In-Depth Analysis of Canada's GDP Growth and Inflation Relationship (1961-2025)

## 📖 Project Overview

This project provides a comprehensive analysis of the relationship between Canada's quarterly Real GDP Growth and its quarterly Inflation Rate, using over 60 years of historical data from Statistics Canada. The primary objective was to test the classic economic hypothesis (**Phillips Curve Hypothesis**) that a high rate of economic growth is associated with a high rate of inflation.

The analysis moves beyond a simple correlation check by examining the relationship from multiple perspectives:
- **Short-Term (Quarter-over-Quarter):** To capture the immediate, volatile relationship between the two metrics.
- **Long-Term (Year-over-Year):** To smooth out short-term noise and identify underlying trends.

This project serves as a portfolio piece demonstrating a complete data science workflow, from handling messy, real-world data to drawing nuanced, data-driven conclusions.

**[You can view the full analysis in the Jupyter Notebook here.](GDP_Inflation_Analysis.ipynb)**

---
## 🔑 Key Findings

The central conclusion of this analysis is that the simple, direct relationship between GDP growth and inflation, often taught in introductory economics, is **not supported** by the Canadian historical data.

* **No Significant Correlation:** Both short-term (quarterly) and long-term (annual) correlation coefficients are effectively zero, indicating that GDP growth has not been a reliable predictor of inflation.
    * **Quarter-over-Quarter Correlation:** `0.051`
    * **Year-over-Year Correlation:** `0.046`
* **Data Quality is Crucial:** A major part of this project involved identifying and correcting a significant data quality issue in the raw GDP data, where the unit of measurement was inconsistent over time. The final analysis relies on a carefully selected, consistent subset of the data.
* **Historical Context Matters:** The time-series plots reveal a complex economic history, showing periods of high inflation and volatile growth in the 1970s-80s, followed by decades of relative stability. This context helps explain why a simple, static relationship does not hold true over the entire period.

---
## 📊 Final Visualization Dashboard

The final output is a 2x2 dashboard that provides a complete visual summary of the analysis.

<img width="1489" height="1189" alt="image" src="https://github.com/user-attachments/assets/72ed1990-5dd6-4de8-b46f-99d8e4236caf" />


1.  **Top-Left (QoQ Scatter Plot):** Shows a diffuse cloud of points, visually confirming the lack of a short-term relationship.
2.  **Top-Right (YoY Scatter Plot):** The relationship remains extremely weak, even when smoothed over an annual period.
3.  **Bottom Panels (Time-Series Plots):** Chart the historical journey of both GDP growth and inflation, highlighting key economic events and periods of volatility.

---
## 🛠️ Methodology and Technical Details

The project was conducted in a Jupyter Notebook using Python and the following core libraries: `pandas` for data manipulation and `matplotlib` for visualization.

#### 1. Data Sourcing and Cleaning
* Data was sourced from Statistics Canada tables for Real GDP (36-10-0104-01) and CPI (18-10-0004-01).
* The most critical data cleaning step involved handling the complex structure of the GDP file. The analysis identified that the file contained multiple metrics, and the correct approach was to isolate the pre-calculated "Percentage change, quarterly" series, rather than calculating it from raw values that had inconsistent units.
* A custom function was developed to handle multiple historical date formats in the CPI data (e.g., `'Jan-62'`, `'01-Jan'`) to create a consistent datetime index.

#### 2. Feature Engineering and Merging
* Monthly CPI data was resampled to a quarterly frequency (`.resample('QE').mean()`) to align with the GDP data.
* The two datasets were merged into a final, analysis-ready DataFrame using a common datetime index.
* Year-over-Year (YoY) metrics were calculated for both inflation (`.pct_change(periods=4)`) and GDP growth (`.rolling(window=4).mean()`) to enable a longer-term perspective.

#### 3. Analysis and Visualization
* Scatter plots were used to visually assess the linear relationship between the variables.
* Time-series plots were used to understand the historical behavior of each metric.
* The Pearson correlation coefficient (`.corr()`) was used to provide a quantitative measure of the strength and direction of the linear relationship.

