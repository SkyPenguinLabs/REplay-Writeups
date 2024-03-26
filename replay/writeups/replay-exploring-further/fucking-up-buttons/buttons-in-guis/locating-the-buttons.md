---
cover: ../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Locating The Buttons

Sadly, locating buttons on a graphical application is really difficult to do statically and the best thing we have to do is just assume and see if a series of tests (_such as changing the data, or watching the results of our modifications happen_) can proof that we found a button.

However, we are not at a total loss. This is because that we can still get very close and assume this is happening.

## Methodologies and Steps

When we think about buttons- we imagine that the program must be setting a global or even temporary status on that one button to detect whether or not the button was pressed. Well, in order for the button and widget to do anything, we need to actually check the state of the button status.

If we did not check the state, then the code we have for all buttons would execute at the same time resulting in a crash. So for this section, here are some things to consider when looking for buttons.

### Rendering Loop

When looking for a button or some form of widget within the GUI, there are ways to locate them. While not being good for every single type of button in the application, but it helps to an extent. One of the best ways to find buttons that are on the main page of the application by tracing the initialization of the GUI all the way to the main render loop.

I highly suggest looking for system API calls that can help you with finding the rendering configurations for the backend of the application if they exist.&#x20;

### Render Loop Control Flow

The control flow of a rendering loop especially for the main Window is going to be important to see how the program actually handles buttons and tabs being pressed. If you have followed or taken a look at a majority of the writeups, you might have noticed some images going over the CFG of the main rendering loop actually looked like two separate local bricks.&#x20;

This is because they are.&#x20;

Sometimes, we are not always going to want to mash our code together, even if the compiler wants to but we will forget about that for right now. In other moments, we may want to separate them into local bricks as shown below.

```
{
    // button setup
}

{
    if (tab == 10) {/*stuff*/}
    if (tab == 11) {/*stuff*/}
}
```

This is mainly preference but also can be helpful for organizing conditions and control flow.&#x20;

### Other Things

Additionally, you can also check the following list of items.

* Strings indicating the tabs or buttons
* Same function being used in the same area
* Same status / variable being set&#x20;
* Specific order of data being pushed to the same variable



