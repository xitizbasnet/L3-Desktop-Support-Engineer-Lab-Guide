# Lab 5: PowerShell Automation for Desktop Support

## Background & Objective

Develop PowerShell scripts to automate repetitive desktop support tasks, reduce manual **MTTR (Mean Time To Resolution)**, and improve consistency across the infrastructure.

> ⚙️ **Lab Focus:** Diagnostic automation, automated troubleshooting, bulk user/device management, monitoring, alerting, reporting, and secure PowerShell scripting practices.

---

## Task 5.1: Diagnostic Health Check Script

Create an automated PowerShell health-check solution that collects system diagnostics, validates critical services, gathers network information, and produces reports for support teams.

### Procedure

**Step 1:** Create PowerShell script to collect system diagnostics automatically.

**Step 2:** Gather:

* Windows version
* Installed patches
* Driver versions
* Disk space
* Memory
* CPU

**Step 3:** Check services status:

* Antivirus
* Firewall
* Windows Update
* Networking

**Step 4:** Collect network information:

* DNS servers
* Default gateway
* IPv4 addresses
* IPv6 addresses

**Step 5:** Generate color-coded report:

* 🟢 **Green** — OK
* 🟡 **Yellow** — Warning
* 🔴 **Red** — Critical

**Step 6:** Save output to CSV and HTML for easy sharing with support teams.

**Step 7:** Schedule via Task Scheduler to run weekly; aggregate results for monitoring.

**Step 8:** Example commands:

```powershell
Get-ComputerInfo
Get-HotFix
Test-NetConnection
```

> 💡 **Automation Tip:** Standardizing health-check output makes it easier for support teams to compare systems, identify recurring issues, and prioritize remediation.

---

## Task 5.2: Automated Troubleshooting Script

Develop PowerShell automation that can execute common remediation actions based on the identified issue type.

### Procedure

**Step 1:** Create script to automatically run common fixes based on issue type.

**Step 2:** Network connectivity check:

* Ping
* DNS resolution
* Firewall rules validation

**Step 3:** Application install/repair:

**Uninstall → Reinstall → Verify installation**

**Step 4:** Clear cache/temp files:

* `%temp%`
* `%appdata%`
* Browser caches

**Step 5:** Reset application settings:

* Remove registry keys
* Reset to defaults

**Step 6:** Log collection:

* Gather application logs.
* Export Event Viewer logs.
* Collect diagnostic files.

**Step 7:** Generate report:

* Pre-remediation status
* Post-remediation status
* Actions taken
* Results

**Step 8:** Example: Script to repair Office 365, reset network adapters, clear caches.

> ⚠️ **Change Control:** Automated remediation can modify system configuration or delete cached data. Validate scripts in a controlled environment and implement appropriate safeguards before production use.

---

## Task 5.3: Bulk User/Device Management

Use PowerShell to automate repetitive Active Directory (AD) user and device management operations while maintaining appropriate authorization and audit controls.

### Procedure

**Step 1:** Create script to manage AD users in bulk:

* Add attributes
* Remove attributes
* Modify attributes

**Step 2:** Reset user password: validate against AD password policy.

**Step 3:** Bulk disable inactive accounts: compare login times with current date.

**Step 4:** Distribute software licenses: query license server, assign to users.

**Step 5:** Query device inventory:

* Hardware specifications
* OS version
* Last login
* IP address

**Step 6:** Generate CSV reports for auditing:

* Device compliance
* User permissions
* Licenses

**Step 7:** Implement approval workflow: script queues requests, requires manager approval.

**Step 8:** Example commands:

```powershell
Get-ADUser
Set-ADUser
Get-ADComputer
Export-CSV
```

> 🔐 **Security Consideration:** Bulk account and device operations can have significant operational impact. Ensure scripts enforce appropriate authorization and approval workflows before making changes.

---

## Task 5.4: Monitoring & Alert Automation

Create automated monitoring and alerting scripts to detect common endpoint health conditions and initiate appropriate remediation or notification workflows.

### Procedure

**Step 1:** Create script to monitor disk space; alert if usage **>80%**.

**Step 2:** Monitor service status; auto-restart critical services if stopped.

**Step 3:** Monitor process resource usage; kill runaway processes exceeding thresholds.

**Step 4:** Generate daily health reports:

* Performance metrics
* Errors
* Warnings

**Step 5:** Send alerts via email:

* Severity level
* Affected systems
* Recommended actions

**Step 6:** Log all actions to central repository for compliance/audit trail.

**Step 7:** Schedule via Task Scheduler with proper credentials/permissions.

**Step 8:** Example commands:

```powershell
Get-Process
Get-Volume
Restart-Service
Send-MailMessage
```

> 📊 **Monitoring Principle:** Automated monitoring should produce actionable information. Include the affected system, severity, relevant diagnostic information, and recommended action in generated alerts whenever possible.

---

# Best Practices & Tips

The following practices should be applied when developing, testing, deploying, and maintaining PowerShell automation:

* **3 Always use `-WhatIf` parameter first to preview changes before executing on production**
* **3 Implement proper error handling: Try-Catch-Finally blocks to capture and log errors**
* **3 Use managed service accounts for scripts running with elevated permissions (security best practice)**
* **3 Log all script actions with timestamps; maintain audit trail for compliance**
* **3 Test scripts on 1-2 systems before scaling to entire environment**
* **3 Implement confirmation prompts for destructive actions: disable accounts, delete data**
* **3 Use encoding/encryption for sensitive data: API keys, passwords, connection strings**
* **3 Keep scripts modular: separate functions for reusability, easier testing & maintenance**

> 🧪 **Test Before Deployment:** Test scripts on **1–2 systems** before scaling automation across the environment. Validate both successful and failure scenarios.

> 🛡️ **Production Safety:** Use the `-WhatIf` parameter where supported to preview potentially destructive operations before executing them against production systems.

> 🚨 **Error Handling:** Implement `Try-Catch-Finally` blocks to capture errors, perform required cleanup, and record diagnostic information.

> 🔐 **Credential Security:** Use managed service accounts for scripts requiring elevated permissions where supported by the environment. Never embed passwords, API keys, or other sensitive credentials directly in scripts.

> 📝 **Auditability:** Log script actions with timestamps and maintain an appropriate audit trail for administrative and compliance purposes.

> 🧩 **Modular Design:** Keep scripts modular by separating functionality into reusable functions. This improves testing, troubleshooting, maintenance, and future development.

> ⚠️ **Destructive Operations:** Implement confirmation prompts or equivalent safeguards for operations such as disabling accounts or deleting data. Ensure that automated actions follow applicable approval and change-management requirements.
