# Deployment Plan

## Overview

This document outlines the implementation strategy for building the Enterprise Cloud Security Operations Center (SOC). The deployment is divided into multiple phases to ensure that every component is fully understood, tested, and documented before introducing additional complexity.

Each phase concludes with validation steps to verify the environment is functioning correctly before progressing to the next stage.

---

# Deployment Strategy

The project follows an incremental deployment model.

Each completed phase becomes the foundation for the next phase.

The deployment process consists of:

Planning

↓

AWS Infrastructure

↓

Wazuh Installation

↓

Agent Enrollment

↓

Log Collection

↓

Attack Simulation

↓

Threat Detection

↓

Incident Investigation

↓

Threat Hunting

↓

Detection Engineering

↓

Threat Intelligence

↓

Reporting

---

# Phase 0 – Planning

Objective

- Define project goals
- Design architecture
- Document infrastructure
- Prepare deployment plan

Deliverables

- Project documentation
- Architecture documentation
- Infrastructure design
- Deployment roadmap

Status

Completed

---

# Phase 1 – AWS Infrastructure

Objective

Build the cloud infrastructure required for the SOC.

Tasks

- Create a VPC
- Configure networking
- Create subnets
- Configure routing
- Configure Security Groups
- Launch EC2 instances
- Configure Elastic IP
- Verify connectivity

Deliverables

- Functional AWS infrastructure
- Secure networking
- Accessible Wazuh server

---

# Phase 2 – Wazuh Deployment

Objective

Deploy the Wazuh platform.

Tasks

- Install Wazuh
- Configure Dashboard
- Configure Manager
- Configure Indexer
- Verify installation

Deliverables

- Operational SIEM platform

---

# Phase 3 – Endpoint Onboarding

Objective

Enroll monitored endpoints.

Tasks

- Install Wazuh Agent on Kali
- Install Wazuh Agent on Ubuntu
- Verify connectivity
- Confirm log ingestion

Deliverables

- Multiple monitored endpoints

---

# Phase 4 – Log Collection

Objective

Understand the telemetry collected by the SIEM.

Tasks

- Authentication logs
- System logs
- Process monitoring
- File Integrity Monitoring
- Inventory collection

Deliverables

- Centralized log visibility

---

# Phase 5 – Attack Simulation

Objective

Generate realistic security events.

Activities

- SSH Brute Force
- Nmap Scan
- Privilege Escalation
- File Modification
- Malware Simulation
- Reverse Shell
- Web Enumeration

Deliverables

- Real security alerts

---

# Phase 6 – Detection

Objective

Analyze security alerts.

Tasks

- Alert triage
- Rule analysis
- Alert severity
- MITRE ATT&CK mapping

Deliverables

- Investigated alerts

---

# Phase 7 – Threat Hunting

Objective

Perform proactive investigations.

Activities

- Search suspicious processes
- Search failed logins
- Hunt persistence
- Hunt privilege escalation
- Hunt lateral movement

Deliverables

- Threat hunting reports

---

# Phase 8 – Detection Engineering

Objective

Improve detection capabilities.

Tasks

- Create custom rules
- Create custom decoders
- Tune alerts
- Reduce false positives

Deliverables

- Custom detection content

---

# Phase 9 – Threat Intelligence

Objective

Enrich investigations.

Integrations

- VirusTotal
- AbuseIPDB
- GeoIP

Deliverables

- Enriched investigations

---

# Phase 10 – Incident Response

Objective

Handle incidents using structured workflows.

Tasks

- Evidence collection
- Timeline reconstruction
- Root cause analysis
- Containment
- Recovery
- Lessons learned

Deliverables

- Incident reports

---

# Project Completion Criteria

The project is considered complete when:

- AWS infrastructure is operational.
- Wazuh is deployed successfully.
- Multiple endpoints are monitored.
- Simulated attacks generate alerts.
- Alerts are investigated.
- Detection rules are customized.
- Threat hunting exercises are completed.
- Professional documentation is published.

---

# Change Management

Changes to the infrastructure should follow this process:

Plan

↓

Document

↓

Implement

↓

Validate

↓

Commit to GitHub

This ensures the repository remains reproducible and every architectural decision is traceable.

---

# Current Status

Current Phase:

Planning Complete

Next Phase:

AWS Infrastructure Deployment