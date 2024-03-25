---
cover: ../../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Locating RCE

## Methods and Applicable Theories For Locating RCE

Locating RCE on a client side application depends on the complexity on the application. Many times, you will have to did through hundreds of functions and soooo much information just to even locate it. So we need to make this as easy as we can and base it purely on how the application is moving data and what you as a user can influence.&#x20;

The sections below demonstrate this in depth.

### Logical bases  - What

Since we are looking for RCE, we are looking for system calls, anything relevant to system calls and any function known to be vulnerable to RCE by nature. For example, using something like a data serialization function via files as you may do in something like Pythons Pickle library. However, this is dangerous if you do not check or scan the contents of the file before loading it or even bother to setup security systems.

Due to the pure and utter shitty design in the file format and library, its extremely easy to slide some malicious code in there and get it executed on the machine.

> Knowing what we have to look for&#x20;

Sometimes, its also not all in the functions, other times it is the way data is being processed. This leaves us to our next step.

### Structure - How

When looking for RCE, we must consider **how** the application is taking data and if it is going in or out of the application. The following systems would be of interest to you if you were looking for RCE.

* Anything relevant to IO in the app that triggers system processes (_think password input_)
* Anything relevant to your client sending and receiving data (_think pkt\_senders_)
* Any packet capturing systems, packet monitoring systems, and more (_think listeners_)
* Anything that may have to do with opening and reading files again (_think config & plugin_)
* Anything that involves existing command processes or starts shells (_think sub processes_)
* and more...

So pretty much - **we need to know how data is coming in and out of the program**.

### Location - Where

The location is simple. Just choose a point of how data gets into the application- e.g: by listening for packets from other clients or servers and connections. Take that point, and try to find it statically or dynamically in the program.

### The fun stuff

As explained in previous sections, especially in this entire series. You may actually need to do all the tracing for the function yourself. This includes trying to look for specific symbols relevant to system calls. Here, I have provided a subpage for finding system shown below.

