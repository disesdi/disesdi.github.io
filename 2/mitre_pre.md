[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)



# Intro To MITRE PRE-ATT&CK Part 1: Tactics, Techniques, & Reconnaissance 

### By <a href="https://disesdi.github.io/contact.html" target="_blank" rel="noopener noreferrer">Disesdi</a> | *2022/10/17*

-------

*Breaking Pre-ATT&CK down, piece-by-piece*

-------


## Introduction

In this post, I'll be talking about MITRE ATT&CK, a popular cybersecurity framework. I'll give a brief intro to terms like *tactics* & *techniques,* and how they're used in the framework. We'll also go over the initial stages of a cyberattack as modeled in the Pre-ATT&CK matrix. 

Finally, we'll focus on the *Reconnaissance* tactical phase as part of an overall attack model.

Let's go!


## What Is MITRE ATT&CK?

MITRE ATT&CK is a framework for understanding how malicious intruders attack network systems. It's a way of modeling the various processes and/or events that make up a cyberattack, in an effort to help defenders prepare & secure their systems.

The ATT&CK framework has been widely adopted. Disciplines that integrate ATT&CK principles include intrusion detection, threat hunting, security engineering, threat intelligence, red teaming, and risk management.<sup>[1]</sup>

You can read the paper detailing ATT&CK’s creation & development [here](https://www.mitre.org/news-insights/publication/mitre-attck-design-and-philosophy).

## What Does *ATT&CK* Stand For?

The *ATT&CK* in MITRE ATT&CK stands for *Adversarial Tactics, Techniques, & Common Knowledge*.

There are 14 goals, or *tactics*, in MITRE ATT&CK.<sup>[2]</sup> 


***Fourteen Tactics Of The MITRE ATT&CK Matrix:***
>
*1. Reconnaissance*

*2. Resource Development*

*3. Initial Access*

*4. Execution*

*5. Persistence*

*6. Privilege Escalation*

*7. Defense Evasion*

*8. Credential Access*

*9. Discovery*

*10. Lateral Movement*

*11. Command & Control*

*12. Collection*

*13. Exfiltration*

*14. Impact*



Today we’re going to focus on what comes before that: the first stages, called PRE-ATT&CK.

Speaking of *tactics*, let’s define some terms before we dive in.

## What Are *Tactics* In The ATT&CK Framework?

In MITRE ATT&CK, *Tactics* represent the attacker’s goal during a particular phase of an attack.<sup>[3]</sup> Tactics are the reason to employ a particular technique–they are the end result an attacker is hoping for when they are applying any procedure in an attack.

> *”Tactics represent the "why" of an ATT&CK technique or sub-technique. **It is the adversary's tactical goal: the reason for performing an action.**” [MITRE](https://attack.mitre.org/tactics/enterprise/) <sup>[3]</sup>*

There are fourteen Enterprise tactics. You can find the full list [here](https://attack.mitre.org/tactics/enterprise/).

## What Are *Techniques* In The ATT&CK Framework?

If tactics represent the goals of an attack, *techniques* represent the methods for achieving those goals.<sup>[4]</sup>

> *”Techniques represent 'how' an adversary achieves a tactical goal by performing an action. For example, an adversary may dump credentials to achieve credential access.” [MITRE](https://attack.mitre.org/techniques/enterprise/).<sup>[4]</sup>* 

The techniques are broad categories, with sub-techniques increasing in specificity, and finally specific *procedures* for implementation. 

For example, the Reconnaissance tactical phase can involve the technique of[active scanning](https://attack.mitre.org/techniques/T1595/)<sup>[5]</sup>, which itself has three *sub-techniques:* [scanning IP blocks](https://attack.mitre.org/techniques/T1595/001/),<sup>[6]</sup> [vulnerability scanning](https://attack.mitre.org/techniques/T1595/002/),<sup>[7]</sup> and [wordlist scans](https://attack.mitre.org/techniques/T1595/003/).<sup>[8]</sup> 

There are 191 techniques identified in the Enterprise ATT&CK framework, with 385 supporting sub-techniques. You can read the full list of Enterprise Techniques [here](https://attack.mitre.org/techniques/enterprise/).

## Pre-ATT&CK Tactics: *Reconnaissance* and *Resource Development*

There are two *tactics* in the Pre-ATT&CK matrix: *Reconnaissance* and *Resource Development*. 

In this post I’ll be focusing on **Reconnaissance**.

### What Is *Reconnaissance* In MITRE Pre-ATT&CK?

*Reconnaissance* focuses primarily on information collecting: gathering intelligence on the target using a variety of techniques.<sup>[9]</sup>

These techniques include performing network scans, gathering information about the hardware, software etc that a target relies on; gathering information about victims such as names, email addresses, and other personal information; stealing credentials to gain unauthorized access; and more.


> In the Reconnaissance phase *“the adversary is trying to gather information they can use to plan future operations.” [MITRE](https://attack.mitre.org/tactics/TA0043/) <sup>[9]</sup>*


You can read the full list of Reconnaissance techniques in the ATT&CK framework [here](https://attack.mitre.org/tactics/TA0043/).

Here’s the longer definition of the Reconnaissance tactical phase:

*”Reconnaissance consists of techniques that involve adversaries actively or passively gathering information that can be used to support targeting. Such information may include details of the victim organization, infrastructure, or staff/personnel. This information can be leveraged by the adversary to aid in other phases of the adversary lifecycle, such as using gathered information to plan and execute Initial Access, to scope and prioritize post-compromise objectives, or to drive and lead further Reconnaissance efforts.” 
[MITRE](https://attack.mitre.org/tactics/TA0043/) <sup>[9]</sup>*

The MITRE PRE-ATT&CK matrix maps to the first two stages of the cyberattack life cycle, also called [The Cyber Kill Chain](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html):<sup>[10]</sup> Reconnaissance and Weaponization. This period of the attack lifecycle is especially critical, because the attacker is passively–rather than actively–engaged with the target in ways that may not be detectable.<sup>[11]</sup>

The steps in the Pre-ATT&CK phase can pay off big for attackers. The US [Cybersecurity & Infrastructure Security Agency](https://www.cisa.gov/)<sup>[12]</sup> maintains a [public list of risks & vulnerabilities mapped to the ATT&CK framework](https://www.cisa.gov/sites/default/files/publications/FY20_RVAs_Mapped_to_the_MITRE_ATTCK_Framework_508_corrected.pdf);<sup>[13]</sup> check it out to see some of the attack vectors and how they relate to later stages of the attack lifecycle.

The Pre-ATT&CK Matrix helps the people defending systems to understand how attackers find & choose their entry points, before the actual attack occurs.<sup>[14]</sup>

## Conclusion

In this post, we’ve introduced the MITRE ATT&CK framework, defined *tactics* and *techniques* within the framework, looked at how the Pre-ATT&CK Matrix relates to the overall system, unpacked the *Reconnaissance* phase & why it’s so critical for defenders, and [listed resources](#references) for further study.

In Part 2, we’ll take a look at *Resource Development* in Pre-ATT&CK.

Thanks for reading!

-------


## [*Contact me >>*](https://disesdi.github.io/contact.html)


-------


## References


1. “MITRE ATT&CK: Design and Philosophy.” 2020. MITRE. Accessed October 17, 2022. https://www.mitre.org/news-insights/publication/mitre-attck-design-and-philosophy.


2. “Matrix - Enterprise.” n.d. MITRE ATT&CK®. Accessed October 17, 2022. https://attack.mitre.org/matrices/enterprise/.


3. “Tactics - Enterprise.” n.d. MITRE ATT&CK®. Accessed October 17, 2022. https://attack.mitre.org/tactics/enterprise/.


4. “Techniques - Enterprise.” n.d. MITRE ATT&CK®. Accessed October 17, 2022. https://attack.mitre.org/techniques/enterprise/.


5. “Active Scanning, Technique T1595 - Enterprise.” 2020. MITRE ATT&CK®. Accessed October 17, 2022. https://attack.mitre.org/techniques/T1595/.


6. “Active Scanning: Scanning IP Blocks, Sub-technique T1595.001 - Enterprise.” 2020. MITRE ATT&CK®. Accessed October 17, 2022. https://attack.mitre.org/techniques/T1595/001/.


7. “Active Scanning: Vulnerability Scanning, Sub-technique T1595.002 - Enterprise.” 2020. MITRE ATT&CK®. Accessed October 17, 2022. https://attack.mitre.org/techniques/T1595/002/.


8. “Active Scanning: Wordlist Scanning, Sub-technique T1595.003 - Enterprise.” 2022. MITRE ATT&CK®. Accessed October 17, 2022. https://attack.mitre.org/techniques/T1595/003/.


9. “Reconnaissance, Tactic TA0043 - Enterprise.” 2020. MITRE ATT&CK®. Accessed October 17, 2022. https://attack.mitre.org/tactics/TA0043/


10. “Cyber Kill Chain®.” n.d. Lockheed Martin. Accessed October 17, 2022. https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html.


11. Poston, Howard. 2020. “MITRE ATT&CK® Framework Matrices: An Overview \| Infosec Resources.” Infosec Resources. Accessed October 17, 2022. https://resources.infosecinstitute.com/topic/mitre-attck-framework-matrices-an-overview/.


12. CISA: Homepage. Accessed October 17, 2022. https://www.cisa.gov/.


13. “RVAs Mapped to the MITRE ATT&CK Framework.” n.d. CISA. Accessed October 17, 2022. https://www.cisa.gov/sites/default/files/publications/FY20_RVAs_Mapped_to_the_MITRE_ATTCK_Framework_508_corrected.pdf.


14. “What is MITRE Att&ck?” n.d. L7 Defense. Accessed October 17, 2022. https://www.l7defense.com/cyber-security/what-is-mitre-attack-matrix-and-evaluation-spreadsheet/.

-------

[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)

