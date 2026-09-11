# Healthcare Patient Tracking Analysis – Power BI

## Aim

To analyze healthcare patient tracking data using Power BI and develop an interactive dashboard for monitoring patient status, stay duration, insurance, extensions, and authorization details.

## Procedure

1. Imported the healthcare patient tracking dataset from Excel into Power BI.
2. Cleaned and transformed the data using Power Query.
3. Removed unnecessary blank columns and unwanted blank records.
4. Trimmed spaces from text fields and verified appropriate data types.
5. Created DAX calculations for patient count, actual stay, expected stay, stay variance, and discharge variance.
6. Analyzed patient status, insurance, extension, and authorization information.
7. Identified relationships between insurance and patient status, and between extension and authorization.
8. Created charts, KPI cards, a matrix, table, and date slicer.
9. Designed an interactive one-page healthcare tracking dashboard.
10. Derived key insights and recommendations from the analysis.

## DAX Measures and Calculations

### Total Patients

```
Total Patients =
COUNTROWS('Healthcare Patients')
```
## Active Patients
```
Active Patients =
CALCULATE(
    [Total Patients],
    'Healthcare Patients'[Status] = "Active"
)
```
## Discharged Patients
```
Discharged Patients =
CALCULATE(
    [Total Patients],
    'Healthcare Patients'[Status] = "Discharged"
)
```
## Pending Extension
```
Pending Extension =
CALCULATE(
    [Total Patients],
    'Healthcare Patients'[Status] = "Pending Extension"
)
```
## Actual Stay Days
```
Actual Stay Days =
IF(
    ISBLANK('Healthcare Patients'[Actual Discharge Date]),
    BLANK(),
    DATEDIFF(
        'Healthcare Patients'[Admission Date],
        'Healthcare Patients'[Actual Discharge Date],
        DAY
    )
)
```
## Expected Stay Days
```
Expected Stay Days =
IF(
    ISBLANK('Healthcare Patients'[Admission Date]) ||
    ISBLANK('Healthcare Patients'[Estimated Discharge]),
    BLANK(),
    DATEDIFF(
        'Healthcare Patients'[Admission Date],
        'Healthcare Patients'[Estimated Discharge],
        DAY
    )
)
```
## Stay Variance
```
Stay Variance =
IF(
    ISBLANK('Healthcare Patients'[Actual Stay Days]),
    BLANK(),
    'Healthcare Patients'[Actual Stay Days]
        - 'Healthcare Patients'[Days Approved]
)
```
## Discharge Variance
```
Discharge Variance =
IF(
    ISBLANK('Healthcare Patients'[Actual Discharge Date]),
    BLANK(),
    DATEDIFF(
        'Healthcare Patients'[Estimated Discharge],
        'Healthcare Patients'[Actual Discharge Date],
        DAY
    )
)
```

## Dashboard Visuals
* **Total Patients** – KPI Card
* **Active Patients** – KPI Card
* **Discharged Patients** – KPI Card
* **Pending Extension** – KPI Card
* **Patient Status Distribution** – Donut Chart
* **Patient Distribution by Insurance** – Bar Chart
* **Patient Extension Status** – Column Chart
* **Patient Authorization Status** – Column Chart
* **Insurance vs Patient Status** – Stacked Column Chart
* **Extension vs Authorization Status** – Matrix
* **Actual Stay Days by Patient** – Column Chart
* **Admission Date** – Slicer

# An interactive Power BI dashboard was created to provide a consolidated view of healthcare patient tracking information.

| Metric | Result |
| :--- | :--- |
| Total Patients | 46 |
| Active Patients | 28 |
| Discharged Patients | 10 |
| Pending Extension | 8 |
| Highest Insurance | Aetna – 9 patients |
| Longest Actual Stay | 34 days |
## Key Insights
* **Patient Distribution:** Active patients constitute the largest group, accounting for 28 of the 46 total patients.
* **Status Breakdown:** 10 patients are currently discharged, while 8 remain in "Pending Extension" status.
* **Insurance Trends:** Aetna represents the highest patient volume, covering 9 patients.
* **Stay Duration:** Analysis reveals that several discharged patients remained hospitalized beyond their estimated discharge dates.
* **Operational Focus:** Monitoring extension and authorization statuses is essential to identify cases requiring immediate administrative follow-up.
## Recommendations
Monitor patients approaching or exceeding their approved stay duration for timely extension and authorization follow-up.
Use the dashboard to support discharge planning and identify patients requiring insurance or authorization attention.
## Tools Used
* **Power BI:** Data visualization and dashboard creation.
* **Power Query:** Data cleaning, transformation, and preparation.
* **DAX:** Calculated measures and metrics for performance analysis.
* **Microsoft Excel:** Source data management.

## Dashboard 
<img width="837" height="628" alt="Screenshot 2026-09-11 165112" src="https://github.com/user-attachments/assets/9459e17c-8765-487b-b0cd-d49e5d42a66f" />


## Result

The healthcare patient tracking data was successfully cleaned, analyzed, and visualized in Power BI. The resulting dashboard provides an interactive view of patient status, insurance, stay duration, extensions, and authorization information.
