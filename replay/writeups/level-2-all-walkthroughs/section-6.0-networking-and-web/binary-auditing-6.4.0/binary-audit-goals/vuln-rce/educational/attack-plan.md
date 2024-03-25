---
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Attack Plan

To go about finding RCE depends on how our situation is and what our situation is currently. For this, we can split this into a few sections to define the parts of our attack plan or hunting plan and then finish it all in the end.

{% hint style="info" %}
Remember that we need to have the following information in order to formulate a good attack plan.\
\
Where are we looking, \
What are we looking for, \
How can we make this easier, \
What is our end goal
{% endhint %}

### How do we approach this scenario

The way we approach RCE should have been clear when we talk about locating it. We want to locate specific calls and systems such as data parsing libraries (_json data, XML data, etc_) and even specific input calls like `system` which can eventually lead to RCE if the state is right.

Now, RCE can be treated like everything out- test the applications inputs, see what may run command processes.&#x20;

{% hint style="info" %}
If you want to learn how to find that, you can use process monitor from the Windows sysinternals suite to figure this out as some applications run commands but run them in the background.\
\
If you can figure out where that is happening, then you can easily figure out where you need to go.
{% endhint %}

So we are going to first find a area of interest which if you were following along in [vuln-double-free](../../vuln-double-free/ "mention")was pretty clear. We will be targeting that login via remote endpoint system.

### Kickstarting the hunt!

If you want to try this on your own, look and try to find system calls and functions in which your input can in fact influence the output results. Note that there are areas of interest that you should look to see if they use or rely on system.

* The GUI main panel rendering function (the function we saw all the buttons and logic)
* REplays web server
* The GUIs input functions
* The GUIs handlers and thread routines

### Our plan in detail

Our plain in detail can boil down to the following points.

* <mark style="color:red;">Where are we looking:</mark> We are going to be looking in the auto authentication via remote endpoint example in [vuln-double-free](../../vuln-double-free/ "mention") .
* <mark style="color:red;">What are we looking for:</mark> We will be looking for any system calls that is being executed around that area of interest.
* <mark style="color:red;">How can we make this easier (how does the hunt become easy)</mark>: We can search and highlight areas of importance and areas that are most likely to handle input with system execution.&#x20;
* <mark style="color:red;">What is our end goal:</mark> To proof that the RCE exists within the application Via RE and also make sure we can document how we were able to make payloads.

## Steps in depth

Before we move on, I want to make sure that for this, we understand all of the information we have gathered so far.

### What we know right now

For what we know, most of this ties into what was explained in the previous vuln.&#x20;

* We understand that the program shown in [vuln-double-free](../../vuln-double-free/ "mention")is executing system commands and we were able to verify that.
* We understand that the user input is not being cleaned and only checks for https which means we must include that in the payload
* We also know that the program will crash if the payload is not done properly. Either way, we just need to verify that the command worked in some shape or form.

### Steps to take

* <mark style="color:red;">S1: Analyze the input area</mark>              -> find the code where the data is being pushed to execute the information. We analyzed this in [vuln-double-free](../../vuln-double-free/ "mention")but not in depth.
* <mark style="color:red;">S2: Analyzing the command exec</mark> -> find where the command is being executed and how it works in depth. This means basically explaining the order of data pushed before the program executes the command.
* <mark style="color:red;">S3: Crafting The Payload</mark>                 -> Crafting a payload that actually works based on analysis, being able to summarize and proof the vulnerability.&#x20;

&#x20;

&#x20;
