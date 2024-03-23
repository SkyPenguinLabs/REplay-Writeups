---
cover: ../../../../../.gitbook/assets/image.avif
coverY: 0
---

# 2: Running REplay

To run REplay, there are a few things you should know.

### REplays initiation

The first thing REplay must do before actually being live to use is first initiate the required data and information. This means downloading the proper files or installing indexes depending on the level and verifying information.

{% hint style="info" %}
Note that none of these files are actually malicious. It is a bunch of dummy data that is there for the purpose of the exploit code being registered into the program (_but due to invalid data, the exploit will fail all the time making it semi-simulation_)&#x20;
{% endhint %}

So when you start REplay the first time around, it might need to be reloaded.&#x20;

### REplays permissions&#x20;

for Level 1, elevated permissions are not required, but for level 2 they will be. This is due to-

* Permissions to start local connections
* Permissions to lock files&#x20;
* Permissions to read processes&#x20;
* Permission to execute specific commands
* and more&#x20;

So if you want to be bug free when running it and exploring the GUI, then you need to make sure that it runs in an elevated permission zone.

### REplay is technically malware

REplay was designed to mimick a fancy game cheat that was on the market for many different games. This game cheat actually utilizes <mark style="color:purple;">WinAPI</mark> calls such as `ReadProcessMemory`, `WriteProcessMemory`, and many other functions and symbols relevant to anti-analysis and more.

Windows defender ill delete REplay as it will detect it as a virus. You will need to whitelist REplay and all of the files it downloads remotely. **THIS IS ALSO WHY I SUGGEST USING A ISOLATED DIRECTORY**&#x20;

