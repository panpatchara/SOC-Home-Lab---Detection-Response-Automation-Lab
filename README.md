# SOC-Home-Lab---Detection-Response-Automation-Lab
# SOC Detection & Response Automation Lab

## 📌 Overview

This project simulates a real-world Security Operations Center (SOC) environment by building a detection and response pipeline using Splunk and Shuffle SOAR.

The lab focuses on detecting suspicious authentication activities (e.g., RDP logins) and automating incident response workflows.

---

## 🧠 Objectives

* Build a SIEM-based monitoring system using Splunk
* Detect suspicious login events (Event ID 4624, Logon Type 10)
* Automate incident response using Shuffle SOAR
* Integrate alerting via Slack and email
* Simulate real SOC analyst decision-making

---

## 🏗️ Architecture

The lab environment consists of:

* Windows Server (Domain Controller)
* Windows Test Machine
* Splunk Server (Ubuntu)
* Shuffle SOAR Platform
* Slack for alert notifications

Data Flow:

1. Windows logs → Splunk (SIEM)
2. Splunk detects suspicious activity
3. Alert triggers Shuffle playbook
4. SOC analyst receives notification
5. Automated/Manual response executed

---

## 🔍 Detection Logic

### Splunk Query

```spl
index=panubuntu-ad EventCode=4624 (Logon_Type=7 OR Logon_Type=10)
Source_Network_Address=* 
Source_Network_Address!="-" 
Source_Network_Address!="40.*"
| stats count by _time, ComputerName, Source_Network_Address, user, Logon_Type
```

### Key Detection Focus:

* External RDP logins (Logon Type 10)
* Suspicious successful logins
* Unknown source IP addresses

---

## ⚙️ Automation (SOAR)

### Workflow:

* Trigger: Splunk Alert
* Send notification to SOC Analyst (Slack/Email)
* Analyst decision:

  * YES → Disable domain user (Active Directory)
  * NO → No action

### Features:

* Automated alert handling
* Human-in-the-loop decision making
* Active Directory integration for containment

---

## 🚨 Incident Response

* Detection of suspicious login activity
* Alert generation via SIEM
* Notification via Slack
* Optional automated containment (disable user account)
* Logging and monitoring for further investigation

---

## 📊 Tools & Technologies

* Splunk (SIEM)
* Shuffle (SOAR)
* Windows Server (Active Directory)
* Slack (Notification)
* Ubuntu Server

---

## 📸 Screenshots

(Add screenshots here)

---

## 📈 Key Skills Demonstrated

* SIEM monitoring and log analysis
* Security event detection (Windows logs)
* SOAR automation and playbook design
* Incident response workflow design
* SOC operations simulation

---

## 🚀 Future Improvements

* Add threat intelligence enrichment (IP reputation)
* Integrate MITRE ATT&CK mapping
* Automate IP blocking (firewall integration)
* Enhance detection rules for brute-force attacks

---

## 👤 Author

Panpatchara Naneplai
SOC Analyst (Entry-Level)
