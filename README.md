# Okta Identity & Access Management (OKPRO1) Implementation

## 📌 Project Overview
This repository documents a comprehensive identity and access management (IAM) deployment based on the Okta Certified Professional exam blueprint. The objective was to provision a simulated workforce, enforce Zero Trust access controls via network zones and MFA, integrate external SaaS applications, and automate group memberships using Okta Expression Language.

*   **Organization:** Simulated Enterprise (Okta Developer Tenant)
*   **Target Tenant:** `trial-6733240.okta.com`
*   **User Base:** Employees across Executives, Finance, Accounting, and IT/Security departments.
*   **Core Technologies:** Okta Admin Console, Okta Integration Network (OIN), SAML 2.0, Secure Web Authentication (SWA), Okta FastPass, Okta Expression Language.

---

## 🛠️ Phase 1: Implement and Manage User Identities
**Objective:** Provision the organization's directory, configure custom profiles, and automate group memberships.

*   **Directory Provisioning & Profiles:** Provisioned users (e.g., Nina Shah, Alano Clinning, Aksel Edgeley) into the Universal Directory. Extended the base Okta User Profile by creating a custom string attribute named `Region` with an enumerated list (AMER, APAC, EMEA).
*   **Automated Group Memberships:** Configured Okta Group Rules to automate identity lifecycles. Created a rule named `Finance and Accounting Employees` utilizing Okta Expression Language: `(user.department=="Finance" || user.department=="Accounting") && user.userType=="Employee"`.
*   **Delegated Administration:** Created a Custom Admin Role named `Suspend and Unsuspend Users` scoped to a custom Resource Set (`All Users`). This ensures granular, least-privilege administrative access compared to standard Super Admin assignments.

![phase 1](Screenshots/definegroups10.png)

---

## 🔒 Phase 2: Authentication and Security Enforcement
**Objective:** Enforce secure access, deploy phishing-resistant MFA, and apply contextual access policies.

*   **Authenticator Configuration:** Deployed Okta Verify as a required factor, utilizing Device Bound, Hardware Protected, and Phishing Resistant (Okta FastPass) characteristics. Enabled Email as an optional auto-enrolled authenticator.
*   **Contextual Access & Network Zones:** Created a Dynamic Network Zone named `Allowed Countries` restricting access strictly to United States IP addresses. 
*   **Authentication & Session Policies:** 
    *   **Global Session Policy:** Configured a standard policy enforcing a maximum session lifetime of 12 hours with a 30-minute idle timeout.
    *   **Authentication Policies:** Created a `Restricted Countries` rule requiring step-up authentication. Bound specific sign-on requirements to the `IT/Security` group, enforcing zero-trust principles for high-privilege users.

*[Insert Screenshot: Okta Authentication Policies or Network Zones Dashboard]*

---

## ⚙️ Phase 3: Application Integration (OIN)
**Objective:** Integrate enterprise SaaS applications and manage identity provisioning to external workloads.

*   **Microsoft Office 365 (Provisioning):** Integrated Office 365 (`izreal909.onmicrosoft.com`) via the Okta Integration Network. Authenticated the API integration to automate user account creation, updates, and deactivation directly from Okta.
*   **Zendesk (SWA Integration):** Added Zendesk via the OIN utilizing Secure Web Authentication (SWA). Configured the integration so the "User sets username and password," and mapped baseline access via the `Everyone` group.
*   **Salesforce (SAML 2.0 Integration):** Deployed a Salesforce Sandbox instance using SAML 2.0. Generated active SHA-2 SAML Signing Certificates and configured Identity Provider (IdP) metadata to establish trust between Okta and Salesforce.

*[Insert Screenshot: Salesforce SAML 2.0 Configuration or App Assignments]*

---

## 🛡️ Phase 4: Troubleshooting and Auditing
**Objective:** Audit system events, troubleshoot access issues, and monitor user lifecycles.

*   **System Log Auditing:** Actively monitored the Okta System Log to verify configuration success. Tracked specific events such as `Authentication of user via MFA` (Okta Verify/FastPass), `Group membership rule triggered`, and `Create okta group`.
*   **Identity Troubleshooting:** Utilized diagnostic logs to trace specific actor events (e.g., IP address mapping to the `Allowed Countries` zone) and verify that step-up authentication policies were appropriately evaluating targets based on their group attributes.

*[Insert Screenshot: Okta System Log MFA Event Verification]*

---
**Author:** Elijah Howard  
**Certifications:** Okta Certified Professional (In Progress), SC-300, CompTIA Security+, CySA+, CSAP, Network+
```eof

This Markdown file captures the essence of your Okta lab activities, directly mirroring the structure you used for your Entra ID project. Let me know if you need any adjustments to the bullet points or formatting!
