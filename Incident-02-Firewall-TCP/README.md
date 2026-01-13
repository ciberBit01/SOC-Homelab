# Incident 02 – Firewall Misconfiguration Affecting TCP Sessions

**Date:** 2026-01-03  
**Role:** SOC Analyst Level 1  
**Environment:** Virtualized homelab (Windows Client + pfSense Firewall)

---

## 1. Executive Summary

An incident was identified where web traffic (HTTP/HTTPS) was disrupted on a Windows host within a virtualized homelab environment.  
The issue prevented normal internet navigation, causing web pages to freeze and eventually fail to load.

The root cause was traced to a misconfiguration in the pfSense firewall, where improperly adjusted TCP-related rules affected ports 80 and 443.  
The incident was resolved by disabling the problematic firewall rules, restoring normal network connectivity.

---

## 2. Environment

- **Firewall:** pfSense  
- **Client OS:** Windows  
- **Network Type:** Virtualized homelab  
- **Affected Services:** HTTP (80), HTTPS (443)

---

## 3. Detection

The incident was detected when a user attempted to access multiple websites and experienced:
- Web pages freezing for several seconds
- Connection timeouts
- Browser error messages indicating failure to reach the site

Initial suspicion pointed to a possible network or firewall-related issue.

---

## 4. Impact

- Loss of web connectivity on the affected host
- Inability to access HTTP and HTTPS services
- Partial disruption of normal internet usage

The issue impacted only one host and did not spread laterally.

---

## 5. Analysis

Basic connectivity tests were performed to isolate the issue:

- **Ping tests** to public IPs and domains resulted in packet loss
- **Access by IP address** failed, ruling out DNS as the primary cause
- **Browser testing** showed delayed loading followed by connection failure
- **Firewall log review** revealed blocked TCP traffic on ports 80 and 443

Further inspection of pfSense firewall rules identified recently modified TCP-related rules that could interfere with session establishment and termination.

---

## 6. Root Cause

The root cause was a series of firewall rule adjustments that improperly handled TCP traffic, impacting essential TCP behavior on ports 80 and 443.

These misconfigurations prevented proper TCP session handling, resulting in broken or incomplete web connections.

---

## 7. Remediation

- Identified the firewall rules affecting TCP traffic on ports 80 and 443
- Disabled the misconfigured rules
- Verified connectivity restoration using:
  - Ping
  - Web browser access
  - Firewall log validation

Normal web traffic was successfully restored.

---

## 8. Lessons Learned

- Firewall rule changes must be reviewed carefully before and after deployment
- Misconfigured TCP rules can cause partial connectivity issues that are not immediately obvious
- Continuous monitoring of firewall logs is essential to detect unintended traffic blocks
- Even small configuration changes can have significant service impact
