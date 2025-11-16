# 🛡️ Suricata + Splunk Integration Lab

A hands-on cybersecurity project focused on detecting network scans and
suspicious traffic by integrating **Suricata IDS** with **Splunk**, and
analyzing events alongside **UFW firewall logs**.

This lab demonstrates how Suricata alerts, firewall activity, and Splunk
searches work together to build strong detection engineering skills.

------------------------------------------------------------------------

## 🎯 Objective

To install and configure **Suricata IDS**, forward Suricata logs to
**Splunk**, generate network activity (Nmap scans), and validate
detections using both **Suricata (eve.json)** and **UFW firewall logs**.

------------------------------------------------------------------------

## 🧩 Lab Setup

-   **IDS:** Suricata\
-   **Log Collector / SIEM:** Splunk Enterprise\
-   **Firewall:** UFW (Ubuntu)\
-   **Attacker/Test Machine:** 192.168.204.129\
-   **Monitored Machine:** akshay2

------------------------------------------------------------------------

## ⚙️ Task 1: Install and Configure Suricata

Suricata generates an `eve.json` file where all alert events are logged.

### 🔹 Splunk Search Query

Used to verify Suricata logs coming into Splunk:

    host=akshay2 source="/var/log/suricata/eve.json" src_ip="192.168.204.129"

**Result:** Suricata successfully detected the Nmap scans performed from
the test machine.

------------------------------------------------------------------------

## ⚙️ Task 2: Block Attacker Using UFW

### 🔹 Block the Source IP

``` bash
sudo ufw deny from 192.168.204.129
```

### 🔹 Monitor Live Firewall Logs

``` bash
tail -f /var/log/ufw.log
```

**Example Log Entry:**

    [UFW BLOCK] SRC=192.168.204.129 DPT=34197 PROTO=TCP FLAGS=PSH,FIN,URG

------------------------------------------------------------------------

## ⚙️ Task 3: Ingest UFW Logs into Splunk

### 🔹 Splunk Search Query

    host=akshay2 source="/var/log/ufw.log" SRC="192.168.204.129"

**Result:** Splunk successfully captured firewall block events,
confirming the correlation between Suricata alerts and UFW actions.

------------------------------------------------------------------------

## 🖼 Screenshots

<img width="1920" height="1020" alt="suricata_logs_splunk" src="https://github.com/user-attachments/assets/8ea0e3b3-bb85-4fc6-ab01-037b4186c7cb" />
<img width="1920" height="1020" alt="nmap_blocked_kali" src="https://github.com/user-attachments/assets/e63edd4b-9ed8-42e9-a785-8ff959ee80bc" />
<img width="1920" height="1020" alt="ufw_raw_blocked" src="https://github.com/user-attachments/assets/4f7b9cff-4195-4123-9cab-62d723b44d80" />
<img width="1920" height="1020" alt="ufw_logs_splunk_blocked" src="https://github.com/user-attachments/assets/06bed708-46cf-4851-bd61-bac749fadb3d" />

------------------------------------------------------------------------

## 🏁 Conclusion

This project helped me:\
- Detect Nmap scans using **Suricata IDS**\
- Visualize alerts inside **Splunk dashboards**\
- Block traffic using **UFW firewall rules**\
- Correlate Suricata, UFW, and Splunk logs for deeper visibility\
- Strengthen skills in **SOC monitoring**, **network security**, and
**detection engineering**

------------------------------------------------------------------------

## 🔖 Tags

`#Suricata` `#Splunk` `#UFW` `#IDS` `#SIEM` `#CyberSecurity` `#BlueTeam`
`#DetectionEngineering` `#HandsOnLearning` `#Nmap`
