---
cover: ../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# DOUF - Double Free

{% hint style="info" %}
This is why we should not copy/paste code. If we copy and paste lines of code, there is a chance we might get distracted and miss making the appropriate changes not only making a nightmare for debugging but also a security issue!
{% endhint %}

### What is it?

Double free is essentially taking a block of memory and freeing it more than once. This can become an issue because we are telling the program that it must free a block of memory that no longer exists in its state.

### How is it a security risk?

Basically, by freeing the same chunk twice and then reallocating it, the freed chunk's user data is overwritten with the pointer. When an attacker such as ourselves who wants to get deep inside starts writing data into the reallocated chunk, it will constantly overwrite the pointer of the previously freed chunk which will then allow the attacker to control where the next chunk is allocated by manipulating the data within the realloacted chunk.&#x20;

That is a pretty base rundown, super bleak, ik- binary exploitation as mentioned in [warning.md](warning.md "mention") is not my fancy field of the century.

### How can it be prevented?

Just ensure that you are not freeing the same block of memory twice.
