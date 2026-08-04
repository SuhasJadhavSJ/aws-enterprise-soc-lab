# System Architecture

## Overview

The Enterprise Cloud Security Operations Center (SOC) is designed using Amazon Web Services (AWS) as the cloud platform and Wazuh as the centralized Security Information and Event Management (SIEM) solution.

The architecture follows a centralized monitoring model where security events from multiple endpoints are collected, analyzed, and presented through a single management dashboard.

The design emphasizes simplicity, scalability, and cost efficiency while remaining close to the architecture used in enterprise SOC environments.

---

# Architecture Goals

The architecture is designed to achieve the following objectives:

- Centralize security logs
- Detect malicious activities
- Support incident investigations
- Monitor endpoint health
- Provide a scalable monitoring platform
- Minimize infrastructure cost
- Support future expansion

---

# High-Level Architecture

```

+-----------------------------------------------------------+
\|                      Internet                             |
+--------------------------+--------------------------------+
|
|
HTTPS / SSH
|
+-----------------------------------------------------------+
\| AWS Cloud                           |
\| |
\| +-------------------------------+ |
\| | Ubuntu EC2 Instance | |
\| | | |
\| | +-------------------------+ | |
\| | | Wazuh Dashboard | | |
\| | +-------------------------+ | |
\| | | Wazuh Manager | | |
\| | +-------------------------+ | |
\| | | Wazuh Indexer | | |
\| | +-------------------------+ | |
\| +-------------------------------+ |
+--------------------------+--------------------------------+
|
Encrypted Agent Communication
|
+-------------------------+------------------------+
| |
| |
+---------------+ +------------------+
| Kali Linux | | Windows Agent |
| (Host) | | (Future Phase) |
+---------------+ +------------------+
|
+------------------+
| Linux Agent |
| (Future Phase) |
+------------------+

```

---

# Architecture Components

## AWS Cloud

AWS provides the cloud infrastructure required to host the centralized SOC.

Responsibilities include:

- Compute resources
- Networking
- Storage
- Secure remote access
- Scalability

---

## Ubuntu EC2 Server

The Ubuntu EC2 instance serves as the primary SOC server.

Responsibilities:

- Hosting Wazuh
- Receiving endpoint logs
- Running detection rules
- Storing alerts
- Providing dashboard access

---

## Wazuh Manager

The Wazuh Manager is responsible for:

- Receiving logs from agents
- Decoding events
- Rule evaluation
- Alert generation
- Agent management

---

## Wazuh Indexer

The Wazuh Indexer stores:

- Security events
- Alerts
- Agent information
- Historical logs

The Indexer enables fast searching and dashboard visualization.

---

## Wazuh Dashboard

The Dashboard provides:

- Security monitoring
- Alert visualization
- Agent management
- Threat hunting
- Compliance reports
- Vulnerability information

---

## Wazuh Agents

Endpoints run Wazuh Agents responsible for collecting telemetry.

Examples include:

- Authentication logs
- Process creation
- File changes
- System inventory
- Package information
- Network activity

Initially, the Kali Linux host will be enrolled as the primary monitored endpoint.

Additional agents will be added in later phases.

---

# Data Flow

The SOC follows the following workflow:

1. Activity occurs on an endpoint.
2. The Wazuh Agent collects the event.
3. The event is securely transmitted to the Wazuh Manager.
4. The Manager processes the event.
5. Detection rules are evaluated.
6. Alerts are generated if malicious behavior is detected.
7. Alerts are indexed by the Wazuh Indexer.
8. The Dashboard displays the results.
9. The SOC analyst investigates the alert.
10. Findings are documented and remediation actions are taken if required.

---

# Communication Flow

Endpoint

↓

Wazuh Agent

↓

Encrypted Communication (TCP)

↓

Wazuh Manager

↓

Rule Engine

↓

Alert

↓

Indexer

↓

Dashboard

↓

SOC Analyst

---

# Future Expansion

The architecture is intentionally designed to support additional security services without requiring major redesign.

Planned future integrations include:

- Windows Endpoint Monitoring
- Additional Linux Servers
- AWS CloudTrail
- VPC Flow Logs
- Suricata IDS
- Sigma Rules
- YARA Rules
- Threat Intelligence Feeds
- VirusTotal Integration
- AbuseIPDB Integration
- Security Automation
- Incident Response Playbooks

---

# Security Considerations

The architecture follows several security principles:

- Principle of Least Privilege
- Encrypted agent communication
- Restricted inbound access
- Centralized log management
- Regular system updates
- Secure SSH access
- Controlled security group rules

---

# Architecture Summary

The architecture provides a centralized, scalable, and cost-efficient SOC platform capable of monitoring multiple endpoints, detecting security events, supporting investigations, and serving as a foundation for advanced security operations.

The modular design allows future expansion while maintaining a simple deployment suitable for AWS Free Tier resources.