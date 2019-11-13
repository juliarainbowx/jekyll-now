---
layout: post
title: How to create an Analog Clock with Python and Turtle
published: true
---
You can find working demo on [Repl.it](https://repl.it/@juliarainbowx/Analog-Clock).

![Analog Clock](https://github.com/juliarainbowx/juliarainbowx.github.io/blob/master/images/analog-clock.png)

Code for this lesson:

```python
#! /usr/bin/env python3
#! -*- coding:utf-8 -*-

import turtle
import time

SCALE = 1.7

def draw_clock():
    tick = turtle.Turtle()
    tick.speed(100)
    tick.shape("circle")
    for i in range(60):
        if i % 5 == 0:
            tick.pensize(10)
            tick.penup()
            tick.forward(200*SCALE)

            tick.pendown()
            tick.forward(10*SCALE)
            tick.penup()
            tick.backward(40*SCALE)

            writer = turtle.Turtle()
            writer.shape("blank")
            writer.speed(100)
            writer.penup()
            writer.setpos(tick.pos())
            writer.pendown()
            hourval = 3 + i // 5 % 12
            writer.write('{}'.format(hourval if hourval <= 12 else hourval - 12),
                    font = ('Courier', 24), align = "center")
            writer.penup()

            tick.backward(170*SCALE)
        else:
            tick.pensize(5)
            tick.penup()
            tick.forward(200*SCALE)
            tick.pendown()
            tick.forward(5*SCALE)
            tick.penup()
            tick.backward(205*SCALE)
        tick.right(6)
    hour_tick, minute_tick, second_tick = turtle.Turtle(), turtle.Turtle(), turtle.Turtle()
    tm = time.localtime()
    update_hour_tick(hour_tick, tm)
    update_minute_tick(minute_tick, tm)
    update_second_tick(second_tick, tm)
    return hour_tick, minute_tick, second_tick, tm

def update_hour_tick(tick, tm):
    tick.reset()
    tick.clear()
    tick.left(90)
    tick.speed(100*SCALE)
    tick.pensize(10)
    tick.shape("blank")
    # 360/6 = 30/x => x = 0.5
    tick.right((tm.tm_hour % 12) * 30 + tm.tm_min * 0.5)
    tick.backward(30*SCALE)
    tick.forward(160*SCALE)

def update_minute_tick(tick, tm):
    tick.clear()
    tick.reset()
    tick.speed(100)
    tick.shape("blank")
    tick.left(90)
    tick.pensize(6)
    tick.right((tm.tm_min) * 6)
    tick.backward(30*SCALE)
    tick.forward(180*SCALE)

def update_second_tick(tick, tm):
    tick.clear()
    tick.reset()
    tick.speed(100)
    tick.shape("blank")
    tick.color("red")
    tick.left(90)
    tick.pensize(3)
    tick.right((tm.tm_sec) * 6)
    tick.backward(30*SCALE)
    tick.forward(190*SCALE)

if __name__ == '__main__':
    wn = turtle.Screen("Rolex")
    hour, minute, second, tm = draw_clock()
    while True:
        newtm = time.localtime()
        if newtm.tm_hour != tm.tm_hour:
            update_hour_tick(hour, newtm)
        if newtm.tm_min != tm.tm_min:
            update_minute_tick(minute, newtm)
        if newtm.tm_sec != tm.tm_sec:
            update_second_tick(second, newtm)
            tm = newtm
        time.sleep(0.3)
```

