---
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Answer Page

### The answer for this section

One of the buffer overflows exists in the following block.

```
loc_140081BD4:          ; Size
mov     ecx, dword ptr [rsp+1D8h+Caption]
call    malloc_viasize
mov     rsi, rax
test    rax, rax
jnz     short loc_140081BF0
```

The reason this block is vulnerable to BOF is because the buffer never accounts for the length or size of the data type of the data being pushed to the buffer. Because of this, the buffer only takes into account the size of the value its going to be putting in rather than the size of the value multiplied by the size of the datatype. So the correct fix would be something like&#x20;

```
mov     ecx, dword ptr [rsp+1D8h+Caption]
mov     eax, 2
mul     rcx                                ; Note this operator that was not there before
cmovo   rax, r15        
mov     rcx, rax
call    malloc_viasize
```
