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

### What are we doing?

We are basically going to be trying to locate a button and invert what the buttons do. This includes locating the global status variable that the individual tabs to render the right side of the window set.&#x20;

For a logical idea- say ...

* Button A sets `Status` variable to '1' for tab 1
* Button B sets `Status` variable to '2' for tab 2&#x20;

We want to get Button A to really do the same thing Button B is doing by telling A to set the `Status` variable to '2' to represent tab 2. We then need to make the appropriate patches and verify our changes.

### What is our end goal?

Our end goal is to flip the logic of the buttons specifically in the values they set.

### What do we need?

In order to carry out a proper attack- we need to be able to locate buttons by finding common patterns in functions or values that resemble the result or status of the buttons mapped on the GUI. This is quite simple-&#x20;

Then we also need to find the global status variable that the program sets.

### Scenario Layout

To aid the information above, I took some dev knowledge / internal knowledge for this but mainly the scenario is where the program sets a variable to a specific tab number which when checked gets to execute the code that can get rendered onto that tab. You need to trick your friends by giving them a fake cheat that you cracked but a cheat that does not work at all and is in fact completely confusing (_switching buttons make funky people go insane_)

## Finish

To finish this off- we now have a well defined plan that can be carried out and implemented! Lets gooo!

