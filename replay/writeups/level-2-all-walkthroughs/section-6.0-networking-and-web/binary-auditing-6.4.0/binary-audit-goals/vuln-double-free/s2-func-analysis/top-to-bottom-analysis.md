---
description: Analyzing the pseudocode from top to bottom (sub_140022130)
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Top To Bottom Analysis

### Psuedo-code generated

```cpp
char __fastcall sub_140022130(char *a1)
{
  signed __int64 v1; // rbx
  char *InputData; // rdi
  signed __int64 v3; // rcx
  unsigned __int8 v4; // cf
  void *v5; // rcx
  _BYTE *v6; // rax
  _BYTE *v7; // rsi
  char *v9; // rcx
  char v10; // al
  unsigned __int64 v11; // r15
  __int128 *v12; // rbp
  __int64 v13; // rdi
  __int64 v14; // r14
  __int64 v15; // rbx
  __int64 v16; // rcx
  char v17; // bl
  __int64 v18; // rax
  __int128 v19; // [rsp+28h] [rbp-60h]
  const char *v20; // [rsp+38h] [rbp-50h]
  char v21; // [rsp+40h] [rbp-48h]
  __int128 v22; // [rsp+48h] [rbp-40h]
  unsigned __int64 v23; // [rsp+58h] [rbp-30h]
  unsigned __int64 v24; // [rsp+60h] [rbp-28h]

  v1 = -1i64;
  InputData = a1;                               // was v2
  v3 = -1i64;
  do
    ++v3;
  while ( InputData[v3] );
  v4 = __CFADD__(v3, 1i64);
  v5 = (void *)(v3 + 1);
  if ( v4 )
    v5 = (void *)-1i64;
  malloc(v5);                                   // was sub_14009B290
                                                // 
  v7 = v6;
  if ( !v6 )
  {
    v21 = 1;
    v20 = "Memory alloc failed";
    v19 = 0i64;
    sub_140092628(&v20, &v19);
    sub_1400926B8(&v19);
    return 0;
  }
  v9 = InputData;
  do
  {
    v10 = *v9;
    v9[v7 - InputData] = *v9;
    ++v9;
  }
  while ( v10 );
  v22 = 0i64;
  v23 = 0i64;
  v24 = 0i64;
  do
    ++v1;
  while ( InputData[v1] );
  sub_140009870(&v22, InputData, v1);
  v11 = v24;
  v12 = &v22;
  v13 = v22;
  if ( v24 > 0xF )
    v12 = (__int128 *)v22;
  if ( v23 >= 5 && (v14 = (__int64)v12 + v23, (v15 = sub_1400C22A0(v12, 104i64, v23 - 4)) != 0) )
  {
    while ( *(_DWORD *)v15 != 1886680168 || *(_BYTE *)(v15 + 4) != 115 )
    {
      v15 = sub_1400C22A0(v15 + 1, 104i64, v14 - 4 - (v15 + 1));
      if ( !v15 )
        goto LABEL_18;
    }
    free(v7);
    if ( v15 - (_QWORD)v12 != -1 )
    {
      free(v7);
      v17 = 1;
      goto LABEL_20;
    }
  }
  else
  {
LABEL_18:
    free(v7);
  }
  v17 = 0;
LABEL_20:
  if ( v11 > 0xF )
  {
    v18 = v13;
    if ( v11 + 1 >= 0x1000 )
    {
      v13 = *(_QWORD *)(v13 - 8);
      if ( (unsigned __int64)(v18 - v13 - 8) > 0x1F )
        sub_140097A3C(v16, v11 + 40);
    }
    j_j_Free(v13);
  }
  return v17;
}
```

### Analysis

In the first half, the one thing I want you to pay attention to is the assignment and movement of the function argument. Lets analyze this small snippet and chomped snippet of code.&#x20;

```cpp
char __fastcall sub_140022130(char *a1)
{  
  signed __int64 v1; // rbx
  char *v2; // rdi
  v1 = -1i64;
  v2 = a1; // (this is now InputData) 
  //other arguments
  //code
}
```

If you follow where `*a1` and `*v2` are going, you end up understanding that the input data is in fact a  character and is actually similar to the data we saw when our input was being gathered. From there, if you click on _v2 (or InputData)_, you see that it is being used in many loop related contexts. For example,  the brick below is where the character variable (_v2/InputData_) is being used in a loop. Lets check the code.&#x20;

```cpp
  v9 = InputData;
  do
  {
    v10 = *v9;
    v9[v7 - InputData] = *v9;
    ++v9;
  }
  while ( v10 );
  v22 = 0i64;
  v23 = 0i64;
  v24 = 0i64;
  do
    ++v1;
  while ( InputData[v1] );
```

This tells us one thing for certain

* **This program is pretty much copying a null-terminated string**

There are a few things that pinpoint this to me and they are shown in their own sections below.

#### The loop

The loop first starts off where we are basically saying that&#x20;
