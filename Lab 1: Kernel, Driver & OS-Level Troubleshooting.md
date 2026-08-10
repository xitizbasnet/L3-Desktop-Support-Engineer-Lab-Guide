# Lab 1: Kernel, Driver & OS-Level Troubleshooting

## Background & Objective

This lab focuses on diagnosing and resolving complex OS-level issues, including **kernel panics, driver failures, performance degradation, and system stability problems**.

You will learn to:

* Collect diagnostic data.
* Analyze system logs.
* Identify system and driver-related issues.
* Implement targeted fixes.
* Validate system performance after remediation.

> **Lab Focus:** Kernel troubleshooting, driver diagnosis, BSOD analysis, performance investigation, and root cause identification.

---

## Task 1.1: System Health Diagnostics

Use the following procedure to establish the current health of the affected Windows system and collect baseline diagnostic information.

### Procedure

**Step 1:** Access Windows Event Viewer on affected machine (`eventvwr.msc`).

**Step 2:** Check **System**, **Application**, and **Security** logs for critical errors in last 24 hours.

**Step 3:** Export Event Log as `.evtx` file for analysis.

**Step 4:** Run Resource Monitor (`resmon.exe`) to identify abnormal resource usage.

**Step 5:** Document baseline metrics:

* CPU
* Memory
* Disk I/O
* Network utilization

**Step 6:** Compare abnormal patterns against established baseline.

---

## Task 1.2: Driver Issue Diagnosis

Use Device Manager, Windows Update, manufacturer-provided drivers, and built-in Windows repair utilities to identify and resolve driver-related issues.

### Procedure

**Step 1:** Open Device Manager (`devmgmt.msc`) and scan for unknown/problematic devices.

**Step 2:** Check **Driver** tab for outdated or incompatible versions.

**Step 3:** Use Windows Update to pull latest drivers automatically.

**Step 4:** For critical drivers, access manufacturer's support page and download directly.

**Step 5:** Uninstall driver → Restart → Allow Windows to reinstall or manually install.

**Step 6:** Run System File Checker:

```cmd
sfc /scannow
```

> **Note:** Run the command from an elevated prompt.

**Step 7:** Run DISM:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

---

## Task 1.3: Kernel Panic Analysis (BlueScreen/BSOD)

Use Windows crash-dump collection and **WinDbg** to identify the underlying cause of Blue Screen of Death (BSOD) events.

### Procedure

**Step 1:** Enable kernel dump collection:

**Settings → System → About → Advanced system settings**

**Step 2:** Configure dump type:

* Small memory dump (256 MB)
* Automatic restart disabled

**Step 3:** Collect `Memory.dmp` from `C:\Windows\Minidump` or custom location.

**Step 4:** Use Windows Debugging Tools (**WinDbg**) to analyze dump file.

**Step 5:** Identify faulting driver using the following command in WinDbg:

```text
!analyze -v
```

**Step 6:** Cross-reference faulting driver with recent installations/updates.

**Step 7:** Document findings:

* Error code
* Faulting driver
* Potential cause

---

## Task 1.4: Performance Degradation Root Cause

Use Performance Monitor and other Windows administrative tools to establish performance baselines, identify bottlenecks, and implement optimization recommendations.

### Procedure

**Step 1:** Baseline system performance using Performance Monitor (`perfmon.exe`).

**Step 2:** Create custom data collector set targeting:

* CPU
* Memory
* Disk
* Network

**Step 3:** Run for 30 minutes during reported issue timeframe.

**Step 4:** Analyze graph for bottleneck identification.

**Step 5:** Check Task Manager for resource-hogging processes.

**Step 6:** Investigate background services using `Services.msc`.

**Step 7:** Review Startup items and disable non-critical services.

**Step 8:** Implement optimization recommendations and re-baseline.

---

# Best Practices & Tips

The following practices should be applied when performing advanced OS-level troubleshooting:

* **3 Always gather baseline metrics BEFORE making changes—comparison is crucial for validation**
* **3 Use Safe Mode with Networking to isolate driver/software issues from OS level**
* **3 Maintain a drivers inventory spreadsheet with versions, release dates, and known issues**
* **3 Document all changes with timestamp; revert in reverse order if troubleshooting fails**
* **3 For production systems, test updates in lab environment first before deploying to users**
* **3 Enable verbose logging on services for deeper diagnostics (registry edits or admin tools)**
* **3 Keep Windows Update enabled; schedule patches during maintenance windows**
* **3 Collaborate with OEM/vendor support when driver issues persist—request hotfixes if available**

> 💡 **Best Practice:** Always capture the system state and establish a baseline **before making changes**. This provides a reliable comparison point for validating remediation and helps determine whether an implemented change improved or degraded system behavior.

> ⚠️ **Production Consideration:** For production systems, validate driver and operating-system changes in a controlled lab environment before deployment to end users.

> 📋 **Documentation Requirement:** Record all troubleshooting actions, timestamps, findings, changes, and rollback actions. This information supports escalation, incident documentation, and future root cause analysis.
