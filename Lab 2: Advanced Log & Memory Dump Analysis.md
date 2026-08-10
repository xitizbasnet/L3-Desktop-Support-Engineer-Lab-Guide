# Lab 2: Advanced Log & Memory Dump Analysis

## Background & Objective

Master the interpretation of **system logs, memory dumps, and network traces** to identify hidden issues. Learn to correlate events across multiple sources, identify patterns, and construct evidence-based **Root Cause Analysis (RCA)** reports.

> 🔍 **Lab Focus:** Event log analysis, memory dump analysis, network trace analysis, log correlation, timeline construction, and evidence-based RCA.

---

## Task 2.1: Event Log Deep Dive

Use Windows Event Viewer to perform detailed analysis of system events, identify recurring failures, and correlate events with reported user issues.

### Procedure

**Step 1:** Open Event Viewer and navigate to:

**Windows Logs → System**

**Step 2:** Filter logs by **Critical**, **Error**, and **Warning** for last 7 days.

**Step 3:** For each error, note:

* Event ID
* Time
* Source
* Description

**Step 4:** Cross-reference Event IDs with Microsoft documentation (`eventid.net`).

**Step 5:** Export filtered logs to CSV:

**Right-click log → Export**

**Step 6:** Build timeline spreadsheet correlating events with user reports.

**Step 7:** Identify patterns:

* Repeated failures at specific times
* Scheduled tasks
* Recurring events

---

## Task 2.2: Memory Dump Analysis with WinDbg

Use **WinDbg** to analyze memory dump files and identify faulting drivers, exception codes, stack traces, and other indicators of system failure.

### Procedure

**Step 1:** Download Debugging Tools for Windows (SDK).

**Step 2:** Launch WinDbg and open memory dump file:

**File → Open Crash Dump**

**Step 3:** Execute the following command for automatic crash analysis:

```text id="m7p2cx"
!analyze -v
```

**Step 4:** Review:

* Faulting driver
* Stack trace
* Exception code

**Step 5:** Run `!lmi (lsass)` to get module information.

```text id="5f8q1r"
!lmi lsass
```

**Step 6:** Check `!drvobj` for driver details.

```text id="2k9v6n"
!drvobj
```

**Step 7:** Search stack trace for third-party drivers/hooks.

**Step 8:** Document findings with screenshot and analysis notes.

> 📋 **Documentation Requirement:** Include screenshots and analysis notes with the diagnostic case record so the findings can be reviewed during escalation or RCA.

---

## Task 2.3: Network Trace Capture & Analysis

Capture and analyze network traffic to identify connection failures, timeouts, protocol-level issues, and relationships between network behavior and application failures.

### Procedure

**Step 1:** Use Windows Network Diagnostics or Message Analyzer.

**Step 2:** Capture network traffic using:

```cmd id="r4n8zt"
netsh trace start capture=yes scenario=NetConnection
```

**Step 3:** Reproduce network issue while capture is running.

**Step 4:** Stop capture:

```cmd id="x3p7hm"
netsh trace stop
```

**Step 5:** Open ETL file in Message Analyzer and filter by protocol:

* TCP
* DNS
* HTTP

**Step 6:** Identify failed connections:

* Look for RST flags.
* Look for connection timeouts.

**Step 7:** Correlate network issues with application logs and Event Viewer.

**Step 8:** Export findings:

* Packet counts
* Failed connections
* Latency analysis

> ⚠️ **Analysis Tip:** Network traces can contain a large amount of data. Filtering by protocol, IP, or port can reduce analysis overhead and make relevant events easier to identify.

---

## Task 2.4: Log Correlation & Timeline Building

Combine logs from multiple sources to construct a chronological timeline and establish cause-and-effect relationships between system events.

### Procedure

**Step 1:** Collect logs from multiple sources:

* System
* Application
* Security
* Custom app logs

**Step 2:** Export all logs with timestamps to CSV.

**Step 3:** Import CSVs into Excel and create master timeline by timestamp.

**Step 4:** Highlight events in chronological order with color coding by source.

**Step 5:** Identify cause-and-effect relationships.

**Example:**

> Login failure → subsequent permission denied errors

**Step 6:** Document before/after states for each significant event.

**Step 7:** Build narrative:

> **"At 10:15 AM, X happened, triggering Y, resulting in Z"**

This narrative should establish a clear sequence of events and provide evidence supporting the identified root cause.

---

# Best Practices & Tips

The following practices should be applied when collecting, analyzing, correlating, and retaining diagnostic information:

* **3 Always capture baseline/healthy logs for comparison; anomalies stand out against baseline**
* **3 Use timestamp synchronization (NTP) across systems for accurate log correlation**
* **3 Retain logs for minimum 30 days; archive older logs for compliance/historical analysis**
* **3 Document symbols path for WinDbg (Microsoft symbol server) for accurate stack trace resolution**
* **3 Network traces can be large; filter by IP/port to reduce file size and analysis overhead**
* **3 Combine multiple data sources; single log may not tell complete story**
* **3 Use elevated permissions (Run as Administrator) for full system diagnostics access**
* **3 Archive all diagnostic data with case ID for future reference and pattern analysis**

> 💡 **Best Practice:** Always capture a baseline or healthy set of logs whenever possible. Comparing current behavior against known-good data makes anomalies easier to identify.

> 🕒 **Time Synchronization:** Use **NTP** across systems involved in an investigation. Accurate timestamps are essential when correlating events from multiple sources.

> 📦 **Diagnostic Data Retention:** Archive diagnostic data using the applicable **case ID**. This supports future reference, recurring-incident analysis, compliance requirements, and historical pattern identification.

> 🔐 **Access Requirements:** Use **Run as Administrator** when required to obtain full access to system diagnostic information and protected logs.

> 🔎 **RCA Principle:** Do not rely on a single log source. Correlating system, application, security, network, and custom application data provides stronger evidence for determining the actual root cause.
