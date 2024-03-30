---
cover: ../../../../.gitbook/assets/image.avif
coverY: 0
---

# Example

Before reporting, I figured I would also setup an example of what reporting a flaw would be.

### Scenario

Say in this scenario, we execute REplay and it runs fine! When we start clicking around, specifically around the login area, it crashes and Windows throws a thread instance error. We tried repeating, only to have some repeats work and others not.

### Questions based around scenario

Before we move to reporting, we need to ask ourselves some questions.

* _<mark style="color:red;">Does this impact the user experience</mark> -> Yes this does. If the user comes across this bug, it may prevent any dynamic analysis or any form of exploration. Especially in further levels, such as Level2 where we interact more with the application and require it to be used._\

* _<mark style="color:red;">Does this impact the education of a user</mark> -> This does not directly hurt the education of the user, however, it may make future use of the environment useless thus hindering any further advancements into knowledge or practice areas._\

* _<mark style="color:red;">How can this be fixed</mark> -> This issue is too broad and is dependent on the code structure, routines, and more being used within the program. At this moment, I can not provide a valid fix._\

* <mark style="color:red;">How did this impact my experience</mark> -> _This impacted my experience as I was not able to properly use the application for further advancements into the level._

### Reporting Questions

Now that we have our answers for the questions, we can answer these questions to justify the report.

* Where did it happen -> This happened in the login tab of the application\

* How did it happen     -> By clicking on the login tab, when the tab was rendered, the program crashed.\

* Was it repeatable      -> It was repeatable, but it was quite random and not dependent on any one or multitude of actions made on the applications GUI. \

* <mark style="color:orange;">If you are even nicer of a human</mark> - screenshots of the actual flaw happening -> For this scenario, since its made up we do not have a screenshot. But picture a screenshot of Windows pop up errors.\

* How it may be able to impact others (<mark style="color:purple;">if you are really feeling kind</mark>) -> This can impact others by hindering their capability to properly use and learn from the software. Considering that this becomes an issue during the experience of the user, it may be hard to follow along with writeups properly.\

* How did it impact your experience -> I was not able to properly use or analyze the login tab.\

* How it can be fixed (<mark style="color:purple;">in your opinion, this is optional tho and not necessary</mark>) -> As provided above, no fix is currently avalible.\

* What the issue was -> The issue seems to be in relation to one of the threads either on the GUI side or on the backend portion of the application.&#x20;

\
