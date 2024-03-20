---
cover: ../../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# Methods For Locating

Locating Use After Free is actually quite easy- especially if we have good symbol loaders. However, In many scenarios, especially in larger environments- frameworks like IDA-Pro, Binary Ninja, Ghidra, and others will not immediately be able to detect symbols like `free` calls. This means that sometimes, we are left to do the work ourselves unless we can use other methods (that do in fact exist)  to label and find these values ourselves.

### Where do we start?

Initially, starting to locate where use after free may be tough as it can be practically anywhere. Since REplay was designed to be a wonky environment and was also designed with complexity with laziness in mind- we need to go back to our roots and train-isolated to understand how these bugs work.

{% hint style="info" %}
Training in isolation is a method that some reverse engineers use to grasp better skills or sharpen their existing ones for learning how to identify patterns in the code that can become problematic or helpful to their process. We go in depth about that here -&#x20;
{% endhint %}
