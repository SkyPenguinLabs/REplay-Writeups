---
cover: ../../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# UAF - Use After Free

### What is it?

[User after free](https://learn.snyk.io/lesson/use-after-free/) vulnerabilities are pretty much just a security risk that involves using memory after it has been freed. For example, using the result of a `malloc` call after it has been freed using function calls such as `free()` .

### Why is this a security risk?

Use after free is considered a security risk because if memory is used after it has been freed, an attacker can locate this freed memory and execute arbitrary code inside of it. Think of it as an open door to a room that should be full of stuff but isn't- because this room is not full of stuff the attacker can walk in and push whatever they want into that room, even if it is malicious.

### How can this be leveraged?

Use after free vulnerabilities can be quite complex to tackle, but initially, to anyone with seasoned experience- all they need to do is trace and gain control over the freed memory. From there, the attacker can redirect the programs control flow (_meaning execution flow, not logic control flow, my bad for shitty terms_) to execute the code that they have injected. This then allows attackers to gain remote code execution on the machine and a plethora of other things.

