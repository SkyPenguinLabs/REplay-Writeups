---
cover: ../../.gitbook/assets/B2 (1).PNG
coverY: 424.39654893065466
---

# Level 1

This is the easiest and by far most beginner level that this playground has to offer. This level is composed with over 12 questions (**a total of 14 questions**) and 15 objectives (**one more objective that was not a question**).

Below are some sets of information for this level.

> ### Goals / Objectives

* 1: Find the unencrypted API key
* 2: Find the HTTP-BasicAuth formatted username and password
* 3: Find the CTF information block
* 4: Find the encrypted API key
* 5: Crack the first login system
* 6: Modify the variable of the hide menu functionality
* 7: What was the authentication servers name?&#x20;
* 8: Find out what protocol was the authentication server in
* 9: Find out what security systems were used in this CTF
* 10: Figure out a base map of the control flow in the programs first login system. Draw out a pseudo code example of how this works.
* 11: Find the integer based key used to compare the input license in the GUI.
* 12: Figure out where the pre-determined login statement is being made. This is the statement in which is outputted or drawn onto the GUI before the login button and the input box are rendered.
* 13: Find the hotkey that is used to exit the menu and kill the current process
* 14: Crack the login system, do not just make it output that you were logged in

> ### Questions

&#x20;    **Question 1**: What was the unencrypted & plaintext CTF key?

&#x20;    **Question 2**: What was the basic authentication username and password?

&#x20;    **Question 3**: What was the primary API key found dynamically?&#x20;

&#x20;    **Question 4**: What was the information block of the CTF?

&#x20;    **Question 5**: The first log in was crackable in two ways. One of those ways was to switch the logic of the program around. What did you need to do in order to switch it? Answer format - `I changed x to x at` where x is the instructions. Tip: there is a difference between switching the logic and changing the status of a status-variable within the program :D

&#x20;    **Question 6**: What security systems were used in this CTF?

&#x20;    **Question 7**: What was the authentication server where the HTTP auth was used?

&#x20;    **Question 8**: What protocol was the authentication server in?

&#x20;    **Question 9**: On the first login attempt, you may have noticed that the application already outputted that the login failed without you doing anything. What does this mean?

&#x20;    **Question 10**: (**Difficult for beginners**) In the login system, there is no plaintext key that you can see. Instead, the key was integer-based. How did this key system work, what did it do, what was the value(s) of the key, and what was the final string key?

&#x20;    **Question 12**: What `.text` address held the location of the comparison for the logged-in variable? Remember that this was the pre-set variable that was checked before the initial state of both the input and the button are rendered on the GUI. Tell me how you know this :D

&#x20;     **Question 13**: What key was needed to exit and close the game cheat?

&#x20;     **Question 14**: Question #5 was a loop hole, you got the program to say you were logged in, but were never actually logged in. In order to fully make the program show you are logged in, you had to go down a rabbit hole to find some function that was returning a global status. This status was used every time you clicked a button, a new tab, etc that always checked the login status (which is the global status). What did you do to crack the login system to always render you as true? Note: you should also explain how the system works

> ### Required Experience

Many people think that there is required experience for these kinds of things. We think the opposite. This level was designed to toss people into the deep end and let them swim! But really, it is best to have some fundamentals or ideas down- check the list below.

* Knowledge of frameworks like IDA
* Static & Dynamic Analysis Techniques
* Fundamentals of reverse engineering
* Conceptual logic
* Basic Computer Science



