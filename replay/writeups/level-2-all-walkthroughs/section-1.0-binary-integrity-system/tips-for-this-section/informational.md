---
cover: ../../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Informational

In this CTF exists a client-client binary integrity system. This means that the program will be remotely fetching a production hash (placed there by the developers) on a remote server somewhere. Your goal for this section is to...

* 1: Find the remote location where the hash is given
* 2: Find the file that is written to
* 3: Find the hashing algorithm
* 4[: Find out how to bypass the security system to make patches](#user-content-fn-1)[^1]&#x20;

When we do get passed all of this, it will be a bit easier to maneuver to further levels. &#x20;

[^1]: Patches are how we are going to be modifying other values in this system. Since this system was developed poorly, there are multiple ways of doing this.\
    \
    \* Writing to the hash file that was downloaded\
    \
    \* Changing the sleep counter on the thread routine calling the system to a Inf or NaN value\
    \
    \*\
    \
