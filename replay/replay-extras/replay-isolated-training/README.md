---
cover: ../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# REplay - Isolated Training

When reverse engineering applications, you may find yourself stuck occasionally, especially in real world scenarios where the applications might be super complex or just super wonky with the style/flow of the program, you will need to executed isolated training.

### What is isolated training?

Isolating training is where you isolate specific flaws- for example, we create a very simple mock UAF or Use After Free vulnerability in C++. Like the code below.

```cpp
#include <iostream>

int main() {
	int* someage = (int*)malloc(sizeof(int));
	*someage = 5;
	std::cout << "[+] Before free -  " << *someage << std::endl;
	free(someage);
	std::cout << "[-] After free  -  " << *someage << std::endl;
	return 0;
}
```

We then take this code, compile it and toss it into a framework like IDA to give us a good example of how to identify similar patterns. As you get further and further down the line into understanding how to identify these, you will make the code structure more and more complex until you can understand it.&#x20;

When you understand the code enough to recognize what's happening, you can go back to the real world environment and use those skills you developed whilst training in isolation to identify higher and more complex security risks such as the ones studied in isolation.

### How does this help?

Prior developing REplay, I spent a lot of my time in bigger environments right when I started. Sure, it was a great way to throw myself into the weeds and figure it out, but in the long run it hindered me a bit from being able to identify important routines and calls such as `malloc` or `free`.

By training in isolation, or in even much larger environments such as REplay (_but also being able to locate the area of training easily)_ I was not only able to recognize when specific calls were dangerous but also able to discovery and analyze all forms of binary vulnerabilities.

{% hint style="warning" %}
Note that training in isolation, depending on the environment may be hard for you to understand symbol-recognition without automation. This will hinder you later on in environments like REplay which are so big that IDAs mnemonic system might not fully kick in right away- leaving you to discover and analyze these calls on your own.\
\
Alas: in other scenarios, it may be appropriate for you to learn how to analyze these default calls and realize how they are being called and used. You can do this by self building or adding functions like `free` or `malloc` to a massive code base, compiling it, then manually tracing it. Personally, I always like leaving a string that can lead me to tracing these back instantly then being able to analyze standard symbols like `free`.&#x20;
{% endhint %}

## Examples

For this section, I gave you some medium sized examples of what isolated training can look like and represented it in a few small sections.



