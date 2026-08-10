# Lab 3: Endpoint Management Strategy Design

## Background & Objective

Design comprehensive endpoint management strategies covering **imaging, patching, configuration baselines, and compliance**. Bridge gap between security requirements and user experience.

> 🎯 **Lab Focus:** Endpoint imaging, Windows Autopilot, MDT architecture, patch management, Group Policy baselines, configuration management, and compliance.

---

## Task 3.1: Image Design & Optimization

Design and optimize a standardized endpoint image that meets organizational operating-system, application, security, and deployment requirements.

### Procedure

**Step 1:** Define image requirements:

* OS version
* Baseline applications
* Security baseline

**Step 2:** Document organizational standards:

* Disk encryption
* Antivirus
* Firewall rules

**Step 3:** Create golden master:

**Clean VM → Install OS → Apply base patches → Add apps**

**Step 4:** Optimize:

* Remove unnecessary drivers.
* Disable unused services.
* Compress image.

**Step 5:** Capture image using **SCCM/MDT (Microsoft Deployment Toolkit)**.

**Step 6:** Test deploy to **3–5 devices** in pilot group; validate:

* Drivers
* Applications
* Connectivity

**Step 7:** Document:

* Image version
* Build date
* Included applications
* Deployment method

**Step 8:** Version control image: maintain image history for rollback if needed.

> 💡 **Best Practice:** Maintain a clear image version history so previous versions can be identified and restored when a newly released image introduces compatibility or deployment issues.

---

## Task 3.2: MDT/Autopilot Architecture Setup

Design and implement an endpoint deployment architecture using **Microsoft Deployment Toolkit (MDT)** and **Windows Autopilot**.

### Procedure

**Step 1:** Set up Windows Autopilot: register devices with device hashes.

**Step 2:** Create Autopilot deployment profiles specifying:

* Language
* Timezone
* Applications

**Step 3:** Configure Autopilot for pre-provisioning:

* IT technician workflow
* User self-service

**Step 4:** Build MDT deployment share with task sequences.

**Step 5:** Create task sequences:

**Pre-install checks → Format disk → Apply image → Post-config**

**Step 6:** Define post-imaging tasks:

* Join domain
* Install updates
* Deploy applications

**Step 7:** Test end-to-end workflow:

**Boot from media → Complete deployment → Login**

**Step 8:** Document deployment process for help desk with troubleshooting guide.

> 📘 **Operational Guidance:** The deployment process should be documented sufficiently for the help desk to perform standard deployments and troubleshoot common deployment failures without requiring immediate L3 escalation.

---

## Task 3.3: Patch Management Policy Design

Develop a controlled patch-management strategy that balances security, operational stability, deployment risk, and business requirements.

### Procedure

**Step 1:** Survey current environment:

* Count devices
* OS versions
* Criticality levels

**Step 2:** Define patch cycle:

* OS patches — monthly
* Security updates
* Emergency hotfixes

**Step 3:** Create maintenance windows:

* Non-business hours
* Exclude critical servers

**Step 4:** Design rollout strategy:

**Pilot group (5%) → Expanded group (50%) → All devices**

**Step 5:** Establish rollback procedure:

* Test negative scenarios.
* Document approval process.

**Step 6:** Configure WSUS/Windows Update for Business group policy settings.

**Step 7:** Pilot test:

* Deploy patches to lab.
* Monitor system stability.
* Monitor application compatibility.

**Step 8:** Monitor after deployment:

* Update success rate
* Restart compliance
* Issue tickets

> ⚠️ **Change Management:** Patch deployments should follow the organization's applicable change-management, approval, maintenance-window, and rollback requirements.

---

## Task 3.4: GPO Baselines & Configuration Management

Establish standardized Group Policy Objects (GPOs) and configuration baselines to maintain security, consistency, and compliance across managed endpoints.

### Procedure

**Step 1:** Document current security baseline:

* Firewall rules
* Antivirus settings
* Encryption

**Step 2:** Design GPO structure:

**Organizational units by department/function**

**Step 3:** Create GPOs:

* **Computer Configuration** — system settings
* **User Configuration** — user preferences

**Step 4:** Priority GPOs:

* Password policy
* Windows Defender
* Windows Update
* UAC settings

**Step 5:** Test GPO application:

* Apply to test OU.
* Verify settings on member systems.

**Step 6:** Document scope and inheritance:

* Which OU
* Inheritance blocking rules

**Step 7:** Monitor compliance:

* Group Policy Results & analytics
* Audit reports

**Step 8:** Schedule quarterly GPO review for effectiveness and policy drift detection.

> 🔎 **Configuration Management:** Regular GPO reviews help identify policy drift, unintended configuration changes, and policies that are no longer aligned with organizational requirements.

---

# Best Practices & Tips

The following practices should be incorporated into endpoint-management design, deployment, patching, and configuration-management activities:

* **3 Test every image update thoroughly; rushed deployments cause widespread support tickets**
* **3 Use configuration baselines & compliance scanning to detect unauthorized changes**
* **3 Version all images & GPOs: tag releases, maintain change log for each version**
* **3 Establish communication plan: notify users 5 days before patch windows**
* **3 Schedule post-deployment reviews: capture lessons learned, update runbooks**
* **3 Balance security requirements with user experience; gather feedback from pilot groups**
* **3 Keep images lean: only include apps everyone needs; use app deployment for others**
* **3 Implement granular OUs for targeted policies; avoid applying broad policies to entire domain**

> 💡 **Best Practice:** Keep the base image lean. Applications required by only specific user groups should generally be handled through application deployment rather than being embedded into the base image.

> 🔄 **Version Control:** Apply version control to both images and GPOs. Maintain release tags and a change log so administrators can identify exactly what changed between versions.

> 👥 **Pilot Deployment:** Use representative pilot groups to validate technical functionality and user experience before expanding deployments across the organization.

> 📋 **Continuous Improvement:** Conduct post-deployment reviews, capture lessons learned, and update operational runbooks based on deployment outcomes.
