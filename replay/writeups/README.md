---
cover: ../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Writeups

This section is going to be writeups based on the levels. Each level will have a new description- however, there is a lot of how-to more than there is theory based knowledge. If you do not have the proper and fundamental theory on reverse engineering, then you can check out some of the blogs I (Totally\_Not\_A\_Haxxer) have written for theory and conceptual logic applications to reverse engineering.

### Resources To Get Started Written By Me

* Getting Started In RE: [https://medium.com/@Totally\_Not\_A\_Haxxer/reverse-engineering-getting-started-801a6ad3a5be](https://medium.com/@Totally\_Not\_A\_Haxxer/reverse-engineering-getting-started-801a6ad3a5be)\

* Reverse Engineering: Binary Security: [https://medium.com/@Totally\_Not\_A\_Haxxer/reverse-engineering-binary-security-fb62129b773f](https://medium.com/@Totally\_Not\_A\_Haxxer/reverse-engineering-binary-security-fb62129b773f)\

* Reverse Engineering: Cracking Code: [https://read.martiandefense.llc/reverse-engineering-cracking-code-218304fcc1ad](https://read.martiandefense.llc/reverse-engineering-cracking-code-218304fcc1ad)\

* Reverse Engineering: Conceptual Logic: [https://read.martiandefense.llc/reverse-engineering-conceptual-logic-bf64cca5cc8](https://read.martiandefense.llc/reverse-engineering-conceptual-logic-bf64cca5cc8)

## IMPORTANT NOTE

**most** of what we use here is going to be IDA-Pro 7.0. However, you can use whatever framework you want including custom made frameworks.

Since this CTF is a playground which has many different anti-debug techniques, we will mainly be using **static analysis** to hunt down information in the program. While there is **some** dynamic analysis and dynamic parts to this its worth noting that most patching, modifications, etc are all done to the program statically.
