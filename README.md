<div align="center">

# 🏠 Home Lab

### Network Engineering · Security Operations · Detection Engineering

A segmented, security-first home network paired with a virtualized SOC lab —
built for real detection engineering, not just uptime.

<br>

![pfSense](https://img.shields.io/badge/pfSense-212121?style=for-the-badge&logo=pfsense&logoColor=white)
![Proxmox](https://img.shields.io/badge/Proxmox_VE-E57000?style=for-the-badge&logo=proxmox&logoColor=white)
![Wazuh](https://img.shields.io/badge/Wazuh-005C99?style=for-the-badge)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Kali](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-C41E3A?style=for-the-badge)

</div>

<br>

---

## Contents

**Part I — Home Network** *(deployed)*
- [Network Overview](#network-overview)
- [Firewall — pfSense](#firewall-pfsense)
- [VLAN Segmentation](#vlan-segmentation)
- [DNS — Quad9](#dns-quad9)
- [Wireless Access Point](#wireless-access-point)
- [Remote Access — Twingate & Travel Router](#remote-access)
- [Monitoring — Wazuh](#monitoring-wazuh)

**Part II — SOC Detection Lab** *(in progress)*
- [Lab Overview](#lab-overview)
- [Hardware & Hypervisor](#hardware-hypervisor)
- [VM Architecture](#vm-architecture)
- [SIEM — Wazuh SOC Instance](#siem-wazuh-soc)
- [Attack Simulation & Detection Engineering](#attack-simulation)
- [Local AI Log Analysis](#local-ai)

<br>

---

<div align="center">

# Part I — Home Network

*Production network. Deployed and running.*

</div>

---

<a id="network-overview"></a>

## 🗺️ Network Overview

This home lab setup showcases my expertise in advanced network management and cybersecurity practices. By utilizing pfSense, VLANs, managed switches, SIEM integration, and secure remote access via a travel router and VPN, I have built a robust and secure environment that supports a wide range of network activities while ensuring optimal performance and security. This project highlights my ability to design, implement, and manage complex network infrastructures, making me well-prepared for roles in network management and cybersecurity.

<div align="center">
<img width="800" alt="Network diagram" src="./network-diagram.svg" />
</div>

<br>

<a id="firewall-pfsense"></a>

## 🔥 Firewall — pfSense

[![pfSense](https://img.shields.io/badge/pfSense-Website-blue?style=flat-square)](https://www.pfsense.org/)

At the core of my network is a **pfSense firewall**, a powerful open-source solution that provides advanced security, routing, and VPN capabilities. The pfSense setup is integrated with VLAN configurations to ensure segmented and secure communication across different parts of the network. This allows precise control of traffic flow, ensuring each VLAN operates within its designated boundaries for enhanced security.

<br>

<a id="vlan-segmentation"></a>

## 🧩 VLAN Segmentation

A managed switch enforces three distinct VLANs, isolating traffic by function:

| VLAN | Purpose | Isolation |
|:----:|:--------|:----------|
| **VLAN 1** | Default network — general traffic and device communication | Standard |
| **VLAN 2** | Network media — streaming and media devices on an optimized segment | Bandwidth-isolated |
| **VLAN 3** | Test bench — experimentation and staging | **Fully isolated** |

**Test Bench (VLAN 3)** is completely isolated from other network devices. This is critical for testing new configurations, updates, or software without affecting the stability and security of the network — a controlled environment for experimentation and refinement before deployment across the wider infrastructure.

**Network Media (VLAN 2)** keeps media streaming from interfering with other network operations. This dedicated VLAN optimizes bandwidth usage and provides a smooth, uninterrupted experience while maintaining high performance for critical tasks on other VLANs.

<br>

<a id="dns-quad9"></a>

## 🛡️ DNS — Quad9

[![Quad9](https://img.shields.io/badge/Quad9-Website-blue?style=flat-square)](https://quad9.net/)

DNS resolution on port 53 is handled by **Quad9**, a free, security-focused resolver that blocks known malicious domains using threat intelligence from cybersecurity partners.

```
IPv4    9.9.9.9  ·  149.112.112.112
IPv6    2620:fe::fe  ·  2620:fe::9
```

**Why Quad9:**

- **Malware blocking** — automatically blocks domains known for distributing malware, phishing, and botnets, reducing attack surface at the resolution layer
- **Privacy-focused** — does not store personally identifiable information (PII)
- **Global threat intelligence** — integrates feeds from 19+ cybersecurity organizations for real-time protection against emerging threats
- **Resilient** — globally distributed infrastructure delivers high availability and fast resolution even under heavy traffic or disruption

<br>

<a id="wireless-access-point"></a>

## 📶 Wireless Access Point

The wireless access point extends connectivity to wireless devices while maintaining security and performance standards. It supports **multiple SSIDs, each mapped to a specific VLAN**, ensuring wireless traffic is segmented and managed in line with the overall network design — wireless clients land in the correct security zone rather than a flat wireless network.

<br>

<a id="remote-access"></a>

## 🔐 Remote Access — Twingate & Travel Router

[![Twingate](https://img.shields.io/badge/Twingate-Documentation-blue?style=flat-square)](https://www.twingate.com/docs/)

### Twingate — Zero Trust Access

To provide my primary travel laptop with safe, zero-trust access, I added **Twingate** to my main server. I can now connect to my server without leaving it open to the public, guaranteeing that access is verified and approved by strict security policy. By eliminating the need for a conventional VPN, this configuration improves performance and lowers latency while preserving high security — I can safely oversee my server from any location while concealing my network from potential intruders.

**Why Twingate over a conventional VPN:**

| Advantage | What it means in practice |
|:----------|:--------------------------|
| **Least-privilege access** | Rules allow my laptop to reach *only* the required services on my server — not the whole network. Limits blast radius if a device is compromised. |
| **Split tunneling** | Only server traffic routes through the encrypted connection. Normal browsing and streaming aren't slowed by unnecessary rerouting. |
| **No public VPN gateway** | Conventional VPNs expose an internet-facing entry point and are a frequent attack target. Twingate makes internal resources **undetectable to unauthorized users** — no surface for scanning or brute-force. |
| **MFA integration** | Even with compromised credentials, an attacker needs a second factor. |
| **Contextual access control** | Policies can key on device security posture, location, and access time. |

Centralized logging and monitoring also give better visibility into access patterns, making it easier to identify and handle potential risks. This deployment significantly improved both the **security and usability** of my remote server access, consistent with the **Zero Trust Networking** model.

### Travel Router with VPN

A **travel router** connects back to my home network over VPN, allowing secure access to internal resources from anywhere. This protects data when using public or untrusted internet connections — routing traffic through the VPN means I can reach my home network and media securely regardless of the network I'm physically on.

<br>

<a id="monitoring-wazuh"></a>

## 👁️ Monitoring — Wazuh

[![Wazuh](https://img.shields.io/badge/Wazuh-Website-blue?style=flat-square)](https://wazuh.com/)

**Wazuh** runs as the SIEM for the home network, continuously monitoring for threats and anomalies with real-time analysis and alerting. It's integrated with **Discord** for instant notification when devices or services go down, enabling rapid issue resolution and minimal downtime.

> **Note:** This is the *home network monitoring* instance. A separate, purpose-built Wazuh deployment powers the SOC Detection Lab in Part II — see below.

<br>

---

<div align="center">

# Part II — SOC Detection Lab

*Virtualized detection-engineering environment. Build in progress.*

</div>

---

<a id="lab-overview"></a>

## 🎯 Lab Overview

A dedicated, virtualized SOC lab built to do real detection engineering — not just collect logs. The workflow is a closed loop:

```
 Simulate attack  →  Watch what the SIEM catches  →  Find the gaps
        ↑                                                   ↓
   Validate the rule  ←  Write a custom detection  ←────────┘
```

Attack techniques are executed against a disposable target, alerts are evaluated in Wazuh, and any technique that slips past the default ruleset gets a **custom detection rule** written, deployed, and validated. Everything is mapped to **MITRE ATT&CK**.

<br>

<a id="hardware-hypervisor"></a>

## 🖥️ Hardware & Hypervisor

| Component | Spec |
|:----------|:-----|
| **Host** | Lenovo ThinkCentre M710q Tiny |
| **CPU** | Intel i5 (7th gen) |
| **RAM** | 32GB DDR4 SODIMM *(upgraded from 16GB — 2×16GB)* |
| **Storage** | M.2 SSD |
| **Hypervisor** | Proxmox VE |

<br>

<a id="vm-architecture"></a>

## 🧱 VM Architecture

Four VMs share the 32GB host. Memory is managed with **ballooning** so idle VMs release RAM to whichever workload actually needs it.

| VM | Role | RAM | Ballooning |
|:---|:-----|:----|:-----------|
| **Wazuh** | SIEM — manager, indexer, dashboard (all-in-one) | 8–12GB | **Fixed** — the OpenSearch JVM pre-allocates its heap at startup; ballooning risks OOM-killing the indexer mid-run |
| **Ollama** | Local LLM for log analysis and alert enrichment | 4–12GB | Dynamic |
| **Victim** | Disposable attack-simulation target. Snapshotted for instant revert. | 1–4GB | Dynamic |
| **Kali** | Attacker box — enumeration, scanning, offensive tooling | 2–4GB | Dynamic |

**KSM (Kernel Samepage Merging)** is enabled at the host level — since the VMs share similar Debian/Ubuntu base images, deduplicating identical memory pages reclaims meaningful headroom on a 32GB budget.

> **Design note:** attack simulation *never* runs against real endpoints. The Victim VM exists so techniques can be executed aggressively and reverted from snapshot, with zero risk to machines that matter.

<br>

<a id="siem-wazuh-soc"></a>

## 📡 SIEM — Wazuh SOC Instance

Deployed as a single-node **all-in-one** install (manager + indexer + dashboard) on a dedicated Ubuntu Server VM — a VM rather than a container, matching how Wazuh is actually deployed in production environments.

**Firewall rules (pfSense):**

| Port | Protocol | Purpose |
|:-----|:---------|:--------|
| `1514` | TCP/UDP | Agent event ingestion |
| `1515` | TCP | Agent enrollment |
| `443` | TCP | Dashboard (HTTPS) |

<!-- FILL IN AS BUILT -->
**Enrolled agents:**

| Agent | OS | Role |
|:------|:---|:-----|
| *TBD* | *TBD* | *TBD* |

<br>

<a id="attack-simulation"></a>

## ⚔️ Attack Simulation & Detection Engineering

**Atomic Red Team** executes individual, ATT&CK-mapped technique tests against the Victim VM. Each run answers one question: *did the SIEM catch it?*

<!-- FILL IN AS TESTED -->

| Technique | ATT&CK ID | Default Ruleset | Action Taken |
|:----------|:----------|:----------------|:-------------|
| *e.g. OS Credential Dumping* | `T1003` | ❌ Missed | Custom rule written & validated |
| *e.g. Command & Scripting Interpreter* | `T1059` | ✅ Caught | — |

**Custom rules** are drafted in **Sigma** first — portable and vendor-neutral — then converted to Wazuh's XML rule syntax for deployment. Every rule is validated by re-running the Atomic test and confirming the alert fires.

**Tuning log:** noisy default rules that don't apply to a lab environment are documented and adjusted rather than silently ignored — the reasoning behind each tuning decision is recorded.

<br>

<a id="local-ai"></a>

## 🤖 Local AI Log Analysis

An **Ollama** VM runs a quantized local model for alert enrichment and log summarization.

**Why local rather than a cloud API:**

- **Log data never leaves the network.** Auth logs, internal IPs, and hostnames are exactly the data you don't want shipped to a third-party API — a defensible security posture, and a requirement for any real client engagement.
- **No per-token cost** while iterating and testing.

**Architecture — deterministic first, AI second:** events are matched against known ATT&CK signatures and IOC patterns *before* anything reaches the model. Only the ambiguous tail gets sent for AI analysis. Rule-based logic handles the known cases (testable, cheap, fast); the model handles what the rules can't classify.

<br>

---

<div align="center">

*Built and documented as an ongoing exercise in security engineering.*

</div>
