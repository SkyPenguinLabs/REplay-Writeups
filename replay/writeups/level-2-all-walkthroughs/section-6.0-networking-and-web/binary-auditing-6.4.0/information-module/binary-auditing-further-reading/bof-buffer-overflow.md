---
cover: ../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# BOF - Buffer Overflow

Buffer overflows are known as one of the more common types of binary vulnerabilities- as even with modern compiler protections, it is still relatively easy to make a mistake especially when operating with specific and more complex/intricate data types!

### Why is this a security risk?

Buffer overflows happen when a static buffer becomes overflowed with data. For example, a static buffer to old the name of a player in a game- if the name of the player overflows a specific limit such as `43` characters and the length is not checked, a attacker could easily make their username 45 characters and overflow the buffer causing a crash.

Ideally, when the attacker can trace back this crash in the program (either by reading crash logs, debugging, and more) they can then go further by developing shellcode that they can inject into the buffer.

Because an attacker can gain control over the program simply by overwriting the buffer, this allows attackers great amount of leverage for getting code execution on a machine or environment hosting the vulnerable application. &#x20;

### How can this be leveraged?

The exploitation process for buffer overflows can vary drastically depending on the scenario you are in. However, the idea is still the same. Overflow a buffer and overwrite adjacent memory locations, including the return address or function pointers. Because the attacker has over-written the return address, they now can (_with specific payload techniques_) craft payloads that can redirect the execution flow and state of the program to execute the malicious payload injected into the program.



###
