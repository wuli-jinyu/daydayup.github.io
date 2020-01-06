# 基于PC机群的有限元并行计算平台的搭建
---
**有限元计算软件**的并行计算特点如下表：

CAE软件分类|应用软件|并行方式|可扩展性
:--:|:--:|:--:|:--:
1.隐式有限元分析（IFEA）|ABAQUS|pthreads|<8CPU
1.隐式有限元分析（IFEA）|ANSYS|OpenM,MPI|<8CPU
1.隐式有限元分析（IFEA）|MSC.NASTRAN|pthreads,MPI|<8CPU
2.显式有限元分析（EFEA）|LS-DYNA|OpenM,MPI|<64CPU
2.显式有限元分析（EFEA）|PAM-CRASH|OpenM,MPI|<64CPU
2.显式有限元分析（EFEA）|RADIOSS|OpenM,MPI|<64CPU
3.计算流体动力学（CFD）|FLUENT|MPI|<128CPU
3.计算流体动力学（CFD）|STAR-CD|MPI|<128CPU
3.计算流体动力学（CFD）|Power-FLOW|OpenMP,MPI|<128CPU

表中可见，IFEA类应用软件（ABAQUS、ANSYS、MSC.NASTRAN）的可扩展性不是很好。当使用超过8个CPU来处理一个任务时，通常不会再有性能上的提升。实际上，在
实际运算时发现：当采用两个节点进行计算时，计算效率反而不如单个节点，当采用4~8个节点进行计算时，效率明显提高；超过8节点后，计算效率提高不再明显。

**计算机系统**的选择

## MPICH安装
MPI的具体实现一般采用MPICH。MPICH是一个用于高效并行计算的软件包，使用了MPI，给用户提供一个高可用性的应用编程接口，兼顾异构环境和可移植性。
安装MPICH前，所有的主机必须能够建立TCP/IP连接，在所有主机上建立同样的一个账户并设定同样的密码，并授予该账户管理员权限。

在官网上下载最新的安装包http://www.mcs.anl.gov/research/projects/mpich2/index.php，每台pc（每个节点）上安装路径需相同。安装成功后，在“任务管理器”
的“进程”选项卡，可以看到有一个mpd.exe的进程。以后每次启动系统，该进程会自动运行。

## MPICH的注册与配置
每台计算机都需进行注册，而配置只需要在主节点的计算机上进行。
