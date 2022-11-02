[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)


# Thinking About AviationCyber Papers: Assessing Aviation Cybersecurity, Part 1

### By <a href="https://disesdi.github.io/contact.html" target="_blank" rel="noopener noreferrer">Disesdi</a> | *2022/10/29*

-------

*How secure is AviationCyber? And how do we know?*

-------


## Introduction


In this post, I'll be taking a look at a [recent paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9579414) from the world of aviation cybersecurity.

We'll take a look at one view of the state of AviationCyber assessments, as well as a proposed solution. 

Next we'll do a deeper dive into the system proposed in the paper, & see how the paper's authors feel various aviation tech stacks up in terms of cybersecurity.

Let's go!


## Who Is Taking Responsibility, And How? 

There's a socio-psychological phenomenon called *[diffusion of responsibility](https://dictionary.apa.org/diffusion-of-responsibility)*,<sup>[1]</sup> describing how people can sometimes be less inclined to take responsibility for their actions (or inaction) in scenarios when others are present. 


They may assume that someone else is taking charge in one way or another, whether that’s the case or not. 


The American Psychological Association defines *diffusion of responsibility* as ”*the diminished sense of responsibility often experienced by individuals in groups and social collectives.*”<sup>[1]</sup>


When dealing with large, systemic issues there is a very human tendency to assume someone else is taking care of the situation–after all, challenges this big can feel impossible to tackle all on our own.


Sometimes the scope & technical nature of a problem can make it tempting to assume that big brains somewhere else have it handled.


But this might not be the case.


Big problems sometimes have to be broken down and tackled one piece at a time. And as daunting as it might seem on the surface, aviation cybersecurity is no exception.


## What Is The Status Quo?


A foundational question to ask at the beginning of any project is, “where are we now?” We need a way to measure the state of the system that we’re about to work with, so we can understand both where we are starting from, and what success looks like.


In other words, the ability to make assessments is key. Having a means to assess what we know, and what we don’t, is critical to mission safety in any field. Cybersecurity is no different.


## AviationCyber Assessments–Do They Exist?


So it follows that for large and important systems like aviation, systematized cybersecurity assessments would be in place. We might feel justified in thinking the “big brains” somewhere else have it handled.


However, while it might be tempting to assume there is some overarching measurement of how “secure” technologies used in aviation are, the literature indicates that might not be the reality.


Knowing our potential risks, mitigations and areas of cyber resiliency–or lack thereof–is a key first step to improving security overall. 


We can’t defend an attack surface we can’t define.


That’s what interested me about [this paper from October 2021](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9579414).<sup>[2]</sup> 


The authors point out that although there have been a number of diverse pieces surveying wide topics in the AvSec field, there haven’t been any proposals for systematized aviation cybersecurity risk assessment. 


That’s in part because the aviation technologies involved are very different, in some cases involve multiple uses, interact with other safety/redundant systems in various ways, and may have very diverse impacts–all depending on the method of attack.


![avcyber_assmts_1_image_1](https://user-images.githubusercontent.com/110150470/199145879-5d501cee-8cb5-4ddf-938e-82c0ee861d58.png)
*Image: Table of other AvSec works referenced in the paper, along with subjects covered. [Source.](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9579414)<sup>[2]</sup>*


The paper also points out some key factors driving the adoption of digital and connected technologies in aviation. 


## Key Factor: Growth In The Sector == More Connected Tech


One inescapable factor is the modern increase in air traffic and the need to reduce air crew & air traffic control (ATC) workloads, all while maintaining safety in increasingly crowded skies.


The argument is that growth in the aviation sector leads to 3 critical conditions:


> 1) increased workloads for ATC (& the need to reduce workloads by switching to data link communication vs old analog systems).
>
> 2) the need to reduce air traffic separation as skies become more crowded, which requires increasingly precise positional & navigational aids.
>
> 3) the need for fast, effective communication & transparent information sharing to mitigate threats & other safety concerns.


In short, the more air travel increases, the greater the need for adoption of digital/connected technologies–each of which carry new cyberattack potential–which in turn increases the need for attention to cybersecurity.


## Ranking Risk Areas


After proposing their own framework, the paper’s authors identify what they consider to be the top cybersecurity risks in aviation (according to their methodology). 


They are: 


> “*very-high frequency voice communication, satellite-based navigation, and automatic dependent surveillance-broadcast, respectively...*" 


Those with the **lowest** (assessed) risk levels are: 


> "*controller-pilot data link communication, ground-based radio navigation aids, and secondary surveillance radar, respectively...*” <sup>[2]</sup>


### A Deeper Look: Vulnerabilities & Mitigations 


Let’s break this down. The authors list very high frequency (VHF) voice communications, satellite navigation, and automatic dependent surveillance-broadcast (ADS-B) as top security concerns. 


And the literature backs up the potential for numerous vulnerabilities on these platforms: threats to [ADS-B](https://ieeexplore.ieee.org/document/9133434),<sup>[3]</sup> [satellite navigation systems](https://ieeexplore.ieee.org/ielx7/9739/9031610/08882350.pdf),<sup>[4]</sup> and [VHF](https://ieeexplore.ieee.org/document/8171270)<sup>[5][6]</sup> are very well documented.


This isn’t meant to be an exhaustive list–just to give an idea of the scope of interest around these platforms in terms of cybersecurity.


It’s also worth mentioning that there are proposals for solutions to these issues–see [here](https://www.researchsquare.com/article/rs-19635/v1),<sup>[7]</sup> [here](https://www.semanticscholar.org/paper/Detecting-ADS-B-Spoofing-Attacks-Using-Deep-Neural-Ying-Mazer/d52e9b297888544412668baa3d85163278cf0aba),<sup>[8]</sup> and [here](https://ieeexplore.ieee.org/document/8542653)<sup>[9]</sup> as a few examples for ADS-B alone. 


But whether, when and/or how any of these will be adopted in the aviation community remains to be seen.


So VHF, GNSS and ADS-B are (potentially) vulnerable, *and* there are also potential mitigations. 


These are specific technologies in the aviation sector–but what about a general overview? What about assessing the cybersecurity of other aviation technologies?


### How Does The Framework Apply To Other Areas Of Aviation Cybersecurity?


Before we can apply the proposed system to assessing the cybersecurity of real-world aviation technologies, we need to talk about the rating system itself.


The paper follows a [security assessment methodology](https://store.icao.int/en/aviation-security-manual-doc-8973)<sup>[10]</sup> defined by the International Civil Aviation Organization ([ICAO](https://www.icao.int/Pages/default.aspx)),<sup>[11]</sup> which makes sense as a baseline metric for aviation cybersecurity. 


Basically, it involves taking the potential impact of a hypothetical incident, and multiplying that by a risk factor that represents how likely the incident is to occur. 


For example, say a certain type of attack would be absolutely devastating–potentially leading to loss of property, reputation, or worse, loss of life. 


However, pulling it off requires highly specialized skills or training, difficult-to-gain access, and/or maybe some expensive equipment. 


How much should an organization invest in resources to mitigate the possibility of a devastating–but unlikely–attack?


What if the attack doesn’t require special skills or equipment? In this case, more resources might be diverted to this area, because the attack is both feasible and potentially harmful on a large scale.


Curious to see how various aviation systems rank in terms of cyber vulnerability? So was I! For some key results of the paper’s assessment, as well as a deep dive into the methodology itself, check out Part 2. 


![avcyber_assmts_1_image_2](https://user-images.githubusercontent.com/110150470/199144715-fbdcd044-e5df-4b1b-aed7-214ee950d6b1.png)
*Image: A sneak peak at the paper’s Cybersecurity Risk Matrix, which I talk about in Part 2 of this series. [Source here.](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9579414)*


How do you think aviation systems stack up, security-wise? Let me know! 

-------


## [*Contact me >>*](https://disesdi.github.io/contact.html)


-------


## References


1. “Diffusion Of Responsibility.” n.d. APA Dictionary of Psychology. Accessed October 29, 2022. https://dictionary.apa.org/diffusion-of-responsibility.


2. Elmarady, Ahmed Abdelwahab and Kamel Hussein Rahouma. “Studying Cybersecurity in Civil Aviation, Including Developing and Applying Aviation Cybersecurity Risk Assessment.” IEEE Access 9 (2021): 143997-144016.


3. Z. Wu, T. Shang and A. Guo, "Security Issues in Automatic Dependent Surveillance - Broadcast (ADS-B): A Survey," in IEEE Access, vol. 8, pp. 122147-122167, 2020, doi: 10.1109/ACCESS.2020.3007182.



4. Morales-Ferre, Ruben, Philipp Richter, Emanuela Falletti, Alberto de la Fuente and Elena Simona Lohan. “A Survey on Coping With Intentional Interference in Satellite Navigation for Manned and Unmanned Aircraft.” IEEE Communications Surveys & Tutorials 22 (2020): 249-291.


5. M. Strohmeier, I. Martinovic, and V. Lenders, Eds., The Security of Critical Infrastructures: Risk, Resilience and Defense. Oxford, U.K.: Springer, ch. Securing the Air-Ground Link in Aviation, 2020, pp. 131–154.


6.  O. Osechas, M. Mostafa, T. Graupl, and M. Meurer, ‘‘Addressing vulnerabilities of the CNS infrastructure to targeted radio interference,’’ IEEE Aerosp. Electron. Syst. Mag., vol. 32, no. 11, pp. 34–42, Nov. 2017.


7. Wang, Jing, Yunkai Zou and Jianli Ding. “ADS-B spoofing attack detection method based on LSTM.” EURASIP Journal on Wireless Communications and Networking 2020 (2020): 1-12.


8. Ying, Xuhang, Joanna Mazer, Giuseppe Bernieri, Mauro Conti, Linda Bushnell and Radha Poovendran. “Detecting ADS-B Spoofing Attacks Using Deep Neural Networks.” 2019 IEEE Conference on Communications and Network Security (CNS) (2019): 187-195.


9. H. Yang, Q. Zhou, M. Yao, R. Lu, H. Li and X. Zhang, "A Practical and Compatible Cryptographic Solution to ADS-B Security," in IEEE Internet of Things Journal, vol. 6, no. 2, pp. 3322-3334, April 2019, doi: 10.1109/JIOT.2018.2882633.


10. Doc 8973: Aviation Security Manual, 12th ed, International Civil Aviation Organization (ICAO), Montreal, QC, Canada, 2020


11. “ICAO.” n.d. Home. Accessed October 29, 2022. https://www.icao.int/Pages/default.aspx.


-------

[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)
