---
title: hello
date: 2018-07-10 21:09:19
tags: python
---
```
import tkinter.filedialog
from tkinter import *


class App:

    filed_lable = Label()
    filed_input = Entry()

    def __init__(self, master):

        frame_top = Frame(master)
        frame_top.pack()

        self.button = Button(frame_top, text="QUIT", fg="red", command=frame_top.quit)
        self.button.pack(side=LEFT)

        self.hi_there = Button(frame_top, text="Hello", command=self.say_hi)
        self.hi_there.pack(side=LEFT)

        self.filed_input = Entry(frame_top)
        self.filed_input.pack()





    def say_hi(self):
        frame_bottom = Frame(root)
        frame_bottom.pack()
        print("---------------hello---------------")
        text = self.filed_input.get()
        self.filed_input.delete(0,len(text))
        self.filed_lable = Label(frame_bottom,text=text)
        self.filed_lable.pack()
        filename = tkinter.filedialog.askopenfilename(filetypes=[("任意格式","*")])


root = Tk()
app = App(root)

root.mainloop()
root.destroy()  # optional; see description below
