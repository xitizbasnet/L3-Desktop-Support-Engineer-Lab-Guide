# Lab 6: SCCM & Intune Configuration Management

## Background & Objective

Master enterprise endpoint management platforms (**SCCM for on-premises, Intune for cloud-based**) for software deployment, patch management, compliance reporting, and device configuration.

> 🎯 **Lab Focus:** SCCM application deployment, patch management, Intune enrollment, configuration profiles, compliance policies, conditional access, reporting, and automated remediation.

---

## Task 6.1: SCCM Application Deployment

Use SCCM to package, deploy, monitor, and document enterprise applications across targeted device collections.

### Procedure

**Step 1:** Create new application in SCCM Console:

* Application name
* Publisher
* Version

**Step 2:** Create deployment type:

* Specify installer file
* Installation command
* Uninstall command

**Step 3:** Configure detection rules:

* Registry key
* File existence
* Script-based detection

**Step 4:** Test installation locally:

* Run installer.
* Verify installation.
* Validate detection rule.

**Step 5:** Create collection: query by device type, user, department for targeted deployment.

**Step 6:** Deploy application:

* Select collection.
* Availability schedule.
* Deadline.
* Required/optional.

**Step 7:** Monitor deployment: track progress in SCCM Deployments view; troubleshoot failures.

**Step 8:** Document application:

* Version
* Installer source
* Deployment schedule
* Support contact

> 💡 **Deployment Tip:** Validate the installer and detection rule locally before creating the production deployment. An incorrect detection rule can cause SCCM to report inaccurate installation status or repeatedly attempt an installation.

---

## Task 6.2: SCCM Patch Management Configuration

Configure SCCM software-update capabilities to provide controlled, phased patch deployment and compliance reporting.

### Procedure

**Step 1:** Configure Software Update Point (SUP): point to Windows Server Update Services (WSUS).

**Step 2:** Configure automatic deployment rules (ADRs):

* Define patch schedule.
* Define classification.

**Step 3:** Create collection for initial patch deployment:

* Pilot group
* Business hours

**Step 4:** Set deployment deadline:

* Stagger across time zones.
* Allow 2–3 week deployment window.

**Step 5:** Configure update search:

* Monthly Tuesday patches
* Emergency zero-days

**Step 6:** Monitor patch compliance:

* Track devices needing updates.
* Track deployment status.

**Step 7:** Report on compliance:

* Which devices are missing patches.
* Reasons for non-compliance.

**Step 8:** Automate: use PS script to pre-stage patches, compress updates, optimize bandwidth.

> 🔄 **Phased Deployment:** Use pilot collections and staged deployment windows to identify application compatibility or endpoint issues before patches reach the broader organization.

> ⚠️ **Emergency Updates:** Emergency zero-day updates may require an accelerated deployment process based on organizational risk assessment, approval requirements, and applicable change-management procedures.

---

## Task 6.3: Intune Device Enrollment & Configuration

Configure Intune enrollment and device-management capabilities for cloud-based endpoint administration.

### Procedure

**Step 1:** Set up Azure AD Connect for user synchronization.

**Step 2:** Configure device enrollment restrictions:

* Allow/block platforms:

  * Windows
  * iOS
  * Android

**Step 3:** Create enrollment profiles:

* Corporate-owned device policies
* Personally-owned device policies

**Step 4:** Configure conditional access: require device compliance for accessing cloud resources.

**Step 5:** Create compliance policies:

* Antivirus status
* Firewall enabled
* Disk encryption required

**Step 6:** Monitor enrollments:

* Device count
* Enrollment success rate
* Platform distribution

**Step 7:** Troubleshoot enrollment:

* Review Intune audit logs.
* Check Azure AD connector health.

**Step 8:** Document enrollment process for IT onboarding teams.

> 📘 **Operational Guidance:** Enrollment documentation should clearly describe the expected enrollment workflow, supported platforms, common failure conditions, and escalation procedures for IT onboarding teams.

---

## Task 6.4: Intune Configuration Profiles & Compliance

Use Intune configuration and compliance policies to standardize endpoint settings and enforce organizational requirements.

### Procedure

**Step 1:** Create device configuration profile:

* Wi-Fi
* VPN
* Email settings

**Step 2:** Create device compliance policy:

* OS version requirement
* Password complexity

**Step 3:** Create conditional access rule: if non-compliant, block access to sensitive apps.

**Step 4:** Create app configuration profile: deploy apps with preconfigured settings.

**Step 5:** Assign profiles to user groups:

* Department
* Role
* Security requirements

**Step 6:** Monitor compliance:

* Track device compliance status.
* Track remediation actions.

**Step 7:** Generate reports:

* Compliance status by user/device/policy
* Trends over time

**Step 8:** Automate remediation: auto-remediate non-compliant devices when possible.

> 🔐 **Compliance Principle:** Configuration profiles, compliance policies, and conditional access should work together to establish the desired security and management state for organizational devices.

---

# Best Practices & Tips

The following practices should be applied when designing, deploying, monitoring, and maintaining SCCM and Intune configurations:

* **3 Test application deployments on 5-10 devices before scaling to entire organization**
* **3 Use pilot/staging collections for phased rollouts; minimize risk of organizational impact**
* **3 Configure clear deadline policies; balance IT control with user flexibility**
* **3 Monitor deployment status continuously; investigate and remediate failures quickly**
* **3 Use maintenance windows to prevent disruptions during business hours**
* **3 Maintain detailed documentation: application versions, deployment schedule, contacts**
* **3 Set up monitoring alerts for compliance drift; act quickly to remediate**
* **3 Regularly audit deployments and compliance status; adjust policies based on metrics**

> 🧪 **Pilot First:** Test application deployments on **5–10 devices** before scaling to the entire organization. Use representative pilot users and devices where possible.

> 🚦 **Phased Rollouts:** Use pilot and staging collections to progressively expand deployments. This reduces organizational impact and provides opportunities to detect issues before broad deployment.

> ⏱️ **Deadline Management:** Configure clear deployment deadlines that balance IT control with user flexibility. Consider time zones, business schedules, maintenance windows, and restart requirements.

> 📊 **Continuous Monitoring:** Monitor deployment and compliance status continuously. Investigate failed deployments and non-compliant devices promptly to prevent configuration drift.

> 📚 **Documentation:** Maintain detailed records of application versions, deployment schedules, configuration settings, support contacts, and relevant operational procedures.

> 🔎 **Compliance Monitoring:** Configure monitoring alerts for compliance drift and establish clear remediation workflows.

> 🔄 **Continuous Improvement:** Regularly audit deployments and compliance status. Use operational metrics and reporting trends to adjust policies, deployment strategies, and remediation procedures.
