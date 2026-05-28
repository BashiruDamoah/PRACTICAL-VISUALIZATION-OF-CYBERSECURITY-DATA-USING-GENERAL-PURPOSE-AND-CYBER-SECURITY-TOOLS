# PRACTICAL-VISUALIZATION-OF-CYBERSECURITY-DATA-USING-GENERAL-PURPOSE-AND-CYBER-SECURITY-TOOLS
Applying visualization techniques to cybersecurity-related datasets using one general-purpose tool and one cyber-specific tool, as well as clearly documenting and explaining the generated visuals and the insights they offer, are the objectives of this practical project.
# Practical Visualization of Cybersecurity Data

Applying general-purpose and cyber-specific visualization tools to cybersecurity attack datasets — producing five Python-based charts and three Kibana dashboards with full documentation.

**Author:** Damoah Bashiru

---

## Project Overview

This project demonstrates how visualization techniques can be applied to cybersecurity data using two different categories of tools:

- **Task 1** — General-purpose visualization using Python (Matplotlib & Seaborn)
- **Task 2** — Cyber-specific visualization using Kibana (Elastic Stack)

The dataset used is the public **Cybersecurity Attacks Dataset** from Kaggle (`cybersecurity_attacks.csv`), containing attack records with timestamps, attack types, severity levels, packet lengths, anomaly scores, and more.

---

## Repository Structure

```
├── notebooks/
│   └── Task1_Cyber_Visualizations.ipynb
├── data/
│   └── cybersecurity_attacks.csv
├── charts/
│   ├── bar_chart_attack_types.png
│   ├── line_chart_attacks_over_time.png
│   ├── heatmap_attacks_hour_day.png
│   ├── pie_chart_severity_distribution.png
│   └── scatter_packet_vs_anomaly.png
├── kibana_screenshots/
│   ├── timeline_security_events.png
│   ├── heatmap_attack_patterns.png
│   └── top10_attack_types.png
└── README.md
```

---

## Tools and Environment

### Task 1 — Python
| Tool | Purpose |
|---|---|
| Python 3 | Core language |
| pandas | Data loading and manipulation |
| matplotlib | Chart generation |
| seaborn | Statistical visualizations |
| Jupyter Notebook | Interactive development environment |

### Task 2 — Kibana (Elastic Stack)
| Tool | Purpose |
|---|---|
| Elasticsearch | Data indexing and search backend |
| Kibana | Dashboard and visualization frontend |

---

## Setup Instructions

### Python Environment

```bash
# Clone the repository
git clone https://github.com/<your-username>/cybersecurity-visualization.git
cd cybersecurity-visualization

# Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install pandas matplotlib seaborn jupyter

# Launch Jupyter Notebook
jupyter notebook
```

### Kibana Setup

```bash
# Install Elasticsearch
sudo apt install elasticsearch -y

# Install Kibana
sudo apt install kibana -y

# Start services
sudo systemctl start elasticsearch
sudo systemctl start kibana

# Access Kibana at
http://localhost:5601
```

Then upload `cybersecurity_attacks.csv` via **Integrations → Upload File** in the Kibana UI.

---

## Visualizations

### Task 1 — Python Visualizations

**Visualization 1 — Bar Chart**
- Title: *Number of Attacks by Attack Type*
- Purpose: Compare the frequency of DDoS, Malware, and Intrusion attacks
- Key insight: DDoS attacks are the most frequent category

**Visualization 2 — Line Chart**
- Title: *Number of Cyber Attacks Over Time (Daily)*
- Purpose: Show temporal trends in attack activity from 2020–2023
- Key insight: Attack frequency is relatively consistent with no major seasonal drop-off

**Visualization 3 — Heatmap**
- Title: *Attack Frequency by Hour of Day and Day of Week*
- Purpose: Identify time-of-day and day-of-week attack patterns
- Key insight: Attacks are broadly distributed across all hours and days with no extreme peaks

**Visualization 4 — Pie Chart** *(additional)*
- Title: *Distribution of Attack Severity Levels*
- Purpose: Show proportions of Low, Medium, and High severity attacks
- Key insight: Severity levels are roughly equally distributed (~33% each)

**Visualization 5 — Scatter Plot** *(additional)*
- Title: *Packet Length vs Anomaly Score (colored by Severity)*
- Purpose: Explore the relationship between packet size and anomaly score
- Key insight: No strong linear correlation — anomaly scores appear independent of packet length across all severity levels

---

### Task 2 — Kibana Visualizations

**Visualization 1 — Timeline of Security Events**
- Aggregates attack occurrences over time using an area chart
- Useful for detecting coordinated attack campaigns and activity spikes

**Visualization 2 — Attack Pattern Heatmap**
- Maps attack intensity by timestamp
- Reveals recurring patterns and peak activity windows for proactive defense

**Visualization 3 — Top 10 Attack Types Bar Chart**
- Ranks the most frequent attack categories in the dataset
- DDoS attacks dominate, emphasizing the need to prioritize availability protection

---

## Requirements

```
pandas
matplotlib
seaborn
jupyter
```

Install all at once:

```bash
pip install pandas matplotlib seaborn jupyter
```

---

## Key Takeaways

- General-purpose tools (Python/Seaborn) are highly flexible for statistical and exploratory analysis.
- Cyber-specific tools (Kibana) excel at real-time, interactive dashboards and time-series monitoring.
- DDoS is consistently the dominant attack type in this dataset, accounting for the largest share across all visualizations.
- Time-of-day heatmaps show attacks are distributed across all hours, suggesting automated rather than human-operated attack behavior.

---
