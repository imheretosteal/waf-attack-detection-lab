# WAF Architecture – SafeLine Web Application Firewall Lab

## 1. Architecture Overview

This lab demonstrates how a **Web Application Firewall (SafeLine WAF)** protects a vulnerable web application by acting as a **reverse proxy security layer**.

Two environments were analyzed:

| Scenario | Security Level | Description |
|--------|----------------|-------------|
| Before WAF | Vulnerable | Web server exposed directly to the internet |
| After WAF | Protected | Traffic filtered through SafeLine WAF |

The objective of this project is to show how a WAF can **detect and block malicious HTTP requests before they reach the backend server.**

---

# 2. System Components

| Component | Role | Operating System |
|----------|------|------------------|
| Kali Linux | Attacker machine used to simulate attacks | Kali Linux |
| SafeLine WAF | Web Application Firewall inspecting HTTP traffic | Ubuntu |
| Apache Web Server | Backend server hosting the web application | Ubuntu |
| DVWA | Vulnerable web application used for testing | PHP |
| MySQL Database | Database storing application data | MySQL |

---

# 3. Network Architecture

## Before WAF (Vulnerable Architecture)

In this architecture the web server is **directly exposed to attackers**.

    Internet / Attacker
            │
            ▼
    Kali Linux
            │
            ▼
    Web Server (Apache)
            │
            ▼
    DVWA Application
            │
            ▼
    MySQL Database


    
### Explanation

| Layer | Function |
|------|----------|
| Attacker | Sends malicious HTTP requests |
| Web Server | Receives traffic directly |
| DVWA | Processes user input |
| Database | Stores application data |

Without a security layer, attackers can exploit vulnerabilities such as:

- SQL Injection
- Command Injection
- Cross-Site Scripting (XSS)

---

# 4. Protected Architecture (After WAF Deployment)

After SafeLine WAF is deployed, it sits between the attacker and the web server.

        Internet
            │
            ▼
    Kali Linux (Attacker)
            │
            ▼
 SafeLine WAF (HTTPS - Port 443)
            │
            ▼
 Apache Web Server (Port 8080)
            │
            ▼
    DVWA Application
            │
            ▼
    MySQL Database


    
### Explanation

| Layer | Role |
|------|------|
| Attacker | Attempts to exploit vulnerabilities |
| SafeLine WAF | Inspects incoming HTTP requests |
| Web Server | Serves application content |
| DVWA | Processes application logic |
| Database | Stores application data |

The **WAF filters malicious requests** before they reach the web server.

---

## 5. Request Processing Flow

The following diagram shows how requests travel through the system when the Web Application Firewall is active.

```text
User / Attacker Request
        │
        ▼
Internet Traffic
        │
        ▼
SafeLine WAF Inspection
        │
        ├── Malicious Request Detected
        │        │
        │        ▼
        │     Request Blocked
        │
        ▼
Forward Valid Request
        │
        ▼
Apache Web Server
        │
        ▼
DVWA Application
        │
        ▼
MySQL Database
        │
        ▼
Response Returned to User
```

The WAF acts as a reverse proxy security layer, inspecting incoming HTTP traffic before forwarding it to the backend web server.

---

## 6. Attack Simulation Workflow

The attack testing process used in this lab environment.

```text
Attacker (Kali Linux)
        │
        ▼
Send Malicious Input
        │
        ▼
DVWA Input Field
        │
        ▼
Application Processes Input
        │
        ▼
Database Query Executed
        │
        ▼
Response Returned to Attacker
```

### Attack Types Tested

| Attack Type | Description |
|-------------|-------------|
| SQL Injection | Manipulates database queries to retrieve unauthorized data |
| Command Injection | Executes system commands on the server |

---

## 7. WAF Detection Workflow

When the SafeLine Web Application Firewall is enabled, all incoming traffic is analyzed before reaching the backend application.

```text
Incoming HTTP Request
        │
        ▼
SafeLine WAF Analysis
        │
        ├── Signature Detection
        ├── Pattern Matching
        └── Security Rules
        │
        ▼
Attack Detected
        │
        ▼
Request Blocked
        │
        ▼
Access Forbidden Response
```

This prevents malicious requests from reaching the vulnerable application.

---

## 8. Architecture Diagram

### WAF Protected Architecture

![WAF Architecture](waf-architecture.png)

This architecture demonstrates the reverse proxy design, where the WAF sits between the attacker and the backend infrastructure.

| Component | Role |
|-----------|------|
| Attacker (Kali Linux) | Sends malicious requests |
| SafeLine WAF | Inspects and filters incoming traffic |
| Apache Web Server | Hosts the DVWA application |
| DVWA Application | Vulnerable web application used for testing |
| MySQL Database | Backend database storing application data |

---

## 9. Attack Evidence

### SQL Injection Successful (Before WAF)

![SQL Injection Success](https://github.com/bhargavi-c-cyber/waf-attack-detection-lab/blob/main/cmd-injection-success.png)

*Figure: SQL injection attack successfully executed when the application was directly exposed.*

---

### Command Injection Successful (Before WAF)

![Command Injection Success](cmd-injection-success.png)

*Figure: Command injection allowing system commands to be executed on the server.*

---

## 10. WAF Blocking Evidence

### SQL Injection Blocked

![SQL Injection Blocked](https://github.com/bhargavi-c-cyber/waf-attack-detection-lab/blob/main/sql-injection-blocked.png)

*Figure: SafeLine WAF detecting and blocking a malicious SQL injection attempt.*

---

## 11. WAF Monitoring Dashboard

SafeLine provides monitoring features such as:

- Request statistics
- Blocked attack attempts
- Traffic analysis
- Security rule detection

![WAF Dashboard](https://github.com/bhargavi-c-cyber/waf-attack-detection-lab/blob/main/waf-dashboard-stats.png)

---

## 12. Security Benefits of Using a WAF

| Benefit | Description |
|--------|-------------|
| Attack Prevention | Blocks malicious HTTP requests |
| Traffic Monitoring | Provides visibility into incoming traffic |
| Application Protection | Prevents exploitation of vulnerabilities |
| Reverse Proxy Security | Adds a security layer before the web server |

---

## 13. Key Learning Outcomes

This project demonstrates practical understanding of:

- Web Application Firewall deployment
- Reverse proxy security architecture
- OWASP Top 10 vulnerability testing
- Attack detection and mitigation
- Web application security monitoring
- Secure infrastructure design
