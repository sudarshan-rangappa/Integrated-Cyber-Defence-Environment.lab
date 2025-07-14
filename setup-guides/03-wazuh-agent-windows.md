# 🪟 Wazuh Agent Setup on Windows

This guide covers the installation of the Wazuh agent on Windows endpoints, including the Windows 11 client and the Windows Server 2025 Domain Controller.

---

## 🖥️ Windows 11 Client (TARGET)

1. Login to Wazuh Dashboard.
2. Navigate to **Agents** → **Add Agent**.
3. Fill in the following details:
   - Platform: `Windows`
   - Name: `TARGET`
   - IP: `192.168.33.130`
4. Copy the generated PowerShell script.
5. On the Windows 11 machine, open PowerShell as Administrator.
6. Paste and run the script to install and register the agent.

✅ Agent installed and successfully appeared in the Wazuh Dashboard.

---

## 🖥️ Windows Server 2025 (AD-DC)

1. Login to Wazuh Dashboard.
2. Go to **Agents** → **Add Agent**.
3. Fill in:
   - Platform: `Windows`
   - Name: `AD-DC`
   - IP: `192.168.33.129`
4. Run the generated PowerShell script on the AD server.
5. Agent service was installed, started, and successfully registered.

✅ The AD server began forwarding logs to the Wazuh Manager.

---

## 🔄 Post-Installation Checks

- Confirm both agents are listed as **active** in Wazuh Dashboard.
- Check logs under the **Security**, **PowerShell**, and **Sysmon** modules.
- Verify that `ossec.log` on the Windows machines shows successful communication.

---

## 📎 Related

- See [`10-sysmon-audit-logging.md`](10-sysmon-audit-logging.md) for extended visibility.
- Wazuh Docs: https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html
