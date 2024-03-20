---
cover: ../../../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Known barriers in binary integrity RE

One thing many do forget to account for during their practice in RE is the applications and barriers of their knowledge (extending from CTFs) and the real world.

Here, we teach you how to bypass a very lazily and cheaply made binary integrity system that hardly needs internet connection other than to fetch the remote hash. In the real world- this is not exactly how it works even when they are client side integrity systems. Check out some of the examples below.

* **Server Sided Systems:** Most systems in todays world are server sided. So nothing remains that can be tampered with as far as remote hashes or anything since they are not saved on the system. While there are ways to bypass server side integrity checking (_e.g: where logic for checking the hashes is on the server_) it becomes quite difficult.
* **Signature based:** Many libraries might not be targeting the entire binary, such as this one. And they might not also be using hashes. Instead, they use a mix and mash of algorithms, custom implementations and signatures of specific sections of the binary (_like `.text` which is modifiable_) where they remain encrypted and hidden from plain sight to check the integrity of the binary being run.
* **Dynamic Checkers:** One of the other ways to get around the signature based system depends on how **often** the system checks it. If the system checks it, maybe you can write a program that runs adjacent to the existing program that you want to modify and build an exploit to constantly change those values dynamically. But if you can not attach debuggers and so on from there, it most definitely will become more trivial to do this. Nonetheless, it also depends on the factor that if the system is checking every other second (_which is really irresponsible use of resources to any developer and not worth it_) or if it just checks once the application starts. The idea of having routine checks helps ensure that dynamic and static patches were not made and are not currently being made.

There are some other methods of checking and verifying but these are some massive roadblocks. Can not forget about other various obfuscation techniques and more.&#x20;

