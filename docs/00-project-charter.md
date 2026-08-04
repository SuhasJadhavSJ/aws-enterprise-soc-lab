# Project Charter

## Project Title

Enterprise Cloud Security Operations Center (SOC) on AWS using Wazuh

---

## Project Overview

This project aims to design, build, and operate a production-inspired Security Operations Center (SOC) hosted on Amazon Web Services (AWS) using Wazuh as the Security Information and Event Management (SIEM) platform.

Unlike traditional installation guides that focus only on deployment, this project emphasizes understanding the complete SOC lifecycle—from architecture and infrastructure design to threat detection, investigation, incident response, and continuous improvement.

The objective is to gain practical experience with enterprise SOC operations while producing a well-documented, portfolio-ready project.

---

## Problem Statement

Organizations generate large volumes of security logs from servers, endpoints, cloud services, and applications. Without centralized monitoring, malicious activities such as brute-force attacks, unauthorized access, malware execution, and privilege escalation can remain undetected.

Security Operations Centers (SOCs) solve this challenge by continuously collecting, analyzing, and investigating security events.

This project recreates a simplified enterprise SOC environment in AWS to understand how modern SOC teams detect, investigate, and respond to cyber threats.

---

## Project Objectives

The primary objectives of this project are:

- Build a cloud-hosted SOC environment using AWS.
- Deploy Wazuh as the SIEM platform.
- Collect logs from multiple endpoints.
- Simulate realistic cyber attacks.
- Detect malicious activities using Wazuh.
- Investigate alerts using structured methodologies.
- Map attacks to the MITRE ATT&CK framework.
- Develop custom detection rules.
- Perform threat hunting activities.
- Produce professional documentation and incident reports.

---

## Scope

### Included

- AWS Infrastructure
- Wazuh Deployment
- Linux Endpoint Monitoring
- Windows Endpoint Monitoring (Future)
- Log Collection
- File Integrity Monitoring
- Threat Detection
- Threat Hunting
- Detection Engineering
- Incident Response
- Threat Intelligence Integration
- Security Reporting

### Excluded (Initial Version)

- High Availability (HA)
- Multi-region Deployment
- SOAR Automation
- Commercial Security Products
- Enterprise Active Directory Integration

These features may be implemented in future versions of the project.

---

## Constraints

The following constraints apply to this project:

- AWS Academy credits ($200 / 6 months)
- Kali Linux as the primary local workstation
- Cost-efficient architecture
- Preference for open-source tools
- Portfolio-focused implementation

---

## Expected Outcomes

By the completion of this project, the SOC should be capable of:

- Monitoring multiple endpoints
- Detecting suspicious activities
- Investigating security alerts
- Generating incident reports
- Mapping attacks to MITRE ATT&CK
- Supporting threat hunting activities
- Demonstrating real SOC workflows

---

## Success Criteria

The project will be considered successful if it can:

- Collect logs from all configured endpoints
- Detect simulated attacks
- Generate actionable alerts
- Support complete incident investigations
- Produce reproducible documentation
- Be deployable by following this repository

---

## Project Status

**Current Phase:** Planning & Design

No cloud infrastructure has been deployed yet.
The current objective is to finalize the architecture and implementation plan before provisioning AWS resources.

---

## Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | August 2026 | Initial Project Charter |