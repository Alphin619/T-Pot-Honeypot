# 🍯 HoneyPot - T-Pot

## 📌 <ins>Objective</ins>
Set up a T-Pot honeypot to capture attacker interactions through brute-force attacks, log commands, and analyze attack telemetry. The goal was to gain hands-on experience with honeypots, attack detection, and SOC-style threat analysis.

---

## <ins>Overview</ins>
T-Pot is an all-in-one honeypot platform integrating **20+ honeypots**, storing logs in Elasticsearch, and providing multiple tools to visualize, analyze, and enrich attacker data.

---

## 🧪<ins>Environment Setup</ins>
1. Download Ubuntu 24.04.3 Live Server: [Ubuntu ISO](https://releases.ubuntu.com/24.04/ubuntu-24.04.3-live-server-amd64.iso)
2. Launch VM in VirtualBox:
   - Adapter 1: Bridged with Promiscuous Mode (capture real attacks)
   - Adapter 2: NAT (admin access/web interface)
   - 16GB RAM & 250GB Storage
3. Install Docker:  
`wget https://wiki.kitpro.us/install-docker.sh`  
`sudo chmod +x install-docker.sh`  
4. Clone T-Pot repository and set ownership:  
`git clone https://github.com/telekom-security/tpotce.git`  
`sudo chown -R <username:username> /home/<username>/tpotce`  
`cd tpotce`  
![IMG-20260211-WA0017](https://github.com/user-attachments/assets/e5921366-40d4-48d6-b22e-50b31956ee6f)

### Install T-Pot:  
`./install.sh`  
Select (H) Hive deployment  
<img width="924" height="788" alt="Screenshot 2026-02-07 161025" src="https://github.com/user-attachments/assets/26e0329e-a26b-4c59-a13a-f6466eb19cf2" />  
Create admin user for web interface  
> ⚠️Note: SSH port changes from 22 → 64295, reboot after installation.  
<img width="983" height="754" alt="Screenshot 2026-02-07 162756" src="https://github.com/user-attachments/assets/2491e190-b47f-4c65-9b44-7f93c0acc6a2" />

#### Verify Docker is running:  
`docker ps` should show Active (running)  
![IMG-20260211-WA0016](https://github.com/user-attachments/assets/1ef27cbc-d88d-4db1-b09a-a9dbadb3b261)

#### Accessing the Dashboard  
Open browser: `https://<vm-ip>:94297`  
Login with credentials created during setup.

---

![IMG-20260211-WA0010](https://github.com/user-attachments/assets/34c061c6-9398-4078-bc62-9460f793c9ff)

## <ins>Tools Overview</ins>
| Tool           | Purpose                           | Notes                                                |
| -------------- | --------------------------------- | ---------------------------------------------------- |
| **Attack Map** | Visualizes real-time attacks      | Shows source IPs, geo-location, and attack intensity |
| **Kibana**     | Analyze honeypot logs             | Timeline, correlation, filtering per honeypot        |
| **Elasticvue** | Inspect raw Elasticsearch indices | Debug ingestion, check document health               |
| **CyberChef**  | Decode attacker payloads          | Analyze base64, hex, URLs, malware strings           |
| **SpiderFoot** | Enrich IPs/domains with OSINT     | Provides context for attribution and risk assessment |

### <ins>Testing & Results</ins>

Performed brute-force attacks from Kali Linux:  
`ssh Thebigman@<tpot-ip>`  
<img width="711" height="250" alt="Screenshot 2026-02-10 232531" src="https://github.com/user-attachments/assets/f11d0b34-ab45-4d07-8f6d-558a3d7b6cdc" />

`telnet <tpot-ip>`  
<img width="1344" height="509" alt="Screenshot 2026-02-11 151928" src="https://github.com/user-attachments/assets/6ee5495e-8bba-48e7-b41c-1b097ba07707" />

#### Dashboard provided:  
- Honeypot alert counts  ![IMG-20260211-WA0012](https://github.com/user-attachments/assets/ecd2e7a9-43cd-4c85-b48f-a4fb576388c1)

- Ports targeted  ![IMG-20260211-WA0013](https://github.com/user-attachments/assets/a58b743c-53a3-4b65-b2e9-c2fdbf55732b)

- Source IP addresses  ![IMG-20260211-WA0014](https://github.com/user-attachments/assets/5dc8fed0-33f5-43bf-8d27-e19145ee6aba)

- Commands executed and counts
  
#### Observed logs in Cowrie dashboard:  
![IMG-20260211-WA0015](https://github.com/user-attachments/assets/d63d5f2e-92a1-483d-8028-d99e601a0272)
- Captured attempted usernames & passwords  
- Commands executed inside honeypot  
- Number of attempts per user/command

--- 

## <ins>Summary</ins>
- Honeypots successfully captured attacker activity  
- Elasticsearch stored logs reliably  
- Kibana allowed detailed analysis and correlation  
- Attack Map provided visualization  

### Outcome:
End-to-end deployment, attack simulation, and telemetry analysis achieved with T-Pot, demonstrating hands-on experience with modern honeypot-based threat detection and SOC monitoring.
