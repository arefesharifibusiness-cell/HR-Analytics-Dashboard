## We Hire, But We Don't Retain

This project combines an **interactive HR analytics dashboard** with an **analytical report** to explore why an increase in headcount does not necessarily translate into greater organizational capacity.

The core challenge is not hiring — it is turning new hires into retained employees.

---

## Key Findings

| Metric | Value |
|---|---:|
| Active employees | 3,911 |
| Annual turnover rate | 34.7% |
| Share of exits from employees with less than one year of tenure | 68% |
| Workforce concentration across Operations, Sales, and Technology | More than half of the organization |

### What the Data Shows

- Over the past three years, the organization nearly doubled its headcount. However, a substantial share of hiring appears to have replaced employees who left. In 1405 (the Persian calendar year), approximately 73 employees left for every 100 hires.
- The highest turnover rates were in Executive roles (39.4%), Operations (28.9%), and Customer Service (26.8%).
- New hires are the most vulnerable group. In Technology, 30.7% of new employees leave within their first year.
- Employees who have received at least one promotion appear more likely to stay: 21.6% of retained employees had been promoted, compared with 12.2% of employees who left. This is a **correlation, not proof of causation**.

## Three Priorities

1. Reduce first-year employee attrition.
2. Manage risk in teams with both high headcount and high turnover.
3. Align compensation, performance, and career development.

## Eight-Step Action Plan

- Develop a first-year employee retention program.
- Investigate turnover by employee segment.
- Assess the impact of direct managers.
- Review salaries and bonuses.
- Establish clear career paths.
- Track first-year attrition as a separate KPI.
- Estimate the actual cost of employee turnover.
- Develop a predictive attrition model.

Full report: [`human-capital-analysis.pdf`](./human-capital-analysis.pdf)

---

## Dashboard Features

The dashboard is a standalone interactive HTML file generated with Python and uses a glassmorphism-inspired design.

- Multi-select filters for **department** and **job level**, applied across all tabs.
- Five KPIs: active employees, turnover rate, new hires, average salary, and average time to promotion.
- **Jalali (Persian calendar) dates** on trend-chart axes, using `jdatetime`.
- Four tabs and 18 interactive Plotly charts:

| Tab | Contents |
|---|---|
| Overview | Headcount trends, monthly hiring and exits, and distributions by education, department, and job level |
| Retention & Attrition | Turnover by department, job level, and tenure; comparison of employees who left and stayed |
| Compensation | Average salary by department and job level; bonus distribution across departments |
| Performance & Promotion | Performance and engagement, time to promotion, and salary by performance level |

To display a dashboard screenshot, add an image at `docs/dashboard-preview.png` and uncomment or add:

`![Dashboard](docs/dashboard-preview.png)`

---

## Getting Started

### Requirements

- Python 3.9 or later
- Internet access to load Plotly and fonts from a CDN

Install the required packages:

```bash
pip install pandas jdatetime openpyxl
```

### Run the Dashboard

1. Prepare the Excel input file with a sheet named `Employees`.
2. Update the file paths and date settings at the top of `final_glass.py`:

```python
INPUT_FILE  = "path/to/HR_Analytics.xlsx"
OUTPUT_FILE = "path/to/HR_Dashboard.html"

DATA_END_DATE = pd.Timestamp("2026-09-01")  # Data end date
PERIOD_START  = pd.Timestamp("2025-09-01")  # Start of turnover measurement period
```

3. Run the script:

```bash
python final_glass.py
```

4. Open the generated HTML file in your browser.

### Required Input Columns

| Column | Description |
|---|---|
| `Department` | Organizational department |
| `Job_Level` | Job level |
| `Education` | Education level |
| `Hire_Date` | Employee hire date |
| `Termination_Date` | Termination date; blank for active employees |
| `Last_Promotion_Date` | Most recent promotion date; blank if never promoted |
| `Monthly_Salary` | Monthly salary |
| `Annual_Bonus` | Annual bonus |
| `Performance_Score` | Performance score |
| `Engagement_Score` | Engagement score |

---

## Metric Definitions

- **Active employee as of date T:** `Hire_Date <= T` and (`Termination_Date` is blank or after T).
- **Turnover rate:**

  `Number of exits during the period / Average headcount at the beginning and end of the period * 100`

- **Time to promotion:** The time in years between `Hire_Date` and `Last_Promotion_Date`.

---

## Project Structure

```text
.
├── final_glass.py                 # Dashboard generation script
├── human-capital-analysis.pdf      # Analytical report
├── docs/
│   └── dashboard-preview.png      # Dashboard screenshot (optional)
└── README.md
```

> **Data privacy:** Employee datasets may contain sensitive information. Make sure your source Excel files are excluded from GitHub using `.gitignore` (for example, `*.xlsx`).

---

## Limitations

- The relationship between promotion and retention is correlational and does not establish causation. Further modeling is recommended to investigate this relationship.
- The analysis is descriptive. The effects of direct managers and the actual cost of turnover have not yet been measured; they are included in the proposed action plan.

---

## Tech Stack

`Python` · `pandas` · `jdatetime` · `Plotly.js` · `HTML/CSS`

## Author

**Arefeh Sharifi**
