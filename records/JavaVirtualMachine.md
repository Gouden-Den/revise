这里整理了《深入理解Java虚拟机 JVM高级特性与最佳时间(第三版)》的内容
**Java内存区域与内存溢出异常<br/>**
`运行时数据区`<br/>
程序计数器（Program Counter Register）<br/>
记录字节码执行的位置，“线程私有”的内存。<br/>
如果正在执行的是一个Java方法，这个计数器记录的是在执行的虚拟机字节码指令的地址；如果正在执行的是Native方法，这个计数器值则为空（Undefined）。
此内存区域是唯一一个在Java虚拟机规范中没有规定任何OutOfMemoryError情况的区域。<br/>
Java虚拟机栈（Java Virtual Machine Stacks）<br/>
生命周期与线程相同。<br/>
虚拟机栈描述的是Java方法的内存模型：每个方法在执行的同时都会创建一个栈帧用于存储局部变量表、操作数栈、动态链接、方法出口等信息，每一个方法从调用直至执行完成的过程，就对应着一个栈帧在虚拟机栈中入栈到出栈的过程。<br/>
局部变量表所需的内存空间在编译期间完成分配，当进入一个方法时，这个方法需要在帧中分配多大的局部变量空间是完全确定的，在方法运行期间不会改变局部变量表的大小。<br/>
在Java虚拟机规范中，对这个区域规定了两种异常状况：StackOverflowError异常和OutOfMemoryError异常。<br/>
本地方法栈（Native Method Stack）<br/>
与虚拟机栈所发挥的作用是非常相似的，该区用于执行Native方法。<br/>
有两种异常状况：StackOverflowError异常和OutOfMemoryError异常。<br/>
Java堆（Java Heap）<br/>
被所有线程共享。
此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例都在这里分配内存。<br/>
Java堆中还可以细分为：新生代和老年代；再细致一点的有Eden空间、From Survivor空间、To Survivor空间等。<br/>
线程共享的Java堆中可能划分出多个线程私有的分配缓冲区（Thread Local Allocation Buffer，TLAB）。<br/>
有一种异常状况：OutOfMemoryError异常。<br/>
方法区（Method Area）<br/>
被所有线程共享。
用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。<br/>
堆的一个逻辑部分。<br/>
JDK1.7的HotSpot把原本放在永久代的字符串常量池移出。<br/>
有一种异常状况：OutOfMemoryError异常。<br/>
运行时常量池（Runtime Constant Poop）<br/>
是方法区的一部分。<br/>
Class文件中描述的符号引用及翻译出来的直接引用存储在运行时常量池中。<br/>
运行期间也可能将新的常量放入池中，例如String类的intern()方法。<br/>
有一种异常状况：OutOfMemoryError异常。<br/>
直接内存（Direct Memory）<br/>
使用Native函数库直接分配堆外内存。<br/>
有一种异常状况：OutOfMemoryError异常。<br/>
**垃圾收集器与内存分配策略<br/>**
**虚拟机性能监控与故障处理工具<br/>**
**类文件结构<br/>**
**虚拟机类加载机制<br/>**
**虚拟机字节码执行引擎<br/>**
**早期（编译期）优化<br/>**
**晚期（运行期）优化<br/>**
**Java内存模型与线程<br/>**
**线程安全与锁优化<br/>**