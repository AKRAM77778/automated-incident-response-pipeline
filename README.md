# 🚀 Overview

This project implements a zero-touch, closed-loop Security Orchestration, Automation, and Response (SOAR) pipeline. It bridges the gap between high-fidelity threat detection and infrastructure-level containment, reducing the Mean Time to Respond (MTTR) to near-zero.

---

# 🏗️ System Architecture

The architecture follows a decoupled, microservices-based defense-in-depth model:

## 🔍 Detection Layer
- **Suricata (Network IDS)** captures and analyzes malicious network traffic.
- **Wazuh (Host IDS)** collects host-based telemetry, authentication logs, and security events.

## 🧠 Analytical Brain
- **ANAOS SIEM Engine** ingests logs, performs stateful threshold analysis, and enriches events with MITRE ATT&CK classifications:
  - `T1595` — Active Scanning
  - `T1110` — Brute Force

## 🔄 Orchestration Layer
- **Shuffle SOAR** continuously polls the ANAOS REST API and applies boolean logic to eliminate false positives and low-priority noise.

## 🛡️ Enforcement Layer
- **Ansible** dynamically modifies the pfSense firewall routing tables and aliases to immediately isolate malicious hosts at Layer 3.

---

## 📷 Architecture Diagram


<img width="1024" height="559" alt="ARCH" src="https://github.com/user-attachments/assets/dfc10a32-dc4f-4e1a-ad4b-b1ffc86f4388" />

<img width="1024" height="559" alt="ARCH2" src="https://github.com/user-attachments/assets/9802ec02-5d58-4623-bd87-8e4368c73e5b" />

---

# 🛠️ Technical Deep Dive

---

## 1️⃣ Analytical Thresholding (ANAOS API)

Rather than hardcoding static responses, ANAOS exposes stateful alerts through a structured REST API endpoint:


<img width="1024" height="559" alt="B" src="https://github.com/user-attachments/assets/5251da19-2060-4dfa-82d2-69fef97f0ce0" />



