---
description: >-
  Solves Objective: Find out what the seconds were for the lasting effect of the
  beep.
cover: ../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Exact time length of beep

### What is this?

This objective requires us to find out how the length of all the beeps and sounds that are created in the GUI when the user presses a tab on the **left** side of the interface. This is building off of the same result from [finding-functions-via-sound.md](finding-functions-via-sound.md "mention")

### Answer

Each beep takes or holds exactly `950 ms` or 950 miliseconds. We can verify this by looking at the arguments pushed before the `Beep` call is made. Check the assembly below for a demonstration of this.

> In the `?` tab

```wasm
mov     edx, 3B6h       ; dwDuration <------------\
mov     ecx, 0C8h       ;  dwFreq                  |
call    cs:Beep                                    |__ 0x3B6 is 950 in decimal. Since
                                                       this param is defined in milliseconds
                                                       on the MS documentation. We verify that
                                                       950 milliseconds is the amount of time this takes to execute
```

