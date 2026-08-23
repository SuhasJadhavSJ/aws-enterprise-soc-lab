# Wazuh Installation

## 1. Objective

Deploy a single-node Wazuh environment on the AWS `soc-server` instance.

The deployment will host:

- Wazuh Indexer
- Wazuh Server / Manager
- Wazuh Dashboard

The initial objective is to establish a functioning SIEM before onboarding endpoints.

## 2. Deployment Method

The official Wazuh assisted installation method will be used for the initial single-node deployment.

## 3. Server

- Hostname: `ip-10-0-1-162`
- OS: Ubuntu 24.04.4 LTS
- Architecture: x86_64
- vCPU: 2
- RAM: 7.6 GiB
- Storage: approximately 48 GiB root filesystem

## 4. Deployment Constraints

The AWS instance provides less CPU capacity than the Wazuh recommended 4-vCPU configuration for a 1–25 agent quickstart deployment.

Resource utilization will therefore be monitored throughout the lab.

## 5. Installation Status

- [ ] Operating system baseline completed
- [ ] Wazuh installation assistant downloaded
- [ ] Wazuh indexer installed
- [ ] Wazuh server installed
- [ ] Wazuh dashboard installed
- [ ] Wazuh services validated
- [ ] Dashboard accessed
- [ ] First agent enrolled