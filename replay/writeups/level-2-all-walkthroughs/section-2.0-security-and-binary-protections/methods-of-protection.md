---
description: >-
  Solves Objective: Figure out the protection method(s) used within this
  application
cover: ../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Methods of protection

### What is this task?

This task asks that you find all 8 security mechanisms in the program. I will be leaving this up to you but will be leaving the answer here. If you located the thread system which was talked about in [locating-the-thread-management-calls.md](../locating-the-thread-management-calls.md "mention") then you should be able to find all the other security mechanisms and be able to properly bypass them.

### Answer

There were 8 security mechanisms included to prevent people from debugging and modifying the program.

* **Binary Integrity:** This was a client based system that remotely downloaded a hash then self hashed the existing executable being executed and compared the two.\

* **Antidebug:** There were five anti debug systems that were routinely executed for 5 seconds. `CheckRemoteDebuggerPresent` and `IsDebuggerPresent` were the two Windows API calls used for this. The other two systems checked the PEB block and also checked debug registers DR0-DR7. The last and final anti-debug technique was a system that was trying to hide threads from debuggers. \

* **Anti Dumping:** The last two methods of protection were anti-dumping calls.  These calls would prevent people from making dumps and would erase the PE header from memory effectively damaging dumps and another one which increased the size of a PE header. Also two controversal systems.&#x20;

