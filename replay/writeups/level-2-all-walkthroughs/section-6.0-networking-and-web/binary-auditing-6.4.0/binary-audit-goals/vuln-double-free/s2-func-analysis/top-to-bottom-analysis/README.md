---
description: Analyzing the pseudocode from top to bottom (sub_140022130)
cover: ../../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Top To Bottom Analysis

## Psuedo-code generated

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

### Analyzing The Loops

The loop first starts off where we are basically saying that we are going to iterate over _v10_ which becomes a pointer to v9 until a null termination is met.&#x20;

{% hint style="info" %}
In memory, C styled strings are stored as contiguous sequences of characters followed by a null terminator. This null terminator is mostly used in loops where we need to know when the end of the string is to tell the program to jump out of the loop and continue execution.
{% endhint %}

With that note in mind, the following condition shown below is represented in Python

```cpp
  do
    ++v1;
  while ( InputData[v1] );
```

> Python

```python
    while InputData[v1] != '\0':
        v1 += 1
    return InputData[:v1]
```

Basically, it reads characters from our input string stored in `InputData` until it encounters the null character `'\0'`.&#x20;

> Summary of the loop and why its important&#x20;

This part is important because we might be actually analyzing the part of the function that is taking the input data and copying it to the buffer. If you do some good standard [replay-isolated-training](../../../../../../../../replay-extras/replay-isolated-training/ "mention") then you can find out that most functions like `strcpy` act like this.

## Analyzing The Result Conds

Analyzing the conditions that determine the result is most definitely what we want. This is because, if we can analyze how the function works we can also understand where the crash is happening and how the Double Free is a problem in the program.

### Code

For this portion of this page, we will be analyzing this routine code.  This code is what influences the return value and also what influences the result we are expecting on our screen.

```cpp
sub_140009870(&Memory, InputData, v1);
  v10 = v23;
  v11 = &Memory;
  v12 = Memory;
  if ( v23 > 0xF )
    v11 = (__int128 *)Memory;
  if ( v22 >= 5 && (v13 = (__int64)v11 + v22, (v14 = sub_1400C22A0(v11, 104i64, v22 - 4)) != 0) )
  {
    while ( *(_DWORD *)v14 != 1886680168 || *(_BYTE *)(v14 + 4) != 115 )
    {
      v14 = sub_1400C22A0(v14 + 1, 104i64, v13 - 4 - (v14 + 1));
      if ( !v14 )
        goto LABEL_18;
    }
    free(v6);
    if ( v14 - (_QWORD)v11 != -1 )
    {
      free(v6);
      v16 = 1;                                  // // Good, assign true
      goto LABEL_20;
    }
  }
  else
  {
LABEL_18:
    free(v6);
  }
  v16 = 0;                                      // false (error code)
LABEL_20:
  if ( v10 > 0xF )
  {
    v17 = v12;
    if ( v10 + 1 >= 0x1000 )
    {
      v12 = *(_QWORD *)(v12 - 8);
      if ( (unsigned __int64)(v17 - v12 - 8) > 0x1F )
        sub_140097A3C(v15, v10 + 40);
    }
    j_j_free(v12);
  }
  return v16;
}
```

### Laying out what we know for analysis

In order to analyze this function- we should have a good understanding of the behavior. Check out the small points below that can lay this out for us.

* <mark style="color:red;">The function is returning a boolean</mark>: Analyzing the way the function is being called, and also analyzing the return value of the above source code indicates that the single character result is actually a Boolean true or false value.
* <mark style="color:red;">The function does not crash when the data is invalid</mark>: This tells us the double free only happens in the condition where the characters are checked and the result is read (_either within another function or the one we are analyzing_)

This will help us narrow down what we need to analyze. For the sake of this writeup and extra space, I was able to cut it down to the brick of code below which we will be analyzing.

```cpp
sub_140009870(&Memory, InputData, v1);
  v10 = v23;
  v11 = &Memory;
  v12 = Memory;
  if ( v23 > 0xF )
    v11 = (__int128 *)Memory;
  if ( v22 >= 5 && (v13 = (__int64)v11 + v22, (v14 = sub_1400C22A0(v11, 104i64, v22 - 4)) != 0) )
  {
    while ( *(_DWORD *)v14 != 1886680168 || *(_BYTE *)(v14 + 4) != 115 )
    {
      v14 = sub_1400C22A0(v14 + 1, 104i64, v13 - 4 - (v14 + 1));
      if ( !v14 )
        goto LABEL_18;
    }
    free(v6);
    if ( v14 - (_QWORD)v11 != -1 )
    {
      free(v6);
      v16 = 1;                                  // // Good, assign true
      goto LABEL_20;
    }
  }
  else
  {
LABEL_18:
    free(v6);
  }
  v16 = 0;                                      // false (error code)
```

As you can see there are already notes.

### Analyzing the code

The code we have above is pretty easy to read mainly towards the end and is confusing at the top. Firstg **let me declare the obvious**.

* `v16` -> This is the variable that holds our return status. The return status is 0 if the condition failed triggering the error response. If the condition is true and the character was found, the buffer is freed and then <mark style="color:red;">v16</mark> gets assigned 1 meaning true and to execute the commands (_also as we saw_).
* `There are more than two calls to free with the same buffer`: This should not really happen with the same value within as close proximity as they are- or even just at all, especially if a crash is happening. If you notice, <mark style="color:red;">free</mark> is getting called with `free(v6)` which is the buffer that holds our string.

Now, lets focus on the main routine, where the weird brainfucky shit is happening shown below.

```cpp
sub_140009870(&Memory, InputData, v1);
  v10 = v23;
  v11 = &Memory;
  v12 = Memory;
  if ( v23 > 0xF )
    v11 = (__int128 *)Memory;
  if ( v22 >= 5 && (v13 = (__int64)v11 + v22, (v14 = sub_1400C22A0(v11, 104i64, v22 - 4)) != 0) )
  {
    while ( *(_DWORD *)v14 != 1886680168 || *(_BYTE *)(v14 + 4) != 115 )
    {
      v14 = sub_1400C22A0(v14 + 1, 104i64, v13 - 4 - (v14 + 1));
      if ( !v14 )
        goto LABEL_18;
    }
    free(v6);
    if ( v14 - (_QWORD)v11 != -1 )
    {
      free(v6);
      v16 = 1;                                  // // Good, assign true
      goto LABEL_20;
    }
  }
  else
```

For the sake of this CTF, I have moved this analysis to its own page to explain the brainfuck that is the pseudocode analysis.

{% content-ref url="deep-analysis/" %}
[deep-analysis](deep-analysis/)
{% endcontent-ref %}
