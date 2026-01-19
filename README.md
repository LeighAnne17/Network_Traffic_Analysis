# Network Traffic Analysis

**Author:** Nonkanyiso(Leigh-Anne) Ndimande  
**Project Type:** Cybersecurity & Data Analysis Portfolio Project  
**Tools Used:** Python, Pandas, Matplotlib, Seaborn, Scipy, Google Colab  
**Dataset:** Simulated network traffic logs (`network_traffic_dataset.csv`)

---

##  Project Overview

In today’s digital world, networks generate massive amounts of data every second. Understanding this data is crucial for **maintaining security**, detecting unusual behavior, and preventing cyber threats.  

This project dives into **network traffic logs** to identify patterns, trends, and anomalies. It combines **data analysis, visualization, and basic anomaly detection** to provide insights that could be used by network security teams or analysts.  

The goal is not just to crunch numbers but to **tell a story with data**, demonstrating both **technical skills** and **cybersecurity awareness**.

---

## Dataset

The dataset is a **simulated network traffic log** designed to resemble real-world scenarios. Each record represents a packet sent over a network and includes:

- `timestamp`: When the packet was sent  
- `source_ip`: IP address sending the packet  
- `destination_ip`: IP address receiving the packet  
- `protocol`: TCP, UDP, or ICMP  
- `destination_port`: Port number the packet is sent to  
- `packet_size_bytes`: Size of the packet in bytes  

This dataset allows analysis of **network activity, traffic patterns, and potential anomalies**, all while keeping it safe and ethical.

---

## 🔍 What I Did

1. **Data Cleaning & Exploration:**  
   Loaded the dataset, checked for missing values, and explored general traffic trends.

2. **Protocol & Port Analysis:**  
   Examined which protocols and ports are most common. This highlights normal network activity and can point out suspicious usage patterns.

3. **Top IP Analysis:**  
   Identified the most active source and destination IPs — a useful step to spot unusually heavy network users or potential threats.

4. **Traffic Over Time:**  
   Visualized how traffic varies daily. Peaks can indicate high activity times or unusual surges in network traffic.

5. **Anomaly Detection:**  
   Applied Z-score based detection to find packets that are unusually large or small. Anomalous packets could be benign errors or early indicators of network issues or attacks.

6. **Insights :**  
   Interpreted findings to provide actionable recommendations for monitoring and securing networks.

---

## 📈 Key Insights

- **TCP dominates traffic**, followed by UDP and ICMP, reflecting typical network behavior.  
- **Certain IP addresses generate or receive significantly more traffic** — these could be servers, heavy users, or potential points of interest for security monitoring.  
- **Port usage analysis** shows common HTTP/HTTPS traffic, but minor spikes on unusual ports could indicate scans or probing attempts.  
- **Packet size anomalies** highlight outliers that deserve further investigation.  

---

## Why This Project Matters

- Demonstrates **real-world cybersecurity thinking**: analyzing network logs, identifying anomalies, and interpreting patterns.  
- Shows **data literacy**: cleaning, visualizing, and extracting insights from large datasets.  
- Bridges **cybersecurity & data analysis**, a rare and highly valuable combination for internships, bursaries, and portfolio presentation.

---

##  How to Run

1. Open the notebook in **Google Colab**.  
2. Upload `network_traffic_dataset.csv` when prompted.  
3. Run the notebook **cell by cell** to view visualizations and analyses.  
4. Download the cleaned dataset (`network_traffic_cleaned.csv`) if desired.  

---

## 👩‍💻 About the Author

Nonkanyiso(Leigh-Anne) Ndimande Data Analyst | Aspiring Data Scientist | AI & Cybersecurity Enthusiast

This project is part of my growing portfolio focused on:

• Data Analytics

• Data Science

• Machine Learning

•Artificial Intelligence

•Cybersecurity & Threat Analysis
