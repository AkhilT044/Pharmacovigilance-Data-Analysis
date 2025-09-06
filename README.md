# Analysis of Drug Safety Signals in FAERS Data

[](https://www.python.org/downloads/)
[](https://opensource.org/licenses/MIT)

This project presents a comprehensive data analysis of the FDA's Adverse Event Reporting System (FAERS) to identify potential drug safety signals. The goal is to evaluate unusual or disproportionately reported drug-adverse event combinations that may indicate safety concerns.

## Project Objective

To develop a reproducible **workflow** that ingests and cleans raw FAERS data, applies robust statistical methods to identify disproportionate reporting signals, and presents the findings through clear visualizations and a prioritized, actionable report.

## 📈 Business Value

In the pharmaceutical industry, post-market drug safety surveillance is critical for patient health and regulatory compliance. This analysis provides direct value by:

  * **Enabling Proactive Insights:** Enables a shift from reactive to proactive analysis by systematically flagging potential safety concerns early.
  * **Prioritizing Resources:** Helps pharmacovigilance teams focus their limited time and resources on the most statistically significant signals.
  * **Supporting Data-Driven Decisions:** Provides objective, statistical evidence to support decisions on whether a deeper clinical investigation into a drug-event pair is warranted.

## 💾 Data Source and Acquisition

This project analyzes data from the FDA's Adverse Event Reporting System (FAERS). There are two primary methods for acquiring this data:

### 1\. FAERS Quarterly Data Files (Method Used in this Project)

This analysis is built on the bulk ASCII data files provided directly by the FDA. These files contain the complete dataset for a given quarter.

  * **Advantage:** Access to the complete, comprehensive dataset, ideal for deep historical analysis.
  * **Source:** [FAERS Quarterly Data Extract Files](https://fis.fda.gov/extensions/FPD-QDE-FAERS/FPD-QDE-FAERS.html)

### 2\. openFDA API (Alternative Method)

An alternative approach is to use the openFDA API, which provides a more accessible, real-time way to query the data.

  * **Advantage:** Excellent for rapid prototyping, fetching smaller samples of recent data, or for applications that require live data without the overhead of downloading and parsing large files.
  * **Data Format:** The API returns data in JSON format.
  * **Source:** [openFDA Drug Event API Documentation](https://open.fda.gov/apis/drug/event/)

## 🔬 Key Methodologies & Concepts Explained

This analysis is built on established principles of pharmacovigilance. Here are the core concepts explained simply:

### What is Pharmacovigilance?

Pharmacovigilance is the science and activities relating to the detection, assessment, understanding, and prevention of adverse effects or any other drug-related problem. Essentially, it's about monitoring a drug's safety once it's on the market and being used by the general population.

### What is Disproportionality Analysis?

This is the core statistical method used in the project. Since we don't know the total number of people taking each drug, we can't calculate true risk. Instead, we look for **disproportionality**.

**Analogy:** Imagine a giant database of patient side effect reports. If "headaches" make up 1% of all reports for all drugs, but they make up 20% of all reports for "Drug X", we would say headaches are **disproportionately reported** for Drug X. This doesn't prove Drug X *causes* headaches, but it generates a strong statistical signal that it's worth investigating.

### Key Metrics Used

1.  **Proportional Reporting Ratio (PRR):** The most intuitive metric. It's a simple ratio comparing the reporting rate of an event for a specific drug to the reporting rate of that same event for all other drugs. A PRR \> 2 is often considered a potential signal.

2.  **Empirical Bayes Geometric Mean (EBGM):** A more advanced and robust metric. Its key advantage is **shrinkage**. It adjusts the signal score based on the number of reports, "shrinking" the scores of signals with very little evidence towards the average. This helps reduce false alarms from random noise and increases our confidence in the signals we do find. We use the **EB05 score**, the lower bound of a 90% confidence interval, to flag our most credible signals.

## ⚙️ The Analytical Workflow

The project is broken down into a clear, reproducible workflow managed across several Jupyter Notebooks:

1.  **Data Ingestion & Cleaning (`01_ingest_and_clean.ipynb`):** Raw ASCII text files from a FAERS quarterly release are ingested, merged, and cleaned. The output is a set of analysis-ready Parquet files.
2.  **Statistical Analysis (`02_disproportionality_PRR_EB.ipynb`):** The clean data is transformed into a contingency table format. PRR and robust EBGM/EB05 scores are calculated for every drug-event pair.
3.  **Reporting & Visualization (`03_eda_and_report.ipynb`):** The final, scored results are used to generate key visualizations and a deep-dive analysis of the top-ranked safety signal.

## 📊 Key Results & Visualizations

The analysis provides both a high-level overview of the data and a specific, prioritized list of signals.

### 1\. Overall Data Context

First, we establish a baseline by looking at the most frequently reported drugs and adverse events in the dataset. This helps contextualize the signals we find later.

> *Caption: This chart shows the drugs with the most unique adverse event reports. The list is typically dominated by widely prescribed medications, which provides a baseline for reporting volume.*

> *Caption: This chart shows the most common adverse events reported across all drugs. These often include general symptoms like headache and nausea, representing the "background noise" of the dataset.*

### 2\. The Signal Landscape: Volcano Plot

This is the primary visualization for our results. It allows us to see all drug-event pairs at once, plotting their **statistical significance (Y-axis)** against their **signal strength (X-axis)**. The most compelling signals are in the **top-right quadrant**.

> *Caption: Each dot is a unique drug-event pair. The red dots are signals flagged as statistically robust (EB05 \>= 2). Our focus for investigation is on the signals that are furthest to the top and right.*

### 3\. Deep Dive on the Top Signal

After identifying the most robust signal from the Volcano Plot, we perform a deep dive to profile the reports that generated it. For this analysis, our top signal was **[Drug Name]** and **[Adverse Event]**.

**Reports by Country (Top 10)**
| Country | NumberOfReports |
| :--- | :--- |
| UNITED STATES | 152 |
| CANADA | 25 |
| UNITED KINGDOM | 18 |
| GERMANY | 12 |
| ... | ... |

**Reports by Age Group**
| AgeGroup | NumberOfReports |
| :--- | :--- |
| 65+ (Elderly) | 110 |
| 45-64 (Adult) | 85 |
| 18-44 (Adult) | 22 |
| 0-17 (Child/Adolescent) | 3 |

**Reports by Month (for the Quarter)**
| Month | NumberOfReports |
| :--- | :--- |
| 2024-01 | 75 |
| 2024-02 | 81 |
| 2024-03 | 94 |

**Insight Summary:** Our deep dive into the top signal reveals a distinct pattern. The reports are predominantly from the **United States**, heavily concentrated in the **65+ (Elderly)** demographic, and reporting showed a slight **upward trend** during the quarter. This provides a clear profile for a clinical review team to begin their investigation.

## 📁 Project Structure

```
pharma-signal-analysis/
├── data/
│   ├── raw/
        └── faers_ascii_2024q4
            └── ASCII
                ├── DEMO24Q4
                ├── DRUG24Q4
                └── REAC24Q4
│   └── processed/    # Cleaned, processed Parquet files (Files in this folder created after you run the given python code in notebook)
├── notebooks/
│   ├── 01_ingest_and_clean.ipynb
│   ├── 02_disproportionality_PRR_EB.ipynb
│   ├── 03_eda_and_report.ipynb
│   ├── top_drugs_barchart.png
│   ├── top_events_barchart.png
│   └── volcano_plot.png

faers_ascii_2024q4
## 🚀 How to Reproduce

1.  Clone the repository: `git clone [URL]`
2.  Create a Python virtual environment: `python -m venv venv` and `source venv/bin/activate`
3.  Install the required packages: `pip install -r requirements.txt`
4.  Download the desired FAERS quarterly data (ASCII files) and place them in the `data/raw/` directory.
5.  Run the Jupyter notebooks in numerical order.

## ⚠️ Limitations & Future Work

  * **Limitations**:

      * **Correlation is not Causation**: This analysis identifies statistical associations, not confirmed causal links.
      * **Reporting Biases**: The data is subject to under-reporting (many AEs are never reported) and stimulated reporting (e.g., media attention can cause a spike in reports).
      * **Confounding Factors**: The analysis does not fully control for factors like the underlying disease (**confounding by indication**).

  * **Future Work & Potential Data Science Extensions**:
    The current analysis provides a robust foundation. Future work could extend this project into the **data science** realm by:

      * **MedDRA SOC Mapping**: Integrating a MedDRA dictionary to analyze signals at the System Organ Class level.
      * **Time Series Forecasting**: Processing multiple quarters of data to build predictive models for signal trends.
      * **NLP on Narratives**: Using Natural Language Processing to extract richer context from the free-text narratives included in the case reports.
