# 南京大学 2024操作系统概述
老师：[绿导师原谅你了](https://space.bilibili.com/202224425)
参考网站：[学习资料](https://jyywiki.cn)；[视频网站](【01-操作系统概述 (操作系统的历史、学习操作系统的方法) [南京大学2024操作系统]】 https://www.bilibili.com/video/BV1Xm411f7CM/?share_source=copy_web&vd_source=59bc8df6868294a3f1b4a3da6dd33c18)

### 绪论
- 为何要学？
    - ...发展的历程创建了这个知识领域和课程
    - 你可以just for fun吗？
    - 你能承受一个高风险高回报的事情吗（能否不只看保研？）

##### 应用视角的操作系统
- **一切都是状态机**：CPU的运行就是从一个状态到另一个
    - 程序则由内存和寄存器组成；syscall能将程序完全操作系统
- 程序把要执行的功能告诉操作系统，操作系统再调用其他程序，完成后交给原程序
    - 操作系统提供令应用程序舒适的API
- 一个递归调用是怎么实现的？
    - 函数除了在栈帧中保存了自己的变量内容，还保存了一个“自己的”PC

- C语言可以认为是一种高级汇编语言，它能和汇编语言很好地对应起来
- 编译优化：最重要的三板斧：函数内联；常量传播；死代码消除；
    - 系统调用是使程序计算结果可见的唯一方法，故而只有一种东西是不能优化的：`syscall`
    - 状态机的视角:满足C/汇编状态机生成的所有syscall序列完全一致，任何优化都是允许的
        - 当然编译器可以提供一些不可优化标注

```
GDB的TUI source
```

##### 硬件时机的操作系统
- **一切都是状态机**Everything is a state machine
- reset行为是程序员和硬件的第一个互动接口；“固件firmware”早期是ROM，运行配置，加载操作系统
- reset后初始化硬件：BIOS"Basic I/O System";
    - UEFI (Unified Extensible Firmware Interface)：提供更丰富的支持(例如设备驱动程序)
        - 指纹锁、山寨网卡上的PXE网络启动、USB蓝牙转接器连接的蓝牙键盘
- Firmware将磁盘开始的512字节搬到内存中，在某种条件下其就会启动

——遇到困难时要确定自己明确的问题；你找到了问题后就可以找东西来帮你，如果你真的发现一个东西没人能帮你，那么恭喜你，你可以自己创造一个世界上没有过的好帮手了。

##### 数学视角的操作系统
- 程序是一个“数学严格”的对象；Everything is a state machine；程序实际上是为了适应计算机而设计出的，但程序语言也是自然语言的变化。
- 我们可以写一个“检查证明”的程序 profile system

- 尽可能的将需要证明的性质用assertions表达出来（暴力枚举带来的启发）
- 容易阅读(self-explain)的代码是好代码——能把代码和需求联系起来
- 容易验证(self-evident)的代码是好代码——能把代码和正确性证明联系起来

- 进程，系统调用，上下文切换，调度；这些很简单的过程就是操作系统的原理
- “迁移”：操作系统任意选择进程执行一步
- 计算机中的不确定性：**调度**：状态机的选择不确定；**I/O**：系统外的输入不确定
- 既然擦做系统是一个状态机，我们就可以用一个简单的程序来模拟它；实际上，我们完全可以用一个图暴力枚举一个程序的执行可能性
    - **"model checking"**

### 并发
#### 多处理器编程


### 虚拟化



### 持久化

