# 🚨 Windows Failed Login Detection Using IBM QRadar CE

This project demonstrates how to forward Windows Security Logs to **IBM QRadar Community Edition** using **NXLog**, and create a detection rule for failed login attempts (Event ID `4625`). The rule triggers a custom event in QRadar CE to simulate alerting and detection.

---

## 📌 Objectives

- ✅ Forward logs from a Windows VM to QRadar using NXLog
- ✅ Parse Event ID `4625` (failed login attempts)
- ✅ Create a custom detection rule in QRadar CE
- ✅ Generate a synthetic event when the rule matches
- 🚫 Note: QRadar CE does **not support offense generation** from custom rules

---

## 🧰 Tools Used

| Tool | Purpose |
|------|---------|
| 🖥️ Windows 10 VM | Log source for failed login events |
| 📤 NXLog (CE) | Log forwarder from Windows to QRadar |
| 🛡️ IBM QRadar CE | SIEM platform for log collection and rule creation |
| 🛠️ VMware Workstation | Virtualization environment |

---

## 🔄 Log Flow Diagram
Windows VM (NXLog) --> QRadar CE (UDP 514) --> Log Activity --> Custom Rule --> Synthetic Event

