[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)


# Buses On Planes Part 1: A Quick Introduction To Digital Avionics Networks

### By <a href="https://disesdi.github.io/contact.html" target="_blank" rel="noopener noreferrer">Disesdi</a> | *2022/10/26*

-------

*Modern avionics buses play a crucial role in aviation. But what exactly is a bus, and what is it doing on a plane?*

-------


## Introduction


This is Part 1 of a 3-part series on digital avionics buses.

In this post, we’ll be looking at what digital avionics buses are, how they work, and what role they play in aviation cybersecurity. 

We’ll talk about airworthiness characteristics for digital systems, and finally, we’ll discuss how likely it is that a malicious actor–like a hacker–could access a plane’s flight controls via the wifi.

Let’s go!


## Binary Unit System (BUS)


You may hear a lot of different origins for the word *bus* in the context of computer networks. I’ll tell you what my engineering professors told me.


In electronics systems like avionics, a *bus* is actually an acronym: it stands for *Binary Unit System*. It’s a means of moving information around. 

Buses transfer data between other components.<sup>[1]</sup> They can be either physical or software-derived.<sup>[2]</sup> 

As you can probably imagine, buses exist in a host of industrial applications.

Modern avionics buses are critical to flight operations. They enable communications among an aircraft’s electronics. By connecting avionics systems digitally, avionics buses dramatically reduce onboard wiring,<sup>[3]</sup> saving considerable cost and weight.<sup>[4]</sup>

These electronics can include sensors, computers, displays, actuators & other IT components. You might see them referred to as *Line Replaceable Units* or LRUs. Buses connect LRUs so they can communicate. 

If you’re thinking that sounds like a network, you’re right. Avionics buses are the *digital avionics networks* that enable onboard communication of an aircraft’s electronic systems. 

Like all aircraft components, avionics networks must undergo airworthiness certification. This process is lengthy and expensive. 

These systems are used in flight, in safety critical applications, so they have special certification requirements. 

## Airworthiness Characteristics For Digital Systems

Because avionics buses are used in what are called *safety-critical* systems, they must be *highly reliable.*<sup>[5]</sup> They need to be able to demonstrate performance well above networks used in other applications.

In safety-critical systems, reliability may prevent loss of life. Avionics systems often have one important thing in common: their failure would jeopardize flight safety. 

Because of this, digital avionics systems must share some common characteristics to be considered airworthy. 

> *Characteristics of Digital Avionics Systems:*
>
> * High data rate
> * High reliability & integrity (airborne specific)
> * Real time capability
> * Deterministic behavior

One characteristic that digital avionics systems share with other applications is the need for a high data rate. However, aviation requires a much greater level of reliability and data integrity than many commercial applications. 

Avionics systems also need real-time capability, and highly deterministic behavior–we need to know what they will do under specific circumstances, reliably.


## Hacking Flight Control Systems Through Onboard WiFi?


In 2015, a security consultant named Chris Roberts was [detained by the FBI](https://www.washingtonpost.com/news/morning-mix/wp/2015/05/18/hacker-chris-roberts-told-fbi-he-took-control-of-united-plane-fbi-claims/)<sup>[6]</sup> after a flight where tweeting about his ability to access flight control systems via the in-flight entertainment system. 

According to an FBI warrant, Roberts also claimed to have at some point briefly taken partial control of a plane. FBI investigators found evidence of tampering on Seat Electronic Boxes (SEBs) where Roberts had been sitting, from which he claimed to have [physically accessed the plane's networks](https://www.wired.com/2015/05/feds-say-banned-researcher-commandeered-plane/) using an ethernet cable.<sup>[7]</sup> 

Attorneys from The Electronic Frontier Foundation (EFF) [represented Roberts](https://www.eff.org/deeplinks/2015/04/united-airlines-stops-researcher-who-tweeted-about-airplane-network-security) in the investigation.<sup>[8]</sup> Aircraft manufacturers & some aviation experts, however, [denied the attack was possible](https://www.theguardian.com/technology/2015/may/19/hacker-chris-roberts-claim-seized-control-boeing-airliner-disputed-experts).<sup>[9]</sup>

The aviation certification requirements that aircraft systems and components go through are far more stringent than any consumer application.<sup>[2][10]</sup> This means that any electronic element onboard an aircraft has been examined and tested much more rigorously than  something like your home network, or your local coffee shop’s wifi.

Not only are the networks highly tested, they are often distinct from passenger wifi & infotainment systems. There are proposals for increased use of wifi in aircraft systems,<sup>[11][12]</sup> but as of now, these have significant reliability and security hurdles to overcome still. 

In fact, many commercial aircraft currently use wired networks that are completely, *physically* separate from whatever networks passengers may have access to.<sup>[13]</sup> While attack vectors have been theorized,<sup>[14]</sup> as of this writing, they haven't been publicly demonstrated.

Currently, in most aircraft, there is no mechanism for [lateral movement](https://www.paloaltonetworks.com/cyberpedia/what-is-lateral-movement)<sup>[15]</sup> among the onboard networks.<sup>[16]</sup>

So as dramatic as it might sound, hacking into an avionics network via the in-flight wifi is probably not going to happen. 


## Conclusion

In this post, we took a quick look at what defines digital avionics buses & how they work. 

We also introduced airworthiness characteristics for digital systems, and looked at the (un)likelihood that a hacker could access a plane’s flight controls via the wifi--with the important caveats that attacks *have* been proposed, planes are becoming increasingly networked, and proposals to integrate more wifi systems to save weight, maintenance and fabrication costs could all change the cyber threat model for aircraft.

In order to understand avionics buses better, next we need to understand some important modes of signal transmission, which I’ll cover in *Buses On Planes Part 2: Topologies, Transmission Modes, & LRUs*.

Thanks for reading!


-------


## [*Contact me >>*](https://disesdi.github.io/contact.html)


-------


## References



1. “Networks and Busses \| Digital Communication \| Electronics Textbook.” All About Circuits, https://www.allaboutcircuits.com/textbook/digital/chpt-14/networks-and-busses/. Accessed 26 October 2022.


2. Schuster, T. and D. Verma. “Networking concepts comparison for avionics architecture.” 2008 IEEE/AIAA 27th Digital Avionics Systems Conference (2008): 1.D.1-1-1.D.1-11.


3. Işık, Yasemin. “ARINC 629 data bus standard on aircrafts.” (2010).


4. C. Furse and R. Haupt, “Down to the wire [aircraft wiring],” IEEE Spectrum, vol. 38, no. 2, pp. 34–39, 2001


5. Hope, David C.. “Towards a Wireless Aircraft.” (2011).


6. Wm, Justin. 2015. “Hacker Chris Roberts told FBI he took control of United plane, FBI claims.” The Washington Post. Accessed 26 October 2022. https://www.washingtonpost.com/news/morning-mix/wp/2015/05/18/hacker-chris-roberts-told-fbi-he-took-control-of-united-plane-fbi-claims/.


7. Zetter, Kim. 2015. “Feds Say That Banned Researcher Commandeered a Plane.” WIRED. Accessed 26 October 2022. https://www.wired.com/2015/05/feds-say-banned-researcher-commandeered-plane/.


8. Crocker, Andrew. 2015. “United Airlines Stops Researcher Who Tweeted about Airplane Network Security from Boarding Flight to Security Conferences.” Electronic Frontier Foundation. Accessed 26 October 2022. https://www.eff.org/deeplinks/2015/04/united-airlines-stops-researcher-who-tweeted-about-airplane-network-security.


9. Gibbs, Samuel. 2015. “Aviation experts dispute hacker's claim he seized control of airliner mid-flight.” The Guardian. Accessed 26 October 2022. https://www.theguardian.com/technology/2015/may/19/hacker-chris-roberts-claim-seized-control-boeing-airliner-disputed-experts.


10. Ricker, Tony. “Avionics bus technology: Which bus should i get on?” 2017 IEEE/AIAA 36th Digital Avionics Systems Conference (DASC) (2017): 1-12.


11. Park, Pangun, Hossein Shokri Ghadikolaei and C. Fischione. “Proactive fault-tolerant wireless mesh networks for mission-critical control systems.” J. Netw. Comput. Appl. 186 (2021): 103082.


12. Abdulrab, Hakim Q. A., Fawnizu Azmadi B. Hussin, Azrina Abd Aziz, Azlan Awang, Idris Ismail and P. Arun Mozhi Devan. “Reliable Fault Tolerant-Based Multipath Routing Model for Industrial Wireless Control Systems.” Applied Sciences (2022): n. pag.


13. Y. C. Yeh, “Safety critical avionics for the 777 primary flight controls
system,” in IEEE DASC, 2001


14. Freiherr, Greg. “Will Your Airliner Get Hacked? \| Air & Space Magazine.” Smithsonian Magazine. Accessed 26 October 2022. https://www.smithsonianmag.com/air-space-magazine/will-your-airliner-get-hacked-180976752/.



15. “What Is Lateral Movement?” n.d. Palo Alto Networks. Accessed 26 October 2022. https://www.paloaltonetworks.com/cyberpedia/what-is-lateral-movement.


16. Park, Pangun, Piergiuseppe Di Marco, Junghyo Nah and C. Fischione. “Wireless Avionics Intracommunications: A Survey of Benefits, Challenges, and Solutions.” IEEE Internet of Things Journal 8 (2021): 7745-7767.


-------

[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)
