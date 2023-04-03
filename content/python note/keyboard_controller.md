---
title: Keyboard controller
description: Keyboard controller
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
---

```python
from pynput.keyboard import Listener, Key, Controller

# MONITORING THE KEYBOARD
def on_press(key):
 print('{0} pressed'.format(key))

def on_release(key):
 print('{0} released'.format(key))

 if key == Key.esc:
  # stop Listener
  return False

if __name__ == "__main__":

 # CONTROLLING THE KEYBOARD
 # keyboard = Controller()

 # # press and release space
 # keyboard.press(Key.space)
 # keyboard.release(Key.space)

 # # type lower case a
 # keyboard.press('a')
 # keyboard.release('a')

 # # type two upper case A
 # keyboard.press('A')
 # keyboard.release('A')
 # with keyboard.pressed(Key.shift):
 #  keyboard.press('a')
 #  keyboard.release('a')

 # keyboard.type('Hello World')

 with Listener(on_press=on_press, on_release=on_release) as listener:
  listener.join()
```
