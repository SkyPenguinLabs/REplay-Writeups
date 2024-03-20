---
description: 'Solves Objective: Find out how the Beeps are created'
cover: ../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Beep creation

### What is this?

This objective requires us to find out how the beeps and sounds are created in the GUI. This is building off of the same result from [finding-functions-via-sound.md](finding-functions-via-sound.md "mention")

### Answer

This program uses the Windows API `Beep()` function. As analyzed in the import table and verified by analyzing the disassembly of the individual tabs. Code example below.

```
mov     edx, 3B6h       ; dwDuration
mov     ecx, 0C8h       ; dwFreq
call    cs:Beep <-----------------------|
mov     cs:dword_140156D58, 13h         | Windows API call imported from Kernel32
                                        | https://learn.microsoft.com/en-us/windows/win32/api/utilapiset/nf-utilapiset-beep
```

