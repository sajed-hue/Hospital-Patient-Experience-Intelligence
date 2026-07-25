# Hospital Patient Experience Intelligence

<p align="center">
  <strong>Exploratory Data Analysis, Opportunity Scoring, and Digital Solution Mapping for 4,792 U.S. Hospitals</strong>
</p>

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/Python-3.9%2B-blue">
  <img alt="Pandas" src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458">
  <img alt="Matplotlib" src="https://img.shields.io/badge/Matplotlib-Visualisation-orange">
  <img alt="Jupyter" src="https://img.shields.io/badge/Jupyter-Notebook-F37626">
  <img alt="Status" src="https://img.shields.io/badge/Status-Completed-success">
</p>

---

## Executive Summary

This project analyses patient-experience data from **4,792 hospitals across the United States** to identify performance gaps, understand the factors most strongly associated with patient recommendations, and prioritise hospitals that may benefit from digital healthcare solutions.

The analysis goes beyond descriptive statistics. It introduces a transparent, correlation-weighted **Technology Opportunity Score** that converts hospital performance gaps into a ranked business-development opportunity list.

### Main conclusions

- **3,176 hospitals** have complete patient-experience records and are included in statistical and opportunity-scoring analysis.
- **1,616 hospitals (33.72%)** are missing one or more patient-experience scores.
- **Discharge information** is the weakest metric nationally, with an average score of approximately **85.66**.
- **Nurse communication** has the strongest relationship with patient recommendation, with a correlation of approximately **0.81**.
- Approximately **29%** of hospitals with complete data underperform across two or more patient-experience drivers.
- Digital discharge and care-transition solutions represent the largest mapped technology opportunity in this dataset.

---

## Table of Contents

- [Business Problem](#business-problem)
- [Project Objectives](#project-objectives)
- [Research Questions](#research-questions)
- [Dataset](#dataset)
- [Data Quality Strategy](#data-quality-strategy)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Technology Opportunity Score](#technology-opportunity-score)
- [Digital Solution Mapping](#digital-solution-mapping)
- [Business Recommendations](#business-recommendations)
- [Project Structure](#project-structure)
- [Installation and Usage](#installation-and-usage)
- [Limitations](#limitations)
- [Future Development](#future-development)
- [Pre-Publication Checklist](#pre-publication-checklist)
- [Author](#author)

---

## Business Problem

Hospitals collect patient-experience survey results, but raw scores alone do not provide a clear decision framework.

Hospital leaders, consultants, and healthcare technology providers still need to determine:

- Which hospitals have the greatest improvement needs.
- Which patient-experience dimensions are underperforming.
- Which performance drivers are most closely associated with patient recommendations.
- Which hospitals need a targeted solution versus a broader engagement platform.
- Which digital solution category best matches each hospital's weakest area.
- Where a healthcare technology provider should prioritise outreach or pilot programmes.

This project transforms survey data into an analytical and commercial prioritisation framework.

---

## Project Objectives

1. Validate the quality and completeness of the hospital dataset.
2. Explore hospital ratings and patient-experience score distributions.
3. Compare hospital performance across states and cities.
4. Measure relationships between experience drivers and patient recommendations.
5. Identify hospitals with multiple low-performing indicators.
6. Build a transparent Technology Opportunity Score.
7. Rank hospitals by potential digital-intervention opportunity.
8. Map each hospital to a recommended digital solution category.
9. Translate analytical results into practical business recommendations.

---

## Research Questions

| # | Research Question |
|---:|---|
| 1 | What is the distribution of overall hospital ratings? |
| 2 | What are the average patient-experience scores? |
| 3 | Which states contain the largest numbers of hospitals? |
| 4 | Which states have the highest and lowest patient recommendation scores? |
| 5 | How strongly is nurse communication associated with patient recommendation? |
| 6 | How strongly is doctor communication associated with patient recommendation? |
| 7 | How strongly is discharge information associated with patient recommendation? |
| 8 | Which metric has the strongest relationship with patient recommendation? |
| 9 | Which hospitals underperform across multiple indicators? |
| 10 | Which hospitals represent the strongest technology opportunities? |
| 11 | Which digital solutions best match the observed performance gaps? |

---

## Dataset

### Dataset summary

| Property | Value |
|---|---:|
| Total hospital records | 4,792 |
| Total columns | 9 |
| Complete patient-experience records | 3,176 |
| Records with missing experience data | 1,616 |
| Missing-data rate | 33.72% |
| Duplicate rows | 0 |
| Duplicate facility IDs | 0 |

### Data dictionary

| Column | Data Type | Description | Expected Range |
|---|---|---|---|
| `facility_id` | String | Unique hospital identifier | Unique |
| `facility_name` | String | Hospital name | — |
| `city` | String | Hospital city | — |
| `state` | String | Two-letter state abbreviation | — |
| `overall_rating` | Numeric | Overall hospital rating | 1–5 |
| `nurse_communication` | Numeric | Positive nurse-communication score | 0–100 |
| `doctor_communication` | Numeric | Positive doctor-communication score | 0–100 |
| `discharge_information` | Numeric | Positive discharge-information score | 0–100 |
| `patient_recommendation` | Numeric | Percentage recommending the hospital | 0–100 |

> **Important:** The official source URL, publication date, and licence are not documented in the current notebook. Add them before publishing the repository.

---

## Data Quality Strategy

The project uses two analytical datasets.

### `clean_df`

Contains all **4,792 hospitals** and is used for analyses that do not require complete patient-experience scores, such as:

- Hospital counts by state.
- Hospital counts by city.
- Geographic coverage.
- Missing-data assessment.

### `experience_df`

Contains the **3,176 hospitals** with complete patient-experience records and is used for:

- Descriptive statistics.
- Correlation analysis.
- Outlier analysis.
- Low-performance classification.
- Technology Opportunity Score.
- Digital solution mapping.

### Missing-value decision

Missing experience scores are not filled with zero or the overall average.

Imputation would introduce unsupported assumptions:

- Filling with zero would incorrectly classify a hospital as an extreme underperformer.
- Filling with a mean would make an unreported hospital appear average.
- Either approach could distort correlations and hospital rankings.

Therefore, incomplete records are retained for geographic analysis and excluded only from calculations that require complete scores.

---

## Methodology

### 1. Data loading

- Loaded the CSV with Pandas.
- Preserved `facility_id` as a string to retain leading zeros.
- Used `pathlib.Path` for a clear and portable file path.

### 2. Initial inspection

Reviewed:

- Shape.
- Column names.
- Data types.
- Sample records.
- Descriptive statistics.
- Unique values.
- Missing values.
- Duplicate rows and identifiers.

### 3. Data cleaning

- Removed duplicate rows where applicable.
- Standardised hospital names, cities, and state abbreviations.
- Converted score columns to numeric values.
- Validated rating and percentage ranges.
- Created a complete-data flag.
- Separated the full geographic dataset from the statistical dataset.

### 4. Exploratory data analysis

The notebook includes:

- Rating-frequency analysis.
- Score histograms.
- Descriptive-statistics tables.
- Hospital counts by state and city.
- State-level patient-recommendation comparisons.
- Scatter plots between experience drivers and patient recommendation.
- Correlation matrix and heatmap.
- IQR-based outlier analysis.

### 5. Reliable state comparison

State averages are calculated only for states with at least **20 reporting hospitals**.

This reduces the risk of ranking states using unstable averages based on very small samples.

### 6. Low-performance classification

For each driver metric, a hospital is flagged as low-performing when its score falls within the bottom national quartile.

The three drivers are:

- Nurse communication.
- Doctor communication.
- Discharge information.

A `low_indicator_count` records whether a hospital underperforms in zero, one, two, or all three areas.

### 7. Opportunity scoring

Each hospital's performance gap is weighted by the corresponding metric's relationship with patient recommendation.

### 8. Solution mapping

The weakest patient-experience driver determines the most relevant digital solution category.

---

## Key Findings

### Overall rating distribution

Hospital ratings are concentrated in the middle of the 1–5 scale.

| Overall Rating | Hospitals |
|---:|---:|
| 1 | 51 |
| 2 | 501 |
| 3 | 1,344 |
| 4 | 1,037 |
| 5 | 243 |

A rating of **3** is the most common, followed by a rating of **4**.

### Average patient-experience performance

| Metric | Mean Score |
|---|---:|
| Nurse communication | 91.24 |
| Doctor communication | 90.67 |
| Patient recommendation | 86.96 |
| Discharge information | 85.66 |

**Discharge information is the weakest national performance area.**

### Geographic concentration

The states containing the largest numbers of hospitals are:

| Rank | State | Hospitals |
|---:|---|---:|
| 1 | Texas | 406 |
| 2 | California | 338 |
| 3 | Florida | 191 |
| 4 | Illinois | 177 |
| 5 | Ohio | 164 |

### State-level patient recommendation

Among states with at least 20 reporting hospitals:

| Highest-Performing States | Average Score |
|---|---:|
| Nebraska | 89.57 |
| Wisconsin | 89.57 |
| Utah | 89.56 |

| Lowest-Performing States | Average Score |
|---|---:|
| New York | 84.34 |
| New Mexico | 84.46 |
| New Jersey | 84.48 |

### Relationship with patient recommendation

| Driver | Pearson Correlation |
|---|---:|
| Nurse communication | 0.81 |
| Doctor communication | 0.75 |
| Discharge information | 0.71 |

All three relationships are positive and strong.

Nurse communication is the strongest patient-experience driver among the three analysed components.

### Multi-indicator underperformance

| Low-Performing Indicators | Hospitals |
|---:|---:|
| 0 | 1,733 |
| 1 | 527 |
| 2 | 417 |
| 3 | 499 |

A total of **916 hospitals** underperform across two or three indicators.

This represents approximately **28.8%** of hospitals with complete experience data.

### Outlier analysis

| Metric | Outliers | Percentage |
|---|---:|---:|
| Overall rating | 51 | 1.61% |
| Nurse communication | 91 | 2.87% |
| Doctor communication | 86 | 2.71% |
| Discharge information | 61 | 1.92% |
| Patient recommendation | 49 | 1.54% |

Outliers were retained because the low-end observations are directly relevant to identifying underperforming hospitals.

---

## Technology Opportunity Score

The Technology Opportunity Score ranks hospitals by combining:

1. The size of each hospital's performance gap.
2. The relative importance of each driver to patient recommendation.

### Step 1: Calculate the performance gap

```text
Performance Gap = 100 - Hospital Score
```

### Step 2: Normalise correlation-based weights

| Driver | Approximate Weight |
|---|---:|
| Nurse communication | 0.36 |
| Doctor communication | 0.33 |
| Discharge information | 0.31 |

### Step 3: Calculate the composite score

```text
Technology Opportunity Score =
    0.36 × (100 - Nurse Communication)
  + 0.33 × (100 - Doctor Communication)
  + 0.31 × (100 - Discharge Information)
```

### Interpretation

- A **higher score** indicates greater underperformance across important patient-experience drivers.
- A **lower score** indicates stronger performance and less immediate improvement opportunity.
- The score is designed for prioritisation, not as proof that a digital product will produce a specific outcome.

### Why this score is stronger than a simple average

A simple average treats every metric as equally important.

This model assigns more weight to metrics that show a stronger relationship with patient recommendation, producing a more business-relevant ranking.

---

## Digital Solution Mapping

Each hospital is mapped to a digital solution using its weakest experience driver.

| Weakest Driver | Recommended Digital Solution |
|---|---|
| Nurse communication | Real-time nurse rounding and bedside communication application |
| Doctor communication | Physician messaging and telehealth follow-up platform |
| Discharge information | Digital discharge-instructions and care-transition application |

### Estimated national demand by solution category

| Recommended Solution | Hospitals |
|---|---:|
| Digital discharge-instructions application | 3,045 |
| Physician messaging or telehealth platform | 102 |
| Nurse rounding and communication application | 29 |

### Interpretation

Discharge information is the weakest driver for the overwhelming majority of hospitals in the complete-data sample.

This suggests that digital discharge instructions, medication guidance, follow-up reminders, multilingual content, and care-transition support may represent the broadest technology opportunity.

However, the result should not be interpreted as a final market-size estimate because the dataset does not include:

- Hospital budgets.
- Technology maturity.
- Existing vendors.
- Procurement readiness.
- Hospital size.
- Annual patient volume.
- Ownership structure.

---

## Business Recommendations

### Priority 1: Target high-opportunity hospitals

Begin with hospitals that combine:

- A high Technology Opportunity Score.
- Low patient recommendation.
- Two or three low-performing indicators.
- Sufficient data completeness.

These hospitals have the clearest analytical case for intervention.

### Priority 2: Lead with discharge and care-transition solutions

Because discharge information is the most frequent weak point, the strongest initial product concept is a digital discharge platform containing:

- Personalised discharge instructions.
- Medication reminders.
- Follow-up appointment reminders.
- Multilingual patient education.
- Symptom and recovery guidance.
- Escalation instructions.
- Post-discharge feedback collection.

### Priority 3: Segment hospitals by intervention type

| Hospital Profile | Recommended Approach |
|---|---|
| One weak indicator | Targeted single-purpose solution |
| Two weak indicators | Integrated communication workflow |
| Three weak indicators | Broad patient-engagement platform |
| High scores across all indicators | Lower-priority sales prospect or benchmarking partner |

### Priority 4: Enrich the opportunity list

Before starting outreach, add:

- Hospital size.
- Ownership type.
- Estimated revenue.
- Number of beds.
- Patient volume.
- Current digital tools.
- Decision-maker contacts.
- Procurement status.
- Geographic sales priority.

This converts the analytical ranking into a qualified lead-generation dataset.

### Priority 5: Validate with pilots

The score should be tested through pilot projects.

A useful pilot should measure:

- Change in patient recommendation.
- Change in discharge-information score.
- Follow-up completion.
- Readmission-related indicators where available.
- Patient engagement.
- Staff adoption.
- Cost of implementation.
- Return on investment.

---

## Project Structure

```text
hospital-patient-experience-intelligence/
│
├── Project.ipynb
├── hospital dataset.csv
├── README.md
├── requirements.txt
├── data/
│   ├── raw/
│   └── processed/
├── outputs/
│   ├── figures/
│   └── tables/
└── src/
    └── analysis.py
```

### Current minimum structure

```text
├── Project.ipynb
├── hospital dataset.csv
└── README.md
```

---

## Installation and Usage

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd hospital-patient-experience-intelligence
```

### 2. Create a virtual environment

#### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

#### macOS or Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install pandas numpy matplotlib jupyter ipykernel
```

Or install from `requirements.txt`:

```bash
pip install -r requirements.txt
```

### 4. Launch the notebook

```bash
jupyter notebook Project.ipynb
```

Run the cells from top to bottom.

### 5. Optional reproducibility command

```bash
jupyter nbconvert --to notebook --execute Project.ipynb --output Project_executed.ipynb
```

---

## Requirements

Recommended environment:

- Python 3.9+
- pandas
- numpy
- matplotlib
- jupyter
- ipykernel

Generate exact installed versions using:

```bash
pip freeze > requirements.txt
```

---

## Limitations

1. **Correlation does not establish causation.**  
   Strong relationships do not prove that improving a specific metric will directly increase recommendations.

2. **Missing data may not be random.**  
   Hospitals without reported scores may differ systematically from reporting hospitals.

3. **The opportunity score is a heuristic.**  
   It is a transparent prioritisation model, not a validated predictive or causal model.

4. **The model does not include commercial readiness.**  
   A hospital with a high analytical score may not have the budget or operational readiness to purchase a solution.

5. **The solution mapping uses the weakest metric only.**  
   Some hospitals may require a combined intervention.

6. **State averages hide hospital-level variation.**  
   Geographic comparisons should not replace hospital-specific evaluation.

7. **No temporal analysis is included.**  
   The current notebook analyses one dataset snapshot rather than changes over time.

8. **The official dataset source is not documented.**  
   Source, date, and licence must be added before public publication.

---

## Future Development

- Build an interactive Streamlit or Power BI dashboard.
- Export the full ranked hospital opportunity table.
- Add a map of hospital opportunity scores.
- Analyse year-over-year changes.
- Add hospital ownership and bed-count information.
- Build hospital segments using clustering.
- Develop a predictive model for patient recommendation.
- Compare rural and urban hospitals.
- Add confidence intervals to state comparisons.
- Integrate public contact and procurement data.
- Create a lead-scoring pipeline combining analytical need and commercial readiness.
- Validate the Technology Opportunity Score using pilot outcomes.

---

## Pre-Publication Checklist

Before publishing the repository:

- [ ] Rename the CSV file to exactly `hospital dataset.csv`, or update the notebook path.
- [ ] Add the official dataset source URL.
- [ ] Add the dataset publication date and licence.
- [ ] Replace the duplicated nurse-communication visual with the intended discharge-information analysis.
- [ ] Revise the outdated notebook text stating that opportunity scoring is outside the project scope.
- [ ] Export important charts into an `outputs/figures` folder.
- [ ] Export the ranked opportunity table into `outputs/tables`.
- [ ] Create `requirements.txt`.
- [ ] Clear unnecessary notebook outputs or re-run the notebook from top to bottom.
- [ ] Add a repository screenshot or dashboard preview.
- [ ] Add an appropriate project licence.
- [ ] Replace `<your-repository-url>` with the real GitHub URL.

---

## Suggested Repository Description

> Exploratory analysis of patient-experience data from 4,792 U.S. hospitals, including correlation analysis, hospital opportunity scoring, and digital healthcare solution mapping.

---

## Suggested GitHub Topics

```text
data-analysis
exploratory-data-analysis
healthcare-analytics
patient-experience
python
pandas
matplotlib
jupyter-notebook
healthtech
market-analysis
lead-generation
```

---

## Author

**Sajed Kittaneh**

Data Analysis · Healthcare Analytics · Technology Opportunity Research

---

## Licence

Add the selected licence before publishing.

For an educational and portfolio project, the **MIT Licence** is a common option for code.  
Dataset usage must follow the original dataset's licence and terms.
