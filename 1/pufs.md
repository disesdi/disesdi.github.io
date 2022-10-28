[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)


# Evaluating Robustness of Physical Unclonable Functions (PUFs) For Unmanned Aerial System Authentication With Random Forests & Gradient Boosting 

### By <a href="https://disesdi.github.io/contact.html" target="_blank" rel="noopener noreferrer">Disesdi</a> | *2022/10/23*

-------

### *Code available [here >>]()*

-------

## Introduction

This project explores machine learning attacks on Physical Unclonable Functions (PUFs), which have been proposed as an authentication method for resource-constrained and security-vulnerable applications such as Unmanned Aircraft Systems (UAS), and Internet of Things (IOT) devices.


## Background

###  UAS Prevalence & Security Vectors

Unmanned Aircraft Systems are becoming an increasingly mainstream–and vital–part of modern life. The US Cybersecurity & Infrastructure Security Agency (CISA) names UAS/drones as "[critical infrastructure](https://www.cisa.gov/unmanned-aircraft-systems)", citing use cases as diverse as firefighting, to the delivery of critical medical supplies.<sup>[1]</sup>

Drone use has skyrocketed, particularly among the general public. According to [the FAA  as of 2022](https://www.faa.gov/uas), of the over 867,000 drones currently registered, more than half a million (535,461) are registered as recreational.<sup>[2]</sup>

With widespread use, security concerns around malicious drone activity have risen to the fore.

According to CISA,<sup>[1]</sup> malicious UAS activity may include:

* *Weaponized or Smuggling Payloads – Depending on power and payload size, UAS may be capable of transporting contraband, chemical, or other explosive/weaponized payloads.*


* *Prohibited Surveillance and Reconnaissance – UAS are capable of silently monitoring a large area from the sky for nefarious purposes.*


* *Intellectual Property Theft – UAS can be used to perform cyber crimes involving theft of trade secrets, technologies, or sensitive information.*


* *Intentional Disruption or Harassment – UAS may be used to disrupt or invade the privacy of other individuals.*<sup>[1]</sup>

Given the potential for serious misuse of the technology, securely identifying and authenticating UAS is a critical challenge. However, UAS-specific security constraints, as well as the proliferation of industry-wide security challenges already existent in the underlying technologies, are complicating factors that must be weighed in any solution.

In addition to their potential for malicious misuse, UAS have a number of well documented cyber attack vectors, with various proposals for mitigation in the literature.<sup>[3]</sup>  Cybersecurity risks are prevalent in UAS to such an extent that CISA also published a [Cybersecurity Best Practices For Operating Commercial UAS](https://www.cisa.gov/sites/default/files/publications/CISA%20Cybersecurity%20Best%20Practices%20for%20Operating%20Commerical%20UAS%20%28508%29.pdf), with a number of recommendations for operators.<sup>[4]</sup>


### Resource Constraints & Security Needs

As both their use and susceptibility to attacks increase, IOT and UAS devices share a need for system-wide security improvements to reduce the attack surface. 

UAS and IOT devices also share a common characteristic of being resource-constrained;<sup>[5]</sup> that is, these devices often have physical size and, in aerospace applications in particular, weight considerations. 

These considerations co-exist and interact with the need for optimizing computational performance on already small devices. 

Due to the combination of security needs and resource constraints, authentication of these systems is of particular interest.

Specifically, their constraints, combined with the ways in which these systems operate in the wild, make familiar methods of authentication increasingly less practical for application within UAS & IOT machines.

### Public Key Infrastructure (PKI)

Public Key Infrastructure (PKI) is a widely used encryption system, where each user has two sets of keys: public keys, and private keys. One key is used for encryption; the other key is used for decryption.

While the public keys can be shared, the private keys must remain a secret in order for the system to remain uncompromised.

Because these keys must be kept secret, and because they must always be readily accessible, they may be physically hard-coded onto machines using any of several methods.

### Antifusing

Antifuse technology is a widely-used process for programming integrated circuits (ICs) that has been proposed for key storage.<sup>[6]</sup> Antifuse can be thought of as the opposite of fusing--rather than breaking connections, an antifuse process closes the circuit & creates a permanent conductive path between transistors. 

The antifuse process works by applying voltage to a layer of silicon joining two metal layers. The silicon is non-conductive until the voltage is applied, at which point it becomes a conductive polysilicon, forming a connection between the metal layers.

Two drawbacks to this approach are evident. First, the need to hard-code keys adds an additional fabrication step to the device manufacturing process. This comes with its own additional supply chain and security considerations.

Second, once keys are hard-coded into a device, they cannot be changed. This means that should the keys become compromised, the entire device itself becomes compromised. 

It is also important to note that UAS and IOT devices are often resource-constrained, while cryptography is always a resource-intensive endeavor.

### Hardware Solutions & Attacks

Hardware-based security proposals similarly carry the disadvantage of being highly susceptible to Man-In-The-Middle (MITM) & cloning attacks,<sup>[5]</sup> where attackers can steal and copy authentication functions to mimic the real agent/device.

These potential attack vectors carry significant implications for aerospace applications such as UAS,<sup>[8]</sup> where physical and computing resource constraints intensify, while need for security and reliability also increases.

### Physical Unclonable Functions (PUFs)

Physical Unclonable Functions (PUFs), based on the unique electronic signatures of the agent’s hardware, have been proposed as a solution for authentication in resource-constrained UAS and IOT environments.<sup>[9][10]</sup> PUF authentication works via a set of challenge-and-response pairs (CRPs) exchanged between the authenticator and the system being authenticated.

Two significant problems exist with regard to PUF authentication methods. First, strong PUF authentication requires a very large CRP space.<sup>[10]</sup> This conflicts with resource constraints in UAS  and other aerospace devices. 

Second, PUF CRPs are subject to machine learning attacks.<sup>[11]</sup> Given a dataset of CRPs, machine learning models have been demonstrated to be capable of guessing pair components with high efficacy.  

There have been a number of proposals for mitigations to PUF security vulnerabilities, including blockchain-based fixes,<sup>[12][13][14]</sup> as well as machine learning-enhanced systems,<sup>[15]</sup> and ring oscillator & other field-programmable gate array (FPGA)-implemented solutions.<sup>[16][17]</sup> The degree to which they can/will be practically implemented in UAS devices remains to be seen.

## Methods and Results

PUF authentication is based on a set of challenge and response sequences; because of their implicit randomness these may not be exact matches to CRP data in the enrollement database. Successful authentication typically requires error rates between challenges and responses below 10%.<sup>[18]</sup>  Helper functions may be deployed for certain PUFs to correct error rates and improve authentication. 

The presence of this gradient opens a vector for exploitation by machine learning models.<sup>[19]</sup> 

### Model Training & Scoring

The problem was modeled as binary classification of correct & incorrect CRP elements. Models were trained in two cohorts, with the two top performers from Round 1 advancing to Round 2. 

Four classifiers were initially trained & made predictions without parameter tuning: Gaussian Naive Bayes, Support Vector Machine, Random Forests, and XGBoost. A second round of training for top performers Random Forests & XGBoosts involved tuning parameters to increase estimators & depth, respectively. 

***Cohort 1:*** 
> 
> * Gaussian Naive Bayes
>
> * Support Vector Machine
>
> * XGBoost

***Cohort 2:***
>
> * Random Forest *(estimators increased to 99)*
>
> * XGBoost *(max tree depth increased to 11)*

Trained on a publicly-available CRP dataset containing approximately 12,000 rows, models were immediately able to guess accurately over 50% of the time, using out-of-the-box classifiers from the `sklearn` python library.

The use of extreme gradient boosting, using the `XGBClassifier` algorithm from the `xgboost` library, raised initial scores models to over 56%.

Raising the number of estimators in Random Forest and increasing tree depth for XGBoost improved single model scores for each to more than 57%, using out-of-the-box models and minimal tuning. Results are summarized in the table below.

|          Model         | Parameter Optimization   | Score  |
|:----------------------:|--------------------------|--------|
| Gaussian Naive Bayes   | None                     | 53.90% |
| Support Vector Machine | None                     | 56.03% |
| XGBoost                | None                     | 56.00% |
| Random Forests         | None                     | 56.67% |
| Random Forests 2       | Number of Estimators: 99 | 57.07% |
| XGBoost 2              | Max Tree Depth: 11       | 57.40% |



Given the ease with which scores can be increased with rudimentary parameter tuning, it is easy to imagine the vulnerability of PUF authentication to modeling attacks.

These results are in line with current academic literature,<sup>[20]</sup> and were acheived using a Jupyter Notebook kernel running inside a Linux virtual machine hosted on a Chromebook laptop. Increasingly large datasets and computationally intensive methods have increasingly accurate results. 

*Code available [here >>]()*


-------

### [*Contact me >>*](https://disesdi.github.io/contact.html)

-------
-------

## References


1. “UAS - Critical Infrastructure.” n.d. CISA. Accessed October 18, 2022. https://www.cisa.gov/unmanned-aircraft-systems.


2. “Unmanned Aircraft Systems (UAS).” n.d. Federal Aviation Administration. Accessed October 18, 2022. https://www.faa.gov/uas.


3. Bora Ly & Romny Ly (2021) Cybersecurity in unmanned aerial vehicles (UAVs), Journal of Cyber Security Technology, 5:2, 120-137, DOI: 10.1080/23742917.2020.1846307


4. “Cybersecurity Best Practices for Operating Commercial Unmanned Aircraft Systems (UASs).” n.d. CISA. Accessed October 18, 2022. https://www.cisa.gov/sites/default/files/publications/
CISA%20Cybersecurity%20Best%20Practices%20for%20
Operating%20Commerical%20UAS%20%28508%29.pdf


5. Majid, Mamoona, Shaista Habib, Abdul Rehman Javed, Muhammad Rizwan, Gautam Srivastava, Thippa Reddy Gadekallu and Chun-Wei Lin. “Applications of Wireless Sensor Networks and Internet of Things Frameworks in the Industry Revolution 4.0: A Systematic Literature Review.” Sensors (Basel, Switzerland) 22 (2022): n. pag.


6. S. -Y. Chou, Y. -S. Chen, J. -H. Chang, Y. -D. Chih and T. -Y. J. Chang, "11.3 A 10nm 32Kb low-voltage logic-compatible anti-fuse one-time-programmable memory with anti-tampering sensing scheme," 2017 IEEE International Solid-State Circuits Conference (ISSCC), 2017, pp. 200-201, doi: 10.1109/ISSCC.2017.7870330.


7. Alkatheiri, Mohammed Saeed, Sajid Saleem, Mohammed A. Alqarni, Ahmad O. Aseeri, Sajjad Hussain Chauhdary and Yu Zhuang. “A Lightweight Authentication Scheme for a Network of Unmanned Aerial Vehicles (UAVs) by Using Physical Unclonable Functions.” Electronics (2022): n. pag.


8. Tsao, Kai-Yun, Thomas Girdler and Vassilios G. Vassilakis. “A survey of cyber security threats and solutions for UAV communications and flying ad-hoc networks.” Ad Hoc Networks 133 (2022): 102894.


9. Alladi, Tejasvi, Vishnu Venkatesh, Vinay Chamola and Nitin Chaturvedi. “Drone-MAP: A Novel Authentication Scheme for Drone-Assisted 5G Networks.” IEEE INFOCOM 2021 - IEEE Conference on Computer Communications Workshops (INFOCOM WKSHPS) (2021): 1-6.


10. Shamsoshoara, Alireza, Ashwija Reddy Korenda, Fatemeh Afghah and Sherali Zeadally. “A survey on physical unclonable function (PUF)-based security solutions for Internet of Things.” Comput. Networks 183 (2020): 107593.


11. Laguduva, V.R., Katkoori, S. & Karam, R. Machine Learning Attacks and Countermeasures for PUF-Based IoT Edge Node Security. SN COMPUT. SCI. 1, 282 (2020). https://doi.org/10.1007/s42979-020-00303-y


12. Patil, Akash Suresh, Rafik Hamza, Hongyang Yan, Alzubair Hassan and Jin Li. “Blockchain-PUF-Based Secure Authentication Protocol for Internet of Things.” ICA3PP (2019).


13. Patil, Akash Suresh, Rafik Hamza, Alzubair Hassan, Nan Jiang, Hongyang Yan and Jin Li. “Efficient privacy-preserving authentication protocol using PUFs with blockchain smart contracts.” Comput. Secur. 97 (2020): 101958.


14. Wang, Weizheng, Qiu Chen, Zhimeng Yin, Gautam Srivastava, Thippa Reddy Gadekallu, Fawaz Jaber Alsolami and Chunhua Su. “Blockchain and PUF-Based Lightweight Authentication Protocol for Wireless Medical Sensor Networks.” IEEE Internet of Things Journal 9 (2022): 8883-8891.


15. E. Dubrova, O. Näslund, B. Degen, A. Gawell and Y. Yu, "CRC-PUF: A Machine Learning Attack Resistant Lightweight PUF Construction," 2019 IEEE European Symposium on Security and Privacy Workshops (EuroS&PW), 2019, pp. 264-271, doi: 10.1109/EuroSPW.2019.00036.


16. Pundir, Nitin, Noor Ahmad Hazari, Fathi H. Amsaad and Mohammed Y. Niamat. “A novel hybrid delay based physical unclonable function immune to machine learning attacks.” 2017 IEEE National Aerospace and Electronics Conference (NAECON) (2017): 84-87.


17. Pramudita, Resa, Surya Ramadhan, Farkhad Ihsan Hariadi and Adang Suwandi Ahmad. “Implementation Ring Oscillator Physical Unclonable Function (PUF) in FPGA.” 2018 International Symposium on Electronics and Smart Devices (ISESD) (2018): 1-5.


18. Cambou, Bertrand Francis, Christopher Philabaum, Duane Booher and Donald Telesca. “Response-Based Cryptographic Methods with Ternary Physical Unclonable Functions.” Lecture Notes in Networks and Systems (2019): n. pag.


19. Babaei, Armin and Gregor Schiele. “Physical Unclonable Functions in the Internet of Things: State of the Art and Open Challenges.” Sensors (Basel, Switzerland) 19 (2019): n. pag.


20. Ebrahimabadi, Mohammad Haghir, Mohamed F. Younis and Naghmeh Karimi. “A PUF-Based Modeling-Attack Resilient Authentication Protocol for IoT Devices.” IEEE Internet of Things Journal 9 (2022): 3684-3703.

-------

[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)
