# Phishing Email Analysis — SOC Investigation Report

## 1. Executive Summary

A simulated phishing email was analyzed to identify indicators of phishing and potential credential-harvesting activity.

The investigation included email header analysis, sender and Reply-To verification, SPF/DKIM/DMARC authentication checks, URL analysis, attachment static analysis, SHA-256 hashing, and IOC extraction.

**Final Verdict:** Phishing Email
**Severity:** High
**Analysis Type:** Static / Safe Analysis

---

## 2. Email Analysis

### Sender Information

* **Display Name:** Microsoft Security
* **Sender:** `security@micros0ft-support.example`
* **Reply-To:** `account-verification@fake-support.example`
* **Source IP:** `192.0.2.55`

### Header Findings

* The sender uses a look-alike domain containing `micros0ft`.
* The **From** and **Reply-To** addresses use different domains.
* The email creates urgency by claiming the account will be suspended within 24 hours.

---

## 3. Email Authentication

| Mechanism | Result | Observation                            |
| --------- | ------ | -------------------------------------- |
| SPF       | FAIL   | Sender authentication failed           |
| DKIM      | FAIL   | Email signature verification failed    |
| DMARC     | FAIL   | Domain authentication/alignment failed |

The failure of all three authentication mechanisms is a strong indicator that the email should not be trusted.

---

## 4. URL Analysis

**Suspicious URL:**

`http://login-microsoft-security.example/verify`

### Findings

* Uses **HTTP** instead of HTTPS.
* Uses a Microsoft-themed look-alike domain.
* The `/verify` path supports an account-verification lure.
* The same URL was also found inside the HTML attachment.

The URL was analyzed without opening or executing it.

---

## 5. Attachment Analysis

**Attachment:** `Account_Verification.html`

The attachment was analyzed using static methods only.

### SHA-256

`577E3F06DBA034B55BA85E8EBEFD852A4C7CCC72C4F41A855DABA6F15742580B5`

Static content inspection identified the following embedded URL:

`http://login-microsoft-security.example/verify`

The attachment was **not executed or opened in a browser**.

---

## 6. Indicators of Compromise (IOCs)

| IOC Type     | Value                                                               |
| ------------ | ------------------------------------------------------------------- |
| Sender Email | `security@micros0ft-support.example`                                |
| Reply-To     | `account-verification@fake-support.example`                         |
| Domain       | `micros0ft-support.example`                                         |
| Source IP    | `192.0.2.55`                                                        |
| URL          | `http://login-microsoft-security.example/verify`                    |
| Attachment   | `Account_Verification.html`                                         |
| SHA-256      | `577E3F06DBA034B55BA85E8EBEFD852A4C7CCC72C4F41A855DABA6F15742580B5` |

---

## 7. Key Findings

1. Look-alike sender domain detected.
2. From and Reply-To addresses do not match.
3. SPF authentication failed.
4. DKIM authentication failed.
5. DMARC authentication failed.
6. Suspicious account-verification URL identified.
7. HTML attachment contained the same suspicious URL.
8. SHA-256 hash was generated for the attachment.

---

## 8. Final Verdict

### 🔴 HIGH-SEVERITY PHISHING EMAIL

The combined evidence strongly indicates a simulated phishing attempt designed to create urgency and direct the recipient toward an account-verification resource.

The sample is considered **phishing/suspicious**, with potential credential-harvesting intent.

---

## 9. Recommended SOC Actions

* Do not click the suspicious URL.
* Do not open or execute the attachment.
* Quarantine the email.
* Block identified malicious/suspicious indicators where appropriate.
* Search the environment for the extracted IOCs.
* Review authentication and endpoint logs for related activity.
* Report the incident according to the organization's incident-response process.

---

## 10. Analysis Tools

* Windows PowerShell
* Text Editor
* Static file analysis
* SHA-256 hashing
* IOC extraction

**Note:** This project uses a safe, simulated phishing email and reserved `.example` indicators for educational purposes.
