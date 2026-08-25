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

- [x] Operating system baseline completed
- [x] System packages updated
- [x] Server rebooted successfully
- [x] Post-reboot health verified
- [ ] Wazuh installation assistant downloaded
- [ ] Wazuh indexer installed
- [ ] Wazuh server installed
- [ ] Wazuh dashboard installed
- [ ] Wazuh services validated
- [ ] Dashboard accessed
- [ ] First agent enrolled

## 6. Installation Assistant Verification

The official Wazuh installation assistant was downloaded to the SOC server and verified before execution.

- File: `wazuh-install.sh`
- File size: approximately 204 KB
- Executable permission: enabled
- Script header: Wazuh installer

The installer was verified before execution to avoid running an unverified or incorrectly downloaded deployment script.

## 7. Installation Result

The Wazuh assisted installation completed successfully through the Dashboard deployment and post-install configuration stages.

### Components Installed

- Wazuh Indexer
- Wazuh Server / Manager
- Wazuh Dashboard
- Filebeat

### Installation Observations

- Wazuh Dashboard installation completed successfully.
- Wazuh Dashboard post-install configuration completed.
- Wazuh Dashboard service started successfully.
- Filebeat service started successfully.
- Wazuh internal users were updated.
- A backup of the internal users was created under `/etc/wazuh-indexer/internalusers-backup`.

### Current Status

Installation completed without an error being reported in the provided output.

Service-level validation is required before considering the Wazuh deployment operational.

## 8. Post-Installation Network Baseline

After Wazuh installation, listening services were compared with the pre-installation baseline.

### Wazuh Services Observed

| Port | Process | Function |
|---:|---|---|
| 1514/TCP | `wazuh-remoted` | Wazuh agent communication |
| 1515/TCP | `wazuh-authd` | Agent enrollment |
| 55000/TCP | `python3` | Wazuh API |
| 443/TCP | `node` | Wazuh Dashboard |
| 9200/TCP | `java` | Wazuh Indexer |
| 9300/TCP | `java` | Wazuh Indexer cluster communication |

The Wazuh Indexer ports 9200 and 9300 were observed listening only on the loopback interface, reducing direct network exposure.

The Wazuh API listens on port 55000, but external access is controlled by the AWS Security Group.

### Baseline Comparison

Before Wazuh installation, the primary externally listening TCP service was SSH on port 22.

After installation, Wazuh introduced listeners for agent communication, enrollment, API access, and the Dashboard.

## 9. Wazuh Service Validation

Post-installation service validation was performed using systemd and the Wazuh control utility.

### Systemd Validation

The following core services were confirmed active:

| Service | Status |
|---|---|
| wazuh-manager | Active |
| wazuh-indexer | Active |
| wazuh-dashboard | Active |
| filebeat | Active |

No failed systemd units were reported.

### Wazuh Manager Component Validation

Core Wazuh processes including the following were confirmed running:

- wazuh-modulesd
- wazuh-monitord
- wazuh-logcollector
- wazuh-remoted
- wazuh-syscheckd
- wazuh-analysisd
- wazuh-execd
- wazuh-db
- wazuh-authd
- wazuh-apid

Several optional components were not running because they are not required for the initial single-node SOC deployment.

### Validation Result

The initial Wazuh single-node deployment is operational and ready for Dashboard access and endpoint onboarding.