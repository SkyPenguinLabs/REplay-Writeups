---
description: >-
  Locate the buffer overflow in the programs binary via reverse engineering
  techniques
cover: ../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# Vuln: Buffer Overun

Buffer over runs, commonly referred to as buffer overflows are by far one of the most common stack and heap based vulnerabilities and when working with system APIs, might also be one of the most common mistakes to make!&#x20;

{% hint style="info" %}
For further information on buffer overflows, visit [bof-buffer-overflow.md](../../information-module/binary-auditing-further-reading/bof-buffer-overflow.md "mention")
{% endhint %}

### What is this objective/goal?

The objective of this task is to make sure we can analyze the binary in some shape or form to recognize security faults in the program on a muchhh more lower level. In this case, we will need to not only create a diagram for hunting these kind of security issues, but will also need to locate at least one of the buffer overflows that exist within this program.

{% hint style="info" %}
Hint: For every request picked up by the server- a user gets to influence. This is something developers never anticipated users finding- and requires an administrative ID to use!
{% endhint %}

To finish this goal we must:

* _Find the BOF and explain how it is an issue_
* _Explain what we learned_
* _Build a detailed graph explaining how we go about hunting 0days in binaries and why_

## Analyzing & Specialized Recon

In order to first understand what we are looking for and exactly how to go about it, we need to build out some sort of idea as to **how** we are going to be locating this. Sadly, there are not nearly enough binary scanning tools out there open to the public and even if they are- they are **mostly** trashy. Any '_good_' software out there for binary auditing is wayyyy too pricy for us- so we are going old school and going to build out what I like to call - 'attack path'

Attack paths are ways to describe the sequence of steps or methods we can use to gain unauthorized access to a system, find vulnerabilities and exploit them- and more!

For now, lets define some important points.

### What are we looking for?

Ideally, when looking for binary vulnerabilities which are like finding a needle in a haystack, we can actually define what specific vulnerability we are expecting the most. For example-

* _if we know the application is doing operation on data_
* _If we know the application also allows for a ton of user input_&#x20;
* _If we know the application docs tell the user not to do something with inputs_

Then we most likely can expect to find buffer overflows. For this section, I have provided a general template of questions and answers.

> Area: User input

* How often does the application ask for user input?
* Are there specific restrictions to the user input?
* Is the user input allowing for everything?
* Is the application acting like a desktop app but is really a web app? (helpful for web based vulns)
* Is the application manipulating or copying or saving the data anywhere?
* Where is the user input going?
* What data types are used for the user input?

> Area: Memory Management

* How is the application using system memory?
* Do we see any Windows APIs for heap-based allocation?
* Are exports like 'free' and 'malloc' used?

Just as a basic idea for you!

### Our scenario

This GUI, if you spent time exploring it- uses user input quite frequently in both the application window itself and even the web server.&#x20;

Since the developers made this web server clearly for admins, it means that the developers did not anticipate that the users would be reaching this server or even knowing it existed- we can assume that they might not care how the user input is handled.

> Why do we not expect devs to handle input here?

Well if this is an admin only login- we can expect either devs on testing teams or admins who know how to use the software in and out are the only ones being thought of. If the development team does not expect a user to input anything- then they cross security or care off the list if they are hollow-headed enough or ignorant enough.&#x20;

> What are we looking for?

In this scenario, we are going to be looking for some form of buffer overflow or something for comparing data on the backend of the web application or manipulation for the admin-ID. This is because we expect the admin-ID to be encoded or hashed to compare a hash in a remote database or something where data will be moved, copied, or compared.

### Our attack path - Text based

{% hint style="info" %}
Note that documenting is about one of the most important things during this phase. Understanding how we are going to go about things- logging it and logging rabbit holes and findings or possible other entry points and places to explore is super important. Read more in \
\
\- [security-research-application.md](../../../../../../replay-extras/security-research-application.md "mention")\

{% endhint %}

For our attack path- we are going to be looking over a fe~~w~~ things.&#x20;

> Final Decision: What are we looking for

We know we are looking for a buffer overflow- specifically heap considering our scenario. So we can expect to look at calls like the following.

* Routines that use '<mark style="color:blue;">malloc</mark>' around known user-input areas
* Routines that use data manipulation functions like `strcat` or `sprintf` even `strcat`&#x20;
* Routines that use '<mark style="color:red;">calloc</mark>' or '<mark style="color:red;">relloc</mark>'
* Routines that use file operations like '<mark style="color:red;">fopen</mark>' or '<mark style="color:red;">fwrite</mark>' even '<mark style="color:red;">fread</mark>' or Windows APIs that use file operations unsafely such as '<mark style="color:blue;">CreateFile</mark>'
* And other calls alike that rely on buffers

Since we now know what we are looking for, we can demonstrate a sample path that defines what we are going to be looking for.

* <mark style="color:purple;">**Answer**</mark>: For this final thought, we are looking for any calls that revolve around memory management or string copying and management / manipulation around the user input section

> Final Decision: Area of importance

Before building our attack path, we want to also select an area of importance which means what area is the most susceptible to this flaw.

* <mark style="color:purple;">**Answer**</mark>: For this final thought, assuming that the admin panel was most likely not thought of or cared for much (especially its limited use) we can assume that this is a good area of interest, a way or area to look at. The area subject is going to be user input since the server allows users to take in user input

> Final thoughts: How data is being fed to the program

Since we know this is not happening in the CLI and is certainly not in the GUI- we can expect the server to be taking in a specific input via web requests.&#x20;

This means that we want to specifically look in areas where the program uses '_<mark style="color:red;">recv</mark>_' calls.&#x20;

{% hint style="info" %}
Now, if you need to again- go back to pages like [use-after-free-1](../../../../../../replay-extras/replay-isolated-training/examples/use-after-free-1/ "mention") which can help you understand analyzing calls like 'recv' that might not show up right away. Or learning how to trace them in a program!&#x20;
{% endhint %}

* <mark style="color:purple;">**Answer**</mark>: For this final thought, the data is coming into the program via web request specifically a post request to the API endpoint on the server.



To find out how to do this challenge, go to the next page!
