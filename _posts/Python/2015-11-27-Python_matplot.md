---
layout: post
author: Ericson
date: 2015-11-27
title: Python Matplot画图
category: python
tag: [python,matplot]
---

最近在写论文，本来用visio画图，然后发现用latex显示的visio图不够精美，查了资料，发现有很多精美的制作图片的软件，所以选用python来画图，正好可以学习下python语法。

python主要是用matplot和numpy这两个库来画图，后一个库主要是用作处理数字。不废话，上代码：
``` python
import matplotlib.pyplot as plt
plt.rcParams['text.usetex'] = True
plt.rcParams['mathtext.default'] = 'bf'
# plt.rcParams['lines.linewidth'] = 2
plt.rcParams['font.size'] = 12
time = []  # time
x = []  # x axis
job1 = []  # job1
job2 = []  # job2
job3 = []  # job3
job4 = []  # job4
job5 = []  # job5
job6 = []  # job6
file = open('F:\\test\\HYAS')
for line in file:
    line_split = line.strip('\n').split(',')
    time.append(long(line_split[0]))
    x.append(0)
    size = len(line_split) - 1
    for i in range(size):
        items = line_split[i + 1].split(':')
        if int(items[0]) == 1:
            job1.append(float(items[1]))
        if int(items[0]) == 2:
            job2.append(float(items[1]))
        if int(items[0]) == 3:
            job3.append(float(items[1]))
        if int(items[0]) == 4:
            job4.append(float(items[1]))
        if int(items[0]) == 5:
            job5.append(float(items[1]))
        if int(items[0]) == 6:
            job6.append(float(items[1]))
    while len(job1) < len(time):
        job1.append(0)
    while len(job2) < len(time):
        job2.append(0)
    while len(job3) < len(time):
        job3.append(0)
    while len(job4) < len(time):
        job4.append(0)
    while len(job5) < len(time):
        job5.append(0)
    while len(job6) < len(time):
        job6.append(0)
realtime = []
temp = time[0]
for item in time:
    realtime.append(float(item - temp) / 1000000000)
for i in range(len(job1)):
    job2[i] += job1[i]
for i in range(len(job2)):
    job3[i] += job2[i]
for i in range(len(job3)):
    job4[i] += job3[i]
for i in range(len(job4)):
    job5[i] += job4[i]
for i in range(len(job5)):
    job6[i] += job5[i]
print time
print realtime
print job1
print sum(job6)/len(job6)
plt1, = plt.plot(realtime, job6, color='magenta')
plt2, = plt.plot(realtime, job5, color='yellow')
plt3, = plt.plot(realtime, job4, color='black')
plt4, = plt.plot(realtime, job3, color='blue')
plt5, = plt.plot(realtime, job2, color='green')
plt6, = plt.plot(realtime, job1, color='red')
plt.fill_between(realtime, x, job1, facecolor='red')
plt.fill_between(realtime, job1, job2, facecolor='green')
plt.fill_between(realtime, job2, job3, facecolor='blue')
plt.fill_between(realtime, job3, job4, facecolor='black')
plt.fill_between(realtime, job4, job5, facecolor='yellow')
plt.fill_between(realtime, job5, job6, facecolor='magenta')
# # plt.fill_between(x,y,t,facecolor="b")
plt.xlabel('Time(s)',fontsize=16)
plt.ylabel('Memory(G)',fontsize=16)
plt.xlim(0, 600)
plt.ylim(0, 62)
# plt.legend([plt1, plt2, plt3, plt4, plt5, plt6], ['job6', 'job5', 'job4', 'job3', 'job2', 'job1'])  # make legend
leg=plt.legend([plt1,plt2,plt3,plt4,plt5,plt6],['job6','job5','job4','job3','job2','job1'])
leg.get_frame().set_alpha(0.2)
plt.show()
```
