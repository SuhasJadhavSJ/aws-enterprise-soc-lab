# AWS Resource Plan

## Overview

This document defines every AWS resource required to deploy the Enterprise Cloud Security Operations Center (SOC). It serves as the deployment blueprint and ensures that all infrastructure is planned before provisioning resources.

The objective is to create a secure, scalable, and cost-effective environment while remaining within the AWS credit budget.

---

# Deployment Region

Selected Region:

Asia Pacific (Mumbai)

Reason:

- Lower network latency from the local workstation.
- Supported by all required AWS services.
- Consistent with previous AWS deployments.

---

# AWS Resources

| Resource | Name | Purpose |
|----------|------|---------|
| VPC | soc-vpc | Isolated network |
| Internet Gateway | soc-igw | Internet connectivity |
| Public Subnet | soc-public-subnet | Hosts Wazuh Server |
| Private Subnet | soc-private-subnet | Hosts monitored Ubuntu endpoint |
| Route Table | soc-public-rt | Public routing |
| Route Table | soc-private-rt | Private routing |
| Security Group | soc-server-sg | Firewall for Wazuh Server |
| Security Group | soc-client-sg | Firewall for Ubuntu endpoint |
| EC2 | soc-server | Wazuh Manager, Indexer and Dashboard |
| EC2 | soc-client-01 | Ubuntu monitored endpoint |
| Elastic IP | soc-server-eip | Static public IP |
| Key Pair | soc-key | SSH authentication |

---

# EC2 Instance Specifications

## SOC Server

Operating System

Ubuntu Server 24.04 LTS

Purpose

Hosts:

- Wazuh Dashboard
- Wazuh Manager
- Wazuh Indexer

Recommended Instance

t3.medium

Storage

50 GB General Purpose SSD (gp3)

Reason

Wazuh Indexer requires additional memory and storage compared to a standard Linux server.

---

## SOC Client

Operating System

Ubuntu Server 24.04 LTS

Purpose

Monitored Linux endpoint

Recommended Instance

t3.micro

Storage

20 GB gp3

---

# Networking

VPC

10.0.0.0/16

Public Subnet

10.0.1.0/24

Private Subnet

10.0.2.0/24

Availability Zone

Single AZ (Initial Deployment)

Reason

Reduces cost while supporting future expansion.

---

# Elastic IP

Allocated To

SOC Server

Reason

Provides a static public address for:

- Dashboard access
- SSH administration
- Agent enrollment

---

# Resource Naming Convention

All resources follow a consistent naming standard.

Examples:

soc-vpc

soc-public-subnet

soc-private-subnet

soc-server

soc-client-01

soc-server-sg

soc-client-sg

---

# Resource Tags

Every AWS resource will include the following tags.

| Key | Value |
|------|-------|
| Project | Enterprise-SOC |
| Environment | Lab |
| Owner | Suhas |
| ManagedBy | Manual |
| Purpose | Security Operations |

---

# Estimated Infrastructure

Initial Deployment

1 × VPC

2 × Subnets

1 × Internet Gateway

2 × Route Tables

2 × Security Groups

2 × EC2 Instances

1 × Elastic IP

1 × Key Pair

---

# Cost Optimization

To remain within the AWS budget:

- Stop unused EC2 instances.
- Delete unused EBS volumes.
- Remove unused Elastic IPs.
- Use a single Availability Zone.
- Minimize unnecessary storage allocation.
- Monitor AWS Billing regularly.

---

# Validation Checklist

Before deployment begins, verify:

- AWS region selected
- Resource names finalized
- CIDR ranges reviewed
- Security principles approved
- Budget reviewed
- Documentation completed

Once all validation checks pass, infrastructure provisioning can begin.