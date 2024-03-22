---
description: A small page designed to showcase how we can locate double free
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Educational

{% hint style="info" %}
Make sure you go to [iof-integer-overflow.md](../../../information-module/binary-auditing-further-reading/iof-integer-overflow.md "mention") to explore how integer overflows actually work in more complex scenarios. This will help you finish this section.
{% endhint %}

## Locating Double Free

This one happens rarely and is a result of programmer sleepiness or  laziness. Either way, its a huge problem as it will eventually cause the program to crash and fault. However, the fun thing about double free is that finding them is easy.

### Methods

There is one primary method that can be done pretty easily. That is going to be listed in steps below.

* <mark style="color:red;">**Step 1 ->**</mark> <mark style="color:red;"></mark><mark style="color:red;">Find all occurrences of '</mark><mark style="color:red;">**free'**</mark> which includes mapping out the function 'free' if the compiler statically embeds the function without naming it and also includes mapping out the function base.&#x20;
* <mark style="color:red;">**Step 2 ->**</mark> <mark style="color:red;"></mark><mark style="color:red;">When you find all occurrences</mark>, look for more than one free in the same subroutine close to one of the free calls. Many functions will use more than one block of memory on the heap- so its important to understand&#x20;
* <mark style="color:red;">**Step 3 ->**</mark> <mark style="color:red;">Analyze the data and check for two free()</mark> calls which are all appointed to the same block of memory.&#x20;



