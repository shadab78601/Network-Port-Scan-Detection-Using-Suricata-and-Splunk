Network Port Scan Detection using Suricata IDS and Splunk SIEM

Network Port Scan Detection using Suricata IDS and Splunk SIEM
Project Overview
This project demonstrates how to detect Nmap SYN Port Scan activity using Suricata IDS integrated with Splunk Enterprise in a virtual SOC lab.
A custom Suricata detection rule was created to identify reconnaissance activity generated from a Kali Linux attacker machine. The generated alerts were forwarded to Splunk using Splunk Universal Forwarder, where dashboards were built for real-time visualization and analysis.
This project simulates how a SOC Analyst detects and investigates network reconnaissance attacks.


Attacker
(Kali Linux)
192.168.30.20
        │
        │ Nmap SYN Scan
        ▼
Victim
(Ubuntu + Suricata IDS)
192.168.30.16
        │
        │ eve.json
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Enterprise
(Windows Host)
192.168.1.97


Objective
Detect Nmap SYN Port Scanning
Create Custom Suricata Detection Rule
Forward IDS Logs to Splunk
Build SOC Monitoring Dashboard
Perform Threat Hunting using Splunk Search

Technologies Used
Ubuntu Linux
Kali Linux
Windows 11
Splunk Enterprise
Splunk Universal Forwarder
Suricata IDS
Nmap
VirtualBox
Detection Workflow
Installed and configured Suricata IDS on Ubuntu.
Installed Splunk Universal Forwarder.
Connected Universal Forwarder to Splunk Enterprise.
Monitored Suricata eve.json.
Created a custom Suricata rule to detect Nmap SYN scans.
Restarted Suricata and validated configuration.
Performed an Nmap SYN scan from Kali Linux.
Generated IDS alerts.
Forwarded alerts to Splunk.
Built dashboards to visualize attack activity.

Custom Detection Rule
alert tcp any any -> $HOME_NET any (
msg:"LOCAL Nmap SYN Scan Detected";
flags:S;
threshold:type both, track by_src, count 20, seconds 5;
sid:1000001;
rev:2;
)


Attack Simulation

Attacker Machine (Kali)
sudo nmap -sS -Pn -T4 192.168.30.16

Splunk Searches

Alert Signature
source="/var/log/suricata/eve.json" event_type=alert
| stats count by alert.signature

Top Attacker IP
source="/var/log/suricata/eve.json" event_type=alert
| stats count by src_ip

Alert Timeline
source="/var/log/suricata/eve.json" event_type=alert
| timechart count

Destination Ports
source="/var/log/suricata/eve.json" event_type=alert
| top dest_port
Dashboard

The dashboard contains:

Alert Signature Statistics
Top Source IP Address
Alert Timeline
Destination Port Distribution

Results

✅ Successfully detected Nmap SYN Scan
✅ Custom Suricata Rule Triggered
✅ Alert Generated
✅ Alert Forwarded to Splunk
✅ Dashboard Successfully Created


Skills Demonstrated

SIEM Monitoring
Threat Hunting
IDS Configuration
Suricata Rule Writing
Splunk Search Processing Language (SPL)
Linux Administration
Security Monitoring
Network Traffic Analysis
Detection Engineering
SOC Analyst Workflow

Future Improvements

Email Alerting
Splunk Correlation Searches
Automated Incident Response
SOAR Integration
MITRE ATT&CK Mapping

Learning Outcome

Through this project, I learned how IDS solutions detect reconnaissance activity, 
how custom detection rules are developed,
how security telemetry is forwarded into a SIEM, 
and how SOC dashboards are used to monitor and investigate security events.




