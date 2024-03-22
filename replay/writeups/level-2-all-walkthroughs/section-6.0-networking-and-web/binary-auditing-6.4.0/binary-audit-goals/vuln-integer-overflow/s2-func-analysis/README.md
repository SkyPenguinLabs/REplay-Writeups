---
description: Analyzing the input function
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# S2: Func Analysis

As explained in the previous step, [s1-input-analysis](../s1-input-analysis/ "mention"), I assume you already know how to get to the function input using methods that are quite simple (designed like that for ease of access to the routine). With that, you should be in the same area.

<figure><img src="../../../../../../../../.gitbook/assets/FirstShotLocation_Input_REplay_log.png" alt=""><figcaption></figcaption></figure>

## Analyzing the routine

This routine and actually entire area is kinda funky to read. So we are going to go and translate this to Pseudocode. If you are not used to this, despite us doing this once- simply follow the steps below.

* Go to `View` in the top bar of the window
* Open Subviews>Generate Pseudocode&#x20;

or you can use F5.

{% hint style="warning" %}
Sometimes, IDA can give you issues about section read permissions and the format of data. For now, ignore that as it does not cuase much of an issue for us.
{% endhint %}

### Finding a range&#x20;

For us to go deeper into this function, we need to be able to hardfocus on one area. And for us, that is the location of where the condition gets executed if a previous condition gets executed.

> Ring any bells? No?

If it did not ring any bells, basically, we are looking for the condition where if I press a button, the code gets executed.

{% hint style="info" %}
Think of GUIs as one giant while true loop. Code is constantly executing and the only way to prevent widgets from messing up and executing when they are not supposed to- is to make them into conditions. Basically, if the button was pressed, then boom the code is executed. If we did not have a condition to check if the button was pressed or not, the second the button renders, the code would be executed and cause entire rendering issues and even crashes!
{% endhint %}

For that, we are going to be analyzing the pseudocode shown below.

<figure><img src="../../../../../../../../.gitbook/assets/Pseudocode.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
In IDA, pseudocode can become a pain to work with! So, if you really want to focus on the code itself and analyze it, right click on the pseudocode dump and then click on the button that lets you generate an HTML document as said 'generate HTML'. This will produce a syntax highlighted HTML file.&#x20;
{% endhint %}

If you want to copy and paste it, then here is the pseudocode so you can break it down yourself. Personally, I always use an editor inside of a code note to do the documentation as you will see later.

```cpp
if ( !(unsigned __int8)sub_14005C570("Press to get player data", &v194) )
    {
LABEL_92:
      if ( !*(_BYTE *)(*(_QWORD *)(qword_140158EE8 + 16096) + 187i64) )
      {
        v56 = *(_QWORD *)(qword_140158EE8 + 19480);
        if ( v56 )
        {
          if ( !(*(_BYTE *)(*(_QWORD *)(v56 + 8) + 44i64 * *(signed __int16 *)(v56 + 120) + 4) & 8) )
            --*(_DWORD *)(*(_QWORD *)(qword_140158EE8 + 16096) + 240i64);
        }
      }
LABEL_96:
      sub_14006D760();
      goto LABEL_97;
    }
    sub_140036D00(qword_140159B80);
    sub_14005BBD0("Checking username -- ");
    ((void (*)(void))sub_140036DA0)();
    LOBYTE(v49) = 65;
    v50 = sub_1400225D0(&unk_140158DC0, v49);
    v51 = v50;
    if ( v50 == -1 )
    {
      MessageBoxA(0i64, "BADDDD BOY", "info tab (BAD)", 0);
LABEL_91:
      LOBYTE(v52) = 66;
      *(float *)&dword_140155DC4 = (float)(char)(v51 + (unsigned __int64)sub_1400225D0(byte_140158DEA, v52) + 90) * 0.5;
      goto LABEL_92;
    }
    sub_140007220(lpText, (unsigned int)v50);
    v53 = (const CHAR *)lpText;
    if ( v205 > 0xF )
      v53 = lpText[0];
    MessageBoxA(0i64, v53, "info tab (GOODDDDD)", 0);
    v52 = v205;
    if ( v205 <= 0xF )
      goto LABEL_91;
    if ( v205 + 1 < 0x1000
      || (v54 = v205 + 40, v55 = *((_QWORD *)lpText[0] - 1), (unsigned __int64)&lpText[0][-v55 - 8] <= 0x1F) )
    {
      sub_14009014C();
      goto LABEL_91;
    }

```

Now that we have our range, we need to analyze that range, and dig deeper! Lets go down the rabbit hole Allice!&#x20;
