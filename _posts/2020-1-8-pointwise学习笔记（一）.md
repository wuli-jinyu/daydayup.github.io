# pointwise学习笔记（一）
---
最近老师让研究一下如何把fluent计算的气动热作为Abqus传热分析的边界条件进行计算。看了一些论文，思路大体如下：首先，fluent计算一机翼在高速流场下的
表面气动力，然后利用编程或者MPCCI软件将fluent的热流密度转化为Abqus的温度边界，在abqus里进行稳态计算。而首个拦路虎就是fluent气动热计算。fluent里的
网格为流场网格，与我们平时用hypermesh画固体的网格大为不同。常用的画流体网格的软件通常为ICEM（ansys自带）和pointwise。ICEM画非结构网格功能强大，门槛较高；
pointwise画网格精度较高，上手快。

## 拦路虎Ⅰ————三维机翼流场网格

快捷键|功能
:--:|:--:
Ctrl+right mouse|旋转
Shift+right mouse|平移
middle mouse|缩放
Shift+middle mouse|局部放大和缩小

打算先拿一个机翼做气动热仿真，安装pointwise软件后，在安装目录文件夹内有预先画好的二维翼型流场网格(pointwise\PointwiseV18.0R1\tutorials\2DAirfoil)
,该翼型为NACA6412。所以想得到一三维机翼的流场网格，将此二维翼型流场网格做适当拉伸即可。
二维翼型网格的生成可以参考：
https://blog.csdn.net/weixin_38262871/article/details/77946253

三维机翼流场网格（由二维翼型拉伸所得）参考：
https://wenku.baidu.com/view/b1f376a855270722182ef7b3.html

注意事项：
1.先拉伸一次，然后将翼梢的网格补全，这是重点。然后将补全后的翼梢端的整个圆柱面再次拉伸。形成整个流场。
2.补全翼梢时要注意分割，线条以及节点数目的划分，在分界处要进行融合处理
3.最后设置求解器以及边界条件，再输出CAE文件.cas（选所有blocks，在pointwise中Database表示边界几何，connectors表示网格边线，domains表示二维网格，blocks表示三维网格）


