# CodeAlpha_project_Network_Intrusion_DetectionSystem
# 🛡️ Network Intrusion Detection System (NIDS) using Suricata

This project demonstrates a working **Network-Based Intrusion Detection System (NIDS)** using **Suricata**, a powerful open-source threat detection engine. It monitors network traffic, detects suspicious activities (like ping floods, port scans, etc.), and logs alerts.

---

## 📌 Objective

The goal of this task is to:

- Install and configure a NIDS (Suricata) on Windows
- Add or customize rule sets to detect suspicious network activity
- Generate real-time alerts
- Optionally visualize the alerts from logs
- Simulate test attacks like ICMP ping, port scans, etc.

---

## 🧰 Tools & Technologies

| Tool         | Description                                |
|--------------|--------------------------------------------|
| Suricata     | Open-source NIDS/IPS/NSM engine            |
| WinPcap/Npcap| Network packet capture drivers for Windows |
| Windows CMD  | Used to run Suricata and simulate attacks  |
| Notepad/IDE  | Edit rule files and configuration files    |

---

## 🛠️ Installation & Setup

### 1. Download & Install Suricata (Windows)
- Download from: [https://suricata.io/download/](https://suricata.io/download/)
- Install and ensure it's placed in:  
  `C:\Program Files\Suricata`

### 2. Install WinPcap or Npcap
- Download and install from:  
  [https://npcap.com/#download](https://npcap.com/#download)

### 3. Add Suricata to Environment Path
To use `suricata.exe` from any directory, add this to your PATH:

 `C:\Program Files\Suricata`

Configuration Steps
4. Verify Installation
Run:
suricata.exe -V
5. Configure the suricata.yaml
Update default-rule-path and enable local.rules in:
C:\Program Files\Suricata\suricata.yaml
Ensure it includes:
rule-files:
  - local.rules
6. Create & Add Rules (Including local.rules)
What is local.rules?

local.rules is a custom rule file where you can define network intrusion detection rules.

By default, this file may not be present in your installation directory, so you can create it manually.

How to Get local.rules:

Option 1: Create local.rules from scratch

Navigate to the rules directory:
C:\Program Files\Suricata\rules\
Create a file called local.rules and add custom rules.
Option 2: Download Sample Rules

Suricata comes with predefined rule sets (some can be downloaded from online repositories).

If you need to download a rule set:

Get Emerging Threats (ET) Rules:

Use the following link to get rules:
Emerging Threats Rule Sets

Extract the .tar.gz file and place the .rules files in the Suricata rules directory (C:\Program Files\Suricata\rules\).

Make sure to include a reference to these rule files in the suricata.yaml configuration.

Running Suricata
✅ Test Configuration
suricata.exe -T -c "C:\Program Files\Suricata\suricata.yaml" -v
✅ Start Live Capture
suricata.exe -c "C:\Program Files\Suricata\suricata.yaml" -i <Interface_Number> -v
