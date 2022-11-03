[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)


# Real Time Embedded Systems: A Quick Primer


### By <a href="https://disesdi.github.io/contact.html" target="_blank" rel="noopener noreferrer">Disesdi</a> | *2022/11/01*

-------

*What are embedded systems, and what makes a system ‘real-time’?*

-------


## Introduction

In this post, I’ll be talking about what types of systems are embedded, what makes a system real time, and what doesn’t. We’ll also look at some different types of real time systems & contrast them to other types of computing.

The goal is to give a quick & simple introduction to real time embedded systems.

Let’s go!

## What Are Embedded Systems?

An embedded system is a computer system that has a dedicated purpose, within a larger electronic or mechanical system.<sup>[1]</sup> “Computer system” in this context means a processor, memory, and any peripheral I/O (input/output) devices that help the system do its job.

A key to understanding embedded systems is specificity. Embedded systems are designed to do a specific job, and while they might work at varying levels of complexity, it’s that *dedicated functionality* that makes them *embedded*.

General computing is the opposite of embedded systems. Most consumer computers (like laptops) are examples of general computing–they are designed to perform many diverse tasks. They have to do so reliably, or consumers won’t like their experience. 

As an example, laptops mostly do not need the level of specialization found in embedded systems to function and meet user expectations. And in fact such specialization would make general functionality impossible. 

But it is important to note that consumer computers also contain embedded systems working within to enable all the processes and applications these machines run.

Embedded systems can be very simple, or very complex, with a number of peripheral systems & devices working in concert. They are found in surprising places, from media players to the antilock brakes in cars to, of course, aircraft flight controls.

What makes a system embedded, regardless of the application, is dedication to a specific purpose.

This gives rise to a more concise definition:

> ***Embedded System: A compute node that provides a specific service by processing inputs & returning responses as part of a larger system.***

Some embedded systems are also what are called *real time systems*--systems that operate with additional timing constraints. Compute nodes that provide a specific service as part of a larger system, subject to strict timing deadlines, are called *real time embedded systems*.<sup>[1]</sup>

## What Makes A System Real Time?

Real time systems are systems that operate within timing constraints, aka deadlines. 

Real time systems are subject to real-time constraints–in other words, they must deliver responses within specific time periods or by specific deadlines, depending on the system.<sup>[2]</sup> 


Crucially, this response timing has to be *guaranteed*.

Adding the real time constraint to our definition from above, we can come to a more complete understanding of real time embedded systems:

> ***Real-time embedded systems are compute nodes providing a specific service by processing inputs and returning responses guaranteed within a predetermined timing scheme.***

The timing guarantee is critical to what makes a system real time. 

It’s easy to see why operating in real time is vital to systems like avionics. If signals are not received, processed, and sent back out quickly, critical flight functions might fail. Real time functionality of these systems is necessary for flight safety. Failure to operate within deadlines could result in loss of life.

### Real Time Vs Fast

A common misconception about real time systems, even among some engineers, is that the criteria for the category is based on speed–how fast a system can run.<sup>[3]</sup> 

But that’s not true.

What is not necessarily widely understood, even among engineers, is the degree to which computer behavior is non-deterministic. Computers are temperamental machines.

If you’ve ever used a computer and had it act in a way you didn’t expect, you probably know this intuitively: different runs of programs can have different results. 

They also can–and do–take different lengths of time to complete seemingly identical processes.

For this reason, when we’re talking about computers and code, calculations for various processes often include minimum and maximum speeds, averages, or estimates. 

This brings to light a critical distinction: speed vs reliability.

Although real time systems require rapid responses, they also require that the timing of these responses operates at microsecond precision levels. The *variance* of the latency–the wait between processes or signals–must be consistent.

Latency variations between program iterations are so common and well-known, they have their own name: *compute jitter*.<sup>[4]</sup>


![real_time_systems_intel](https://user-images.githubusercontent.com/110150470/199603476-21e55726-3115-4a3f-a339-5a3793bbce7f.png)

*Image: Timeliness, Syncronization, Latency, and Compute Jitter. Source: [Intel]( https://www.intel.com/content/www/us/en/robotics/real-time-systems.html) <sup>[4]</sup>*

Real-time is not so much about being fast, it’s about being predictable. Predictable latencies (delays), predictable order of signals, all increase *reliability*. 

Obviously speed is necessary, but safety critical systems demand more: precision timing.
In fact, deterministic–also known as *predictable*--behavior is a crucial facet of real time system operation:

> "*A real-time computer system can be defined as a system that performs its functions
and responds to external, asynchronous events within a predictable (or
deterministic) amount of time.*" <sup>[5]</sup>

Put another way, in a real time system, the outcome of an operation is equally important as the *timing:* 

> "*In a real-time system the correctness of the system behavior depends not only the logical results of the computations, but also on the physical instant at which these results are produced.*" <sup>[6]</sup>

In systems where there is no tolerance for error, fast isn’t good enough.

Not all real time systems are safety critical, however. Within the real time category, there are different applications with different levels of response timing stringency. 

### Hard Vs Soft Real Time

An important defining characteristic of *hard* vs *soft* real time systems are the consequences for failure.

Hard real time systems are often safety-critical, with catastrophic results for failure.<sup>[7]</sup>

These requirements introduce specific constraints and behaviors of hard real time vs soft real time systems.


***Hard Real-Time:***

> * *response time requirements in the order of milliseconds or less* 
>
> * *can result in a catastrophe if deadlines not met*
>
> * *peak-load performance must be predictable and should not violate the predefined deadlines*
>
> * *must remain synchronous with the state of the environment in all cases*
>
> * *temporal accuracy is often the concern here*
>
> * *often safety critical*


***Soft Real-Time:***


> * *response time requirements are higher* 
>
> * *response times are less stringent*
>
> * *a degraded operation in a rarely occurring peak load can be tolerated*
>
> * *possible slowed response time in high load situations is tolerable*
>
> * *non safety critical <sup>[3]</sup>*


Unlike hard real time systems, soft real time systems have greater tolerance for an occasional fault.

Aircraft flight control & antilock braking systems are good examples of hard real-time embedded systems in action. But there are other examples of systems where guaranteed timing performance isn’t so critical.

Video streaming is one such application. Streaming is definitionally real-time–there really isn’t much of a point to it unless packets are delivered in the proper order & when they’re supposed to be. 

But while a lapse in timing for a video application might result in frustration for the user, it will probably not result in loss of life. This is an example of a *soft real-time* system.

In short, in hard real time systems timing performance matters in real & dramatic ways; soft real time systems still operate in real-time, but with less critical performance needs.

### Real Time Vs Best Effort

Real time systems operate in contrast to *best effort systems*. Just like their name implies, these systems make a best effort to deliver messages, but delivery is never guaranteed. And it’s definitely not guaranteed within a specific deadline.

Internet Protocol (IP), operating systems like Unix, Linux, Mac and Windows, and even the Postal Service are all examples of best effort systems.

## Conclusion

In this post, we briefly introduced embedded systems, talked about the definition of hard vs soft real time systems, and looked at some examples of each. We’ve gone over why not just speed, but also timing matters–particularly in safety critical applications. 

Finally, we defined real time systems in contrast to best effort systems, such as Mac, Linux or WIndows operating systems and even the Postal Service.

I hope this was a helpful quick & simple introduction to real time embedded systems. Thanks for reading!


-------


## [*Contact me >>*](https://disesdi.github.io/contact.html)


-------


## References


1. Shaw, Alan C.. “Real-time systems and software.” (2001).


2. Kant, Krishna (May 2010). Computer-Based Industrial Control. PHI Learning. ISBN 9788120339880.


3. Lee, Edward A.. “What Is Real Time Computing? A Personal View.” IEEE Design & Test 35 (2018): 64-72.


4. “Real-Time Systems Overview and Examples.” n.d. Intel. Accessed November 1, 2022. https://www.intel.com/content/www/us/en/robotics/real-time-systems.html.


5. Furht, B., Grostick, D., Gluch, D., Rabbat, G., Parker, J., McRoberts, M. (1991). Introduction to Real-Time Computing. In: Real-Time UNIX® Systems. The Kluwer International Series in Engineering and Computer Science, vol 121. Springer, Boston, MA. https://doi.org/10.1007/978-1-4615-3978-0_1


6. “Real-Time Systems.” n.d. Electrical and Computer Engineering. Accessed November 1, 2022. https://users.ece.cmu.edu/~koopman/des_s99/real_time/.


7. K. G. Shin and P. Ramanathan, "Real-time computing: a new discipline of computer science and engineering," in Proceedings of the IEEE, vol. 82, no. 1, pp. 6-24, Jan. 1994, doi: 10.1109/5.259423.


-------

[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)
