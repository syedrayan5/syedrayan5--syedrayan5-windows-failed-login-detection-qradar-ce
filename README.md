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


## 🔧 NXLog Configuration (Snippet)

Configured in C:\Program Files\nxlog\conf\nxlog.conf

define ROOT C:\Program Files\nxlog
Moduledir %ROOT%\modules
CacheDir %ROOT%\data
Pidfile %ROOT%\data\nxlog.pid
LogFile %ROOT%\data\nxlog.log

<Extension syslog>
    Module      xm_syslog
</Extension>

<Input in>
    Module      im_msvistalog
</Input>

<Output out>
    Module      om_udp
    Host        QRadar IP
    Port        514
    Exec        to_syslog_ietf();
</Output>

<Route 1>
    Path        in => out
</Route>


🕵️‍♂️ QRadar Rule Creation
Rule Tests Stack
✅ When the event QID is one of the following: 28250014 (Windows failed login)

✅ And when the event(s) were detected by log source type: WinCollect or NXLog

✅ Detected by the Local system
![rule creation 1](https://github.com/user-attachments/assets/cd6812c5-af2e-4ba6-9b35-7c37980f0a8f)


Rule Response & Actions
✅ Dispatch New Event

✅ Annotate Event (e.g. "Windows Failed Login Detected")
![rule creation 2](https://github.com/user-attachments/assets/7861c2e7-8043-4cd2-a614-d528379fae32)

📊 QRadar Log Activity
After simulating failed login attempts from the Windows VM:

You can see:

✅ The original failed login logs

✅ The custom dispatched event from your rule
![log activity](https://github.com/user-attachments/assets/42f5db69-5487-43ef-a9c3-7cfb641b509f)


✅ What This Project Demonstrates
Practical understanding of SIEM log forwarding

Ability to create custom detection rules

Experience configuring NXLog

Use of QRadar Rule Wizard for basic correlation

Awareness of SIEM limitations and capabilities





