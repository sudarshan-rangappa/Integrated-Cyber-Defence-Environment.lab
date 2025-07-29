# 🛡️ Integrated Cyber Defense Environment (ICDE)
<img width="3840" height="3649" alt="icde-network-topology" src="https://github.com/user-attachments/assets/02f0d6b9-35a9-4759-90eb-bec93b823a36" />

A virtual SOC simulation built using open-source tools for blue/red team operations.

## 📌 Project Highlights

- 🔍 Real-time detection via Wazuh (SIEM/HIDS)
- 🧠 Automated response using Shuffle (SOAR)
- 🌐 Network monitoring with Suricata (NIDS)
- 🧪 Vulnerability assessment via OpenVAS
- 🐍 Deception techniques using Cowrie honeypot
- 📊 Data aggregation & dashboards using Splunk

## 🧰 Lab Components

| Component     | Tool        | IP               |
|---------------|-------------|------------------|
| AD Server     | Win Server  | 192.168.33.129   |
| Target Client | Win 11      | 192.168.33.130   |
| Attacker VM   | Kali Linux  | 192.168.33.143   |
| SIEM Server   | Wazuh       | 192.168.33.131   |
| SOAR Server   | Shuffle     | 192.168.33.149   |
| IDS           | Suricata    | 192.168.33.144   |
| Honeypot      | Cowrie      | 192.168.33.142   |
| Vuln Scanner  | OpenVAS     | 192.168.33.147   |
| Logging       | Splunk      | 192.168.33.128   |

## 📂 Structure

- `setup-guides/`: Step-by-step setup for each tool
- `integrations/`: Wazuh ↔ Splunk, Wazuh ↔ Shuffle, Telegram
- `red-team-tests/`: Simulated attack test cases
- `results/`: Screenshots, logs, analysis
- `report/`: Final project files (PDF, slides)

## 📈 Results

- ✅ Telegram alerts for SSH brute-force
- ✅ Port scan detection via Suricata
- ✅ Full AD simulation with logging
- ✅ Log correlation verified in Splunk

## 📄 License

MIT License
