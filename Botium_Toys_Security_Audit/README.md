# Botium Toys Security Audit

## Project Overview
This project features an internal IT security audit conducted for **Botium Toys**, a small U.S. business expanding its footprint in retail and e-commerce. As the organization grows internationally, the IT department must adapt infrastructure to address escalating security challenges, mitigate potential regulatory fines, and preserve operational continuity.

The audit evaluates the company's current security posture across administrative, technical, and physical domains using the **NIST Cybersecurity Framework (NIST CSF)** guidelines, ensuring compliance with global data privacy frameworks like **PCI DSS** and **GDPR**.

---

## Audit Parameters & Scope
* **Scope:** The entire security program at Botium Toys, assessing all physical/digital assets alongside internal processes and control compliance.
* **Risk Score:** Rated at **8 out of 10** (Fairly High) due to critical control gaps.
* **Potential Impact:** Rated as **Medium** because asset classification boundaries are currently undefined.

---

## Repository Structure
This repository documents the entire audit process, organizing input parameters alongside the final deliverable:
* 📄 `Botium-Toys-Scope-goals-and-risk-assessment-report.pdf` - The baseline operational scope, asset matrix, and risk report used as source data.
* 📄 `Control-categories.pdf` - Standard mapping guidelines utilized to categorize organizational safety measures.
* 📄  `Controls-and-compliance-checklist.pdf` - My finalized and audited Controls & Compliance Checklist (Core Deliverable).

---

## Core Findings & Identified Control Gaps

### 1. Administrative / Managerial Controls
* **Vulnerability:** Internal access structures lack the application of Least Privilege and Separation of Duties. 
* **Impact:** All employees possess unchecked authorization to view corporate internal databases, including customer credit cards, PII, and SPII.
* **Policies:** Corporate password policies remain nominal, dropping below baseline industry requirements for complexity (lacking enforcement of length and special characters). No centralized password manager is present.
* **Business Continuity:** Total absence of formalized Disaster Recovery Plans (DRP).

### 2. Technical Controls
* **Vulnerability:** Local cryptographic measures are completely absent.
* **Impact:** Financial and personal tracking data are captured, processed, transmitted, and retained locally in plaintext.
* **Network & Endpoint Security:** While active perimeter defense is managed through a localized firewall and endpoint antivirus is monitored, the corporate network lacks an Intrusion Detection System (IDS) to catch live malicious activity.
* **Data Recovery:** The company does not currently maintain backups of critical data.
* **Legacy Systems:** End-of-life hardware assets are actively maintained but operate without clear regular scheduling or predefined response instructions.

### 3. Physical / Operational Controls 
* **Status:** This category is fully implemented and secure.
* **Measures:** The adjoining corporate warehouse, storefront, and administrative site are properly guarded via up-to-date CCTV surveillance, physical locks, and fire detection/prevention arrays.

### 4. Regulatory Compliance Status
* **PCI DSS:** Non-compliant due to lack of encryption on cardholder data and overly broad employee access.
* **GDPR:** Partially compliant. While data privacy controls are weak, the IT department successfully established a plan to notify E.U. customers within 72 hours of a security breach.

---

## Recommendations Summary
* Enforce **Least Privilege Access Profiles** (Preventative Administrative control) to segregate staff permissions based strictly on job scope.
* Deploy full **Data Encryption Protocols** (Deterrent Technical control) for cardholder data environments and private databases.
* Build a resilient **Backup Policy** and an actionable **Disaster Recovery Plan (DRP)** (Corrective controls) to ensure business continuity.
* Integrate an **Intrusion Detection System (IDS)** (Detective Technical control) and an enterprise-wide **Centralized Password Management System**.
