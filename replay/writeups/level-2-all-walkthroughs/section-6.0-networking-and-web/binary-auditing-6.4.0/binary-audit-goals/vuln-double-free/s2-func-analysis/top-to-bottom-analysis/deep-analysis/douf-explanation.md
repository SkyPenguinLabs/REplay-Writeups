---
description: Answer page
cover: ../../../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# DOUF Explanation

To cut this right in half here and save more time than was already wasted, this program is vulnerable to a double free vulnerability which happens when the program returns a true status indicating the string "https" existed within the parsed and given input.

> The flaw (source)

```cpp
    while ( *v14 != 0x70747468 || *(v14 + 4) != 115 )
    {
      v14 = sub_1400C22A0(v14 + 1, 104i64, v13 - 4 - (v14 + 1));
      if ( !v14 )
        goto LABEL_18;
    }
    free(v6);
    if ( v14 - v11 != -1 )
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

As you can see by reading the code, the function `free` is being called multiple times on the same exact memory location.

> Execution and Bug flow (_proof via src_)

You see, when the function realizes that `v14` or our input data does not have the phrase "_https_" the program returns a true value by assigning `v16 = 0`. Before the value is set to 0, the value `v6` is freed only once.

However, if you look to see the condition below which checks if the result of function at <mark style="color:red;">v14</mark> did not fail, you see a different story.&#x20;

```cpp
    free(v6);
    if ( v14 - v11 != -1 )
    {
      free(v6);
      v16 = 1;                                  // // Good, assign true
```

As you can see, before the condition happens, the buffer or memory allocated at <mark style="color:red;">v6</mark> is being freed. Then _AGAIN_ once the condition is true, the condition executes to free the buffer once again. Note that v6 holds the allocated memory (_buffer for this case_) and then assigns <mark style="color:red;">v16</mark> which is the return value to <mark style="color:green;">1</mark> or <mark style="color:green;">true</mark>.&#x20;

When the function returns true and frees <mark style="color:red;">v6</mark> twice, the program will crash shortly after the function returns.&#x20;

> In order to exploit this ...

In order to exploit the flaw, an attacker would need to craft a malicious payload that is able to trigger the condition and trick the program into crashing once it hits the free calls and has accepted that the string includes <mark style="color:red;">https</mark>.&#x20;

{% hint style="info" %}
this means that when the attacker is crafting their payload, they will have to include https somewhere within the input.
{% endhint %}



