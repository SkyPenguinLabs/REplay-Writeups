---
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Attack Plan

### How we are going to approach this?

Well, since our goal is to find and locate a double-free vulnerability, we can actually attack specific points in the GUI that may crash. This is because, when you free a block of memory more than once- the program will try to grab uninitialized memory resulting in the crash.&#x20;

**Alas**:

* Anything that crashes, check and analyze it- if you can, attach a debugger and inspect where the crash is happening specifically.&#x20;

When we analyze those crashes, we want to look for any memory allocation especially heap allocation using functions like `malloc` then trace the data malloc returns and then continue to  search for any calls that will free that memory. This also includes a extra function that frees the already freed memory.

### Kickstarting this&#x20;

If you want to go ahead and speed run the first part- hop into the GUI and start checking for user inputs that are accepted and see what they do- then try to get them to crash by utilizing them in improper ways and etc. Then hop into IDA and locate the function that led to the initial crash.

### Our plan in detail

Our plan is going to boil down into these components shown below:

* <mark style="color:red;">Where are we looking</mark>: User input functions, specifically ones we have not explored that crash&#x20;
* <mark style="color:red;">What are we looking for</mark>: Anything to do with user input and operations on that data that crashes
* <mark style="color:red;">How can we make this easier</mark>: Use pseudocode generators for high-level representations
* <mark style="color:red;">What is our end goal:</mark> Figure out how the crash happens, and explain the double free issue here

So we are going to tackle a user input field, convert its entire base to pseudo-code, analyze the psedocode in depth and check for any operations happening on the data from our input.
