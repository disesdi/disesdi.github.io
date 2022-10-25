[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)


# AviationCyber Attack Case Study: Sunwing Airlines 2022

### By <a href="https://disesdi.github.io/contact.html" target="_blank" rel="noopener noreferrer">Disesdi</a> | *2022/10/22*

-------

*Sunwing Airlines & Airline Choice, April 2022: A Phishing + 3rd Party/Supply Chain Breach In The Aviation Sector*

-------


## Phishing Definition:

"*A technique for attempting to acquire sensitive data, such as bank account numbers, through a fraudulent solicitation in email or on a web site, in which the perpetrator masquerades as a legitimate business or reputable person.*"

–Source: [NIST](https://csrc.nist.gov/glossary/term/phishing)<sup>[1]</sup> 

## Supply Chain Attacks Definition:

"*A type of cyberattack that targets a trusted third-party vendor who offers services or software vital to the supply chain.*"

–Source: [Crowdstrike](https://www.crowdstrike.com/cybersecurity-101/cyberattacks/supply-chain-attacks/)<sup>[2]</sup>

## Attack Prevalence

### Phishing Attacks

Research published by the FBI’s Internet Crime Complaint Center (IC3) noted 241,342 phishing-specific complaints in 2020 alone, with adjusted losses of over $54 million.<sup>[3]</sup>


According to IBM, phishing scams were on average the second costliest type per breach, at an average cost of $4.65 million for each incident, as well as **the second most common** incident type.<sup>[4]</sup>


### Supply Chain Attacks

In 2021, 64% of organizations experienced an attack on their software supply chain, largely due to reliance on open source software.<sup>[5]</sup>


Supply chain attacks on open source software packages **increased by 650%** in 2021.<sup>[6]</sup>


“*Based on our analysis and industry data, we estimate that software supply chain attacks more than tripled in 2021, as compared to 2020, with more vulnerabilities and attacks discovered every month.*”<sup>[7]</sup> –[Argon 2021 Software Supply Chain Security Report](https://1665891.fs1.hubspotusercontent-na1.net/hubfs/1665891/Assets/Argon%20Security%20-%202021%20Software%20Supply%20Chain%20Security%20Report.pdf)

### Cyber Attacks in Aviation

"*Cyber-attacks reported to or identified by the European Air Traffic Management Computer Emergency Response Team rose by 530% between 2019 and 2020*"

"*39% of organisations experiencing cyber-attacks in 2020
assessed that these attacks had had a medium to high impact on their operations*"<sup>[8]</sup>

–Source: [Eurocontrol](https://www.eurocontrol.int/sites/default/files/2021-07/eurocontrol-think-paper-12-aviation-under-cyber-attack.pdf)

## Affected Organization: Sunwing Airlines

Sunwing Airlines is a low-cost Canadian air carrier headquartered in Toronto, Canada. Their callsign is "Sunwing". 

Sunwing Airlines was founded in 2005, and had approximately 1,500 employees as of 2015. The airline has a fleet of 27 aircraft, and offers passenger air service to Canada, the United States, Mexico, Central & South America, & the Caribbean.<sup>[9]</sup> 


## Security Incident

In April 2022, a third party software provider used by the airline for check in and boarding was hacked via a phishing scam, causing 5 days of extensive delays as the airline was forced to process passengers by hand. At least 188 flights were affected. The provider, Airline Choice, is an Illinois (USA) based company.<sup>[10][11]</sup> 


Sources:
1. https://toronto.citynews.ca/2022/04/21/sunwing-cyberattack-flight-delays-pearson/
2. https://www.shlegal.com/insights/aviation-is-facing-a-rising-wave-of-cyber-attacks-in-the-wake-of-covid


## Timeline

Sunwing Airlines Supply Chain & Phishing Attack on 3rd Party Vendor Airline Choice attack timeline begins in April 2022:

* **April 2022**: Airline Check-In & Boarding Software Provider  Airline Choice Is Compromised via phishing scam 


* **April 18**: Sunwing Airlines announces a technical issue with a provider has caused a nationwide outage; flights are delayed or canceled leaving passengers stranded


* **April 19**: Sunwing Airlines tweets that employees have begun processing flights by hand as the system is still out; thousands of passengers remain stranded in "chaos"


* **April 20**: Airline CEO Mark Williams states in an interview that systems remain down with no timeline for return to normal operations; customer data may have been breached


* **April 20**: Canadian authorities reportedly suspend some Sunwing operations to ensure the breach is resolved


* **April 22**: Sunwing operations begin to return to normal, after five days of passenger delays and canceled flights


## Vulnerabilities

### Summary:

Reliance on a 3rd party provider for a critical infrastructure function without either proper cybersecurity vetting, or redundancy/backup plans, caused passenger delays, loss of public trust, and regulatory action for the airline.

**Vulnerability #1**: *Airline relied on single vendor for all boarding & check-in services; no backups were in place in case of total system failure*

**Vulnerability #2**: *The vendor was ill prepared to resist & detect both the initial phishing attack, as well as the exploits launched against the network once the attackers gained access*

**Vulnerability #3**: *The Airline either did not have a mechanism in place to properly vet security policies of 3rd party vendors, or mechanisms were inadequate.*

**Vulnerability #4**: *The airline did not have solid communication strategies in place for dealing with media & other parties, resulting in passenger confusion & regulatory shutdown*


## Costs & Prevention

### Costs

While this particular breach is very recent and it is difficult to know the specific amounts yet, we can surmise that the loss of flights over five days as well as public trust will prove to be very costly for all parties involved.

### Prevention

* **Proper vetting** of 3rd party suppliers


* **Internal audits** of 3rd party suppliers & data sharing


* **Backup plans** for critical functions like boarding & check in


* **Incident response** & communications strategies in place 


* **Plan specifically** for 3rd party breaches

-------


## [*Contact me >>*](https://disesdi.github.io/contact.html)


-------


## References

1. “phishing - Glossary, CSRC.” n.d. NIST Computer Security Resource Center. Accessed October 20, 2022. https://csrc.nist.gov/glossary/term/phishing.


2. “What is a Supply Chain Attack?” 2021. CrowdStrike. https://www.crowdstrike.com/cybersecurity-101/cyberattacks/supply-chain-attacks/.


3. “Untitled.” n.d. Internet Crime Complaint Center(IC3). Accessed October 20, 2022. https://www.ic3.gov/Media/PDF/AnnualReport/2020_IC3Report.pdf.


4. IBM. 2021. “Cost of a Data Breach 2021 Report.” https://www.ibm.com/downloads/cas/OJDVQGRY.


5. “Revenera's 2022 Report on Software Supply Chain Compliance.” n.d. Revenera. Accessed October 20, 2022. https://info.revenera.com/SCA-RPT-OSS-License-Compliance-2022/?lead_source=PR.


6. “State of the Software Supply Chain.” n.d. Sonatype. Accessed October 20, 2022. https://www.sonatype.com/hubfs/Q3%202021-State%20of%20the%20Software%20Supply%20Chain-Report/SSSC-Report-2021_0913_PM_2.pdf?hsLang=en-us.


7. Argon. 2021. “2021 Software Supply Chain Security Report.” https://1665891.fs1.hubspotusercontent-na1.net/hubfs/1665891/Assets/Argon%20Security%20-%202021%20Software%20Supply%20Chain%20Security%20Report.pdf.


8. “Think Paper #12, EUROCONTROL EATM-CERT Services.” 2021. Eurocontrol. https://www.eurocontrol.int/sites/default/files/2021-07/eurocontrol-think-paper-12-aviation-under-cyber-attack.pdf.


9. “Sunwing Airlines.” n.d. Wikipedia. Accessed October 20, 2022. https://en.wikipedia.org/wiki/Sunwing_Airlines.


10. Ranger, Michael, and Michelle Morton. 2022. “More delays at Pearson as Sunwing works to resolve cyberattack.” CityNews Toronto. https://toronto.citynews.ca/2022/04/21/sunwing-cyberattack-flight-delays-pearson/.


11. “Aviation is facing a rising wave of cyber-attacks in the wake of COVID.” 2022. Stephenson Harwood. https://www.shlegal.com/insights/aviation-is-facing-a-rising-wave-of-cyber-attacks-in-the-wake-of-covid.

-------
-------
