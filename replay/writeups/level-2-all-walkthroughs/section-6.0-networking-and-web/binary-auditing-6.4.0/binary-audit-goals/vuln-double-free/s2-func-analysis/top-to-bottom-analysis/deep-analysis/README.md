---
description: Deep analysis on the pseudo-code we found
cover: ../../../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Deep Analysis

## Learning Steps

### What is it?

Deep analysis is exactly what it sounds- taking a component and deeply analyzing it. In the case of pseudo-code, we can take a very specific section of the generation and analyze it as deeply as we can (_which includes dissecting other functions if need be_) and see what we can figure out about the function we are most interested in.

### My analysis methods

Everyone's method of dissecting, labeling, and analyzing functions is going to be different. Some like to go really unique and make their own style while others may just stick to basic annotation, note keeping and more.

For me, I am a bit of a nerd and like using my own method and dissective representations to breakdown specific pieces of logic and data flow throughout the code.

{% hint style="info" %}
Because I am using my own analysis method, you do not need to learn mine as I will explain what it all means when I go through it.&#x20;
{% endhint %}

### Is It Necessary?

Deep analysis takes loads of time if you are new to that specific environment. So deep analysis really only becomes **most** practical when you have a function that actually holds a heavy amount of worth. This includes threading systems, any weird or suspicious non-standard functions, and something relative to what you are looking for. That is the case with this function.

* [x] It is where our input data is
* [x] It is where the program seems to crash
* [x] It is checked after being called and has an error statement
* [x] It is relevant to what we are exploring (faults via crashes)
* [x] It is also a function that holds worth and value to our exploration

## Deep Analysis On The Function

Kicking this right off the bat for where it needs to be- we can have a tasty look at my analysis I got wounded up!

<figure><img src="../../../../../../../../../../.gitbook/assets/PseudoCodeAnalysis (2).png" alt=""><figcaption></figcaption></figure>

Okay, honest impressions- Its a brainfuck, I know- so lets explore it.

> Color key

* <mark style="color:red;">Red</mark>        -> Important
* <mark style="color:yellow;">Yellow</mark>    -> Semi important / informal
* <mark style="color:blue;">Blue</mark>        -> Informational but external
* <mark style="color:green;">Green</mark>     -> information but relevant to data flow

While there were other important highlight here, I wanted to make sure it was as easy to read without all the lines everywhere so I just left the other dissections alone.

### Breaking down the main code section.

The main code section is the code section I did not highlight in the image. The reason I did that is so that we can explore the pseudocode a bit deeper. The code below is annotated with a higher logical representation

```cpp
  v10 = v23;                                                                                                     |                                             +
  v11 = &Memory;                                                                                                 |                                        (0x70747468) -> ptth   (0x73) -> 's' = https
  v12 = Memory;                                                                                                  |                                             |                 |
  if ( v23 > 0xF )                                                                                               |                                        1886680168            115
    v11 = Memory;                                                                                                |                                       _____________________  
  if ( v22 >= 5 && (v13 = v11 + v22, (v14 = sub_1400C22A0(v11, 104i64, v22 - 4)) != 0) ) {                       | <- [important(C)]                     ^    ___ || = OR       ^
    while ( *v14 != 1886680168 || *(v14 + 4) != 115 ) {                                                          | <- [important(B)] COND                ^    ^                 ^
      v14 = sub_1400C22A0(v14 + 1, 104i64, v13 - 4 - (v14 + 1));                                                 | <- [important(A)]|    \ if (v14 != "http" || *(v14 + 4) != "s") -> do {
                                                                                                                 |                  |---->|     sub_1400C22A0(v14 + 1, 104i64, v13 - 4 - (v14 + 1))---\
      if ( !v14 ) {                                                                                              |                  |     |     inc v14 by 1;                         <- changes this |    
                                                                                                                 |                  |     |  
```

&#x20;This brick of code is basically checking for characters `https` while itterating over the value and setting a multitude of conditions to trigger different return statuses. We know that this in fact checking for characters HTTPS because in the while loop shown below, the decimal values can be converted to ASCII representation.

```
while ( *v14 != 1886680168 || *(v14 + 4) != 115 ) { 
________________|                            |__________________________
hex (0x70747468) -> 0x70 (p), 0x74 (t)                    hex (0x73) -> 's'
                    0x74 (t), 0x68 (h)
                                
```

For this, we put it all together and get - "`https`" which is good because this means we are in fact checking if the string includes this (_as we proofed with the tests_).

## Now what? - Answer page

Well now we can actually analyze the results and the conditions to see exactly how the DOUF was found.

{% content-ref url="douf-explanation.md" %}
[douf-explanation.md](douf-explanation.md)
{% endcontent-ref %}
