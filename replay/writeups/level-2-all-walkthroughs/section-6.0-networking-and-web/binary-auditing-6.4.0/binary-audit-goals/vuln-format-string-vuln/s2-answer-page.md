---
cover: ../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# S2: Answer Page

Figuring this out was not so hard- check out the answers below.

> Identification & Explanation of Findings

The program is vulnerable to a string formatting vulnerability when the user inputs their password- this is because, unlike static text being pushed to "_ImGui\_Text_" call functions (**since they do not need one and can not be changed**), one function, specifically the one that outputs the user input onto the GUI- requires a format specifier.&#x20;

If there is no format specifier or proper security checks for input handling, then the program will result in faults and exposure of internal information (such as stack values) that can be further leveraged to exploitation.

> Proof

The proof lies in this code brick shown below.

```
call    sub_14005E9C0
mov     rcx, cs:qword_14015AC60
call    sub_140036AE0
lea     rcx, aLastPassword ; "Last password...:"
call    ImGui_Text
call    sub_14005E9C0
mov     rcx, rdi
call    ImGui_Text
```

Specifically in the last two lines.

```
mov     rcx, rdi
call    ImGui_Text
```

Because no format specifier is loaded, and the user input is immediately taken from the input scanner and thrown into the GUI text function. Because there is no checking or sanitization prior, the function pretty much lets users input anything they want- including formatting symbols such as `%x` or `%p`.

