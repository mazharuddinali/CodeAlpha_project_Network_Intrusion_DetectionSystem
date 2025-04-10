# CodeAlpha_project_Network_Intrusion_DetectionSystem
Network Intrusion Detection System using Suricata (Windows Setup)
Overview
This project sets up a Network-based Intrusion Detection System (NIDS) using Suricata on a Windows machine. Suricata is a powerful open-source threat detection engine capable of real-time intrusion detection (IDS), inline intrusion prevention (IPS), network security monitoring (NSM), and offline pcap processing.

This README guides you through:

Installing Suricata

Configuring rules (including custom local rules)

Generating suspicious traffic

Monitoring alerts

Parsing logs using Python

🧰 Requirements
Windows OS

Python (for log parsing)

WinPcap/Npcap (required by Suricata)

Suricata for Windows

✅ Installation Steps
1. Install Npcap
Suricata depends on Npcap for packet capturing.

Download Npcap: https://nmap.org/npcap/

Run the installer and make sure the following options are checked:

Install Npcap in WinPcap API-compatible Mode

Support loopback traffic ('Npcap Loopback Adapter')

2. Install Suricata
Download Suricata for Windows: https://www.openinfosecfoundation.org/download/

Install it to the default location:
C:\Program Files\Suricata

3. Update Rules (Optional but Recommended)
Suricata includes a rule updater, but on Windows, it might not be pre-installed.

You can manually download the Emerging Threats rules, extract them, and move selected .rules files to:
`C:\Program Files\Suricata\rules`
Update suricata.yaml to include these rule files if needed.

4. Add a Local Rule
1) Navigate to:
C:\Program Files\Suricata\rules
2) Create a file named local.rules if it doesn't exist.

3)  Open it as Administrator and paste the following sample rule:
alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)

4) In suricata.yaml, make sure local.rules is included. Look for the rule-files section and verify:
rule-files:
  - local.rules

5. Run Suricata in Test Mode (Verify Setup)
Open Command Prompt as Administrator:
cd "C:\Program Files\Suricata"
suricata.exe -T -c "C:\Program Files\Suricata\suricata.yaml" -v
This will validate your configuration and rules.

6. Run Suricata to Monitor Traffic
Run this to start Suricata in IDS mode:

suricata.exe -c "C:\Program Files\Suricata\suricata.yaml" -i 1 -v

Replace -i 1 with your actual network interface number if different.


7. Generate Suspicious Activity
To trigger the sample rule, open Command Prompt and ping any address:

ping 8.8.8.8
Suricata will log this ICMP activity as an alert based on the rule.

8. Parse Alerts using Python
Use this Python script to parse the alerts from eve.json:

``import json
import os

log_file = "C:\\Program Files\\Suricata\\log\\eve.json"

if not os.path.exists(log_file):
    print("eve.json not found.")
else:
    with open(log_file, "r") as file:
        for line in file:
            try:
                data = json.loads(line)
                if "alert" in data:
                    print(f"\nALERT: {data['alert']['signature']}")
                    print(f"Source IP: {data['src_ip']} -> Destination IP: {data['dest_ip']}")
                    print(f"Timestamp: {data['timestamp']}")
            except json.JSONDecodeError:
                continue``

💡 How to Add More Rules?
Download additional .rules files (e.g., from Emerging Threats).

Place them in C:\Program Files\Suricata\rules.

Add filenames to the rule-files list in suricata.yaml.

Restart Suricata.
