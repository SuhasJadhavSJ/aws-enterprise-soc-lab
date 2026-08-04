# Network Design

## Overview

A well-designed network is the foundation of any secure cloud environment. This document defines the network architecture for the Enterprise Cloud Security Operations Center (SOC) hosted on AWS.

The design follows cloud security best practices by separating internet-facing resources from internal systems while maintaining secure communication between all components.

---

# Network Objectives

The network is designed to:

- Securely host the Wazuh platform.
- Isolate monitored endpoints.
- Minimize the attack surface.
- Allow secure administration.
- Support future expansion.
- Simulate a real enterprise cloud environment.

---

# VPC Design

A dedicated Virtual Private Cloud (VPC) will be created instead of using the default AWS VPC.

**VPC Name**

soc-vpc

**CIDR Block**

10.0.0.0/16

This provides 65,536 IP addresses, which is more than enough for future expansion.

---

# Subnet Design

## Public Subnet

Name

soc-public-subnet

CIDR

10.0.1.0/24

Purpose

Hosts the Wazuh Server.

Resources

- Wazuh Server
- Elastic IP

---

## Private Subnet

Name

soc-private-subnet

CIDR

10.0.2.0/24

Purpose

Hosts monitored internal systems.

Resources

- Ubuntu Agent

The private subnet will not receive public IP addresses.

---

# Internet Gateway

Name

soc-igw

Purpose

Provides internet connectivity to resources in the public subnet.

Without the Internet Gateway, the Wazuh Dashboard and SSH access would not be possible.

---

# Route Tables

## Public Route Table

Name

soc-public-rt

Routes

Destination

0.0.0.0/0

Target

Internet Gateway

Associated Subnet

Public Subnet

---

## Private Route Table

Name

soc-private-rt

Associated Subnet

Private Subnet

Initially, the private subnet will not have direct internet access. Additional components such as a NAT Gateway may be introduced in future phases if required.

---

# Security Groups

## SOC Server Security Group

Name

soc-server-sg

Inbound Rules

| Protocol | Port | Purpose |
|----------|------|---------|
| SSH | 22 | Remote administration |
| HTTPS | 443 | Wazuh Dashboard |
| Wazuh Agent | 1514 | Agent communication |
| Wazuh Registration | 1515 | Agent enrollment |
| Wazuh API | 55000 | API communication |

Outbound Rules

Allow all outbound traffic.

---

## SOC Client Security Group

Name

soc-client-sg

Inbound Rules

| Protocol | Port | Purpose |
|----------|------|---------|
| SSH | 22 | Remote administration |

Outbound Rules

Allow all outbound traffic.

---

# Communication Flow

Kali Linux

↓

SSH

↓

SOC Server

↓

Private Network

↓

Ubuntu Agent

---

# Log Flow

Ubuntu Agent

↓

Wazuh Agent

↓

TCP 1514

↓

Wazuh Manager

↓

Rules Engine

↓

Indexer

↓

Dashboard

↓

SOC Analyst

---

# Dashboard Access

Browser

↓

HTTPS

↓

Elastic IP

↓

Wazuh Dashboard

---

# SSH Administration

Administrator

↓

SSH

↓

SOC Server

↓

SSH

↓

Ubuntu Agent

---

# Future Network Expansion

The network has been designed to support:

- Windows Endpoint
- Additional Linux Servers
- CloudTrail
- VPC Flow Logs
- Suricata IDS
- Zeek
- Bastion Host
- VPN Access
- Multi-AZ Deployment

---

# Security Considerations

The following security principles will be followed:

- Principle of Least Privilege
- Restricted inbound traffic
- Private internal communication
- Secure SSH authentication
- Encrypted Wazuh agent communication
- Minimal exposed services
- Security Group based firewall

---

# Validation Checklist

Before deployment begins:

- VPC CIDR confirmed
- Subnet CIDRs confirmed
- Security Groups reviewed
- Route Tables planned
- Internet Gateway planned
- Resource names finalized

Once these checks are complete, AWS infrastructure provisioning can begin.