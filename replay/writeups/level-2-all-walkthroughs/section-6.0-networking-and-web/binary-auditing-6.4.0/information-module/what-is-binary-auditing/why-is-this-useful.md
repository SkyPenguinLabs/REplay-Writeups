---
cover: ../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# Why is this useful?

Your first question upon asking is how exactly is binary auditing useful? Why should you learn it? To be completely honest with you, binary auditing is a super under rated area of expertise due to its prime limited use. While you can learn a lot working in this area and practicing to uncover vulnerabilities, many say it is something that's really not **super useful.**&#x20;

### **Where this changes**

The one immediate thing I will say though is that if you plan on getting into hardware hacking, IoT security research and fields alike, then you might want to consider taking up that skill. This is because, despite compiler optimization being a real world problem and making internal code a mess, being able to recognize flaws in systems that are heavily influenced by user interaction is going to be beneficial in a wide range of scenarios. For example, lets say you find some application on a IoT device when analyzing its firmware.

You realize that this device crashes upon login- so you reverse engineer the binary, find the location of the login and where its crashing, then further analyze to see where exactly and why exactly the issue is happening.

Understanding how to verify and recognize and even trace these bugs in a program will lead to some exploration of flaws or genuine concerns that can be reported.

### Main use cases

Generally, binary auditing can be used anywhere- however, it may become helpful in scenarios or areas of research like the two below.

* **IoT Security:** This will be due to auditing binaries developed for the devices services (that are custom to the developers or device)
* **Malware/Blackhat frameworks**: Malware and blackhat frameworks (**e.g: DDoS panels, or those really weird sketchy 'free' game cheats**) are a good example of where it might also be used in some "_realistic_" realm. I do not put this one as a prime priority because most people reverse engineering malware or blackhat frameworks also have a end goal- either to crack it or build some YARA rule for detection (_malware_).



