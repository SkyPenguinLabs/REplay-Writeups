---
cover: ../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Buttons In GUIs

Before we go on a jumble to find buttons within a GUI and also start reversing their values- we need to really get behind what specific buttons are and how they may work in a GUI.

## Tackling Buttons

The first thing to know is that buttons in applications such as GUIs are usually boiling down to the following inner workings.

{% hint style="info" %}
Do not believe that this is all that goes into buttons- there is a LOT more that happens and can be done with them but I want to note the most significant information for this CTF.
{% endhint %}

### The input

The input to the button is usually going to be someone clicking the button. When the button detects it has been pressed, or a signal has been received by the widget listener, the button that was pressed will tell the button to execute the information.

Usually, buttons will detect their input like this.

```
if (ButtonPressed(0xdeadbeaf)) {
    // Rendering
} 
// Continue if it was not pressed
```

And this condition is executed for each time the frame is rendered.&#x20;

### The result&#x20;

The result of buttons being pressed can mainly be segmented into two results.

* A global state is written to define what the program should do next
* The button just executes the code and will return like normal

### Our scenario

For our scenario, we analyzed that throughout REplay, the GUI seems to be using some sort of configuration or just a large set of namespaces to globally access information's. For example, the password was never a local variable setup, it was in the same area as the username, adminID, and other relevant storage fields with constant buffer limits.

Since we see this, we can imagine that (_especially with control flow analysis_) the buttons, for tabs, are setting the current status of a global variable to set the "_menutab_" in the program which is read and checked before rendering the frame.&#x20;
