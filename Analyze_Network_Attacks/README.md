# Analyze Network Attacks

## Project Overview
This project features a cybersecurity incident report and log analysis conducted for a web server experiencing a critical network interruption. As organizations rely heavily on e-commerce and web availability, identifying anomalous traffic patterns and diagnosing server availability issues is essential to mitigating business downtime and preserving operational continuity.

The project evaluates raw packet capture (PCAP) data from a simulated network event, maps out the mechanics of the attack using the **TCP/IP Protocol Suite**, and outlines technical remediation steps to harden infrastructure against future availability threats.

---

## Audit Parameters & Scope
* **Scope:** Internal web server infrastructure (`192.0.2.1`) hosting corporate resources.
* **Incident Classification:** Denial of Service (DoS) / SYN Flooding.
* **Business Impact:** High availability disruption, resulting in connection timeouts for legitimate website visitors.

---

## Repository Structure
This repository documents the entire incident analysis process, organizing input data alongside the final deliverable:
* 📄 `HTTP-log.pdf` - The baseline packet capture log containing raw network traffic metrics and handshake states used as source data.
* 📄 `Cybersecurity-incident-report.pdf` - My finalized and documented Cybersecurity Incident Report (Core Deliverable).

---

## Technical Analysis & Core Findings

### 1. Baseline Traffic vs. Anomalous Activity
* **Normal Behavior:** Early log entries show legitimate source IPs (e.g., `198.51.100.23` and `198.51.100.14`) establishing healthy connections with the web server via port 443. These users completed the standard TCP three-way handshake and successfully loaded web elements (`HTTP/1.1 200 OK`).
* **Anomalous Volume:** Starting at timestamp `3.390692`, a single malicious source IP (`203.0.113.0`) began transmitting a continuous, high-velocity stream of automated TCP requests to the web server.

### 2. Exploitation of the TCP Three-Way Handshake
* **The Vulnerability:** Under normal conditions, a client sends a `SYN` packet, the server responds with a `SYN-ACK` and reserves memory space, and the client closes the loop with an `ACK` packet. 
* **The Mechanism:** The malicious actor (`203.0.113.0`) flooded the server with `SYN` packets but intentionally withheld the final `ACK` responses. This forced the web server to keep thousands of temporary half-open connection slots reserved in its system buffer.

### 3. Operational Impact & Malfunction
* **Resource Exhaustion:** The continuous volume of incomplete connection requests depleted the web server’s internal resource capacity.
* **Denial of Service:** With system buffers fully saturated, the server became completely overwhelmed. It could no longer open new connection sockets, forcing incoming legitimate traffic to experience strict connection resets (`[RST, ACK]`) or drop entirely into `HTTP/1.1 504 Gateway Time-out` states.

---

## Recommendations Summary
* **Deploy Network-Based Rate Limiting:** Configure edge firewalls or Intrusion Prevention Systems (IPS) to throttle the maximum number of simultaneous `SYN` requests allowed from a single source IP address.
* **Reduce SYN-ACK Timeout Windows:** Optimize the server's TCP configuration to decrease the time a connection slot remains reserved while waiting for an unreturned `ACK` packet, allowing resources to free up faster.

