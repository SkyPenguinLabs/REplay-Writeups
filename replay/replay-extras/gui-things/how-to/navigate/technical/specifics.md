---
cover: ../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Specifics

This is the specific section of the application that lists all the libraries and other external requirements the build and more information that does not come shipped with the application.

### [Basic information](#user-content-fn-1)[^1] (1)

* OS                 -> Windows
* Arch              -> X64
* Language    -> C++20
* Charset        -> Multi byte

### [Security information](#user-content-fn-2)[^2] (2)

* Data Obfuscation       -> Uses two different XOR algorithms (compile time string encryption)
* Anti Application          -> Thread that checks if blacklisted applications are running
* Anti Debug (13x)         -> 13 different unique anti-debug systems on one thread
* Anti Dumping              -> Inactive for level 1-2 but it checks for dumpers
* Anti Virtualization      -> inactive for level 1-2 but checks for virtualization artifacts
* Anti Window                -> Some windows and window classes are done
* Other                             -> over 23 other security systems exist, they are unused in L1-L2

### [Binary Vulnerabilities](#user-content-fn-3)[^3] (3)&#x20;

* Buffer Overflow  x1
* Use After Free x1&#x20;
* Double Free x2
* Integer Overflow x2
* Format String x5

### [Web vulnerabilities](#user-content-fn-4)[^4] (4)

* XSS (only one right now, for basic PoC)

### [Security concerns](#user-content-fn-5)[^5] (5)

* No input checks x22
* No data typing checks x40
* No character checking x10
* No data sanitization x3
* No integrity checks on files or required data x4
* Inactive anti debug systems that never work (too much) +20

### [Libraries ](#user-content-fn-6)[^6] (6 \[imports])

* KERNEL32.dll
* USER32.dll
* WS2\_32.dll
* D3D11.dll
* DWMAPI

### [Libraries ](#user-content-fn-7)[^7]\(7 \[called])

* `NTDLL.dll`

### [Third Party](#user-content-fn-8)[^8] (8)

* SkCrypt
* XorStr
* Nlohmann JSON
* Lazy Importer



[^1]: What you will learn to reverse engineer

[^2]: What is being looked for&#x20;

[^3]: To help you explore binary auditing more



[^4]: To start a new concept for REplay

[^5]: To help with your analysis and understanding

[^6]: So you can understand and handle errors properly

[^7]: What the program interacts with remotely

[^8]: To know who made this CTF possible in some aspects and objectives
