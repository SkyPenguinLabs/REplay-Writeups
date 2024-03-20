---
cover: ../../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# Auditing Methods

Binary auditing is as mentioned previously, a field that requires a ton of different methodologies. Here, we will be going over some basic methods that can help you find and search for binary vulnerabilities and also verify them.&#x20;

## Where to start

The first question I asked myself when I was told to audit a binary for vulnerabilities is - "where exactly do I start?"

This is actually for some reverse engineers a hard question to answer at times- this is because binary vulnerabilities are not always going to be dependent on imports (_unless they are, e.g: importing and using dangerous functions from Windows or Linux plugins/libraries/dynamic\_link\_libraries_). Instead, it will be dependent on the **way data is being handled** and **where** data is being handled as well. Lets check some basic ideas below that can help you.

### First: Investigate

The first thing you want to do before going on your way to search for buffer overflows, integer overflows and other security issues in binaries (especially statically) is going to be analyzing the application itself.

Use it as a user that has NO clue how an application works. You want to toss a bunch of random characters in input boxes, figure out resource download sections, press a bunch of system events and so on from there until the program crashes or faults.

{% hint style="info" %}
The reason we investigate until a crash occurs, is because usually, programs will crash when data is being handled or passed incorrectly. This can ultimately lead to some form of attack if the event or crash you discovered was a result of something in relation to user input.
{% endhint %}

We are going to give ourselves a scenario to learn the methods a bit.&#x20;

> **First Step Scenario:** In this scenario, we have a nice application that allows us to manage our social media platform. However, upon making a password change with a 128 character long password, the program crashes!

Awesome! Now we can further explore.

### Second: Explore

Now we need to open the program in IDA-Pro, Binary Ninja, Ghidra, or another reverse engineering framework (_really whatever you are comfortable with_.)

When you open this program, considering our scenario above- consider looking for the following

* **Login Form Text Data:** Login forms usually have some form of text that is used or loaded as a placeholder. This text is typically grayed out in a sense that allows the user to know what part of the input form equals what. Try to search for these references in the text.
* **Common Imports or Symbols:** This is pretty basic and really most of REplay is done by looking at the import tables, other common symbols and more for further analysis. But really, some devs will use system APIs to compare strings especially in languages like C++. Also any other imported symbols that revolve around comparing data, converting data, sizing data or storing data is worth looking at.
* **Event Handling:** If this interface is utilizing standard event handlers, especially for error handling- then you can find some common symbols, structures and more that can also be used within the login form.
* **From The Bottom Up:** From the bottom up is a way of saying, start from 0 and work your way up the chain in the program. This means, understand how the GUI works- reverse engineer button or GUI widgets and then name them as the more you discover and uncover, the more references you will have. Some buttons may even have custom actions.

There are some others, but for now- this is to just get us to the location of the login form in the program.

{% hint style="warning" %}
Remember that our end goal is to get to the function that handles this data. Because the user input form for the change password part of the application was used, we want to trace back to where our data was being inputted.\
\
**Additionally**: you want to also explore other forms, if it happens on every forms- there is a high chance that the developer automated user input and is using a custom function for it. So for each form, locate them in the binary, and see what functions they call to capture input and try to find the cross references to see if they are in every form and reverse the function that captures and stores the user input collectively.
{% endhint %}

### Third: Analyze

Now, when we find ourselves and have verified that we are in the login function- we want to analyze the function and see if anything sneaky is happening.

{% hint style="info" %}
remember: pay attention to the **way** data is being handled.&#x20;
{% endhint %}

When analyzing the function- try to look for&#x20;

* String or data comparisons and logic
* Arithmetic operations happening on data
* static buffers
* heap allocation functions and symbols
* logic around parsing and handling input data
* error handling methods&#x20;
* data measurement functions
* and more...

This will indicate if our application does or does not have a flaw in its data handling process. If there is no indication of this, then try to trace where the data is going and how its being passed- if possible, try to also pinpoint specific variables and rename them to make sure you keep track of what is what.&#x20;

## Some more 'where' techniques

When looking for specific vulnerabilities, analyzing specific system APIs, especially ones that have to deal with data conversion or data storing is going to be important to look at- this is because, due to the poor design of system APIs like the Windows API, exist many flaws in simply just using the function and passing data to it.&#x20;

You can also look around areas that are '**heap**' or '**stack**' specific, whatever you really picture being most common to the program you are reverse engineering.&#x20;

### Heap Specific - The scope, REplay

Analyzing common heap-memory related functions like the ones below, whilst also analyzing the data being pushed and returned from them is quite important.

* **Free**: Free can be used to free a specific block of memory
* **Malloc**: Malloc is used to allocate memory&#x20;
* **memcpy**: memcpy is used to copy memory from a source to a given destination
* **memset**: Will set a specific block or memory to a given value
* **strncpy**: will copy characters from one string to another

These are just some examples, but heap memory seems to be where developers will make the most mistakes- especially when risking security if it means ease of development, less development time and more performance. Also note that analyzing the way data is used before and after the calling of these functions is important for locating vulnerabilities such as UAFs (User After Free).

