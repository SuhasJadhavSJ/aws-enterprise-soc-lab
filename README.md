# Enterprise Cloud SOC Lab on AWS using Wazuh

## Project Overview

This project documents the design, implementation, and operation of a cloud-based Security Operations Center (SOC) built on Amazon Web Services (AWS) using Wazuh as the Security Information and Event Management (SIEM) platform.

The objective is not only to deploy a SIEM solution but also to understand the complete lifecycle of security monitoring, detection engineering, incident investigation, threat hunting, and continuous improvement. Every configuration, architectural decision, investigation, and lesson learned is documented throughout the project.

---

# Objectives

* Build a production-inspired SOC environment on AWS.
* Deploy and configure Wazuh Manager, Indexer, and Dashboard.
* Collect logs from Linux and future Windows endpoints.
* Investigate real security events and alerts.
* Develop custom detection rules and decoders.
* Perform threat hunting using collected telemetry.
* Map detections to the MITRE ATT&CK framework.
* Produce professional incident reports.
* Document every phase of implementation and operation.

---

# Learning Goals

This project focuses on understanding:

* AWS infrastructure for security operations
* SIEM architecture
* Log collection and normalization
* Endpoint monitoring
* Detection engineering
* Threat intelligence enrichment
* Incident response
* Threat hunting
* SOC analyst workflows
* Security documentation and reporting

---

# Planned Architecture

The SOC environment will consist of:

* AWS-hosted Wazuh Server
* Wazuh Dashboard
* Wazuh Indexer
* Linux endpoint monitoring
* Windows endpoint monitoring (future phase)
* Centralized log collection
* Threat detection engine
* Investigation workflows

A detailed architecture diagram will be created before deployment.

---

# Project Phases

1. Project Planning
2. AWS Infrastructure
3. Wazuh Deployment
4. Agent Enrollment
5. Log Collection
6. Detection Engineering
7. Attack Simulation
8. Incident Investigation
9. Threat Hunting
10. Reporting and Documentation

---

# Repository Structure

* docs/ – Project documentation
* architecture/ – Architecture notes
* diagrams/ – Network and SOC diagrams
* screenshots/ – Configuration evidence
* scripts/ – Automation scripts
* reports/ – Incident reports
* logs/ – Sample log files
* resources/ – Reference material

---

# Current Status

**Phase:** Planning and Architecture

This repository is being developed incrementally. Every phase will include theory, implementation, validation, troubleshooting, screenshots, and lessons learned to create a complete learning resource and portfolio project.
