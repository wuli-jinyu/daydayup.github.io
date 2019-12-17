# 抽签小工具的学习笔记
---
本不是计算机软件专业的的学生，作为一个学上个世纪的经典宏观力学的工科学生能在研究生阶段接触到python，实在是有一点运气的成分。
为了锻炼我这个零基础的新手，导师有机会就会让我尝试一些编程的任务。怕忘记，同时又为了学习Git便开启了此blog。

废话不多说，第一篇便是记录做一个为方便导师开会的抽签小工具的学习过程。具体工作分为三部分：1.抽签的算法2.软件界面3.py程序打包成exe

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

## 生成界面

