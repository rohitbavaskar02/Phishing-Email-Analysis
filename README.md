# 📧 Phishing Email Analysis

A **SOC-focused phishing email investigation project** performed using a safe, simulated phishing email sample.

The objective was to analyze suspicious email characteristics, validate sender authentication, investigate URLs and attachments, extract IOCs, and determine the final phishing verdict using a structured SOC investigation approach.

---

## 🎯 Objectives

* Analyze **email headers and sender information**
* Investigate **From and Reply-To** addresses
* Analyze **SPF, DKIM, and DMARC**
* Perform safe **URL analysis**
* Perform **static attachment analysis**
* Generate a **SHA-256 file hash**
* Extract **Indicators of Compromise (IOCs)**
* Determine the final phishing verdict
* Document the investigation in a **SOC-style incident report**

---

## 🛠️ Tools & Technologies

* **Windows PowerShell**
* **Email Header Analysis**
* **SPF / DKIM / DMARC**
* **Static File Analysis**
* **SHA-256 Hashing**
* **IOC Extraction**
* **Threat Intelligence Concepts**

---

## 🔍 Investigation Workflow

```text
Phishing Email
      ↓
Email Header Analysis
      ↓
Sender & Reply-To Investigation
      ↓
SPF / DKIM / DMARC
      ↓
URL Analysis
      ↓
Attachment Static Analysis
      ↓
SHA-256 Hashing
      ↓
IOC Extraction
      ↓
Final Phishing Verdict
      ↓
SOC Incident Report
```

---

## 1️⃣ Email Header & Sender Analysis

The email headers were reviewed to identify suspicious sender information and infrastructure.

### Key Findings

* Look-alike sender domain using `micros0ft`
* Different **From** and **Reply-To** addresses
* Suspicious source IP
* Urgent account-suspension message

![Email Header Analysis](screenshots/01_Email_Header_Sender_Analysis.png)

---

## 2️⃣ SPF / DKIM / DMARC Analysis

Email authentication results were analyzed to determine whether the sender could be trusted.

| Authentication | Result |
| -------------- | ------ |
| SPF            | ❌ FAIL |
| DKIM           | ❌ FAIL |
| DMARC          | ❌ FAIL |

The failure of all three authentication mechanisms increased the confidence that the email was fraudulent.

![SPF DKIM DMARC](screenshots/02_SPF_DKIM_DMARC_Authentication.png)

---

## 3️⃣ URL Analysis

The suspicious URL identified in the email was:

```text
http://login-microsoft-security.example/verify
```

### Observations

* Uses **HTTP**
* Uses a Microsoft-themed look-alike domain
* Contains an account verification path
* Designed to create urgency and encourage user interaction

The URL was analyzed **without opening or executing it**.

![Suspicious URL Analysis](screenshots/03_Suspicious_URL_Analysis.png)

---

## 4️⃣ Attachment Analysis

The email contained the following attachment:

```text
Account_Verification.html
```

The attachment was analyzed using **static analysis techniques only**.

No browser execution or active interaction with the attachment was performed.

![Attachment Evidence](screenshots/04_Attachment_Evidence.png)

---

## 5️⃣ SHA-256 & Static Analysis

A SHA-256 hash was generated to create a unique fingerprint of the attachment.

The HTML content was also inspected using PowerShell to identify embedded URLs.

### SHA-256

```text
577E3F06DBA034B55BA85E8EBEFD852A4C7CCC72C4F41A855DABA6F15742580B5
```

### Embedded URL Identified

```text
http://login-microsoft-security.example/verify
```

![Attachment Static Analysis](screenshots/05_Attachment_Static_Analysis.png)

---

## 🚨 Indicators of Compromise (IOCs)

| IOC Type       | Indicator                                                           |
| -------------- | ------------------------------------------------------------------- |
| Sender Email   | `security@micros0ft-support.example`                                |
| Reply-To       | `account-verification@fake-support.example`                         |
| Domain         | `micros0ft-support.example`                                         |
| Source IP      | `192.0.2.55`                                                        |
| Suspicious URL | `http://login-microsoft-security.example/verify`                    |
| Attachment     | `Account_Verification.html`                                         |
| SHA-256        | `577E3F06DBA034B55BA85E8EBEFD852A4C7CCC72C4F41A855DABA6F15742580B5` |

Detailed IOC information is available in:

`evidence/IOCs.txt`

---

## 🔴 Final Verdict

**Classification:** Phishing Email
**Severity:** High
**Likely Objective:** Credential harvesting / account compromise

### Main Reasons

* Look-alike sender domain
* From/Reply-To mismatch
* SPF failure
* DKIM failure
* DMARC failure
* Suspicious verification URL
* HTML attachment containing the same URL
* Urgent account-suspension message

The combined indicators strongly support the classification of the sample as a **phishing email**.

---

## 🛡️ Recommended SOC Actions

If this were a real-world incident, recommended actions would include:

1. Quarantine the suspicious email.
2. Do not open or execute the attachment.
3. Do not access the suspicious URL.
4. Search the environment for the extracted IOCs.
5. Block confirmed malicious indicators.
6. Review endpoint and authentication logs.
7. Escalate the incident according to the organization's incident-response process.

---

## 📄 Project Report

A detailed investigation report is available here:

[`Phishing_Email_Analysis_Report.md`](report/Phishing_Email_Analysis_Report.md)

---

## 📁 Project Structure

```text
Phishing-Email-Analysis/
│
├── README.md
│
├── screenshots/
│   ├── 01_Email_Header_Sender_Analysis.png
│   ├── 02_SPF_DKIM_DMARC_Authentication.png
│   ├── 03_Suspicious_URL_Analysis.png
│   ├── 04_Attachment_Evidence.png
│   └── 05_Attachment_Static_Analysis.png
│
├── evidence/
│   └── IOCs.txt
│
└── report/
    └── Phishing_Email_Analysis_Report.md
```

---

## ⚠️ Safety & Disclaimer

This project uses a **safe, simulated phishing email** created for educational purposes.

The sample uses reserved `.example` domains and documentation IP addresses. No real malicious infrastructure, malware, or credential harvesting was used.

The attachment was analyzed using **static techniques only** and was not executed.

---

## 💼 SOC Analyst Skills Demonstrated

* Email Security Analysis
* Phishing Detection
* Email Header Investigation
* SPF / DKIM / DMARC Analysis
* URL Analysis
* Attachment Static Analysis
* SHA-256 Hashing
* IOC Extraction
* Security Investigation
* Incident Reporting

---

## 👨‍💻 Project Type

**Cybersecurity / SOC Analyst Lab Project**

**Focus:** Phishing Detection & Email Security Investigation
