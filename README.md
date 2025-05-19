# 🛰️ Network Traffic Incident Report – DNS & ICMP Analysis

## Scenario 

*This scenario is based on a fictional company:*

As a cybersecurity analyst for an IT services provider, several client customers reported that they were unable to access the client website `www.yummyrecipesforme.com`. Instead, users received a **“destination port unreachable”** error.

I conducted a network traffic investigation using `tcpdump`, a protocol analyzer tool, and discovered ICMP error messages indicating that the DNS server's port 53 was unreachable when queried via UDP.

---
## tcpdump Log

![image](https://github.com/user-attachments/assets/0ab07117-6e7c-466f-988b-4cadcc92ae75)

 
## 📌 Summary of the Problem

- **Protocol involved**: UDP and ICMP  
- **Error Identified**: `udp port 53 unreachable`  
- **Service Impacted**: DNS resolution for `www.yummyrecipesforme.com`  
- **Time of Incident**: 1:24 PM  

The ICMP response confirmed that port 53 (used for DNS queries) was not accepting traffic, preventing DNS resolution and access to the website.

---

## 🔍 Analysis & Findings

- **Incident Discovery**:  
  The issue was reported by multiple clients who were unable to access the website.

- **Analyst Response**:  
  I attempted to access the site, reproduced the error, and launched `tcpdump` to analyze network traffic.

- **Captured Packet Behavior**:
  - A UDP packet was sent from the analyst's IP (`192.51.100.15`) to the DNS server (`203.0.113.2`) on port 53.
  - The DNS server replied with an ICMP message: `udp port 53 unreachable`.
  - This occurred multiple times, indicating a consistent issue.

- **Primary Finding**:  
  DNS server was **not listening on port 53**, preventing resolution of the domain.

- **Probable Cause**:  
  A **"Ping of Death"** or similar denial-of-service event may have caused the DNS server to crash or stop responding on its service port.

---

## 🛡️ Conclusion

The incident revealed that DNS availability was interrupted due to a failure on port 53, confirmed via ICMP traffic analysis. The root cause is suspected to be a **Ping of Death attack**, which disabled the DNS service on the targeted server.

---

## 🧠 Lessons Learned

- Always monitor DNS health and port availability using automated tools.
- Analyze ICMP error codes to understand underlying network service issues.
- Implement protections against denial-of-service attacks on essential services like DNS.

---
### Activity Status
![Status](https://img.shields.io/badge/Status-Analyzed-blue) ![Protocol](https://img.shields.io/badge/Protocol-DNS/ICMP-green) ![Tool Used](https://img.shields.io/badge/Tool-tcpdump-lightgrey) ![Severity](https://img.shields.io/badge/Severity-Moderate-yellow)

---

> _“Every packet tells a story—listen to the ones that signal danger.”_

