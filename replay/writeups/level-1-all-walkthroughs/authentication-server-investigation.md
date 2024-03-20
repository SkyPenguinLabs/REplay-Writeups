---
cover: ../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Authentication Server Investigation

In this application was an authentication server. This server had information that was encrypted and we actually were able to solve it when we solved the CTF information block challenge shown below.

{% content-ref url="find-the-ctf-information-block.md" %}
[find-the-ctf-information-block.md](find-the-ctf-information-block.md)
{% endcontent-ref %}

### What is this?

This page represents all the information such as the authentication server name you need to find in regards to the authentication server in this application. The idea of this is to go back and practice the same skills you used to locate the CTF information block.

Like a head warmer!

### How to solve this?

Dynamically analyze the application using a hex dumping utility like HxD in its active state and use a set of reverse engineering and logical methodologies to find the location of the now decrypted server information.&#x20;

### Answer(s)

If you used the same method as before to get this information, then you should have the same answers as below.

* What is the authentication servers name? -> `auth.server.com`
* What protocol was the server in? -> `HTTP`&#x20;

