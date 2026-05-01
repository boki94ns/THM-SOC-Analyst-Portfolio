# Lab 01 – Phishing Investigation

## 📌 Scenario

An inbound email containing a suspicious external link was detected by the SIEM system. The email targeted a specific employee and requested urgent action related to onboarding.

---

## 🕒 Time of Activity

May 1st 2026, 12:51 – 12:53

---

## 👤 Affected Entities

* User: [j.garcia@thetrydaily.thm](mailto:j.garcia@thetrydaily.thm)
* Sender: [onboarding@hrconnex.thm](mailto:onboarding@hrconnex.thm)
* Domain: hrconnex.thm

---

## 📧 Email Analysis

The email attempts to impersonate an onboarding process and pressures the user to click a malicious link.

![Phishing Email](images/screen1.png)

---

## 🌐 URL Investigation

The embedded URL appears suspicious and does not resolve properly.

![URL Analysis](images/screen2.png)

---

## 🔍 Threat Intelligence

Multiple sources were checked:

* VirusTotal → No reputation
* SecurityTrails → No DNS records
* DNS resolution → Failed

![SecurityTrails](images/screen3.png)

---

## ⚠️ Indicators of Compromise (IOCs)

* Suspicious domain: hrconnex.thm
* External email source
* Phishing subject: *"Action Required: Finalize Your Onboarding Profile"*
* Suspicious URL structure
* Domain does not resolve to an IP
* No reputation in threat intelligence tools

---

## 📊 Classification

**True Positive – Phishing Attack**

Reason:
The email uses social engineering, impersonation, and a malicious link targeting credential harvesting.

---

## 🚨 Escalation

**Yes**

Reason:
High likelihood of credential compromise and targeted attack against employee.

---

## 🛠️ Recommended Actions

* Block domain at email gateway and firewall
* Educate the user about phishing awareness
* Monitor for similar phishing attempts
* Reset credentials if interaction occurred

---

## ✅ Conclusion

This alert represents a targeted phishing attempt designed to harvest user credentials and potentially gain unauthorized access to the organization.

