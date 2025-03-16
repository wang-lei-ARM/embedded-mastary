# embedded-mastary
lean and practice

## 2025年2月23日总结 第一周

主要是进行c语言的总结提高。

### 1.学习了韦东山的c语言加强的课程。

volatile 关键字 map文件查看全局变量


结构体 ：
内存对齐，位域操作（2进制位）

联合体内存共用。

指针，结构体指针和函数指针

链表的插入和删除

全局变量和局部变量从flash到内存的方式
- 全局变量的初始化
类型memcpy，把flash上的数据段，整体拷贝到RAM
- 初始值为0，没有初始化的全局变量，怎么初始化？
- 有100万个这样的变量，都保存再flash上？
- 这些变量在内存里放在ZI段
- 类似memset,把ZI段全部清零

### 2.c语言的本质

系统栈空间的手动分配
push和pop的存取数据顺序

堆的手动分配。

函数的本质：就是一系列的指令：就是一系列的机器码。
从flash 复制到内存。
- 调用函数：让CPU的PC寄存器等于“一系列机器码”的首地址，就是函数地址

指针的本质

- 指针变量，也是一个变量，存放的是“首地址”；对于cpu来说，一个地址对应一个字节。
假设a是int型。首地址是0x2000,0010,第二个字节就是0x2000,0011.第三个字节就i是0x2000,0012

c语言的本质就是内存的读写和修改。

复杂的结构体和字符串等是从flash里拷贝到ram中

### 3.c语言面对对象
1.使用结构体抽象出数据

2.使用函数指针放在数组里

3.使用结构体数组赋值

调用时只需要定义一个数组指针在调用方法就可以了。

判断设备类型 ，选择对应的方法

#### 程序分层

管理层：什么也不用管
输入设备：区分不同的操作系统
内核抽象层 ：区分哪种芯片
芯片抽象层：不同的芯片有没有hal库支持

#### 消抖
使用软件定时器

两个按键就需要两个定时器，够吗？ 使用软件定时器 就够

假如设定了一个闹钟：这时候他记录下当前的时间+增加的时间。 硬件定时 tick 不断在累加，累加到和 当初设定的时间一边长了，就溢出。需要在 systick 函数内循环判断。

#### 显示设备的结构体抽象。

直接读写内存和使用i2c接口 使用屏幕

![alt text](image.png)

可重入和不可重入函数
可重入函数： 多个任务调用这个函数没有问题。

不声明就无法使用？
对于变量来说是对的，对于函数来说是错的。

回调和钩子函数
函数指针，先设置好指向哪个函数。发生啥事件的时候调用这个函数


## 2025年3月2日总结 第二周

主要是进行数据结构与算法的学习。
《数据结构与算法描述c语言》马克·艾伦·维斯

1.冒泡排序.主要是两个for 循环的条件.
2.stm32的CCM区。1000，0000 - 1000，FFFF。F407仅支持数据操作。作为一个ram区
可以进行快速的读写。
3.stm32的内存分布

第一章
数学知识复习：
指数、对数、级数、模运算。

**递归：**
1、基准情形
2、不断推进
3、设计法则
4、合成效益法则

第二章
算法分析

时间复杂度

第三章：表，栈，队列
程序设计的基本法则之一是单例程不应超过一页。
抽象数据类型是数学的抽象
表：数组，链表实现双链表，循环链表，基数排序（桶排序）
栈：链表和数组实现。平衡符合。函数调用，中缀到后缀的转换。
队列：头和尾，双向循环队列。



## 2025年3月9日总结 第三周

学习数据结构c语言版 严蔚敏

第一章 主要是概念 
数据结构相关概念，数据，数据元素，数据项，数据对象，数据结构、逻辑结构、存储结构等。

第二章 线性表

顺序存储和链式存储
初始化，插入，取值，删除，查找

单链表，带头节点和不带头节点。
前插法，后插法，创建单链表 ，循环链表，双向链表，双向循环列表
表的合并

第三章 栈和队列

顺序栈和链栈
顺序栈要双指针。链栈：初始化，入栈，出栈，取值

栈和递归

## 2025年3月16日总结 第四周

主要学习数据结构中的树 。
使用树的话，访问的时间会变快。

递归在树中的应用非常的频繁。容易实现但是难以理解。

树的概念和性质。
二叉树查找树：有序，左子树小于x，右子树大于x。
查找，插入，删除。
AVL树，旋转。
B树。
红黑树。自顶向下插入。

树的基本术语。二叉树的基本定义
遍历二叉树。前中后遍历。
建立，复制，计算深度，统计二叉树节点个数。

网络通信基础。