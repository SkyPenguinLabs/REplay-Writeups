---
cover: ../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Answer Page

### Answer for this objective

There were many areas in this playground where checking for proper data and input was important- but the most obvious was the section in the server where the logic was developed for parsing the responses to the server from the client shown in the code below.

```
loc_1400818CE:
lea     rdx, [rdi+rsi]
mov     r8, rax
lea     rcx, [rsp+1D8h+var_78]
call    sub_140009870
nop
mov     [rsp+1D8h+var_150], rbx
lea     r8, [rsp+1D8h+pbBinary]
lea     rdx, [rsp+1D8h+var_78]
lea     rcx, [rsp+1D8h+var_F0]
call    sub_140087260
nop
xorps   xmm0, xmm0
movups  xmmword ptr [rsp+1D8h+lpMultiByteStr], xmm0
mov     [rsp+1D8h+var_100], rbx
mov     [rsp+1D8h+var_F8], rbx
mov     r8d, 5
lea     rdx, aEmail     ; "email"
lea     rcx, [rsp+1D8h+lpMultiByteStr]
call    sub_140009870
lea     rdx, [rsp+1D8h+lpMultiByteStr]
lea     rcx, [rsp+1D8h+var_F0]
call    JSON_ErrorCaller_Unknown
lea     rdx, [rsp+1D8h+var_B8]
mov     rcx, rax
call    JSON_parse
nop
xorps   xmm0, xmm0
movups  xmmword ptr [rsp+1D8h+lpMultiByteStr], xmm0
mov     [rsp+1D8h+var_100], rbx
mov     [rsp+1D8h+var_F8], rbx
mov     r8d, 8
lea     rdx, aPassword  ; "password"
lea     rcx, [rsp+1D8h+lpMultiByteStr]
call    sub_140009870
lea     rdx, [rsp+1D8h+lpMultiByteStr]
lea     rcx, [rsp+1D8h+var_F0]
call    JSON_ErrorCaller_Unknown
lea     rdx, [rsp+1D8h+var_58]
mov     rcx, rax
call    JSON_parse
nop
xorps   xmm0, xmm0
movups  xmmword ptr [rsp+1D8h+lpMultiByteStr], xmm0
mov     [rsp+1D8h+var_100], rbx
mov     [rsp+1D8h+var_F8], rbx
mov     r8d, 7
lea     rdx, aAdminid   ; "adminID"
lea     rcx, [rsp+1D8h+lpMultiByteStr]
call    sub_140009870
lea     rdx, [rsp+1D8h+lpMultiByteStr]
lea     rcx, [rsp+1D8h+var_F0]
call    JSON_ErrorCaller_Unknown
lea     rdx, [rsp+1D8h+var_D8]
mov     rcx, rax
call    JSON_parse
nop
mov     dword ptr [rsp+1D8h+Caption], 3B353C38h
mov     [rsp+1D8h+var_11C], 565754h
mov     [rsp+1D8h+var_118], 1
mov     rcx, rbx
nop     dword ptr [rax+rax+00000000h]
```

Ideally, we would want to scan the entire payload received before doing anything with it or pick it apart space by space or by specific ranges to scan it for malicious input. Of course, we want to type check, whitelist (_not blacklist_), and also want to ensure the payload is actually a valid payload with pattern scanning systems.

