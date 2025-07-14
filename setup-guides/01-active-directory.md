# 🛠️ Active Directory Configuration

This guide outlines the configuration of the **Windows Server Active Directory Domain Controller (AD DC)** used in the ICDE lab environment.

---

## 🧱 Domain Setup

- **Domain Name**: `home.lab`
- **Server OS**: Windows Server 2025
- **Machine IP**: `192.168.33.129`
- **Computer Name**: `WIN-LREENCL33G8`
- **Role Installed**: Active Directory Domain Services (AD DS)
- **Tools Used**: Server Manager, dcpromo, Group Policy Management

---

## 🧑‍💼 Organizational Units, Groups, and Users

The AD was structured to simulate a real-world enterprise with users, groups, and access roles.

| **OU Name**      | **Groups Inside OU**                 | **Users Inside OU**                                           | **Group Memberships**                                            |
| ---------------- | ------------------------------------ | ------------------------------------------------------------- | ---------------------------------------------------------------- |
| **IT**           | `IT Admins`                          | `AdminUser`                                                   | `AdminUser` → IT Admins, Domain Users                            |
| **Finance**      | `Finance Team`                       | `FinanceUser`                                                 | `FinanceUser` → Finance Team, Domain Users                       |
| **Security**     | `Security Analysts`, `Log Readers`   | `SecurityAnalyst`                                             | `SecurityAnalyst` → Security Analysts, Log Readers, Domain Users |
| **GeneralUsers** | `Remote Access Users`                | `Bob`, `Alice`                                                | `Bob, Alice` → Remote Access Users, Domain Users                 |
| **Workstations** | _(Stores client systems)_            | Windows 11 Client (TARGET)                                    | _(N/A)_                                                          |
| **Servers**      | _(Stores servers)_                   | Wazuh, Splunk, OpenVAS, Cowrie, TheHive, Zeek, Server itself  | _(N/A)_                                                          |

---

## 🪪 User Creation Notes

Users were assigned realistic names and grouped into OUs to simulate department-based access. Group memberships help define:

- Privileges
- Access control via GPO
- Audit scopes

---

## 🛡️ Group Policy Configuration for Logging & Auditing

To support blue team detections and SIEM integration, the following security audit policies were configured.

### ✅ Enable Logon/Logoff Auditing

**Steps:**

1. Open `gpmc.msc` → Default Domain Policy → Edit
2. Navigate to:  
   `Computer Configuration > Policies > Windows Settings > Security Settings > Advanced Audit Policy Configuration > Audit Policies > Logon/Logoff`
3. Enable:
   - `Audit Logon`: ✅ Success, ✅ Failure

**Purpose**:

- Detect brute-force and lateral movement
- Log Event IDs like `4624`, `4625`, `4647`

---

### ✅ Enable PowerShell Logging

**Steps:**

1. Run `gpedit.msc` on the server
2. Go to:  
   `Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell`
3. Enable:
   - `Turn on PowerShell Script Block Logging`
   - `Turn on Module Logging` (set to `*`)

**Purpose**:

- Detects malicious PowerShell usage (e.g., LoLBins, recon, post-exploitation)
- Generates Event IDs: `4104`, `4103` (PowerShell Operational Log)

---

## 🧠 Why Logging Was Enabled

| Logging Type     | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| Audit Logon      | Detect brute-force, unauthorized login attempts, lateral movement       |
| PowerShell Logs  | Detect fileless malware, LOLBins, encoded payloads                      |
| Sysmon (later)   | Correlate detailed process/file/network activity (with Wazuh/Splunk)    |

---

## 🧩 Log Sources Mapped

| Component                | Log Source Location                                         |
|--------------------------|-------------------------------------------------------------|
| Login Activity           | Security Log (`Event IDs: 4624, 4625`)                      |
| PowerShell Execution     | PowerShell Operational Log (`Event ID 4104, 4103`)          |
| Group Policy Audit       | Event Viewer > Group Policy Management                      |

---

## ✅ Next Steps

→ After this configuration:
- **Wazuh agent** was installed on the AD server
- **Sysmon** with Olaf Hartong's modular config was deployed
- Logs were forwarded to the Wazuh Manager and Splunk

---

## 📎 References

- Olaf Hartong Sysmon config:  
  [`https://raw.githubusercontent.com/olafhartong/sysmon-modular/master/sysmonconfig.xml`](https://raw.githubusercontent.com/olafhartong/sysmon-modular/master/sysmonconfig.xml)
