---
cover: ../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Find the integer based key used to compare the input license in the GUI.

## What is this task?

Basically, when you press the Login button on the GUI, the program takes your input and checks it with a hardcoded key value. This value, in the program, sits as a hex value.

I will leave this one up to you considering the skills you have if you have gotten this far- but the answer will still be shown here.

### Answer

The string version of the key is '`__OfF8#K#kkkk___Dldldldl'` while the hex value was a set of hexadecimal numbers which are in the code block below. The way the system worked was it would take the input of integers and then convert them to their ASCII values making the final key.

```crystal
0x5f,0x5f,0x4f,0x66,0x46,0x38,
0x23,0x4b,0x23,0x6b,0x6b,0x6b,
0x6b,0x5f,0x5f,0x5f,0x44,0x6c,
0x64,0x6c,0x64,0x6c,0x64,0x6c 
```

