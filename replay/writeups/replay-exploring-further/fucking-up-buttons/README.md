---
cover: ../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Fucking Up Buttons

Within REplay existed many different Graphical User Interface Widgets (GUI widgets) such as buttons, scrollbars, and more! But what if we woke up one day and decided to cause violence- really sell an existing exploit and make it fake and trigger people when they go to ruin someone else day but instead get their own day ruined? Well, we can do that! Lets fuck up some buttons?

### How are we going to do this?&#x20;

In order to fuck up the buttons, we want to invert the functionality- lets say they click the aimbot button and it actually goes to ESP- or maybe we can mess with some of the text and inject our own sequences into it! All of this can be done with a simple binary patch. For this example, we are going to be using Level 1 which can be downloaded from the page linked below.

{% content-ref url="../../../levels/level-1-3-download.md" %}
[level-1-3-download.md](../../../levels/level-1-3-download.md)
{% endcontent-ref %}

### Important note

I want to note that the way I go about doing this is super weird, but the reason for the weirdness is a creative way to get around specific issues. For this, we will be using IDA-Pro in the first half and the second half we will be going through Ghidra. So make sure you have Ghidra setup prior as we will not be going through that.

