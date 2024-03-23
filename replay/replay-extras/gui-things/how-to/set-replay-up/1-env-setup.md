---
cover: ../../../../../.gitbook/assets/image.avif
coverY: 0
---

# 1: Env Setup

When I was on my main machine as I could not work on a VM during testing, I ended up creating an isolated directory that worked like this.

{% hint style="danger" %}
Note that when you do run REplay, but default, I do not expect for you to have `client.dll.json` and `offsets.json` as the authentic files just laying around. So REplay has a condition at the beginning to generate the files if they do not exist. This is shown in - [file-generation](../navigate/technical/file-generation/ "mention")
{% endhint %}

```
├───DLLs
│       ucrtbase.dll                        // EXTERNAL TO REplay (IGNORE)
│
├───REplay
│       client.dll.json                     <- required || generated if it does not already exists (PROGRAM RESTART REQUIRED)
│       offsets.json                        <- required || generated if it does not already exist (PROGRAM RESTART REQUIRED)
|       imgui.ini                           <- generated 
│       SkyOverlay.exe                      <- Shipped as standard, EXE for REplay
│
└───_____UNKOWN_DIR_____
        index.html                          <- Comes shipped with level 2 of REplay 
```

With this in mind, it is suggested that you follow the same flow as we do here. We have it isolated in one root directory called `CTF_ENV` where `CTF_ENV` includes all of the files you saw right there above.&#x20;

### Why is this environment suggested to prevent bugs?

{% hint style="warning" %}
This portion definitely spoils a lot about the CTF
{% endhint %}

In many points, the CTF needs to access files in a directory one step down from the current directory (_as its hardcoded_) and then also need to re-open files in the same current directory. So it is important that to save your progress and prevent bugs when exploring other levels that you ensure the environment is isolated.

When you have your environment setup, you should be able to move onto the next step which is letting REplay go through its first cycle - [2-running-replay.md](2-running-replay.md "mention").&#x20;
