# 🛡️ Lab 01 – Phishing Investigation (TryHackMe)

---

## 📌 Scenario Overview
An alert was triggered for a **suspicious inbound email containing an external link**.  
The objective of this investigation was to determine whether the alert represents a **true phishing attempt** and assess potential risk.

---

## ⏱️ Time of Activity
May 1st 2026, 12:51 – 12:53

---

## 👥 Affected Entities
- **User:** j.garcia@thetrydaily.thm  
- **Sender:** onboarding@hrconnex.thm  
- **Domain:** hrconnex.thm  

---

## 🚨 Alert Overview

The SOC alert queue shows multiple alerts. The phishing alert (ID 8818) was selected for investigation.

![Alert Overview](images/screen1.png)

---

## 📊 Alert Details

The alert shows an inbound email from an external domain targeting a specific user.

![Alert Details](images/screen2.png)

---

## 📧 Email Analysis

The email contains social engineering elements:
- Urgency ("Action Required")
- Onboarding scenario
- Request for user interaction

![Email Content](images/screen3.png)

---

## 🔗 Embedded Link Analysis

The email includes the following URL: https://hrconnex.thm/onboarding/15400654060/j.garcia


![Embedded Link](images/screen4.png)

🔍 Observations:
- Suspicious domain
- Unusual URL structure
- Contains user-specific identifier

---

## 🌐 URL Reputation Check (VirusTotal)

The full URL was analyzed using VirusTotal.

![VirusTotal Result](images/screen5.png)

Result:
- No reputation found
- URL not indexed

Conclusion:
- Likely newly created or unknown → increases suspicion

---

## 🌍 Domain Analysis (SecurityTrails)

The domain was checked for DNS records.

![SecurityTrails](images/screen6.png)

Result:
- No DNS records found

Conclusion:
- Domain is not established or legitimate

---

## 🖥️ DNS Resolution Test

A local DNS check was performed using the ping command.

![Ping Test](images/screen7.png)

Result:
- Domain could not be resolved

Conclusion:
- Strong indicator of suspicious or non-existent infrastructure

---

## 📊 Classification

Based on all findings, the alert was classified as:

**True Positive – Phishing**

![Classification](images/screen8.png)

---

## 🚨 Escalation Decision

The alert was escalated due to potential credential compromise risk.

![Escalation](images/screen9.png)

---

## ✅ Alert Closure

The alert was successfully closed after investigation.

![Alert Closed](images/screen10.png)

---

## ⚠️ Indicators of Compromise (IOCs)

- Suspicious domain: hrconnex.thm  
- External email sender  
- Phishing subject: "Action Required: Finalize Your Onboarding Profile"  
- Suspicious URL structure  
- No DNS records  
- No threat intelligence reputation  
- Domain not resolvable  

---

## 🧠 Conclusion

This alert represents a **targeted phishing attempt** using a fake onboarding scenario.

The attacker attempts to:
- Trick the user into clicking a malicious link  
- Potentially harvest credentials  
- Gain unauthorized access  

---

## 🛠️ Recommended Actions

- Block domain `hrconnex.thm`  
- Educate user on phishing awareness  
- Monitor for similar attacks  
- Reset credentials if user interaction occurred  

---

## 📌 Skills Demonstrated

- Phishing detection  
- Email analysis  
- Threat intelligence usage  
- Domain investigation  
- SOC alert triage  
- Incident documentation  
