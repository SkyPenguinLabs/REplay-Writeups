---
cover: ../../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# An introduction to beeps

For this section, we are tasked to listen into the menu and find beeps that the menu creates when we go to view a new tab. The beep seems to take quite a while and is interestingly deep. Here, this means that most likely, our program is using a custom implementation of the `Beep` API call or they are actually using [Beep from the windows API](https://learn.microsoft.com/en-us/windows/win32/api/utilapiset/nf-utilapiset-beep).

This exists mainly for testing purposes, and is used in this menu to indicate to the user _(or the developer)_ that the GUI library is going to start rendering the next tab, as it detected that the user pressed on the button. Pretty much, the code looks like this internally.

```cpp
if (ImGui::Button(" Visuals", WND_CONFIG)) {
	if (Configurations.LoggedIn) {
		Beep(200, 950);
		Settings::Tab = 1;
	}
}
```

