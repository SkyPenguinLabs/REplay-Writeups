---
cover: ../../../../.gitbook/assets/image.avif
coverY: 0
---

# Finding Issues

If you find an issue in REplay, I would hope that out of good love and respect for the community, you report the issue and explain how it impacts the education of the players.&#x20;

## Reporting flaws&#x20;

This application was built and designed to help educate the people starting out in reverse engineering who also want to grasp <mark style="color:red;">'real world'</mark>. To ensure quality in production, I want to make sure not ONLY the UX (_<mark style="color:red;">User Experience</mark>_) is amazing, but the writeups, the explanations, and more are as thorough as possible and I can easily do that with community suggestions and it is nice to have them!

### What defines an issue?

REplay was also designed to be vulnerable from design, its not a product, so we want to make sure the issues you find are inside the issue scope which is pretty much anything involving the playground itself that ruins the UX (<mark style="color:red;">User Experience</mark>).&#x20;

**For example:** If you come across an error when rendering the GUI or trying to run the app dynamically and can not find a plausible fixing page for it like the ones defined in [error-handle](../../gui-things/how-to/error-handle/ "mention"), then I will welcome a report for this and make a change to this Gitbook and this Gitbook only.

an issue is usually defined between the lines displayed below.

* Any crashes upon running
* Dynamic import errors (<mark style="color:blue;">if you can not fix it yourself</mark>)
* Thread related issues (<mark style="color:blue;">thread crashing, faulting, collisions, etc</mark>)
* Data related issues (<mark style="color:blue;">e.g: if you were spit out some random data during a level</mark>)
* Invalid info through walkthroughs/explanations & education

and more. So the actual issue comes down to a few questions. Make sure to ask yourself these questions before reporting or taking the time to explain it.

* _Does this impact the user experience?_
* _Does this impact the education of a user?_
* _How can this be fixed?_
* How did this impact my experience?

### What I need from you

If you actually went through the questions and all the questions were answered in a state of "oh wow, this is all actually impactful" then you can move onto building the report and idea of how you can disclose this!

{% hint style="info" %}
We are going based on trust that you will report it. If you do not want to report it, cool! No hard feelings. Here is a leaf to represent a funny plant and a doughnut for your findings\
:leaves: :doughnut:
{% endhint %}

For reporting flaws please explain the following!

* What the issue was
* How it can be fixed (<mark style="color:purple;">in your opinion, this is optional tho and not necessary</mark>)
* How did it impact your experience
* How it may be able to impact others (<mark style="color:purple;">if you are really feeling kind</mark>)
* <mark style="color:orange;">If you are even nicer of a human</mark> - screenshots of the actual flaw happening
* Was it repeatable?
* How did it happen?
* Where did it happen?&#x20;

{% hint style="info" %}
Unlike most bug reporting systems, if it is not repeatable or you can not recreate it, this is okay and I will personally still take it into consideration to look in that area and do multiple tests following the same steps you took to get to that point if you explained it well enough.\
\
If the test shows that I myself did not run into this issue on a new machine (brand new Windows10 VM) then I will probably send a response back saying that the issue was tested and we could not reproduce it- :(&#x20;
{% endhint %}

For further information on what a report page should look like, check out the reporting [example.md](example.md "mention") which is the next page. This demonstrates a sample issue that could not be repeated.

{% hint style="info" %}
If you have found a vulnerability, refer to [vulnerabilities](what-happens-if-i-report/vulnerabilities/ "mention")to see about how that works. I know right, a vulnerability in a program meant to be vulnerable? Fuck yeah! haha
{% endhint %}
