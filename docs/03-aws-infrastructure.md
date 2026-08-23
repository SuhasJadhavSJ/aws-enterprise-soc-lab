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

## Public Subnet Implementation

The public subnet was created successfully inside `soc-vpc`.

- Name: `soc-public-subnet`
- CIDR: `10.0.1.0/24`
- Availability Zone: `ap-south-1a`

The subnet is not yet Internet-accessible. Internet connectivity will be established after configuring the Internet Gateway and public route table.

## Private Subnet Implementation

The private subnet was successfully created inside `soc-vpc`.

- Name: `soc-private-subnet`
- CIDR: `10.0.2.0/24`
- Availability Zone: `ap-south-1a`

The subnet is intended to host internal monitored systems that should not receive direct public IP addresses.

Internet accessibility will be determined by the route configuration and will be intentionally restricted.

## Internet Gateway Implementation

An Internet Gateway named `soc-igw` was created and attached to `soc-vpc`.

The Internet Gateway provides the VPC with a connection point to the public Internet.

At this stage, the public subnet is still not Internet-accessible because no default route to the Internet Gateway has been configured yet.


## Private Route Table Implementation

A private route table named `soc-private-rt` was created and associated with `soc-private-subnet`.

The route table contains the local VPC route:

- `10.0.0.0/16` → Local

No default Internet Gateway route was configured.

This prevents the private subnet from having a direct Internet route through the Internet Gateway.



## Public Route Table Implementation

A public route table named `soc-public-rt` was created and associated with `soc-public-subnet`.

The route table contains:

- `10.0.0.0/16` → Local
- `0.0.0.0/0` → `soc-igw`

The default route allows Internet-bound traffic from the public subnet to reach the Internet Gateway.

The private subnet is intentionally not associated with this route table.

## Wazuh Server EC2 Deployment

The SOC server EC2 instance was successfully launched in the AWS Mumbai region.

### Instance Configuration

- Instance Name: `soc-server`
- Instance Type: `m7i-flex.large`
- Operating System: Ubuntu Server 24.04 LTS
- VPC: `soc-vpc`
- VPC CIDR: `10.0.0.0/16`
- Subnet: `soc-public-subnet`
- Subnet CIDR: `10.0.1.0/24`
- Security Group: `soc-server-sg`
- Root Storage: 50 GiB gp3
- SSH Key Pair: `soc-key`

### Deployment Status

EC2 instance successfully launched.

Infrastructure validation and SSH connectivity testing will be performed before installing Wazuh.


## SSH Connectivity Validation

SSH connectivity from the Kali Linux host to `soc-server` was successfully established.

### Validated Path

```text
Kali Linux
    ↓
Internet
    ↓
AWS Internet Gateway
    ↓
soc-vpc
    ↓
soc-public-subnet
    ↓
soc-server-sg
    ↓
soc-server


## Linux Server Baseline

Baseline measurements were collected immediately after establishing SSH connectivity and before installing Wazuh.

### Operating System

- OS: Ubuntu 24.04.4 LTS
- Kernel: 6.17.0-1017-aws
- Architecture: x86_64

### Compute

- vCPU: 2
- CPU model: Intel Xeon Platinum 8488C
- RAM: 7.6 GiB
- Swap: 0 B

### Storage

- Root filesystem: 48 GiB
- Used: approximately 1.9 GiB
- Available: approximately 46 GiB
- Root utilization: 4%

### Network

- Private IP: `10.0.1.162`
- Subnet: `10.0.1.0/24`
- Default gateway: `10.0.1.1`
- Network interface: `enp39s0`

### Listening Services

| Protocol | Port | Bind Address | Service |
|---|---:|---|---|
| TCP | 22 | `0.0.0.0` / `::` | SSH |
| TCP | 53 | `127.0.0.53` / `127.0.0.54` | systemd-resolved |
| UDP | 53 | `127.0.0.53` / `127.0.0.54` | systemd-resolved |
| UDP | 68 | `10.0.1.162` | DHCP |
| UDP | 323 | `127.0.0.1` / `::1` | chronyd |

### Baseline Assessment

The server is operational and suitable for beginning the lab. However, the instance has only 2 vCPUs compared with Wazuh's recommended 4 vCPUs for a 1–25 agent single-node quickstart deployment.

The lab will therefore monitor CPU, memory, disk utilization, and Wazuh service health during deployment and investigation exercises.

The absence of swap is also recorded as a baseline condition rather than treated as an error. Wazuh indexer memory management will be configured according to the official deployment guidance.

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