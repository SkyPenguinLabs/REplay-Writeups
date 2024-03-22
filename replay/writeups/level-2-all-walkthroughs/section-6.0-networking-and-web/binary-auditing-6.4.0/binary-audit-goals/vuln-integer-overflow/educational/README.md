---
description: >-
  A page and module to give all the information you need on finding Integer
  Overflows
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Educational

{% hint style="info" %}
Make sure you go to [iof-integer-overflow.md](../../../information-module/binary-auditing-further-reading/iof-integer-overflow.md "mention") to explore how integer overflows actually work in more complex scenarios. This will help you finish this section.
{% endhint %}

## How to find Integer Overflows

Integer overflows are one of a kind, and because they usually are not done with calls like malloc where typical BOFs and other vulnerabilities are found- we have to rely on standard methodologies to find and locate them or try anyway.

### GUIs - A major difference

Graphical applications are one of the most annoying types of applications to reverse- in moments, they can be fun. But that fun is quickly lost when you actually are looking for something to attack such as a flaw in the binary that can be used to pop a shell or something. With that, its important that we note; **GUIs have to be thought of from a specific angle and should be delt with differently**.

Since REplay is a GUI, some of methodologies we will be taking a look at purely stick to GUIs in specific due to widgets or unique scenarios.

### Methods of search

{% hint style="info" %}
A good thing to note is that integer overflows are VERRYYY hard to come across in the wild. This is not because they are not common- its just because of how much of a "needle in the haystack" it is to find it.
{% endhint %}

Searching for integer overflows mainly boils down to the question - **where does my input influence the programs mathematical operations?** .

But of course, how do we get there? How do we **know** our data is being used for mathematical operations? Well, there are a few ways. Check some below.

* **We have analyzed string manipulation functions**: Many applications, especially GUIs, are relying a ton on data conversion techniques that are mostly only applicable to their scenario. So they mostly end up building custom string manipulation functions which stretch, delete, pick apart and reorganize, or sort through string data. Of course, to a computer, this is just a set of characters. So if you happen to come across a function that your input data influences, make sure to analyze it through and through.
* **Analyze functions through and through:** The last statement in the previous point made a good statement- you want to analyze the functions through and through. Because of how small integer overflows can be to find, you want to make sure, especially in mathematical functions that you analyze every single step of it and dynamically as well (if you can).
* **Messing With Inputs (Fuzzing kindof):** The next step is to just try your best to "fuck around and find out". By this statement, it means that we find a given input box and we do everything we are not supposed to. If the vendor says that there is a specific range users should NOT pass in characters, then lets explore that and toss 300 characters at it and see what happens. From this, you are able to pinpoint a specific location of a crash if it were to happen- especially if you can use debuggers.
* **Analyze areas you suspect deal with data externally:** This includes any form of receiver for packets, client side listeners, sockets, web requests, and so much more. If you suspect a part of the application is taking data in from an external source- check to see if its validating it and  **what**  that data is. If it has numbers in it- even better!&#x20;
