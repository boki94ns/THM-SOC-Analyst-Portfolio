# Lab 02 – Firewall Blocked Blacklisted URL Investigation (TryHackMe)

## Scenario Overview

This lab documents a firewall alert investigation performed in the TryHackMe SOC Simulator.

The alert was triggered when an internal host attempted an outbound connection to a blacklisted external URL. The firewall successfully blocked the request. The objective of this investigation was to validate the alert, review the network indicators, enrich the destination IP and URL using threat intelligence sources, and determine whether the alert should be classified as a True Positive.

---

## Time of Activity

May 1st 2026, 17:38 – 17:40

---

## Alert Summary

- Event ID: 8816
- Alert rule: Access to Blacklisted External URL Blocked by Firewall
- Severity: High
- Alert type: Firewall
- Datasource: firewall
- Action: blocked
- Firewall rule: Blocked Websites

---

## Affected Entities and Network Indicators

| Field | Value |
|---|---|
| Source IP | 10.20.2.17 |
| Source Port | 34257 |
| Destination IP | 67.199.248.11 |
| Destination Port | 80 |
| URL | http://bit.ly/3sHkX3da12340 |
| Application | web-browsing |
| Protocol | TCP |
| Action | blocked |
| Rule | Blocked Websites |

---

## 1. Alert Queue Review

The investigation started from the alert queue. Event ID 8816 was selected because it was a High severity firewall alert involving access to a blacklisted external URL.

![Alert Queue Review](images/screen1.png)

**What this shows:**  
The SOC simulator shows a High severity firewall alert. The alert indicates that an internal user or host attempted to access an external URL that was already listed in the organization's blacklist or threat intelligence feeds.

---

## 2. Firewall Alert Details

The alert details were reviewed to identify the source, destination, URL, protocol, action, and firewall rule.

![Firewall Alert Details](images/screen2.png)

**What this shows:**  
The internal host 10.20.2.17 attempted an outbound TCP connection to destination IP 67.199.248.11 over port 80. The requested URL was http://bit.ly/3sHkX3da12340. The firewall action was blocked, and the rule that triggered was Blocked Websites.

**Analysis:**  
This is an outbound web-browsing attempt from an internal host to an external destination. The destination port 80 indicates HTTP traffic. The use of a Bitly shortened URL is suspicious because URL shorteners can hide the final destination and are commonly abused in phishing campaigns.

---

## 3. True Positive Classification

After reviewing the firewall event and threat intelligence indicators, the alert was classified as a True Positive.

![True Positive Classification](images/screen3.png)

**What this shows:**  
The alert was marked as True Positive because the blocked outbound connection matched the alert logic and was supported by additional suspicious indicators.

**Analysis:**  
This is not a false positive because the firewall actually blocked an outbound request to a blacklisted URL. The classification does not prove that the internal host is compromised, but it confirms that the alert represents a real suspicious connection attempt.

---

## 4. Case Report – Affected Entities and Initial Reasoning

The case report was completed with the time of activity, affected entities, and the initial reason for classification.

![Case Report Part 1](images/screen4.png)

**What this shows:**  
The report documents the source host, source port, destination IP, destination port, URL, protocol, application, and firewall rule involved in the alert.

**Analysis:**  
The most important affected internal entity is 10.20.2.17. This host attempted to access the blacklisted shortened URL. Because the firewall blocked the connection, there is no evidence from this alert alone that the connection was successful.

---

## 5. Case Report – Classification and Escalation Reason

The report explains why the alert was treated as a True Positive and why escalation was required.

![Case Report Part 2](images/screen5.png)

**What this shows:**  
The report states that the outbound connection attempt was blocked by the firewall and that the URL was a shortened Bitly link.

**Analysis:**  
The alert requires escalation because an internal host attempted to access a URL associated with suspicious activity. Even though the request was blocked, the source host should be reviewed for repeated attempts, user interaction, or possible exposure to phishing content.

---

## 6. Case Report – Remediation and Attack Indicators

The remediation actions and attack indicators were documented in the case report.

![Case Report Part 3](images/screen6.png)

**What this shows:**  
The report recommends keeping the destination URL and IP blocked, monitoring the source IP for repeated attempts, reviewing firewall or proxy logs, checking possible user interaction, and performing endpoint investigation if repeated attempts are detected.

**Analysis:**  
The response should not stop only at blocking the destination. The internal host should also be monitored because repeated connection attempts could indicate user interaction with phishing content, browser redirection, or suspicious endpoint activity.

---

## 7. Escalation Decision

The alert was escalated due to the potential risk of credential harvesting or further suspicious activity.

![Escalation Decision](images/screen7.png)

**What this shows:**  
The alert was marked for escalation.

**Analysis:**  
Escalation is appropriate because the alert is High severity and involves an internal host attempting to access a blacklisted external URL. Escalation means that additional monitoring or review is required, not necessarily that the host is confirmed compromised.

---

## 8. Alert Closure

After classification and documentation, the alert was successfully closed.

![Alert Closed](images/screen8.png)

**What this shows:**  
The alert was closed after being investigated, documented, classified as True Positive, and escalated.

---

## 9. AbuseIPDB – Destination IP Overview

The destination IP address 67.199.248.11 was checked in AbuseIPDB.

![AbuseIPDB Destination IP Overview](images/screen9.png)

**What this shows:**  
AbuseIPDB shows that 67.199.248.11 exists in its database and has been reported 851 times. The Abuse Confidence Score is 13%. The IP is associated with Bitly infrastructure, and the hostname/domain shown is bit.ly.

**Analysis:**  
A 13% Abuse Confidence Score is not a strong standalone proof of malicious activity. However, the large number of historical reports and association with a URL-shortening service support treating this destination as suspicious in the context of this firewall alert.

---

## 10. AbuseIPDB – Abuse Report History

The AbuseIPDB report history was reviewed to understand the type of previous suspicious activity associated with the destination IP.

![AbuseIPDB Report History](images/screen10.png)

**What this shows:**  
The IP has previous reports related to phishing, web attacks, web spam, email spam, spoofing, and unauthorized connection attempts.

**Analysis:**  
The reports show that this infrastructure has been repeatedly associated with suspicious activity. Since Bitly is a legitimate URL-shortening service, the IP itself should not automatically be treated as fully malicious. However, attackers often abuse URL shorteners to hide phishing destinations, and the report history supports the firewall's decision to block the request.

---

## 11. VirusTotal – Destination IP Check

The destination IP address 67.199.248.11 was checked in VirusTotal.

![VirusTotal Destination IP Check](images/screen11.png)

**What this shows:**  
VirusTotal shows that 1 out of 91 security vendors flagged the IP address as malicious.

**Analysis:**  
This is a low detection ratio, so it should not be treated as absolute proof that the IP address is malicious. However, it is still a supporting indicator when combined with the firewall block, AbuseIPDB history, and the suspicious shortened URL.

---

## 12. VirusTotal – Shortened URL Check

The full shortened URL was checked in VirusTotal.

![VirusTotal URL Check](images/screen12.png)

**What this shows:**  
VirusTotal shows that 1 out of 92 security vendors flagged the URL as malicious/phishing. The URL also shows redirect-related behavior such as meta-redirect and multiple redirects.

**Analysis:**  
The URL result is especially relevant because the firewall alert was triggered by access to this specific URL. Even though only one vendor flagged it, the phishing classification supports the alert. The presence of redirects is also important because shortened links can hide the final destination from the user.

---

## 13. VirusTotal URL Vendor Classification

The VirusTotal vendor details show that the URL was specifically categorized as phishing by at least one vendor.

![VirusTotal URL Vendor Classification](images/screen13.png)

**What this shows:**  
The URL was flagged as phishing by a security vendor.

**Analysis:**  
This finding supports the conclusion that the blocked URL is suspicious. It should be used as a supporting indicator, not as the only reason for classification.

---

## Investigation Summary

The firewall blocked an outbound HTTP request from internal host 10.20.2.17 to the shortened URL http://bit.ly/3sHkX3da12340. The destination IP was 67.199.248.11 over TCP port 80.

The URL is a Bitly shortened link. Bitly is a legitimate service, but shortened URLs are commonly abused in phishing campaigns because they hide the final destination from the user.

Threat intelligence checks provided supporting evidence:

- AbuseIPDB shows historical abuse reports for 67.199.248.11.
- AbuseIPDB reports include phishing and other suspicious categories.
- VirusTotal shows low but present malicious detection for the destination IP.
- VirusTotal shows low but present phishing/malicious detection for the shortened URL.
- The firewall rule Blocked Websites successfully blocked the request.

There is no evidence from this alert alone that the connection succeeded or that the internal host was compromised. However, the combination of firewall blocking, blacklisted URL, shortened URL structure, AbuseIPDB history, and VirusTotal detections supports a True Positive classification.

---

## Indicators of Compromise

| Type | Indicator |
|---|---|
| Source IP | 10.20.2.17 |
| Source Port | 34257 |
| Destination IP | 67.199.248.11 |
| Destination Port | 80 |
| URL | http://bit.ly/3sHkX3da12340 |
| Protocol | TCP |
| Application | web-browsing |
| Firewall action | blocked |
| Firewall rule | Blocked Websites |
| AbuseIPDB | 851 reports, 13% Abuse Confidence Score |
| VirusTotal IP | 1/91 vendor flagged as malicious |
| VirusTotal URL | 1/92 vendor flagged as malicious/phishing |

---

## Final Classification

**True Positive – Blocked outbound access to a blacklisted external URL**

---

## Recommended Remediation Actions

- Keep the destination URL blocked.
- Keep the destination IP blocked if aligned with organizational policy.
- Monitor source IP 10.20.2.17 for repeated connection attempts.
- Review firewall and proxy logs for similar outbound requests.
- Check whether the user interacted with a phishing email or suspicious webpage.
- Perform endpoint investigation if repeated attempts are detected.
- Educate the user about risks related to shortened links and suspicious URLs.

---

## Skills Demonstrated

- Firewall alert triage
- Outbound traffic analysis
- Source and destination IP interpretation
- URL reputation analysis
- AbuseIPDB investigation
- VirusTotal investigation
- IOC documentation
- True Positive classification
- Incident report writing

