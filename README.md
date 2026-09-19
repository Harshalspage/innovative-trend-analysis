🌍 Climate Trend Analysis: ITA, Mann-Kendall, and Sen's Slope


📖 Overview

This project applies Innovative Trend Analysis (ITA) and its branches to study long-term climate datasets, including precipitation and water levels. Unlike conventional trend analysis methods, ITA captures subtle patterns, detects structural shifts, and projects future trends, offering deeper insights into climate impacts.

The repository contains R scripts to process raw climate data, run statistical hypothesis testing, and generate visualizations comparing linear regression with robust non-parametric trend estimators.

✨ Key Features

Data Preprocessing: Handles long-format climate data, cleans year formats, and aggregates mean anomalies.

Baseline Adjustment: Adjusts temperature anomalies relative to a historical baseline (1961–1990) for accurate comparison.

Statistical Trend Testing: Implements the Mann-Kendall test to detect monotonic trends in time-series data.

Robust Slope Estimation: Utilizes Sen's Slope estimator to calculate the magnitude of trends, resisting outliers.

Innovative Trend Analysis (ITA): Segments data into halves to visualize sub-trends and shifts that traditional linear regression might miss.

Data Visualization: Generates publication-ready plots using ggplot2 and base R, overlaying linear regression and Sen's slope.

🛠️ Technologies Used

Language: R

Core Packages:

tidyverse (Data manipulation and ggplot2 visualization)

Kendall (Mann-Kendall trend test)

zyp (Sen's Slope estimator)

readr (Data ingestion)

📂 Project Structure
------- 0) Packages ----------.txt: The core R script containing the analysis pipeline.

long_format_annual_surface_temp.csv: The input dataset (Annual Surface Temperature).

README.md: Project documentation.

🚀 Getting Started

Prerequisites
Ensure you have R installed. The script will automatically install missing packages, but you can also install them manually:

R

install.packages(c("tidyverse", "Kendall", "zyp"))
Running the Analysis
Clone the repository to your local machine.

Place your dataset in the expected directory or update the csv_path variable in the script.

R

csv_path <- "path/to/your/long_format_annual_surface_temp.csv"
Run the R script (------- 0) Packages ----------.txt or rename to .R).

🔬 Methodology Breakdown

The analysis pipeline follows these steps:

Data Loading & Cleaning: Imports the CSV, extracts numeric years, and calculates mean annual anomalies.

Filtering & Baseline: Filters data between 1961 and 2022, then calculates anomalies relative to the 1961–1990 baseline.

Mann-Kendall Test: Runs a non-parametric test to determine if there is a statistically significant monotonic trend (increasing or decreasing).

Sen's Slope Estimation: Calculates the median slope of the data to estimate the rate of change per year.

Innovative Trend Analysis (ITA): Splits the time series into two halves (first half vs. second half) and plots them against each other. This reveals sub-trends, shift points, and non-linear patterns.

Visualization:

Plots the raw anomaly time series.

Overlays a linear regression line (Red).

Overlays the Sen's slope line (Green dashed).

Generates an ITA scatter plot with a 1:1 reference line to identify low, medium, and high-value trends.

📊 Key Insights

By applying ITA alongside traditional methods, this project successfully:

Detected subtle climatic shifts that conventional linear regression smoothed over.

Projected future trends with higher confidence by analyzing sub-period behaviors.

Offered a more nuanced understanding of climate impacts on precipitation and water levels.

👤 Author

Harshal Shirsat

LinkedIn: linkedin.com/in/harshal_shirsat

GitHub: github.com/Harshalspage

📄 License

This project is open-source and available under the MIT License.

