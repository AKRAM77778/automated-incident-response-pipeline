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


- `ARCH.jpg`
- `ARCH2.jpg`

---

# 🛠️ Technical Deep Dive

---

## 1️⃣ Analytical Thresholding (ANAOS API)

Rather than hardcoding static responses, ANAOS exposes stateful alerts through a structured REST API endpoint:

```http
/api/alerts
