# Endpoint Security SIEM Lab with Automated Remediation (Wazuh + Docker)

## Overview
This project demonstrates the design, implementation, and validation of an endpoint monitoring and automated remediation system within an isolated virtual lab environment.

The solution simulates real-world attack scenarios across Windows and Linux endpoints and uses a centralised Wazuh SIEM platform to detect, analyse, and respond to suspicious activity.

An AI-assisted automation layer was integrated using Docker to support alert triage and controlled remediation workflows.

---

## Objectives
- Build a fully isolated cybersecurity lab environment
- Collect and centralise endpoint telemetry (Windows & Linux)
- Develop detection rules based on attacker behaviours
- Simulate real-world attack techniques (MITRE ATT&CK aligned)
- Implement automated, controlled remediation workflows
- Validate detection accuracy and response effectiveness

---

## Architecture

The system consists of three main layers:

1. **Endpoints**
   - Windows VM (administrative workstation simulation)
   - Linux VM (service host simulation)

2. **SIEM Layer**
   - Wazuh Manager for log aggregation, correlation, and alerting

3. **Automation Layer**
   - Dockerised AI triage service (Flask + local LLM)
   - Predefined remediation actions (allow-listed)

**Data Flow:**
- Telemetry → SIEM → Alert → AI Triage → Controlled Remediation

---

## Technologies Used

- **SIEM:** Wazuh
- **Virtualisation:** Oracle VirtualBox
- **Operating Systems:** Windows, Ubuntu Linux
- **Logging:** Sysmon, Linux Auth Logs
- **Automation:** Docker, Docker Compose
- **Backend:** Python (Flask)
- **Security Frameworks:**
  - MITRE ATT&CK
  - NIST SP 800-53
  - NIST SP 800-61
  - CIS Controls v8

---

## Key Features

### Centralised Logging & Monitoring
- Endpoint telemetry collected from Windows and Linux systems
- Logs normalised and correlated within Wazuh SIEM

### Detection Engineering
Developed and validated detection rules for:
- Suspicious PowerShell execution
- Privilege escalation (Windows & Linux)
- Authentication anomalies
- Executable file drop behaviour

### Attack Simulation
Simulated attacker behaviours including:
- Script-based execution
- Credential misuse
- Privilege escalation via sudo
- Lateral movement indicators

### Automated Remediation
- AI-assisted alert classification
- Controlled response actions:
  - Account disablement
  - Simulated host isolation
- All actions are allow-listed and auditable

---

## Results

- Successfully validated **5+ detection rules**
- Achieved full visibility across endpoint activity
- Detected:
  - PowerShell abuse
  - Privilege escalation attempts
  - Authentication anomalies
- Automated remediation workflows executed without system instability
- Demonstrated reduction in response time through automation

---

## Example Detection Use Cases

| Use Case | Technique | Severity | Result |
|--------|----------|--------|--------|
| Suspicious PowerShell | Script Abuse | High | Alert Generated |
| Executable Drop | Persistence | Medium | Alert Generated |
| Windows Privilege Escalation | Privilege Abuse | High | Alert Generated |
| Linux Sudo Misuse | Privilege Escalation | High | Alert Generated |
| Authentication Anomaly | Credential Misuse | Medium | Alert Generated |

---

## Security Considerations

- Fully isolated lab environment (no external exposure)
- No real malware used (benign simulation only)
- Remediation actions are:
  - Predefined
  - Reversible
  - Auditable
- AI system restricted to classification (no autonomous execution)

---

## Limitations

- Does not replicate full enterprise-scale infrastructure
- Limited to controlled attack simulations
- AI automation is rule-assisted, not fully autonomous
- Requires further tuning to reduce false positives in production

---

## Future Improvements

- Integrate threat intelligence feeds
- Expand detection coverage (EDR/XDR level)
- Implement RBAC for remediation workflows
- Connect to incident management systems (e.g., Jira, ServiceNow)
- Improve AI-driven decision-making capabilities

---

## How to Run - Setup Instructions

1. Clone the repository
2. Set up VirtualBox environment
3. Deploy:
   - Windows VM
   - Linux VM
   - Wazuh Server
4. Configure Wazuh agents on endpoints
5. Start Docker automation layer:
   docker-compose up -d
6. Generate test events (PowerShell / sudo misuse)
7. Monitor alerts in Wazuh dashboard
