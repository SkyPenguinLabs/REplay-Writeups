---
description: 'Solves Objective: Find out what frequency the beeps are'
cover: ../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Beep frequency

### What is this?

This objective requires us to find the frequency that the beeps for the tabs are using measured in hertz. This is building off of the same result from [finding-functions-via-sound.md](finding-functions-via-sound.md "mention")

### Answer

If we analyze this block

```
mov     edx, 3B6h       ; dwDuration
mov     ecx, 0C8h       ; dwFreq
call    cs:Beep
mov     cs:dword_140156D58, 13h
```

We see that the value of the `dwFreq` argument is `0x0C8`. Converting this to decimal we have 200 as the result.&#x20;

> Summary

The answer to this is that this function, as well as all other beeps (_which we can verify by analyzing other blocks of tabs that use the beep function or condition_) have a frequency of `200 hz`.
