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

## 📊 Alert Overview

![Alert Overview](images/screen1.png)

---

## 📧 Email Details

The email contains a phishing message requesting the user to finalize onboarding.

![Email Content](images/screen2.png)

---

## 🔗 Embedded Link Analysis

The link inside the email redirects to a suspicious domain.

![Suspicious Link](images/screen3.png)

---

## 🌐 URL Investigation

The domain does not resolve properly and appears inactive.

![URL Check](images/screen4.png)

---

## 🔍 Threat Intelligence Check – VirusTotal

No reputation found for the domain.

![VirusTotal](images/screen5.png)

---

## 🔍 Threat Intelligence Check – SecurityTrails

No DNS records found.

![SecurityTrails](images/screen6.png)

---

## 🖥️ Local DNS Resolution Test

Ping test confirms domain cannot be resolved.

![Ping Test](images/screen7.png)

---

## ⚠️ SIEM Alert Classification

Alert classified as phishing.

![Alert Classification](images/screen8.png)

---

## 📝 Case Report Entry

Documented analysis and response actions.

![Case Report](images/screen9.png)

---

## ✅ Alert Closure

The alert was successfully closed as a true positive.

![Alert Closed](images/screen10.png)

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

---

## 🚨 Escalation

**Yes**

---

## 🛠️ Recommended Actions

* Block domain at email gateway and firewall
* Educate the user about phishing awareness
* Monitor for similar phishing attempts
* Reset credentials if interaction occurred

---

## ✅ Conclusion

This alert represents a targeted phishing attempt designed to harvest user credentials and potentially gain unauthorized access to the organization.
