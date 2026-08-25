# Wazuh Agent Onboarding

## Objective

Connect a monitored Ubuntu endpoint to the centralized Wazuh Manager and verify that security telemetry is being received.

## Architecture

```text
Ubuntu Agent
     |
     | TCP 1514
     | TCP 1515 (enrollment)
     v
Wazuh Manager
     |
     v
Wazuh Indexer
     |
     v
Wazuh Dashboard

## 2. Private Endpoint Deployment

The monitored endpoint `soc-client-01` was deployed inside the private subnet.

### Endpoint Configuration

- Instance: `soc-client-01`
- OS: Ubuntu 24.04 LTS
- Instance type: `t3.micro`
- VPC: `soc-vpc`
- Subnet: `soc-private-subnet`
- CIDR: `10.0.2.0/24`
- Public IPv4: Disabled
- Security Group: `soc-client-sg`
- Storage: 10 GiB encrypted gp3

The endpoint intentionally has no public IPv4 address.

Administrative access will be performed through the Wazuh server using the private AWS network.

## 3. Private Network Connectivity

Private connectivity between the Wazuh server and monitored endpoint was validated.

### Test 1 — ICMP

- Source: `10.0.1.162`
- Destination: `10.0.2.45`
- Result: No ICMP response

ICMP was not enabled because it is not required for Wazuh agent communication.

### Test 2 — TCP/22

- Source: `10.0.1.162`
- Destination: `10.0.2.45`
- Protocol: TCP
- Port: 22
- Result: **Successful**

```text
Connection to 10.0.2.45 22 port [tcp/ssh] succeeded!

## 4. Administrative Access

The private endpoint was accessed through the Wazuh server using SSH jump-host connectivity.

### Access Path

```text
Kali Linux
    |
    | SSH
    v
Wazuh Server
10.0.1.162
    |
    | SSH over private network
    v
soc-client-01
10.0.2.45

## 5. Endpoint Baseline

A pre-agent baseline was collected from `soc-client-01`.

### Operating System

- OS: Ubuntu 24.04.4 LTS
- Kernel: 6.17.0-1017-aws
- Architecture: x86_64

### Compute

- vCPU: 2
- CPU model: Intel Xeon Platinum 8259CL
- RAM: 911 MiB
- Available RAM: approximately 558 MiB
- Swap: 0 B

### Storage

- Root filesystem: 8.7 GiB
- Used: 1.9 GiB
- Available: 6.9 GiB
- Utilization: 22%

### Network

- Private IPv4: `10.0.2.45`
- Subnet: `10.0.2.0/24`
- Interface: `ens5`
- Default gateway: `10.0.2.1`
- Public IPv4: None

### Listening Services

| Protocol | Port | Bind Address | Service |
|---|---:|---|---|
| TCP | 22 | `0.0.0.0` / `::` | SSH |
| TCP | 53 | `127.0.0.53` / `127.0.0.54` | systemd-resolved |
| UDP | 53 | `127.0.0.53` / `127.0.0.54` | systemd-resolved |
| UDP | 68 | `10.0.2.45` | DHCP |
| UDP | 323 | `127.0.0.1` / `::1` | chronyd |

### Process Baseline

The endpoint was observed immediately after deployment. No unexpected high-CPU user processes were identified in the sampled process list.

### Baseline Assessment

The endpoint is operational and has no public IPv4 address. SSH access is restricted through the `soc-client-sg` security group using `soc-server-sg` as the source.

The endpoint is ready for Wazuh agent installation.

## 6. Wazuh Communication Connectivity

Connectivity from the private endpoint to the Wazuh server was validated.

| Source | Destination | Protocol | Port | Result |
|---|---|---|---:|---|
| `10.0.2.45` | `10.0.1.162` | TCP | 1514 | PASS |
| `10.0.2.45` | `10.0.1.162` | TCP | 1515 | PASS |

### Interpretation

TCP/1514 is reachable for Wazuh agent communication.

TCP/1515 is reachable for Wazuh agent enrollment.

The private endpoint can therefore communicate with the Wazuh Manager without requiring a public IPv4 address.

### Security Model

The Wazuh agent communicates over the private AWS network.

No public IP is assigned to `soc-client-01`.

No Internet-facing inbound Wazuh ports are required on the endpoint.

## 7. Wazuh Version Compatibility

The Wazuh server version was verified before deploying the endpoint agent.

### Wazuh Server

- Wazuh version: `4.14.7`
- Wazuh type: `server`
- Architecture: `amd64`

### Endpoint

- Operating system: Ubuntu 24.04.4 LTS
- Architecture: `x86_64` / `amd64`

### Compatibility Decision

The endpoint will use the matching Wazuh Agent `4.14.7` AMD64 DEB package.

The agent version is intentionally matched to the Wazuh server rather than using an unversioned `latest` package.

### Status

- [x] Wazuh server version identified
- [x] Endpoint architecture identified
- [x] Compatible agent package identified
- [ ] Agent package transferred
- [ ] Agent installed
- [ ] Agent enrolled
- [ ] Agent telemetry validated

## 8. Agent Package Preparation

The Wazuh Agent package was downloaded from the official Wazuh package repository.

### Package

- Version: `4.14.7`
- Architecture: `amd64`
- Format: Debian package (`.deb`)
- Size: approximately 13 MB
- Filename: `wazuh-agent_4.14.7-1_amd64.deb`

### Validation

The downloaded file was validated using the Linux `file` utility:

```text
Debian binary package (format 2.0)

## 9. Agent Package Transfer and Verification

The Wazuh Agent package was transferred from the Wazuh server staging environment to the private endpoint through the controlled SSH jump-host path.

### Package

- Filename: `wazuh-agent_4.14.7-1_amd64.deb`
- Version: `4.14.7`
- Architecture: `amd64`
- Size: approximately 13 MB
- Format: Debian binary package

### Endpoint Verification

The package was verified on `soc-client-01` using the Linux `file` utility and SHA-256 hashing.

SHA-256:

`5276281b62e887065ecc14d4463cea529cf418529538c8edd6769c9ec550213f`

### Result

Package transfer and integrity verification completed successfully.

The package is ready for installation.

## 10. Wazuh Agent Installation

The Wazuh Agent `4.14.7-1` AMD64 package was installed successfully on
`soc-client-01`.

### Installation Result

```text
Package: wazuh-agent
Version: 4.14.7-1
Architecture: amd64
Status: installed

## 11. Agent Manager Configuration

The installed Wazuh Agent contained the default manager placeholder:

`MANAGER_IP`

The placeholder will be replaced with the private IPv4 address of the Wazuh Manager.

### Manager Configuration

| Setting | Value |
|---|---|
| Manager IP | `10.0.1.162` |
| Agent communication port | `1514` |
| Protocol | TCP |
| Enrollment port | `1515` |

The agent communicates with the Wazuh Manager over the private AWS network rather than using a public IP.


## 12. Manager Address Configuration

The default `MANAGER_IP` placeholder was replaced with the private IP of the Wazuh Manager.

Verified configuration:

```xml
<client>
  <server>
    <address>10.0.1.162</address>
    <port>1514</port>
    <protocol>tcp</protocol>
  </server>
</client>

## 14. Manager-Side Agent Validation

The Wazuh Manager was queried using `agent_control` after starting the
endpoint agent.

### Agent Registration

```text
ID: 001
Name: soc-client-01
Status: Active