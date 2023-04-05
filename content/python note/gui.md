---
title: GUI
description: GUI
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
```python
# explaining how to add menu bars, menus, and toolbars to GUI apps with python and pyqt.

import sys

from PyQt5.QtCore import Qt
from PyQt5.QtWidgets import QApplication, QLabel, QMainWindow, QMenu, QToolBar


class Window(QMainWindow):
 """ Main Window """
 def __init__(self, parent=None):
  super().__init__(parent)

  self.setWindowTitle("Python Menus & Toolbars")
  self.resize(400, 200)
  self.centralWidget = QLabel("Hello, World")
  self.centralWidget.setAlignment(Qt.AlignHCenter | Qt.AlignVCenter)
  self.setCentralWidget(self.centralWidget)
  self._createMenuBar()
  self._createToolBars()

 def _createMenuBar(self):
  
  menuBar = self.menuBar()
  menuBar.setNativeMenuBar(False) # MacOS Solution (!)

  fileMenu = QMenu("&File", self)
  menuBar.addMenu(fileMenu)

  editMenu = QMenu("&Edit", self)
  menuBar.addMenu(editMenu)

  helpMenu = QMenu("&Help", self)
  menuBar.addMenu(helpMenu)

 def _createToolBars(self):

  fileToolBar = QToolBar("File", self)
  self.addToolBar(fileToolBar)

  editToolBar = QToolBar("Edit", self)
  self.addToolBar(editToolBar)

  helpToolBar = QToolBar("Help", self)
  self.addToolBar(helpToolBar)


if __name__ == "__main__":

 # create pyqt5 app. It manages the GUI application's control flow and main settings.
 app = QApplication(sys.argv)

 # create the instance of our Window
 win = Window()
 win.show()
 sys.exit(app.exec_())
```

[Ref](https://realpython.com/python-menus-toolbars/Creating Toolbars)

## Hello world - tkinter

```python
import tkinter
from tkinter import ttk

window = tkinter.Tk()
window.title('Hello world app')
window.geometry('200x100')

def say_hello():
  print('Hello world!')

hello_button = ttk.Button(window, text='Say hello', command=say_hello)
hello_button.pack()

window.mainloop()
```
