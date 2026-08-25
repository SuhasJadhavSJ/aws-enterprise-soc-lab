# INC-001 — Invalid SSH User Authentication Attempt

## 1. Incident Overview

| Field | Value |
|---|---|
| Incident ID | INC-001 |
| Date | 2026-08-23 |
| Severity | Low |
| Status | Investigating |
| Affected Host | `soc-client-01` |
| Host IP | `10.0.2.45` |
| Source IP | `10.0.1.162` |
| Protocol | SSH |
| Destination Port | 22 |
| Account | `wronguser` |
| Authentication State | Pre-authentication |
| Detection Source | Linux SSH logs / Wazuh |

## 2. Objective

Generate a controlled SSH authentication event and validate the complete telemetry pipeline from the monitored endpoint to the Wazuh SIEM.

## 3. Event Evidence

The monitored endpoint generated the following SSH log entry:

```text
2026-08-23T11:10:47.706983+00:00 ip-10-0-2-45 sshd[5906]: Connection closed by invalid user wronguser 10.0.1.162 port 55280 [preauth]