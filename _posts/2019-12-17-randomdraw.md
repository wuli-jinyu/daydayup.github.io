# 抽签小工具的学习笔记
---
本不是计算机软件专业的的学生，作为一个学上个世纪的经典宏观力学的工科学生能在研究生阶段接触到python，实在是有一点运气的成分。
为了锻炼我这个零基础的新手，导师有机会就会让我尝试一些编程的任务。怕忘记，同时又为了学习Git便开启了此blog。

废话不多说，第一篇便是记录做一个为方便导师开会的抽签小工具的学习过程。具体工作分为三部分：1.抽签算法2.用户界面3.py程序打包成exe

## 抽签算法
会议成员分为两个组：学术组、应用组。各组专家的名单保存在C盘chouqian_code2文件夹中（导师只有一个C盘），保存形式为：学术组.txt、应用组.txt。

程序一开始先以只读模式打开txt文件，将参会成员名单读取到lines中：
```
file = open('C:\chouqian_code2\学术组.txt','r')#只读模式打开
lines1 = [ ]
for i  in file:
    lines1.append(i)#给列表添加元素
file.close( )
```
然后用Python随机函数库random将列表lines中的元素打乱（洗牌），这里先新建了一个数字列表list1，将其打乱然后在另一列表list_new中把lines重新安装打乱后的list的数字编号进行重新排序。https://www.jianshu.com/p/b5e95d90e7a4 （random使用方法）
```
import random
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
```
到这里只需要依次输出列表list_new的元素就可以实现参会人员的名字的抽签，这种算法较为简单，属于一次性抽完然后一个一个输出。

## 生成用户界面
python创建可视化界面的方法有好多。Tkinter是python的内置库，教程较多。PyQt据说比较方便（暂未试过），考虑到任务简单且时间较紧，选用tkinter。
tkinter教程可参考：
https://blog.csdn.net/qq_37482202/article/details/84201259  https://www.jianshu.com/p/91844c5bca78
lambda表达式参考：
http://blog.sina.com.cn/s/blog_ac9fdc0b0101n9u6.html
```
import tkinter as tk # 主窗口
window = tk.Toplevel()
window.title("评审专家抽签")   # 窗口标题
window.geometry('1360x700')  # 窗口尺寸 
canvas = tk.Canvas(window,width=1360,height=700,bg='white')
image = Image.open('南航.bmp')
im = ImageTk.PhotoImage(image)
canvas.create_image(680,350,image=im)#设置背景
canvas.pack()

var = tk.StringVar()
lab = tk.Label(window, textvariable=var, bg='green', font=('Arial', 35))
lab.place(x=100,y=430,width=180,height=220)#设置标签，用于显示抽中的专家名字

def tuchulai(btn):#设置按钮函数，点一次按钮，即在var中显示抽中的专家名字，并且在文本框中写入已经被抽过的所有专家的名字
    global count#定义一个全局变量，用于计数
    k = count
    a = int(k)
    a = a+1
    var.set(list_new1[a])
    Listbox.insert(k,list_new1[a])
    k=str(a)
    count = k
    btn.config(text = k) #增加了这一句，更新button上的文本内容，将按钮的名字更新以记录抽取人员个数

count = StringVar() #设置按钮
count = '0' 
botton = tk.Button(window,text = count,font=('宋体',20,'normal'),command = lambda:tuchulai(botton)) 
botton.place(x=145,y=250,width=90,height=40)

first = tk.Label(window,text='学术组',bg='red',font=('宋体',30,'normal'))#设置文本框listbox记录已选名单
first.place(x=100,y=50,width=180,height=100)
Listbox = tk.Listbox(window,bg = 'yellow',font=('宋体',21,'normal'))
Listbox.place(x=400,y=50,width=180,height=600)

window.mainloop() #显示界面语句
```
## 打包py程序
[利用Pyinstaller] https://blog.csdn.net/qq_24624539/article/details/88074501
我安装的是anaconda，自带好多库，打包的时候会导致exe文件很大（打包了很多不必要的库），为了解决这个问题，试过单独建立一个虚拟环境(pipenv)，仅安装所需要的库进行安装，但是打包完反而更大了（取消虚拟环境只需删掉文件夹即可）。所以就直接另外单独安装了一个python3.8，在其根目录仅安装所需要的库，进行打包最后exe的大小仅为之前的十分之一。

## 待改进的点
1.每次重新抽签都需要，重新打开exe,可新建一个按钮用于重新打乱
2.界面巨丑，可以设置多层界面，通过选项进入新的界面

