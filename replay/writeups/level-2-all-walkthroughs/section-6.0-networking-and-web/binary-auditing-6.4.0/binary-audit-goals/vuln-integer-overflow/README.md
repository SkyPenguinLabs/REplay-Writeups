---
cover: ../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# Vuln: Integer Overflow

{% hint style="info" %}
If you are not aware of what integer overflows are then refer to [iof-integer-overflow.md](../../information-module/binary-auditing-further-reading/iof-integer-overflow.md "mention") and vice versa for buffer over-runs [bof-buffer-overflow.md](../../information-module/binary-auditing-further-reading/bof-buffer-overflow.md "mention")
{% endhint %}

Oh cmon, we could not possibly leave the Binary Auditing section without some form action!&#x20;

### What is this task?

This task basically asks that we provide the following.

* Location of a integer overflow vulnerability in the application
* Explain why this is dangerous
* Explain what component this affected
* Explain how you know its an integer overflow
* Finally, explain how this can be prevented

There are some more to this, but we will leave it out for this case.&#x20;

{% hint style="warning" %}
A good note to readers, this is a long section- we will be dissecting pseudocode, building a payload to resemble the affects of the IOF and so much more while digging into answers. This section is an entire CTF on its own, so expect to be redirected a lot, and filled with some cool sets of knowledge!
{% endhint %}

Without further todo, lets get into it shall we!

## Binary Auditing - Integer Overflows

Integer overflows are very sneaky- they are a type of flaw and bug in a program that also will not always crash, sometimes- they affect other components behind the scene. Within REplay, I decided to create a pretty decent sized section to demonstrate how integer overflows are more than just a security issue, but can even lead to product misfires!

This section of understanding how to find integer overflows, what goes into them, the different varients, how to analyze them in bigger environments and also build payloads- will all be split up into their own sub-modules defined under this branch.

