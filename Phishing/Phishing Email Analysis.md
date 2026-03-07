
---

# Phishing Email Analysis – Practical Write-Up

## 1. Introduction to Phishing

Phishing is a type of **social engineering attack** in which attackers attempt to trick victims into revealing sensitive information or executing malicious content.

The most common phishing methods include:

* sending emails containing malicious links
* sending emails with infected attachments
* redirecting victims to fake login pages

Attackers typically use persuasive language to encourage victims to act quickly.

Examples include:

```
"You have won a gift"
"Your account will be suspended"
"Limited time discount"
```

The main goal is to **exploit human trust**, which is considered the weakest link in cybersecurity.

Phishing is widely known as the **most common initial attack vector** used to gain access to systems.

---

# 2. Phishing in the Cyber Kill Chain

Phishing attacks typically occur in the **Delivery phase** of the Cyber Kill Chain.

The Delivery phase is where attackers **deliver malicious content to victims**.

Example attack flow:

```
Reconnaissance → Weaponization → Delivery → Exploitation
```

Example phishing scenario:

```
Attacker sends phishing email
↓
Victim clicks malicious link
↓
Malware downloaded or credentials stolen
```

After the delivery stage, attackers may proceed with:

* exploitation
* persistence
* lateral movement

---

# 3. Email Spoofing

Email spoofing is a technique used to **impersonate legitimate senders**.

Because email protocols were not originally designed with strong authentication mechanisms, attackers can send emails pretending to be:

* banks
* coworkers
* companies
* government organizations

To reduce spoofing risks, several authentication mechanisms were introduced:

* SPF
* DKIM
* DMARC

These mechanisms help verify whether an email was sent by an authorized mail server.

---

# 4. Email Authentication Protocols

## SPF (Sender Policy Framework)

SPF allows domain owners to specify **which servers are allowed to send emails on behalf of their domain**.

When an email is received, the mail server checks whether the sending IP address is authorized.

---

## DKIM (DomainKeys Identified Mail)

DKIM adds a **digital signature to emails**.

This allows receiving servers to verify:

* the sender's identity
* that the message has not been modified

---

## DMARC

DMARC works together with SPF and DKIM.

It allows domain owners to specify **how receiving servers should handle authentication failures**.

Possible actions include:

```
none
quarantine
reject
```

---

# 5. Email Traffic Analysis

When investigating phishing campaigns, analysts examine **email traffic data** to understand the scale and target of the attack.

Important parameters include:

* Sender Address
* SMTP IP Address
* Domain name
* Subject line
* Recipient addresses
* Timestamp

Example:

```
Sender: info@letsdefend.io
SMTP IP: 127.0.0.1
Domain: letsdefend.io
Subject: Invoice Payment
```

Analysts may search the mail gateway for:

* similar sender addresses
* identical subject lines
* emails sent during the same time period

If the same users receive multiple malicious emails, their addresses may have been leaked online.

Attackers may collect email addresses using tools like **theHarvester** on Kali Linux.

---

# 6. Email Headers

An email header contains **metadata about the email transmission process**.

This includes information such as:

* sender
* recipient
* sending server
* routing path

Headers are extremely important in phishing investigations because they help determine **where the email actually originated**.

---

# 7. Important Email Header Fields

### From

Displays the sender's email address.

Example:

```
From: support@company.com
```

However, this field can easily be spoofed.

---

### To

Indicates the email recipient.

It may include:

* CC (Carbon Copy)
* BCC (Blind Carbon Copy)

---

### Date

Shows when the email was sent.

Example format:

```
Wed, 16 Nov 2021 16:57:23
```

---

### Subject

Describes the topic of the email.

Phishing emails often use urgent or attractive subjects.

---

### Return-Path / Reply-To

Indicates where replies should be sent.

Attackers may manipulate this field so replies go to a **different address**.

---

### Message-ID

A unique identifier assigned to every email message.

---

### MIME-Version

Allows email to include attachments and multimedia content.

---

### Received

Shows the path the email traveled through multiple mail servers.

The list is ordered **from newest to oldest**.

The bottom entry usually shows the **originating mail server**.

---

### X-Spam Status

Displays the spam score assigned by spam filters.

If the score exceeds a threshold, the email may be classified as spam.

---

# 8. Accessing Email Headers

### Gmail

1. Open the email
2. Click the three dots (...)
3. Select **Download message**
4. Open the `.eml` file with a text editor

---

### Outlook

1. Open the email
2. Go to **File → Info → Properties**
3. View the **Internet Headers**

---

# 9. Email Header Analysis

When analyzing a suspicious email, analysts ask two main questions.

## Was the email sent from the correct SMTP server?

The **Received field** shows the server path.

Example:

```
Received from 101.99.94.116
```

If the email claims to come from:

```
letsdefend.io
```

but the sending IP does not belong to that domain's mail servers, the email may be **spoofed**.

Tools such as **MXToolbox** can help identify legitimate mail servers.

---

## Do the "From" and "Reply-To" fields match?

Normally, replies should go to the same address.

Legitimate example:

```
From: finance@company.com
Reply-To: finance@company.com
```

Suspicious example:

```
From: finance@company.com
Reply-To: attacker@gmail.com
```

This mismatch may indicate phishing.

---

# 10. Static Analysis

Static analysis involves **examining suspicious emails, URLs, or files without executing them**.

Analysts check:

* URLs
* domain reputation
* attachments
* email structure

Example technique used in phishing emails:

HTML links can hide the real destination.

Example:

```
Displayed link:
https://bank.com

Actual link:
http://malicious-site.com
```

Hovering over the link reveals the real URL.

---

### Domain Age

Phishing domains are often **recently registered**.

Checking domain registration information using WHOIS can reveal suspicious domains.

---

### VirusTotal Analysis

Analysts can check URLs or files using VirusTotal.

However, they should verify **when the scan was performed**.

Example:

If a domain was scanned **9 months ago**, the result may be outdated.

Attackers sometimes scan their own domains in VirusTotal before launching attacks.

---

### IP Reputation

Analysts may check SMTP IP addresses using:

* Cisco Talos
* VirusTotal
* AbuseIPDB

If the IP address is blacklisted, it may belong to a compromised server.

---

# 11. Dynamic Analysis

Dynamic analysis involves executing suspicious files or visiting links in a **controlled environment**.

This is usually done using sandbox systems.

Common sandbox tools include:

* VMRay
* JoeSandbox
* AnyRun
* Hybrid Analysis

Sandboxes allow analysts to observe:

* network connections
* file system changes
* registry modifications
* malware behavior

without risking infection.

---

### Browser Isolation

Tools like **Browserling** allow analysts to open suspicious URLs safely in remote browsers.

However, they may not allow downloading and executing files.

---

### Delayed Malware Execution

Some malware delays execution to avoid detection.

Therefore analysts must allow sufficient time for behavior to appear.

---

# 12. Additional Phishing Techniques

Attackers often abuse legitimate services.

Examples include:

### Cloud Storage Links

Malware may be distributed through:

* Google Drive
* Microsoft OneDrive

These domains are trusted and may bypass filters.

---

### Free Subdomain Services

Attackers may create phishing sites using platforms such as:

* WordPress
* Blogspot
* Wix

Example:

```
secure-login.wordpress.com
```

---

### Online Forms

Attackers may create phishing pages using services like:

* Google Forms

Since the domain belongs to Google, the link may appear legitimate.

---

# 13. SOC Phishing Investigation Checklist

When analyzing phishing emails, SOC analysts typically check:

1. Sender email address
2. SMTP sending IP
3. Email headers
4. Reply-To mismatch
5. URLs inside the email
6. Domain age
7. Attachment types
8. Domain/IP reputation
9. VirusTotal results
10. Suspicious language in the email

These indicators help determine whether the email is malicious.

---


