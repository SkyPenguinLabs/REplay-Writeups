---
description: how, what, why
cover: ../../../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Methodology/Theory

When I was teaching a few people how to get around this, gaining or obtaining the theory was a bit hard to grasp so I felt providing it here would provide much more value to readers or users of the playground!

> How will we locate the system?

Locating the security system purely depends on the environment you are in. Since we are looking for a binary integrity system, we are going to be looking out for many different things. Check the list below for some example checks.

* Remote resources that may contain production hashes
* Hardcoded value or data that may be encrypted (e.g.: of a specific length)
* Static imports or Windows API calls for cryptographic functions
* Module imports that may be third party for cryptographic operations
* Other APIs or system calls used in conjunction with the system
* Plaintext commands or plaintext HTTP information
* File operations (if the system is client side)

and some other things as time goes on. This list is pretty comprehensive for this scope, so as you notice we will narrow it down a bit and follow a very specific methodology but you get the idea.

> What are we looking for specifically?

We are looking for a binary integrity system. This is a system that is either using cryptographic or signature based verification on the current application. In many of these applications, especially cryptographic comparisons, the program will usually try to "hash itself" to grab the current hash of a specific section or the entire program. This means that function calls like `GetModuleFileNameA` are going to be used to get the current filename and format it into a system path to pass off into a internal function that will be hashing the current program being run or module being run that needs to be checked.

> Why?

Binary integrity systems will put a dent in a lot of your work that revolves around software cracking or even base modifcations to products and further reverse engineering / tampering. Learning how to bypass different systems is definitely essential.

