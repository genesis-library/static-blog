---
title: Switching Between 2 Screens Script
toc: true
date: 2022-01-30 13:58:34
tags: automation hammerspoon
categories: automation
---

Welcome to automation zone again!

End of this tutorial you will able to switch between 2 monitors very fast\
with ⇪ + A (or whatever shortcut you want)


## WHY

When using 2 monitors on macOS, switching one screen to another is painful.

First, you have to move your cursor to other screen.
Then, you need to click once to take focus of the screen.

It was such a torture to my soul that I started looking for a solution.

Then Hammerspoon came to rescue me:

## HAMMERSPOON
Hammerspoon provides an API integrated with LUA language which lets you use macOS features easily.

Simple as below:
```
hs.mouse.getCurrentScreen()
```
 
Full code of switching screen and clicking once is down below:
```
local hyperShift = {'ctrl', 'alt', 'cmd', 'shift'}
hs.hotkey.bind(hyperShift, 'a', function()
    local screen = hs.mouse.getCurrentScreen()
    local nextScreen = screen:next()
    local rect = nextScreen:fullFrame()
    local center = hs.geometry.rectMidPoint(rect)
hs.mouse.setAbsolutePosition(center)
hs.eventtap.leftClick(center)
end)
```

To use this code, do this steps below:

```
open ~/.hammerspoon 
nano init.lua // Puth that code inside of this file
```

Then to reload this changes:\
Open Hammerspoon console\
Then click <b>Reload config</b>

Well done! Now you can use ⇪ + A as a swift screen switcher.



