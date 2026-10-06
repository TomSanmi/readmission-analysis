# readmission-analysis
Analysis of 101,766 hospital encounters to identify 30-day readmission risk factors
## The Question

Which patient groups are most likely to be readmitted within 30 days, and what factors seem to matter most?

This matters because a readmission within 30 days usually signals one of three things: the first treatment didn't fully work, the patient wasn't ready to go home, or follow-up care failed. Hospitals are financially penalised for high readmission rates, and patients experience worse outcomes when they return.

---

## The Data

Source: Diabetes 130-US Hospitals for Years 1999–2008 (Strack et al., BioMed Research International, 2014).

· 101,766 hospital encounters across 130 US hospitals
· 50 columns of patient demographics, admission details, diagnoses, and medications
· Filtered to encounters where: the patient was diabetic, the stay was 1–14 days, lab tests were performed, and medications were administered

This is not "all diabetic patients", it's a specific slice of diabetic hospital care.

---

## Method

1. I First looked (before building anything):

· How many rows and columns?
· What do the headers actually mean?
· What values does the target column (readmitted) contain?
· Which columns are mostly empty?
· Any weird formatting?

2. Cleaning:

· Dropped three columns with 40%+ missing values (weight, payer_code, medical_specialty)
· Relabeled ? (the dataset's missing-value marker) to Unknown in race and diag_1/2/3

3. Variable selection — each column had to pass three filters:

· Is it related to the outcome?
· Is it complete enough to use?
· Is it actionable?

4. Analysis:

· Built PivotTables on each candidate variable against readmitted
· Used % of Row Total to compute readmission rates (not raw counts)
· Ranked findings by strength of pattern

---

## Insight

Prior inpatient visits are the strongest predictor of 30-day readmission.

Risk climbed from 8.44% (0 prior visits) to 31.40% (5 prior visits) — a nearly 4× increase.

Prior healthcare utilisation predicts readmission better than any demographic or treatment variable in this dataset.

---

## Supporting Findings

1. Prior ED visits
Readmission risk climbed from 10.47% (0 visits) to 30.75% (4 visits) — a ~3× increase.

2. Number of diagnoses
Risk roughly doubles from 5.94% (1 diagnosis) to 12.38% (9 diagnoses).

3. Length of stay
Risk climbed from 8.18% (1-day stay) to 14.23% (8-day stay), then plateaued.

4. Variables with no effect
Age, gender, medication change, insulin status, and number of procedures showed weak or no relationship with readmission.

---

## Recommendation

Hospitals should target follow-up resources such as discharge calls, medication reviews, home visits — at patients with multiple prior admissions and/or prior ED visits. These groups have the highest measurable risk, and are the ones most likely to benefit from intervention.

---

## Limitations


· Sample bias correction: An early 10,000-row sample suggested a clean age trend that disappeared on the full dataset. Findings are based on the full 101,766 encounters after this correction.

· Small groups in the tails: Beyond 5 prior visits or 9 diagnoses, group sizes drop below 500. Rates there are unreliable. Analysis is limited to where the data is solid.

· Correlation, not causation: Longer stays and prior visits don't cause readmission. They signal sicker patients.


· Filtered population: The dataset only includes diabetics with 1–14 day stays, lab tests, and medications. Findings may not apply to other patient groups.


· Old, US-only data: 1999–2008, 130 American hospitals. Patterns may differ in other regions or in modern practice. 


---

## Tools

· Excel (PivotTables, KPI formulas, dashboard design)

---

## Files

- `README.md` — this document
- `Dashboard.png` — final dashboard screenshot
- [Full Excel workbook (v1.0 release)](https://github.com/TomSanmi/readmission-analysis/releases/tag/v1.0)
-  — includes raw data, pivot analysis, KPI formulas, and dashboard


