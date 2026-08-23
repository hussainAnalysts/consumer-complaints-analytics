# Background & Overview
<img width="1160" height="644" alt="image" src="https://github.com/user-attachments/assets/5f04f05a-e1b2-47af-8894-63e0fb15f702" />

This project provides an enterprise-grade operational analytics engine built to audit customer grievance pipeline performance, regulatory compliance risks, and monetary remediation trends for retail banking operations. Operating within the consumer financial services domain, financial institutions face stringent regulatory oversight from bodies like the Consumer Financial Protection Bureau (CFPB), where failing to respond to grievances within mandatory 15-day Statutory Service Level Agreements (SLAs) triggers regulatory scrutiny, reputational exposure, and civil money penalties.

This project addresses a critical operational friction point: evaluating the structural efficiency of customer complaint processing pipelines, identifying product-level bottleneck drivers, and quantifying the financial impact of SLA non-compliance across **62,516 historical complaint records**. Engineered in alignment with Big 4 advisory standards and Microsoft Excel Financial Modeling guidelines, the underlying workbook integrates a Power Query ETL pipeline, a star-schema Power Pivot Data Model, and DAX measure engines to empower Compliance, Risk, Operations, and Executive Leadership teams.

---

## Data Structure Overview

The underlying dataset is transformed through Power Query into an analytical star-schema Data Model within Power Pivot, isolating raw transaction records from dynamic calculation dimensions.

---

## Executive Summary
An analysis of **62,516 CFPB consumer complaint records** demonstrates strong macro performance with a **93.77% Response Rate** and an average ingestion lag of **1.22 days**. Digital self-service serves as the primary intake backbone, with **Web submissions dominating total intake volume**. However, operational deep-dives reveal critical seasonality and regional compliance vulnerabilities: complaint volume peaks significantly during **July (6.5K complaints)**, while regional untimely rates surge as high as **5.38% in Indiana (IN)** and **5.16% in Oregon (OR)**. Furthermore, product concentration remains heavily weighted toward core retail banking, with **Checking/Savings (24,814 complaints)** and **Credit Cards (16,197 complaints)** accounting for over **65% of total enterprise volume**.


---

## Insights Deep Dive

### 1. Seasonal Volume Surges & Operational Lag
<img width="382" height="226" alt="image" src="https://github.com/user-attachments/assets/3bb8b0b5-3351-4a73-8180-c93045498c82" />

Complaint processing exhibits distinct mid-year seasonality. Volume builds steadily through Q2, surging to an annual peak of **6.5K complaints in July**—a **41.3% increase** over the February trough (**4.6K complaints**). Average processing lag across all channels remains tight at **1.22 days**, driven by high digital submission rates via Web and Mobile intake. However, during the Q3 volume surge (July–August), processing backlogs expand, contributing directly to elevated untimely breach rates in subsequent operational windows.

* **Annual Volume Peak**: $6.5\text{K}$ complaints (July)
* **Annual Volume Trough**: $4.6\text{K}$ complaints (February)
* **Average Enterprise Processing Lag**: $1.22\text{ days}$

### 2. Geographic Compliance Disparities (State-Level SLA Breaches)
<img width="329" height="512" alt="image" src="https://github.com/user-attachments/assets/e44caf85-16fd-4d3d-baa2-2a7c3a238bc3" />

Regional analysis indicates substantial variance in timely response rates across jurisdictions. While overall timely response rates range between **90.91% and 95.04%** across states, key markets experience disproportionately high untimely response rates:
* **Indiana (IN)**: Registers the highest untimely response rate at **5.38%**, significantly above the portfolio baseline.
* **Iowa (IA) & Oregon (OR)**: Follow closely with untimely failure rates of **5.19%** and **5.16%**, respectively.
* **High-Volume Markets**: Major state jurisdictions such as **Pennsylvania (PA - 4.59%)**, **New York (NY - 4.46%)**, and **California (CA - 4.37%)** maintain elevated failure rates that represent large absolute breach volumes due to high underlying population density.

### 3. Product Breakdown & Resolution Pathways
<img width="306" height="341" alt="image" src="https://github.com/user-attachments/assets/1097839d-27cc-4b63-a5cd-a48d4cefb7d5" />

Product volume remains heavily concentrated in retail banking lines. **Checking or savings accounts** account for **24,814 complaints**, followed by **Credit cards (16,197)**, **Credit reporting (7,710)**, and **Mortgages (6,601)**. When examining resolution pathways across the enterprise:

<img width="376" height="333" alt="image" src="https://github.com/user-attachments/assets/673857e4-2c82-4b6e-a088-5a6379962cb4" />

* **Closed with explanation**: Serves as the primary resolution path, covering **41,044 cases (65.65%)**.
* **Closed with monetary relief**: Represents direct financial settlement in **14,697 cases (23.51%)**.
* **Closed with non-monetary relief**: Accounts for **5,273 cases (8.43%)**.
* **In progress / Closed**: Active investigations account for **1,494 cases (2.39%)**, with administrative closures at **8 cases (0.01%)**.

---

## Recommendations & Actionable Next Steps

1. **Deploy Dynamic Capacity Planning for Q3 Volume Surges**: Cross-functional Operations and Workforce Management teams must implement seasonal staffing adjustments ahead of the June–August peak. Reallocating compliance case managers during Q3 will mitigate processing backlogs and prevent the July volume spike (**6.5K cases**) from triggering SLA breaches.
2. **Institute Target Regional Taskforces in High-Risk States**: Operational Risk and Compliance leadership should establish localized taskforces in **Indiana (5.38% untimely)**, **Iowa (5.19%)**, and **Oregon (5.16%)**. Investigating local state-level operational bottlenecks will reduce geographic regulatory exposure.
3. **Automate Triage for Checking & Credit Card Disputes**: Given that **Checking/Savings (24.8K)** and **Credit Cards (16.2K)** comprise over **65% of enterprise complaint volume**, Information Technology and Operations teams should implement automated keyword-based triage and decision trees in Power Query/Power Automate to route high-frequency issues directly to specialized resolution teams.

---

## Data Caveats, Assumptions & Limitations

To ensure transparency and maintain model auditability, the following data hygiene considerations and modeling assumptions are documented:

* **Processing Lag Calculation**: Average lag days ($1.22\text{ days}$) are calculated as `[Date received] - [Date submitted]`. Any record where `Date received` preceded `Date submitted` was adjusted to `0` days in Power Query to eliminate negative duration anomalies.
* **Geographic Mapping Boundaries**: Geographic visualizations rely on standardized 2-letter state postal abbreviations (`State`). Unmapped, territory, or military addresses were categorized under `"Other/Unspecified"` to preserve portfolio totals.
* **Missing Sub-Attribute Imputation**: Text fields containing null values in `Sub-product` and `Sub-issue` were transformed via Power Query to display `"Unspecified"` to ensure dimensional integrity during dynamic aggregation and PivotTable slicing.
* **Static SLA Standard**: The model assumes a uniform **15-calendar-day statutory deadline** across all complaint categories in accordance with CFPB guidelines, without adjusting for custom state-level extension rules.

---
