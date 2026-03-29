# Rx-Mediplus
# Healthcare Analytics Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=flat&logo=microsoft&logoColor=white)
![Healthcare](https://img.shields.io/badge/Domain-Healthcare-brightgreen?style=flat)
![Dataset](https://img.shields.io/badge/Dataset-1%2C000%20Patients-blue?style=flat)
![Dashboards](https://img.shields.io/badge/Dashboards-4-red?style=flat)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat)

A production-grade Power BI report built on a 1,000-row patient dataset spanning **4 hospital branches** and **8 clinical departments** across FY 2024. The report delivers end-to-end visibility across executive performance, clinical outcomes, financial health, and patient demographics — all within a single `.pbix` file with cross-page slicers and interactive drill-downs.

---

## Key Metrics at a Glance

| Metric | Value |
|---|---|
| Total Patients | 1,000 |
| Total Revenue | ₦2.47M |
| Recovery Rate | 73.7% |
| Collection Rate | 35.8% |
| Average Satisfaction Score | 3.0 / 5 |
| Mortality Rate | 1.6% |
| Pending Revenue | ₦806.3K |
| Surgery Revenue | ₦1.8M |

---

## Dashboard Pages

### 1. Executive Overview
> High-level hospital performance for senior leadership.

- KPI cards: Patients, Revenue, Recovery Rate, Follow-up Rate, Satisfaction, Mortality
- Patients by Department (horizontal bar) with Male/Female toggle
- Patients by Month (area chart) with quarterly filter buttons
- Revenue by Payment Status (Paid / Pending / Insurance Processing)
- Recovery Rate breakdown donut (Recovered · Ongoing · Referred · Deceased)
- **Slicers:** Department · Branch · Age Group

---

### 2. Clinical Outcomes
> Departmental benchmarking of recovery, LOS, and treatment mix.

- Recovery Rate % by Department (horizontal bar)
- Outcome by Department (stacked bar: Deceased / Ongoing / Recovered / Referred)
- % of Patients by Treatment Type donut (Surgery · Therapy · Observation · Medication)
- Summary table: Hospital Dept · Recovery Rate % · Avg LOS · Avg Satisfaction · Total Patients
- **Slicers:** Department · Branch · Gender

---

### 3. Financial Performance
> Revenue streams, cost analysis, and insurance classification.

- Revenue by Hospital Branch (clustered bar) with High Cost / Standard Cost toggle
- Avg Cost per Visit by Treatment Type (Surgery ₦6,392 → Observation ₦343)
- Avg Cost per Visit by Department
- Insurance Type Coverage donut (Private 44.2% · Government 36.5% · Uninsured 19.3%)
- Revenue by Insurance Type (bar chart)
- **Slicers:** Month · Insurance Type · Gender

---

### 4. Patient Demographics
> Age-based segmentation, surgical uptake, and outcome mapping.

- Patients by Age Group (bar chart: Middle-Aged Adults 325 → Adolescents 59)
- Outcome by Age Group (stacked bar)
- % of Patients by Treatment Type (surgical vs non-surgical split: 49.5% / 50.5%)
- Department by Outcome table (Deceased · Ongoing · Recovered · Referred)
- **Slicers:** Department · Branch · Gender

---

## DAX Measures

```dax
-- Recovery Rate
Recovery Rate % =
DIVIDE(
    CALCULATE(COUNTROWS(Patients), Patients[Outcome] = "Recovered"),
    COUNTROWS(Patients),
    0
) * 100

-- Collection Rate
Collection Rate % =
DIVIDE(
    CALCULATE(SUM(Patients[Revenue]), Patients[Payment_Status] = "Paid"),
    SUM(Patients[Revenue]),
    0
) * 100

-- Mortality Rate
Mortality Rate % =
DIVIDE(
    CALCULATE(COUNTROWS(Patients), Patients[Outcome] = "Deceased"),
    COUNTROWS(Patients),
    0
) * 100

-- Average Length of Stay
Avg LOS =
AVERAGE(Patients[Length_of_Stay])

-- Pending Revenue
Pending Revenue =
CALCULATE(
    SUM(Patients[Revenue]),
    Patients[Payment_Status] = "Pending"
)

-- Average Satisfaction Score
Avg Satisfaction =
AVERAGE(Patients[Satisfaction_Score])
```

---

## Dataset Schema

The source dataset (`RX Mediplus.csv`) contains 1,000 rows with the following fields:

| Column | Type | Description |
|---|---|---|
| `PatientID` | Text | Unique patient identifier |
| `Age` | Integer | Patient age |
| `Age_Group` | Text | Middle-Aged Adults / Older Adults / Young Adults / Old / Adolescents |
| `Gender` | Text | Male / Female |
| `Department` | Text | One of 8 clinical departments |
| `Branch` | Text | East / Central / North / West |
| `Admission_Date` | Date | Date of hospital admission |
| `Length_of_Stay` | Integer | Days admitted |
| `Treatment_Type` | Text | Surgery / Therapy / Observation / Medication |
| `Outcome` | Text | Recovered / Ongoing / Referred / Deceased |
| `Revenue` | Float | Billed revenue in NGN |
| `Payment_Status` | Text | Paid / Pending / Insurance Processing |
| `Insurance_Type` | Text | Private / Government / Uninsured |
| `Satisfaction_Score` | Float | 1.0 – 5.0 patient rating |

---

## File Structure

```
Healthcare-Analytics-PowerBI/
├── report/
│   ├── RX Medicareplus.pbix       ← main Power BI report file
├── data/
│   └── RX Medicareplus.csv         ← 1,000-row source dataset
├── docs/
│   ├── RX Medicareplus Report Summary.docx ← full written summary report
│   └── screenshots/
│       ├── 01_executive_overview.png
│       ├── 02_clinical_outcomes.png
│       ├── 03_financial_performance.png
│       └── 04_patient_demographics.png
└── README.md
```

---

## How to Use

1. Clone or download this repository.
2. Open `report/Healthcare_Analytics.pbix` in **Power BI Desktop** (free download from Microsoft).
3. If prompted to locate the data source, point it to `data/healthcare_dataset.csv`.
4. Use the slicers on each page to filter by Department, Branch, Gender, Month, or Age Group.
5. Click any visual to cross-filter all other visuals on the same page.

> **Note:** This report was built and tested on Power BI Desktop (March 2024 release). Some visuals may behave differently on older versions.

---

## Key Findings

- **Gynaecology** leads departmental recovery at **78.99%**; Emergency lags at **69.42%**
- **East Branch** generates the highest revenue (₦648,197); West trails by ₦89,959 (−14%)
- Only **35.8%** of billed revenue has been collected — ₦1.58M+ remains outstanding
- **Surgery** accounts for 28% of treatment types but costs **18.6× more** per visit than Observation
- **Middle-Aged Adults** form the largest patient segment at 32.5% of total admissions
- **Neurology** has the highest patient satisfaction score (3.25) despite a below-average recovery rate

---

## Built With

- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) — report authoring
- DAX — all calculated measures and KPIs
- Microsoft Excel / CSV — data preparation

---

## Author

**Abdulhamid Abdulwalid Danjuma** — Data Analyst  
Built as part of an independent healthcare analytics project.
## Twitter
https://x.com/Aabdul_HameedD

## License

This project is released for educational and portfolio purposes. The dataset is synthetic and contains no real patient information.
