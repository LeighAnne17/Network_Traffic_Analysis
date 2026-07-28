# Network Traffic Analysis

**Author:** Nonkanyiso(Leigh-Anne) Ndimande  
**Project Type:** Cybersecurity & Data Analysis Portfolio Project  
**Tools Used:** Python (Pandas, NumPy, Matplotlib, Seaborn, SciPy), Google Colab  
**Dataset:** Simulated network traffic logs (1,000 packet records)  
**Techniques:** Statistical anomaly detection (Z-score), visualization, cybersecurity analysis

---

##  Project Overview

Modern networks generate massive amounts of data every second. Understanding this data is crucial for:
- **Detecting anomalies:** Identifying unusual traffic patterns that could indicate attacks or misconfigurations
- **Network monitoring:** Understanding normal vs. suspicious behavior
- **Security incident response:** Flagging packets for investigation

This project analyzes 1,000 simulated network traffic logs to identify patterns, trends, and potential security threats using data analysis, statistical methods, and visualization.

-----

## Dataset Overview

| Metric | Value |
|--------|-------|
| **Total Packets Analyzed** | 1,000 records |
| **Date Range** | Dec 19, 2025 - Jan 18, 2026 |
| **Fields Tracked** | Timestamp, Source IP, Destination IP, Protocol, Port, Packet Size |
| **Protocols Detected** | TCP, UDP, ICMP |
| **Unique Source IPs** | ~250+ distinct IPs |
| **Unique Destination IPs** | ~250+ distinct IPs |
| **Packet Size Range** | 8 bytes to 64,000+ bytes |

---

### **Data Schema**
```
timestamp          : When the packet was sent (ISO format)
source_ip          : IP address sending the packet (IPv4)
destination_ip     : IP address receiving the packet (IPv4)
protocol           : TCP, UDP, or ICMP
destination_port   : Port number (0-65535)
packet_size_bytes  : Payload size in bytes
packet_size_anomaly: Binary flag (0=normal, 1=anomaly)
```

---


## What I Did

### **1. Protocol Distribution**
| Protocol | Count | % of Traffic | Use Case |
|----------|-------|--------------|----------|
| **TCP** | ~650 | 65% | Web traffic (HTTP/HTTPS), email, file transfer |
| **UDP** | ~280 | 28% | DNS queries, video streaming, VoIP |
| **ICMP** | ~70 | 7% | Network diagnostics (ping, traceroute) |

**Key Finding:** TCP dominates (65%), reflecting typical enterprise network behavior where reliable, connection-oriented communication is preferred.

### **2. Port Analysis**

**Most Frequently Used Ports:**
- Ports in range: 1-65535
- High-frequency ports: Common for HTTP (80), HTTPS (443), DNS (53)
- Unusual port activity: Occasional spikes on uncommon ports (e.g., >50000) suggest non-standard services or potential scanning

**Security Implication:** Unusual port usage (high-numbered, reserved, or rarely-used ports) could indicate:
- Unauthorized services running
- Firewall evasion attempts
- Botnet communication

### **3. Top IP Addresses**

**Most Active Source IPs:** Heavy users correlate with servers or legitimate high-traffic devices
**Most Active Destination IPs:** Popular targets (likely servers or VIPs receiving traffic)

**Security Insight:** Identifying top IPs helps establish baselines for normal network behavior—deviations signal anomalies.

### **4. Traffic Over Time**

Traffic varies across the 30-day observation window:
- **High-traffic periods:** Correlate with normal business hours
- **Low-traffic periods:** Nights/weekends show expected reduction
- **Sudden spikes:** Could indicate legitimate events (backups, updates) or attacks (DDoS, data exfiltration)

### **5. Packet Size Anomaly Detection**

**Statistical Method:** Z-Score Analysis
- **Mean packet size:** ~30,000 bytes
- **Std deviation:** ~20,000 bytes
- **Anomaly threshold:** >3 standard deviations from mean
- **Anomalies detected:** 143 packets flagged

| Anomaly Type | Count | Example Size | Interpretation |
|--------------|-------|--------------|-----------------|
| **Oversized packets** | ~70 | 50,000-65,000 bytes | File transfers, large downloads, video streaming |
| **Undersized packets** | ~73 | <1,000 bytes | Control traffic (SYN, ACK), DNS queries, heartbeats |

**Security Perspective:**
- **Oversized packets:** Could indicate data exfiltration attempts (stealing large files via stealth channels)
- **Undersized packets:** Normal for signaling, but unusual volumes could indicate reconnaissance or DDoS reconnaissance

---

##  Key Findings & Insights

### **Finding 1: Protocol Composition Reflects Normal Network**
**TCP dominates at 65%**, matching typical enterprise networks. This indicates:
- Primary focus on web services and data transfer
- Reliable, connection-oriented communication preferred
- Low ICMP (7%) suggests network diagnostics are minimal

**Actionable Insight:** Sudden increase in UDP traffic could indicate DNS flooding attacks.

### **Finding 2: Packet Size Extremes Warrant Investigation**
**143 anomalies flagged** out of 1,000 packets (14.3% anomaly rate):
- 70 oversized packets: Verify if legitimate data transfers or unauthorized uploads
- 73 undersized packets: Check for unusual control traffic patterns (SYN flooding, heartbeat sweeps)

**Action Item:** Create alert rule: `packet_size > 50,000 bytes OR packet_size < 500 bytes`

### **Finding 3: IP Reputation & Baseline Deviation**
Top source/destination IPs create a **behavioral baseline**:
- Monitor deviations from expected traffic volumes
- Flag IPs with sudden surges (potential compromised hosts)
- Identify new IPs entering top talkers list (network reconnaissance)

### **Finding 4: Port Usage Anomalies**
Unusual ports appearing in traffic:
- Reserved system ports (1-1023) in high volumes: Privilege escalation attempts?
- Random high-numbered ports (50000+): Peer-to-peer, botnet, or file-sharing activity?

**Recommendation:** Whitelist expected ports, blacklist known attack ports.

---

##  Real-World Application

**If I were a network analyst at a company, I'd:**

1. **Daily Monitoring:**
   - Run this analysis on production logs to flag >3 std dev anomalies
   - Alert on protocol changes (e.g., sudden UDP spike = possible DNS attack)
   - Track top talkers and alert if new IPs appear

2. **Weekly Review:**
   - Trend packet size patterns (expected to be stable)
   - Compare current week vs. baseline week
   - Investigate all anomalies flagged (143 out of 1,000 is high; could be overly sensitive threshold)

3. **Incident Response:**
   - When an incident occurs (malware detected, breach), pull logs for that time period
   - Use protocol/port/IP patterns to identify affected systems
   - Correlate with other security tools (IDS/IPS, firewall logs, EDR)

**This project demonstrates I can:**
- Transform raw network logs into actionable security insights
- Apply statistical methods to detect threats
- Think like a security analyst (what's normal? what's suspicious?)
- Communicate findings clearly

---

## 📁 Project Structure

```
Network_Traffic_Analysis/
│
├── Network_Traffic_Analysis.ipynb    # Full analysis notebook (cells 1-10)
├── network_traffic_dataset.csv       # Raw packet logs (1,000 records)
├── network_traffic_cleaned.csv       # Processed dataset with anomaly flags
├── README.md                         # This file
└── requirements.txt                  # Python dependencies
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Pandas** | Data loading, filtering, groupby aggregations |
| **NumPy** | Statistical calculations (mean, std dev) |
| **Matplotlib / Seaborn** | Visualizations (bar charts, scatter plots, timelines) |
| **SciPy** | Advanced statistical functions |
| **Python** | All data processing and analysis |
| **Google Colab** | Cloud-based notebook environment |

---

## 🚀 How to Run

### **Option 1: Google Colab (Recommended - No Setup Required)**
1. Open [Network_Traffic_Analysis.ipynb](Network_Traffic_Analysis.ipynb) in Google Colab
2. Upload `network_traffic_dataset.csv` when prompted (or use the built-in file upload)
3. Run cells 1-10 sequentially:
   - **Cells 1-2:** Load and explore data
   - **Cells 3-4:** Protocol and port analysis
   - **Cells 5-6:** IP address analysis
   - **Cells 7-8:** Time-series traffic trends
   - **Cells 9-10:** Anomaly detection and visualizations
4. Download `network_traffic_cleaned.csv` with anomaly flags

### **Option 2: Local Python Environment**
```bash
# Clone repository
git clone https://github.com/LeighAnne17/Network_Traffic_Analysis.git
cd Network_Traffic_Analysis

# Install dependencies
pip install -r requirements.txt

# Run analysis (equivalent to Jupyter notebook)
python analysis.py  # [Or open Network_Traffic_Analysis.ipynb in Jupyter]
```

### **Requirements** (requirements.txt)
```
pandas>=2.0.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
scipy>=1.10.0
```

---

## 📊 Outputs Generated

| Output | Purpose | Format |
|--------|---------|--------|
| **Protocol Distribution Chart** | Pie/bar chart showing TCP/UDP/ICMP split | PNG |
| **Packet Size Distribution** | Histogram of packet sizes with anomaly overlay | PNG |
| **Top IPs by Traffic** | Horizontal bar chart of most active IPs | PNG |
| **Traffic Over Time** | Time-series line chart showing daily packet volumes | PNG |
| **Anomaly Report** | Summary of flagged packets with details | CSV / Text |
| **network_traffic_cleaned.csv** | Original data + anomaly_flag column | CSV |

---

## 📋 Data Dictionary (Cleaned Dataset)

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| **timestamp** | string | ISO 8601 datetime | 2026-01-17 13:17:29 |
| **source_ip** | string | Sending IP address | 194.255.226.195 |
| **destination_ip** | string | Receiving IP address | 186.249.169.92 |
| **protocol** | string | Layer 4 protocol | TCP, UDP, or ICMP |
| **destination_port** | integer | Target port number | 52763 |
| **packet_size_bytes** | integer | Payload size | 1166 |
| **packet_size_anomaly** | binary | Anomaly flag (0/1) | 0 (normal), 1 (flagged) |

---

## 💬 Why This Project Matters

This project bridges **cybersecurity and data analytics** — a rare and highly valuable combination:

- **Cybersecurity perspective:** Shows understanding of attack patterns, network threats, and incident investigation
- **Data perspective:** Demonstrates ability to extract insights from large, messy datasets
- **Business perspective:** Translates technical findings into actionable security recommendations
- **Practical application:** The techniques used are exactly what SOCs (Security Operations Centers) do daily

---

## **Skills Demonstrated:**
- Exploratory Data Analysis (EDA) — Understanding dataset structure and quality
- Statistical Analysis — Z-score, standard deviation, outlier detection
- Data Visualization — Charts that tell a security story
- Security Thinking — Threat modeling, anomaly interpretation
- Communication — Translating technical findings for non-technical audiences

**Real-World Relevance:**
- Network traffic analysis is core to **SOC (Security Operations Center)** work
- Anomaly detection is used in **intrusion detection systems (IDS)**
- These techniques apply to enterprise cybersecurity roles

---
