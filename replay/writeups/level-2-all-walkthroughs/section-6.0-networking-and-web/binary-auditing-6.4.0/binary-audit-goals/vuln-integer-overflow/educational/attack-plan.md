---
description: Building a detailed plan for our scenario.
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Attack Plan

### How we are going to approach this?

Our goal is to find some form of integer overflow- thankfully, this is a game cheat and game cheat GUIs are ALLLL about numbers. Seriously- just check out this GUI, everything is a number.

* _Local server buffer_
* _Aimbot and geometric configurations_
* _FOV changer is all about camera angles which are floats_
* _Color values which are floats and integers at the same time_
* _Button status which is changeable with other actions_
* _login keys_
* _licenses_
* _admin ids_
* _etc_

So, we are going to try to find the point where numbers could be influenced by a user. Say a user input in the GUI, analyze that user input, see if it does anything with the data and explore from there.

### Kickstarting this&#x20;

if you want, you can try to locate the function that has it by collecting a list of all the user-input related functions and going through all of them one by one and analyzing where their input goes or is stored as we did when we wanted to fully crack the login of the GUI.

### Our plan in detail

Our plan is going to boil down into these components shown below:

* <mark style="color:red;">Where are we looking</mark>: User input functions, specifically ones we have not explored
* <mark style="color:red;">What are we looking for</mark>: Anything to do with user input and operations on that data&#x20;
* <mark style="color:red;">How can we make this easier</mark>: Use pseudocode generators for high-level representations
* <mark style="color:red;">What is our end goal:</mark> Cause a mem leak via IOF or issue resulting in a change on the GUI&#x20;

So we are going to tackle a user input field, convert its entire base to pseudo-code, analyze the psedocode in depth and check for any operations happening on the data from our input.

