# Project Overview

## Introduction

Security Operations Centers (SOCs) are responsible for continuously monitoring, detecting, investigating, and responding to cybersecurity threats across an organization's infrastructure. Modern SOCs rely on Security Information and Event Management (SIEM) platforms to collect logs from multiple systems, correlate events, detect suspicious activities, and assist security analysts during investigations.

This project focuses on designing and implementing a cloud-based Security Operations Center (SOC) using Amazon Web Services (AWS) and Wazuh. The environment is designed to simulate real-world enterprise security operations while remaining cost-effective and reproducible.

---

# Why This Project?

Traditional cybersecurity learning often focuses on installing tools without explaining how they work together. This project takes a different approach by building a SOC from the ground up while understanding every architectural and technical decision.

The objective is not only to deploy Wazuh but also to understand:

- How logs are generated
- How logs travel across the network
- How SIEM platforms process events
- How alerts are generated
- How SOC analysts investigate incidents
- How detection rules are created
- How organizations improve their security posture over time

---

# Why AWS?

Running an enterprise SOC locally requires significant hardware resources, including multiple virtual machines and substantial memory and storage. Since the local workstation has limited hardware, AWS provides a practical cloud environment for hosting the SOC infrastructure.

Using AWS also provides hands-on experience with cloud technologies that are commonly used in modern enterprise environments.

Benefits include:

- Scalable infrastructure
- Remote accessibility
- Enterprise-like deployment
- Reliable networking
- Cost-effective using AWS credits
- Real-world cloud experience

---

# Why Wazuh?

Wazuh is an open-source Security Information and Event Management (SIEM) and Extended Detection and Response (XDR) platform. It provides centralized log collection, endpoint monitoring, threat detection, vulnerability assessment, file integrity monitoring, and security event correlation.

Key capabilities include:

- Log Collection
- Endpoint Security Monitoring
- File Integrity Monitoring (FIM)
- Vulnerability Detection
- Threat Detection
- Compliance Monitoring
- Custom Rules
- MITRE ATT&CK Mapping
- Dashboard Visualization

---

# Technologies Used

| Technology | Purpose |
|------------|---------|
| AWS EC2 | Host the Wazuh server |
| Ubuntu Server | Operating system for Wazuh |
| Wazuh | SIEM platform |
| Kali Linux | Primary monitored endpoint and attack simulation machine |
| Git & GitHub | Version control and project documentation |
| OpenSearch | Log indexing and searching |
| Linux | System administration |
| SSH | Secure remote administration |

Additional technologies will be introduced as the project evolves.

---

# Project Goals

The project is designed to achieve the following objectives:

- Build a production-inspired SOC environment
- Learn SIEM architecture
- Collect and analyze logs
- Simulate cyber attacks
- Investigate security incidents
- Perform threat hunting
- Develop detection rules
- Map attacks to the MITRE ATT&CK framework
- Produce professional documentation

---

# Skills Demonstrated

Upon completion, this project will demonstrate practical experience in:

- Cloud Security
- AWS Infrastructure
- SIEM Deployment
- Security Monitoring
- Endpoint Security
- Log Analysis
- Threat Detection
- Threat Hunting
- Detection Engineering
- Incident Response
- Digital Forensics
- Security Documentation

---

# Project Deliverables

The final project will include:

- AWS-hosted SOC environment
- Fully configured Wazuh deployment
- Multiple monitored endpoints
- Simulated attack scenarios
- Investigation reports
- Threat hunting exercises
- Detection engineering examples
- MITRE ATT&CK mapping
- Comprehensive technical documentation
- Portfolio-ready GitHub repository

---

# Current Phase

The project is currently in the planning stage. Infrastructure deployment has not yet begun. The immediate focus is on defining the architecture, implementation strategy, and documentation standards before provisioning cloud resources.