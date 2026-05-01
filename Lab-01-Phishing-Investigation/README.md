# Lab 01 – Phishing Email Investigation (TryHackMe)

## Scenario Overview

This lab documents a phishing investigation performed in the TryHackMe SOC Simulator.  
The alert involved an inbound email containing a suspicious external link.

The objective was to determine whether the alert was a **True Positive phishing attempt** and document the investigation process.

---

## Time of Activity

**May 1st 2026, 12:51 – 12:53**

---

## Affected Entities

- **Recipient:** `j.garcia@thetrydaily.thm`
- **Sender:** `onboarding@hrconnex.thm`
- **Suspicious domain:** `hrconnex.thm`
- **Suspicious URL:** `https://hrconnex.thm/onboarding/15400654060/j.garcia`

---

## 1. Alert Queue Review

The investigation started from the alert queue, where multiple phishing-related alerts were visible.  
Alert ID **8818** was selected because it involved an inbound email containing a suspicious external link.

![Alert Queue Review](images/screen1.png)

**What this shows:**  
The phishing alert was selected from the SOC alert queue for further investigation.

---

## 2. Alert Assignment

The alert was assigned for investigation before opening the full alert details.

![Alert Assignment](images/screen2.png)

**What this shows:**  
The alert was taken into the analyst workflow so it could be reviewed and documented.

---

## 3. Alert Details and Email Metadata

The alert details show the main email metadata, including sender, recipient, direction, subject, and alert description.

![Alert Details and Email Metadata](images/screen3.png)

**What this shows:**  
The email was inbound and sent from `onboarding@hrconnex.thm` to `j.garcia@thetrydaily.thm`.  
The subject **“Action Required: Finalize Your Onboarding Profile”** indicates urgency and is consistent with phishing social engineering.

---

## 4. Email Body and Suspicious Link

The email body requests the user to finalize an onboarding profile by clicking an external link.

![Email Body and Suspicious Link](images/screen4.png)

**What this shows:**  
The email attempts to make the recipient click a link related to onboarding.  
This is suspicious because onboarding is a believable business process that attackers can abuse to steal credentials.

---

## 5. Full URL Reputation Check – VirusTotal

The full URL from the email was checked in VirusTotal:

`https://hrconnex.thm/onboarding/15400654060/j.garcia`

![VirusTotal Full URL Check](images/screen5.png)

**What this shows:**  
VirusTotal returned **“Item not found”**, meaning the URL had no known reputation.  
This does not prove the URL is safe. In phishing investigations, lack of reputation can increase suspicion because new or rarely used URLs are often used in attacks.

---

## 6. Domain DNS Check – SecurityTrails

The base domain `hrconnex.thm` was checked in SecurityTrails to verify whether DNS records existed.

![SecurityTrails Domain Check](images/screen6.png)

**What this shows:**  
SecurityTrails returned no DNS records for the domain.  
This supports the conclusion that the domain could not be verified as a legitimate or established domain.

---

## 7. Local DNS Resolution Test

A local DNS resolution test was performed using the `ping` command.

![Local DNS Resolution Test](images/screen7.png)

**What this shows:**  
The domain could not be resolved to an IP address.  
This confirms that the domain was not publicly resolvable during the investigation.

---

## 8. True Positive Classification

After reviewing the email, URL, domain reputation, and DNS results, the alert was classified as **True Positive**.

![True Positive Classification](images/screen8.png)

**What this shows:**  
The alert was marked as a valid phishing attempt based on multiple suspicious indicators.

---

## 9. Case Report Documentation

The case report was completed with the affected entities, classification reason, escalation reason, remediation actions, and attack indicators.

![Case Report Documentation](images/screen9.png)

**What this shows:**  
The investigation findings were documented in the case report.  
This includes why the alert was treated as phishing and what actions should be taken.

---

## 10. Alert Closure

The platform confirmed that the alert was successfully completed and closed.

![Alert Closure Confirmation](images/screen10.png)

**What this shows:**  
The phishing alert was closed after being investigated, documented, and classified correctly.

---

## Indicators of Compromise (IOCs)

| Type | Indicator |
|---|---|
| Sender email | `onboarding@hrconnex.thm` |
| Recipient | `j.garcia@thetrydaily.thm` |
| Domain | `hrconnex.thm` |
| URL | `https://hrconnex.thm/onboarding/15400654060/j.garcia` |
| Subject | `Action Required: Finalize Your Onboarding Profile` |

---

## Why This Was Classified as Phishing

The alert was classified as phishing because several indicators appeared together:

- The email used an onboarding theme to gain trust.
- The subject created urgency with **“Action Required”**.
- The email contained an external link requiring user action.
- The full URL had no reputation in VirusTotal.
- The domain had no DNS records in SecurityTrails.
- The domain could not be resolved locally using DNS.

No single indicator alone is enough to prove phishing with absolute certainty.  
However, the combination of these indicators strongly supports a **True Positive phishing classification**.

---

## Final Classification

**True Positive – Phishing**

---

## Recommended Remediation Actions

- Block the sender/domain at the email gateway.
- Monitor for similar emails targeting other users.
- Educate the affected user about phishing indicators.
- Reset credentials if the user clicked the link or submitted information.
- Review email security logs for related activity.

---

## Skills Demonstrated

- SOC alert triage
- Email header and metadata review
- Phishing analysis
- URL reputation checking
- DNS/domain investigation
- Threat intelligence usage
- Case report writing
- Incident classification
