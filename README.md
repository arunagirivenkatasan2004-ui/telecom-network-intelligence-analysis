# Telecom Network Intelligence and Performance Analysis

An exploratory data analysis (EDA) project that investigates telecom network-flow records to understand network status, compare performance indicators, and explore service-level fault patterns using Python.

## Project Overview

Network users may experience buffering, delays, unstable calls, or service interruptions. This project explores network-flow data to understand how performance indicators differ across **Normal**, **Congested**, and **Fault** records.

The analysis focuses on questions such as:

- How are network records distributed across Normal, Congested, and Fault statuses?
- How do latency, throughput, packet loss, jitter, and network load differ by status?
- How does average network load vary by congestion level?
- Which service types have the highest fault rates?
- What data-quality issues should be considered before drawing conclusions?

## Dataset

- **Records:** 50,500
- **Original columns:** 34
- **Columns retained for the focused analysis:** 15
- **Target/status field explored:** `Network_Status`

Key fields include `Protocol_Type`, `Flow_Duration`, `Packet_Count`, `Byte_Count`, `Throughput`, `Latency`, `Packet_Loss`, `Jitter`, `Bandwidth_Utilization`, `Network_Load`, `Service_Type`, `Failure_Count`, `Congestion_Level`, and `Network_Status`.

> **Dataset note:** The CSV file was not included with the uploaded notebook. Add the dataset you are authorized to use at `data/telecom_network_intelligence_dataset_50500.csv` before running the notebook. Check the dataset's license and sharing terms before uploading any data to a public repository. If it must remain private, keep it out of GitHub and follow your organization's data-handling rules.

## Tools and Libraries

- Python
- Pandas — data inspection, cleaning, grouping, and aggregation
- NumPy — derived categories for latency and network load
- Matplotlib — charts
- Seaborn — exploratory visualizations
- Jupyter Notebook — analysis workflow

## Workflow

1. Load and inspect the dataset (`shape`, data types, and null counts).
2. Select 15 columns relevant to the network-performance questions.
3. Check missing values and duplicate rows.
4. Impute missing `Congestion_Level` values with the mode (`Low`) in the current notebook.
5. Review numeric summaries and examine possible outliers in selected performance metrics.
6. Explore network-status distribution, congestion-level load, and latency/load categories.
7. Compare average performance metrics by network status.
8. Calculate service-level fault counts and fault rates.
9. Visualize status distributions, metric comparisons, service fault rates, and network load versus latency.

## Key Findings

The values below are outputs from the notebook; metric units should be verified against the dataset documentation before being described as milliseconds, percentages, or other units.

### Network status distribution

| Network status | Records | Share |
|---|---:|---:|
| Normal | 34,494 | 68.30% |
| Congested | 11,022 | 21.83% |
| Fault | 4,984 | 9.87% |
| **Total** | **50,500** | **100.00%** |

### Average performance by network status

| Network status | Latency | Throughput | Packet loss | Jitter | Network load | Failure count |
|---|---:|---:|---:|---:|---:|---:|
| Normal | 26.72 | 6.26 | 0.23 | 4.65 | 36.07 | 0.07 |
| Congested | 114.60 | 6.46 | 3.25 | 24.36 | 85.62 | 0.52 |
| Fault | 185.48 | 3.11 | 9.66 | 42.51 | 60.73 | 2.24 |

### Service-level fault rates

| Service type | Fault records | Fault rate |
|---|---:|---:|
| AR/VR (`AR_VR`) | 213 | 10.70% |
| Enterprise VPN | 480 | 10.36% |
| VoIP | 604 | 10.05% |
| Web Browsing | 1,153 | 9.93% |

**Interpretation:** Fault records have the highest average latency, packet loss, jitter, and failure count in this dataset. Congested records have the highest average network load. AR/VR has the highest observed service-level fault rate, while Web Browsing has the highest absolute fault count among service types.

These are descriptive associations, not proof that one metric causes network faults.

## Data Quality and Limitations

- `Congestion_Level` has 19,282 missing values (**38.18%** of the records). The current notebook fills these values with the mode (`Low`). Because a large share is missing, this choice may affect the resulting distribution and should be reviewed before operational conclusions are drawn.
- The notebook reports no duplicate rows in the selected dataset.
- The original `Alarm_Type` and `Alarm_Severity` fields were excluded from the focused 15-column analysis; they may be useful in a separate alarm-focused investigation.
- Metric units and definitions should be confirmed from the dataset documentation.
- This project performs EDA and descriptive analysis; it does **not** train a machine-learning model or prove causation.

## Run the Project

### 1. Clone or download this repository

```bash
git clone https://github.com/<your-username>/telecom-network-intelligence-analysis.git
cd telecom-network-intelligence-analysis
```

Replace `<your-username>` with your GitHub username.

### 2. Add the dataset

Place your CSV at:

```text
data/telecom_network_intelligence_dataset_50500.csv
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Launch the notebook

```bash
jupyter notebook telecom_network_intelligence_analysis.ipynb
```

Run the notebook cells from top to bottom from the repository root so the relative dataset path resolves correctly.

## Repository Structure

```text
telecom-network-intelligence-analysis/
├── data/
│   └── README.md
├── telecom_network_intelligence_analysis.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Potential Next Steps

- Investigate why `Congestion_Level` values are missing before selecting an imputation strategy.
- Compare fault rates with confidence intervals and examine possible differences across service types.
- Investigate combinations of latency, packet loss, jitter, network load, and failure count.
- If the use case and labels support it, develop and validate a separate model to flag likely network faults.

## Author

ARUNAGIRI V
LinkedIn [https://www.linkedin.com/in/arunagiri-venkatasan-619928296/]
portfolio[https://portfolio-six-steel-lz1k9ueu6f.vercel.app/#about]
