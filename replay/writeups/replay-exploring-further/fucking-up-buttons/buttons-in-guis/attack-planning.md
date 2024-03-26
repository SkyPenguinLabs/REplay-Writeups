---
cover: ../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Attack Planning

In order to talk about the buttons in the GUI, we need to first draw out what we know and build a valid attack plan. Our attack plan will consist of a series of well defined and directional questions that we can ask ourselves before the engagement to help make sure we chop out time to think.&#x20;

{% hint style="info" %}
Primarily: we will be using the following few questions\
\
\-> What are we looking for?\
\-> What are we doing?\
\-> What is our end goal?\
\-> What do we need?\
\-> Scenario layout
{% endhint %}

## Attack plan

Building an attack plan will be dumped down to answering the points and questions in depth that we defined before.

### What are we looking for?

Ideally, we are looking for anything that resembles a button. The list below demonstrates what could indicate buttons.

* Specific rendering areas which may reveal system and info such as labels for buttons
* Variables being set by the same function with specific text patterns
* Any sort of rendering calls for the graphical library
* Any other external information that can help us identify the code structure of buttons

{% hint style="info" %}
This is where [replay-isolated-training](../../../../replay-extras/replay-isolated-training/ "mention") will help you. By analyzing specific buttons or widgets from libraries like ImGui for C++ GUIs, you can easily find the same pattern which we have used in [finding-system](../../../level-2-all-walkthroughs/section-6.0-networking-and-web/binary-auditing-6.4.0/binary-audit-goals/vuln-rce/educational/locating-rce/finding-system/ "mention"), [tracing-free.md](../../../../replay-extras/reverse-engineering-other-theory-s/tracing-externs/tracing-free.md "mention"), [analyzing-free](../../../../replay-extras/replay-isolated-training/examples/use-after-free-1/analyzing-free/ "mention"), and  [tracing-malloc.md](../../../../replay-extras/reverse-engineering-other-theory-s/tracing-externs/tracing-malloc.md "mention")
{% endhint %}

