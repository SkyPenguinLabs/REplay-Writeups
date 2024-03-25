---
cover: ../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# S2: Analyzing the command exec

Analyzing the command execution step is literally the most simple thing in the world. Shown below is the code for the execution step.

```cpp
      sub_1400093C0(lpText, " && echo your key is && pause", 29i64);
      v58 = lpText;
      if ( *(&v209 + 1) > 0xFui64 )
        v58 = lpText[0];
      system(v58);
```

As you can see, the variable `v58` is the exact value of <mark style="color:purple;">lpText</mark> which was our initial command. After a check is done to ensure the stability of the value, we make a call to the system import and push `v58` into it as the argument.

