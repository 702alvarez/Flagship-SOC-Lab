# 🛡️ Network Detection & Response (NDR) Lab with Security Onion + pfSense

## 🎯 Objective
Design and implement a **Network Detection & Response (NDR) lab** that mirrors real-world SOC environments by integrating pfSense and Security Onion. This project highlights expertise in building and configuring security infrastructure, forwarding and ingesting network logs, detecting adversarial activity with Suricata and Zeek, and performing analyst-level investigations in Kibana.
---

## 🔹 Phase 1: Lab Architecture

<img width="650" height="500" alt="934c0d45-dd5c-4f63-a141-e05e82cbfb5f" src="https://github.com/user-attachments/assets/ba94b100-3060-4454-a88e-f1d2da685968" />


### Components
- **pfSense+ (Netgate 3100)** → Routing, Firewall, DHCP, Syslog forwarder
- **Security Onion** → Core NDR stack:
  - Zeek (protocol analysis)
  - Suricata (IDS/IPS)
  - Elastic Stack (Kibana dashboards, search, analytics)
  - Fleet/Osquery (endpoint visibility)
- **Endpoints**:
  - Windows Server 2022 (AD, DHCP, DNS)
  - Windows 11 client
  - Kali Linux attacker

<img width="1919" height="891" alt="Screenshot 2025-08-26 091457" src="https://github.com/user-attachments/assets/51e6ad40-0951-413e-a439-9a9ad7f8f945" />


---

## 🔹 Phase 2: pfSense Configuration

1. **Syslog Forwarding**
   - Send logs to Security Onion at `192.168.60.20:514`.
   - Categories: Everything (Firewall, DHCP, DNS, etc.).
   
<img width="1918" height="957" alt="Screenshot 2025-08-25 171124" src="https://github.com/user-attachments/assets/a62a34e2-6d26-4047-9b27-45391e0c6d3a" />


2. **Network Services**
   - LAB Subnet: `192.168.60.0/24`
   - Gateway: `192.168.60.1`
   - DHCP Pool: `.50 – .199`
   
<img width="1919" height="955" alt="Screenshot 2025-08-25 171259" src="https://github.com/user-attachments/assets/b1153442-17c9-444b-abef-127d1894ac24" />


3. **Firewall Rules**
   - LAB subnet → any (baseline allow).
   - Will refine for testing detection coverage.
   
<img width="1911" height="895" alt="Screenshot 2025-08-26 091623" src="https://github.com/user-attachments/assets/cd6fded6-764b-4723-8e64-74ae543306f5" />


---

## 🔹 Phase 3: Security Onion Deployment

1. Install Security Onion on a VM with:
   - Management NIC (for UI access)
   - Monitoring NIC (for mirrored/trunked traffic)

2. Verify containers are running with `so-status`.

<img width="571" height="725" alt="Screenshot 2025-08-26 082807" src="https://github.com/user-attachments/assets/dbdae52f-0c2d-47a6-9767-223ea1f4cbe6" />


---

## 🔹 Phase 4: Log Ingestion & Visibility

- pfSense logs successfully ingested into Security Onion.
- Logs searchable under Kibana dashboards.

<img width="999" height="636" alt="Screenshot 2025-08-26 090227" src="https://github.com/user-attachments/assets/e7de4c94-166d-438e-b485-4d74ebdc0fa5" />
<img width="1006" height="638" alt="Screenshot 2025-08-26 092058" src="https://github.com/user-attachments/assets/aae7e379-ec4f-4007-b1d6-e97b6712419d" />

---

## 🔹 Phase 5: Detection (Suricata & Zeek)

### Suricata
- Detects network intrusions and anomalies.
- Sample alerts: ICMP pings, suspicious DNS over HTTPS, possible Kali hostnames.

<img width="1006" height="643" alt="Screenshot 2025-08-26 090312" src="https://github.com/user-attachments/assets/aa58f259-91bf-44e5-ac25-88fdb65f6982" />
<img width="994" height="646" alt="Screenshot 2025-08-26 084419" src="https://github.com/user-attachments/assets/5fe27a05-a6fa-4908-8f03-adc70c4c6964" />

### Zeek
- Provides protocol-level analysis.
- Captures DNS queries, file transfers, and metadata.

<img width="1001" height="638" alt="Screenshot 2025-08-26 090402" src="https://github.com/user-attachments/assets/92835e44-c198-4796-9aa2-7982ea367e84" />
<img width="1014" height="638" alt="Screenshot 2025-08-26 084039" src="https://github.com/user-attachments/assets/5b0139e0-dcf4-4160-b0f5-80deb56af123" />

---

## 🔹 Phase 6: Analyst Workflow

1. **Ingestion Validation** → pfSense logs appear in Kibana.
2. **Detection Review** → Suricata alerts highlight suspicious traffic.
3. **Protocol Context** → Zeek provides DNS/file-level insight.
4. **Correlation** → Events reviewed in Kibana dashboards.

This workflow demonstrates how a SOC analyst can:
- Validate visibility
- Investigate alerts
- Correlate logs for deeper insight

---

## 🔹 Phase 7: Key Takeaways

- **pfSense → Security Onion integration works**: network + system logs forwarded via syslog.
- **Zeek provides rich protocol analytics**: DNS, files, connections.
- **Suricata adds intrusion detection**: signatures catch malicious or suspicious traffic.
- **Elastic dashboards enable investigation**: analysts pivot between alerts, logs, and context.

---

This project proves capability in **network security monitoring, log integration, detection, and SOC analysis workflows** using industry-standard open source tools.
