

# MITRE ATT&CK Framework – Write-Up

## 1. Introduction

The MITRE ATT&CK framework is one of the most important knowledge bases used in cybersecurity today. It provides a **structured database of attacker behaviors** based on real-world cyber attacks.

ATT&CK stands for:

```
Adversarial Tactics, Techniques, and Common Knowledge
```

It was developed by the **MITRE Corporation** to help security teams understand:

* how attackers operate
* what techniques they use
* how to detect and defend against them

Unlike theoretical models, MITRE ATT&CK is based on **real attack campaigns observed in the wild**.

---

# 2. Purpose of MITRE ATT&CK

MITRE ATT&CK helps organizations in several areas:

### 1. Threat intelligence

Security teams can understand **how known attackers operate**.

Example:
APT groups like
Lazarus Group
or
OilRig
have documented techniques.

---

### 2. Detection

SOC analysts use ATT&CK to:

* detect suspicious behavior
* map alerts to attacker techniques

Example:

```
cmd.exe /c systeminfo
```

This could indicate:

```
T1082 – System Information Discovery
```

---

### 3. Security assessment

Penetration testers use ATT&CK to simulate attacks.

Red teams may reproduce real techniques such as:

* credential dumping
* privilege escalation
* lateral movement

---

### 4. Security gap analysis

Organizations use ATT&CK to see:

```
Which techniques can we detect?
Which techniques are invisible to us?
```

---

# 3. Core Components of MITRE ATT&CK

The framework is built around **three main concepts**.

---

# 3.1 Tactics

Tactics represent the **goal of the attacker** during a stage of the attack.

Examples include:

| Tactic               | Description                         |
| -------------------- | ----------------------------------- |
| Initial Access       | How attackers enter the system      |
| Execution            | Running malicious code              |
| Persistence          | Maintaining access                  |
| Privilege Escalation | Gaining higher privileges           |
| Defense Evasion      | Avoiding detection                  |
| Discovery            | Gathering system information        |
| Lateral Movement     | Moving inside the network           |
| Command & Control    | Communicating with attacker servers |
| Exfiltration         | Stealing data                       |

These tactics are organized in the **MITRE ATT&CK Matrix**.

---

# 3.2 Techniques

Techniques describe **how attackers achieve a tactic**.

Example:

Tactic:

```
Discovery
```

Technique:

```
T1082 – System Information Discovery
```

Attackers may use commands like:

```
systeminfo
hostname
uname -a
```

Each technique has a unique ID.

Example:

```
T1059 – Command and Scripting Interpreter
T1027 – Obfuscated Files or Information
```

---

# 3.3 Sub-techniques

Some techniques are broken into **more specific methods**.

Example:

```
T1059 – Command Interpreter
```

Sub-techniques:

```
T1059.001 – PowerShell
T1059.003 – Windows Command Shell
T1059.006 – Python
```

This helps analysts be more precise.

---

# 4. MITRE ATT&CK Matrix

The ATT&CK Matrix is a **visual table of tactics and techniques**.

It shows:

```
Attack stages → Techniques used by attackers
```

Example simplified flow:

```
Initial Access
↓
Execution
↓
Persistence
↓
Privilege Escalation
↓
Discovery
↓
Lateral Movement
↓
Command & Control
↓
Exfiltration
```

This helps analysts understand **the full attack chain**.

---

# 5. Platforms in MITRE ATT&CK

MITRE categorizes techniques by **platforms**.

Platforms include:

* Windows
* Linux
* macOS
* Android
* iOS
* Cloud (Azure / Office365)
* Containers
* Network devices

Example:

Some malware works only on **Windows**, while others may target **Linux servers**.

---

# 6. Threat Groups

MITRE ATT&CK also tracks **Advanced Persistent Threat (APT) groups**.

Examples include:

* Lazarus Group
* OilRig
* APT33

For each group, MITRE documents:

* techniques used
* tools used
* attack campaigns

This helps defenders understand **real attacker behavior**.

---

# 7. Software and Tools

MITRE ATT&CK also lists **malware and tools used by attackers**.

Examples:

| Tool          | Purpose             |
| ------------- | ------------------- |
| Mimikatz      | Credential dumping  |
| Empire        | Post-exploitation   |
| Cobalt Strike | Command and control |
| systeminfo    | System discovery    |

Each tool is mapped to specific **ATT&CK techniques**.

---

# 8. How SOC Analysts Use MITRE ATT&CK

In a Security Operations Center (SOC), analysts often map alerts to ATT&CK techniques.

Example alert:

```
Suspicious PowerShell command executed
```

Mapped technique:

```
T1059.001 – PowerShell
```

This helps analysts understand:

* attacker behavior
* attack stage
* possible next steps

---

# 9. Importance of MITRE ATT&CK

MITRE ATT&CK has become a **global standard in cybersecurity**.

It is widely used by:

* SOC teams
* threat intelligence analysts
* red teams
* penetration testers
* security vendors

Many security tools (SIEM, EDR, XDR) map alerts directly to **ATT&CK techniques**.

---

# 10. Conclusion

MITRE ATT&CK is a powerful framework that helps cybersecurity professionals understand attacker behavior. By organizing tactics, techniques, and real-world threat intelligence, it enables organizations to detect, analyze, and defend against cyber threats more effectively.

For security analysts and penetration testers, understanding MITRE ATT&CK is essential because it provides a **common language for describing cyber attacks** and improving defensive strategies.

---

