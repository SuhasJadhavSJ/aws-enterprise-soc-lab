# AWS Infrastructure Design

## Overview

The Enterprise Cloud SOC will be deployed on Amazon Web Services (AWS) using a custom Virtual Private Cloud (VPC). Rather than using the default AWS networking configuration, a dedicated VPC will be created to simulate an enterprise network architecture and provide a better understanding of cloud networking concepts.

The infrastructure is designed to be secure, modular, cost-effective, and scalable while remaining within the AWS Free Tier credits available for this project.

---

# Infrastructure Objectives

The AWS infrastructure is designed to:

- Host the Wazuh platform securely.
- Separate public-facing and internal resources.
- Demonstrate enterprise cloud networking concepts.
- Support secure communication between monitored endpoints and the SOC server.
- Allow future expansion without redesigning the environment.

---

# Planned AWS Services

| Service | Purpose |
|----------|---------|
| Amazon VPC | Private network for SOC infrastructure |
| Public Subnet | Hosts the Wazuh server |
| Private Subnet | Hosts monitored internal servers |
| Internet Gateway | Internet access for public resources |
| Route Tables | Network traffic routing |
| Security Groups | Instance-level firewall |
| EC2 | Virtual machines |
| Elastic IP | Static public IP for Wazuh |
| IAM | Secure AWS access and permissions |
| EBS | Persistent storage for EC2 instances |

---

# Infrastructure Layout

Internet

↓

Internet Gateway

↓

AWS VPC

├── Public Subnet
│
│ └── SOC-Server (Ubuntu + Wazuh)
│
└── Private Subnet
│
└── SOC-Client-01 (Ubuntu Agent)

↓

Kali Linux Host (Local)

↓

Encrypted Wazuh Agent Communication

---

# EC2 Instances

## SOC-Server

Purpose:

Host the Wazuh platform.

Components:

- Wazuh Manager
- Wazuh Dashboard
- Wazuh Indexer

Operating System:

Ubuntu Server LTS

Public IP:

Elastic IP

---

## SOC-Client-01

Purpose:

Internal monitored Linux endpoint.

Responsibilities:

- Generate authentication logs
- Generate system logs
- Simulate user activity
- Participate in attack simulations

Operating System:

Ubuntu Server LTS

Public IP:

None

Communication:

Private VPC network.

---

## Kali Linux

Purpose:

Primary analyst workstation and attack simulation system.

Responsibilities:

- Remote administration
- SSH management
- Attack simulation
- Investigation
- Threat hunting
- Documentation

This system remains outside AWS.

---

# Network Design

The environment consists of one custom VPC.

Inside the VPC:

- One Public Subnet
- One Private Subnet

Public resources:

- SOC Server

Private resources:

- Ubuntu Endpoint

This separation reduces the exposure of internal systems to the Internet while maintaining secure administrative access.

---

# Security Design

The following security principles will be implemented:

- Principle of Least Privilege
- Minimal inbound ports
- Secure SSH access
- Restricted Security Groups
- Private communication inside the VPC
- Encrypted agent communication

---

## Implementation Status

The custom VPC was successfully created in the AWS Mumbai region.

VPC Name: `soc-vpc`

CIDR: `10.0.0.0/16`

Status: Available

The VPC will serve as the isolated network boundary for the SOC infrastructure.

# Future Expansion

The infrastructure is intentionally designed for future additions, including:

- Windows Endpoint
- Additional Linux Servers
- CloudTrail Integration
- VPC Flow Logs
- Suricata IDS
- Sigma Rules
- YARA Integration
- Threat Intelligence Feeds
- Security Automation
- Malware Analysis Environment

---

# Infrastructure Summary

This AWS infrastructure provides the foundation for the Enterprise Cloud SOC. By separating public and private resources and using core AWS networking services, the environment closely resembles real-world cloud deployments while remaining suitable for learning and experimentation.