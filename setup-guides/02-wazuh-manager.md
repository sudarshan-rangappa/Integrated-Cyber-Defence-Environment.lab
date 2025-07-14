# 🧠 Wazuh Manager Setup (SIEM)

This document covers the installation and configuration of the **Wazuh Manager** on an Ubuntu Server. It serves as the SIEM (Security Information and Event Management) core for log collection, analysis, and rule-based alerting in the ICDE environment.

---

## 📦 Wazuh Server Installation

### 🔧 Environment

- **OS**: Ubuntu Server 22.04 LTS  
- **Hostname**: `wazuh`  
- **IP Address**: `192.168.33.131`

### 🪛 Installation Steps

1. Boot the Ubuntu VM and connect via terminal.
2. Follow the [Wazuh Quick Start Guide](https://documentation.wazuh.com/current/quickstart/index.html).
3. Run the installation script:

   ```bash
   curl -sO https://packages.wazuh.com/4.5/wazuh-install.sh
   sudo bash ./wazuh-install.sh -a
   ```

4. After installation:
   - Access Wazuh UI via: `https://192.168.33.131`
   - Login with the default credentials provided during setup.

---

## ✅ Installation Success

- Wazuh dashboard accessible over HTTPS.
- Login and dashboard loaded successfully.

---

## 🤝 Adding Wazuh Agents

### 🪟 Windows 11 Endpoint (TARGET)

1. Go to **Wazuh Dashboard** → **Agents** → **Add Agent**
2. Select:
   - Platform: `Windows`
   - IP: `192.168.33.130`
   - Name: `TARGET`
3. Run the provided PowerShell script on the Windows client.
4. Agent appeared and connected successfully.

---

### 🪟 Windows Server (AD-DC)

- Platform: `Windows`  
- IP: `192.168.33.129`  
- Name: `AD-DC`  
- Followed same PowerShell agent registration steps.

---

## 🐧 Linux Agent Installations

Installed agents on:

| Hostname | IP Address       | Purpose           |
|----------|------------------|-------------------|
| suricata | 192.168.33.144   | NIDS              |
| cowrie   | 192.168.33.142   | Honeypot          |
| splunk   | 192.168.33.128   | Log Aggregator    |
| openvas  | 192.168.33.147   | Vulnerability Mgmt|

For each:

```bash
curl -sO https://packages.wazuh.com/4.5/wazuh-agent.sh
sudo bash ./wazuh-agent.sh -i
```

Edit agent config:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Set manager IP and restart agent.

---

## 📟 Agent Management

- Agents visible in Wazuh dashboard.
- Logs, FIM, health monitoring accessible per host.

---

## 📤 Log Forwarding to Splunk

➡️ See [`../integrations/wazuh-to-splunk.md`](../integrations/wazuh-to-splunk.md)

---

## 📎 References

- https://documentation.wazuh.com  
- https://packages.wazuh.com/4.5/wazuh-install.sh
