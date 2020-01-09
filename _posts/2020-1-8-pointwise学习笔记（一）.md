# pointwise学习笔记（一）
---
最近老师让研究一下如何把fluent计算的气动热作为Abqus传热分析的边界条件进行计算。看了一些论文，思路大体如下：首先，fluent计算一机翼在高速流场下的
表面气动力，然后利用编程或者MPCCI软件将fluent的热流密度转化为Abqus的温度边界，在abqus里进行稳态计算。而首个拦路虎就是fluent气动热计算。fluent里的
网格为流场网格，与我们平时用hypermesh画固体的网格大为不同。常用的画流体网格的软件通常为ICEM（ansys自带）和pointwise。ICEM画非结构网格功能强大，门槛较高；
pointwise画网格精度较高，上手快。

快捷键|功能
:--:|:--:
Ctrl+right mouse|旋转
Shift+right mouse|平移
middle mouse|缩放
Shift+middle mouse|局部放大和缩小


