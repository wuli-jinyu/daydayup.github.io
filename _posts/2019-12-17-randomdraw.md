# 抽签小工具的学习笔记
---
本不是计算机软件专业的的学生，作为一个学上个世纪的经典宏观力学的工科学生能在研究生阶段接触到python，实在是有一点运气的成分。
为了锻炼我这个零基础的新手，导师有机会就会让我尝试一些编程的任务。怕忘记，同时又为了学习Git便开启了此blog。

   废话不多说，第一篇便是记录做一个为方便导师开会的抽签小工具的学习过程。具体工作分为三部分：1.抽签的算法2.软件界面3.py程序打包

## 抽签算法
算法程序如下:
`import tkinter as tk # 主窗口
import random
import os
from PIL import ImageTk
from PIL import Image
from tkinter import StringVar
os.chdir('C:\chouqian_code2')
window = tk.Toplevel()
window.title("评审专家抽签")   # 窗口标题
window.geometry('1360x700')  # 窗口尺寸 
canvas = tk.Canvas(window,width=1360,height=700,bg='white')
image = Image.open('南航.bmp')
im = ImageTk.PhotoImage(image)
canvas.create_image(680,350,image=im)
canvas.pack()
file = open('学术组.txt','r')#以只读模式读取文件
lines1 = [ ]
for i  in file:
    lines1.append(i)#逐行将文本存入列表lines中
file.close( )
# 标签
var = tk.StringVar()
lab = tk.Label(window, textvariable=var, bg='green', font=('Arial', 35))
lab.place(x=100,y=430,width=180,height=220)
list1 = []
for t in range(50):
    list1.append(t)#生成从1到50的列表
    random.shuffle(list1)#随机打乱列表
i = 0
list_new1=[]
while i< 50:#重新排序
    j = list1[i]
    list_new1.append(lines1[j])
    i=i+1

def tuchulai(btn):
    global count
    k = count
    a = int(k)
    a = a+1
    var.set(list_new1[a])
    Listbox.insert(k,list_new1[a])
    k=str(a)
    count = k
    btn.config(text = k) #增加了这一句，更新button上的文本内容
# 按钮
count = StringVar() 
count = '0' 
botton = tk.Button(window,text = count,font=('宋体',20,'normal'),command = lambda:tuchulai(botton)) #因为事件触发的函数（callback）需要有参数传进入，所以用lambda表达式
# 可以参考下这里：http://blog.sina.com.cn/s/blog_ac9fdc0b0101n9u6.html
# 其实用bind也可以进行事件触发的绑定。
botton.place(x=145,y=250,width=90,height=40)

#标签
first = tk.Label(window,text='学术组',bg='red',font=('宋体',30,'normal'))
first.place(x=100,y=50,width=180,height=100)
#文本框记录已选名单
Listbox = tk.Listbox(window,bg = 'yellow',font=('宋体',21,'normal'))
Listbox.place(x=400,y=50,width=180,height=600)
file = open('应用组.txt','r')#以只读模式读取文件
lines2 = [ ]
for i  in file:
    lines2.append(i)#逐行将文本存入列表lines中
file.close( )
# 标签
var2 = tk.StringVar()
lab2 = tk.Label(window, textvariable=var2, bg='green', font=('Arial', 35))
lab2.place(x=780,y=430,width=180,height=220)
list2 = []
for t in range(47):
    list2.append(t)#生成从1到50的列表
    random.shuffle(list2)#随机打乱列表
i = 0
list_new2=[]
while i< 47:#重新排序
    j = list2[i]
    list_new2.append(lines2[j])
    i=i+1

def tuchulai2(btn):
    global count2
    k2 = count2
    a2 = int(k2)
    a2 = a2+1
    var2.set(list_new2[a2])
    Listbox2.insert(k2,list_new2[a2])
    k2=str(a2)
    count2 = k2
    btn.config(text = k2) #增加了这一句，更新button上的文本内容
# 按钮
count2 = StringVar() 
count2 = '0' 
botton2 = tk.Button(window,text = count2,font=('宋体',20,'normal'),command = lambda:tuchulai2(botton2)) #因为事件触发的函数（callback）需要有参数传进入，所以用lambda表达式
# 可以参考下这里：http://blog.sina.com.cn/s/blog_ac9fdc0b0101n9u6.html
# 其实用bind也可以进行事件触发的绑定。
botton2.place(x=825,y=250,width=90,height=40)
#标签
second = tk.Label(window,text='应用组',bg='red',font=('宋体',30,'normal'))
second.place(x=780,y=50,width=180,height=100)
#文本框记录已选名单
Listbox2 = tk.Listbox(window,bg = 'yellow',font=('宋体',21,'normal'))
Listbox2.place(x=1080,y=50,width=180,height=600)
window.mainloop() `

