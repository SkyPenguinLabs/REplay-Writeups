---
cover: ../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# Vuln: Format String Vuln

### What is this task?

Within the game cheat exists many different binary flaws that you can explore- the most easiest one to discover is going to be a format string bug that exists within the program.

{% hint style="warning" %}
Like web application security, it will take time getting used to fuzzing inputs looking for specific things- so do not feel discouraged if this does not click right away.
{% endhint %}

## Pre game thinking - Logic

Format string vulnerabilities are INSANELY easy to spot out open in the wild and you would be immensely surprised at the amount of GUIs that have faults on this area of things. So, lets kind of pre-game here and think of some ideas of how to spot this. The flow can be broken down into multiple steps.

### **What does a format bug look like on a GUI?**

Well, the format bug is going to be issued when a text call to the GUI is made to render text with a specific formatting, but the formatting is never specified. This allows us to inject characters like `%x` to crawl up the chain gathering bits and pieces of information such as **where** we are and eventually to an exploit if we can find out enough information.&#x20;

Ideally, a string format bug will look like this.

```cpp
				ImGui::Text("Attempt " + i);
				ImGui::NewLine();
				ImGui::Text(input.Password);
```

Libraries like <mark style="color:red;">ImGui</mark> which make text rendering easy usually make you specify a formatting specifier. But because we do not do that here, it becomes a format string bug as the <mark style="color:red;">input.Password</mark> variable is user controlled and not checked or formatted.

A correct example of this would be

```cpp
				ImGui::Text("Last password...:");
				ImGui::NewLine();
				// checking the data type and parsing 
				// the values and what is stored in the buffer
				ImGui::Text("%s" miscConf.Password);
```

specifying that it must be a string.&#x20;

### How do we find these?

Well the main idea would be to first reverse engineer text based calls on the GUI and see if we can find anything of ours. When we find that text function, we would ideally need to analyze it and figure out if its supporting formats or not.

{% hint style="danger" %}
_**In a real world scenario**_, you may best be spending your time just spamming every input you can with format specifiers to see if its vulnerable, then trace the location of that input and analyze the next function.\
\
\> Why trace to the location of the flaw, then analyze the text function?\
\
Truth being told, many applications rely on more than just one text function- maybe due to the fact that one text function is for basic fonts while the other may use a more advanced font or setup requirement. Either way, GUIs are complex- and because of that, it is crucial that we understand the importance of reverse engineering all the functions we can, and being able to pinpoint **where** a flaw might be happening statically. If we can do this dynamically- even better.
{% endhint %}



