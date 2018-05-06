这里整理了《Java编程思想(第4版)》里的内容<br/>
**初始化与清理<br/>**
`构造器`<br/>
    不接受任何参数的构造器叫做默认构造器，Java文档中通常使用术语无参构造器。如果已定义了一个构造器(无论是否有参数)，编译器就不会帮你自动创建默认构造器。在Java中，“初始化”和“创建”捆绑在一起，两者不能分离。<br/>
    方法重载<br/>
`方法名相同而形式参数不同。`<br/>
    如果传入的数据类型(实际参数类型)小于方法中声明的形式参数类型，实际数据类型就会被提升。char型略有不同，如果无法找到恰好接受char参数的方法，就会把char直接提升至int型。<br/>
    如果传入的实际参数大于重载方法声明的形式参数，就得通过类型转换来执行窄化转换。如果不这样做，编译器就会报错。<br/>
`this关键字`<br/>
    this可指“这个对象”或“当前对象”。可以用this调用一个构造器，但却不能调用两个。此外，必须将两个狗傲气调用治愈最起始处，否则编译器会报错。除构造器之外，编译器禁止在其他任何方法中调用构造器。<br/>
`清理：终结处理和垃圾回收`<br/>
    finalize()一旦垃圾回收器准备好释放对象占用的存储空间，将首先调用其finalize()方法，并且在下一次垃圾回收动作发生时，才会真正回收对象占用的内存。<br/>
    对象可能不被垃圾回收。<br/>
    垃圾回收只与内存有关。<br/>
    构造器初始化<br/>
`对象的创建过程`<br/>
    1.即使没有显式地使用static关键字，构造器实际上也是静态方法。因此，当首次创建一个类的对象是，或者是这个类的静态方法/静态域首次被访问时，Java解释器必须查找类路径，以定位类文件。<br/>
    2.然后载入类文件。有关静态初始化的所有动作都会执行。因此，静态初始化只在Class对象首次加载的时候进行一次。<br/>
    3.当用new创建对象的时候，首先将在堆上为对象分配足够的存储空间。<br/>
    4.这块存储空间会被清零，基本类型数据都设置成了默认值，而引用责备设置成了null。<br/>
    5.执行所有出现于字段定义出的初始化动作。<br/>
    6.执行构造器。<br/>
**访问控制权限<br/>**
`包：库单元`<br/>
每个编译单元只能有一个public类，否则编译器就不会接受。如果在该编译单元之中还有额外的类的话，那么在包之外的世界是无法看见这些类的。<br/>
`Java访问权限修饰词`<br/>
public:无论是谁，无论在哪里，都可以访问改成员。
不加访问修饰符:放置同一个包内的方式给成员赋予包访问权。其它包内的其他类也就可以访问改成员了。<br/>
protected:包内可访问；包外继承的可访问。<br/>
private:私有。<br/>
`接口和实现`<br/>
在Jdk1.8之前，接口的方法只能是public abstract的；变量必须是public static final的。<br/>
从Jdk1.8开始，接口可以有static方法和default方法。static只能通过接口名调用，default方法只能通过实现了接口的类的对象调用。一个类实现的不同接口可以有相同的static方法；如果有相同的default方法，类需要覆盖该方法，否则编译失败。<br/>
`类的访问权限`<br/>
public和不加访问修饰符。<br/>
**复用类<br/>**
**多态<br/>**
**接口<br/>**
**内部类<br/>**
**容器<br/>**
**异常<br/>**
**字符串<br/>**
**类型信息<br/>**
**泛型<br/>**
**数组<br/>**
**Java I/O系统<br/>**
`File类`<br/>
renameTo()，用来把一个文件重命名（或移动）到由参数所指示的另一个完全不同的新路径（也就是另一个File对象）下面。这同样适用于任意长度的文件目录。<br/>
`输入和输出`<br/>
InputStream类型<br/>
InputStream的作用是用来表示那些从不同数据源产生输入的类。这些数据包括：字节数组、String对象、文件、“管道”、一个由其他种类的流组成的序列及其他数据源（如Internet连接等）。<br/>
ByteArrayInputStream 允许将内存的缓冲区当作InputStream使用 缓冲区、与FilterInputStream对象相连<br/>
StringBufferInputStream 将String转换成InputStream 字符串（底层实现实际使用StringBuffer）、与FilterInputStream对象相连 deprecated<br/>
FileInputStream 用于从文件中读取信息 字符串（表示文件名），文件或FileDescriptor对象、与FilterInputStream对象相连<br/>
PipedInputStream 产生用于写入相关PipedOutput Stream的数据，实现“管道化的概念” PipedOutputStream、作为多线程中的数据源，与FilterInputStream对象相连<br/>
SequenceInputStream 将两个或多个InputStream对象转换成单一InputStream 两个InputStream对象或一个容纳InputStream对象的容器Enumeration、与FilterInputStream对象相连<br/>
FilterInputStream<br/>
OutputStream类型<br/>
ByteArrayOutputStream 在内存中创建缓冲区，所有送往“流”的数据都要放置在此缓冲区 缓冲区初始化尺寸（可选的）、与FilterOutputStream对象相连<br/>
FileOutputStream 用于将信息写至文件 字符串（表示文件名）、文件或FileDescriptor对象、与FilterOutputStream对象相连<br/>
PipedOutputStream 任何写入的信息都会自动作为相关PipedInputStream的输出，实现“管道化”的概念 PipedInputStream、与FilterOutputStream对象相连<br/>
FilterOutputStream<br/>
`添加属性和有用的接口`<br/>
FilterInputStream和FilterOutputStream分别自I/O类库中的基类InputStream和OutputStream派生而来，这两个类是装饰器的必要条件（以便能为所有正在被修饰的对象提供通用接口）<br/>
FilterInputStream类型
DataInputStream 与DataOutputStream他陪使用，因此我们可以按照可移植方式从流读取基本数据类型（int，char，long等） InputStream、包含用于读取基本类型数据的全部接口<br/>
BufferedInputStream 使用它可以防止每次读取时都得进行实际写操作，代表“使用缓冲区” InputStream，可以指定缓冲区的大小（可选的）、与接口对象搭配<br/>
LineNumberInputStream 跟踪输入流的行号；可调用getLineNumber()和setLineNumber(int) InputStream、仅增加了行号，因此可能要与接口对象搭配使用<br/>
PushbackInputStream 具有“能弹出一个字节的缓冲区”，因此可以将督导的最后一个字符回退 InputStream、通常作为编译器的扫描器，之所以包含在内是因为Java编译器的需要，我们可能永远不会用到<br/>
FilterOutputStream类型
DataOutputStream 与DataInputStream他陪使用，因此可以按照可移植方式向流中写入基本类型数据（int，char，long等） OutputStream、包含用于写入基本类型数据的全部接口<br/>
PrintStream 用于产生格式化输出，其中DataOutputStream处理数据的存储，PrintStream处理显示 OutputStream，可以用boolean值只是是否在每次换行时清空缓冲区（可选的）应该是对OutputStream对象的“final”封装，可能会经常使用到它<br/>
BufferedOutputStream 使用它以避免每次发送数据时都要进行实际的写操作，代表“使用缓冲区”，可以调用flush()清空缓冲区 OutputStream，可以指定缓冲区大小（可选的）、与接口对象搭配<br/>
`Reader和Writer`<br/>
Reader和Writer提供兼容Unicode与面向字符的I/O功能<br/>
InputStreamReader可以把InputStream转换为Reader，OutputStreamWriter可以把OutputStream转换为Writer<br/>
Reader和Writer的操作比InputStream和OutputStream更快<br/>
InputStream Reader 适配器：InputStreamReader<br/>
OutputStream Writer 适配器：OutputStreamWriter<br/>
FileInputStream FileReader<br/>
FileOutputStream FileWriter<br/>
StringBufferInputStream（已弃用） StringReader<br/>
（无相应的类） StringWriter<br/>
ByteArrayInputStream CharArrayReader<br/>
ByteArrayOutputStream CharArrayWriter<br/>
PipedInputStream PipedReader<br/>
PipedOutputStream PipedWriter<br/>
BufferedOutputStream是FilterOutputStream的子类，但是BufferedWriter并不是FilterWriter的子类<br/>
FilterInputStream FilterReader<br/>
FilterOutputStream FilterWriter（抽象类，没有子类）<br/>
BufferedInputStream BufferedReader（也有readLine()）<br/>
BufferedOutputStream BufferedWriter<br/>
DataInputStream DataInputStream<br/>
PrintStream PrintWriter<br/>
LineNumberInputStream（已弃用） LineNumberReader<br/>
StreamTokenizer StreamTokenizer（使用接受Reader的构造器）<br/>
PushbackInputStream PushbackReader<br/>
使用readLine()不应该使用DataInputStream（这会遭到编译器的强烈反对），而应该使用BufferedReader<br/>
未发生变化的类<br/>
DataOutputStream<br/>
FileRandomAccessFileSequenceInputStream<br/>
`自我独立的类：RandomAccessFile`<br/>
RandomAccessFile适用于大小已知的记录组成的文件，可以使用seek()将记录从一处转移到另一处，然后读取或者修改记录。文件中记录的大小不一定都相同，只要我们能够确定那些记录有多大以及它们在文件中的位置即可。<br/>
getFilePointer()用于查找当前所处的文件位置，seek()用于在文件内移至新的位置，length()用于判断文件的最大尺寸。<br/>
构造器需要第二个参数用来指示只是“随机读”（r）还是“既写又读”（rw），它不支持只写文件。<br/>
`文件读写的实用工具`<br/>
System.in 是一个没有被包装过的未经加工的InputStream<br/>
System.out 已经实现被包装成了printStream对象<br/>
System.error 已经实现被包装成了PrintStream对象<br/>
System类提供了一些简单的静态方法调用，以允许我们对标准输入、输出和错误I/O流进行重定向：<br/>
setIn(InputStream)<br/>
setOut(PrintStream)<br/>
setError(PrintStream)<br/>
`进程控制`<br/>
java.io.Process
`新I/O`<br/>
ByteBuffer是唯一直接与通道交互的缓冲器。<br/>
FileInputStream、FileOutputStream以及RandomAccessFile被修改，有getChannel()方法，返回FileChannel(通道)。<br/>
warp()方法将已经存在的字节数组“包装”到ByteBuffer中，不再复制底层的数组。<br/>
对于只读访问，必须显示地使用静态的allocate()方法来分配ByteBuffer。<br/>
使用allocateDirect()可能达到更高的速度。<br/>
一旦调用read()来告知FileChannel向ByteBuffer存储字节，就必须调用缓冲器上的flip()，让它做好让别人读取字节的准备。<br/>
如果我们打算使用缓冲器执行进一步的read()操作，我们也必须得调用clear()来为每个read()做好准备。<br/>
调用rewind()方法，返回到数据开始部分。<br/>
“big endian”（高位优先）将最重要的字节存放在地址最低的存储器单元，“little endian”（低位优先）将最重要的字节放在地址最高的存储器单元。ByteBuffer是以高位优先的形式存储数据的，可以使用ByteOrder.Big_ENDIAN或ByteOrder.LITTLE_ENDIAN改变ByteBuffer的字节排序方式。<br/>
Buffer有四个索引：mark（标记），position（位置），limit（界限）和capacity（容量）。
当FileChannel.read()返回-1时，表示我们已经到达输入的末尾。<br/>
transferTo()和transferFrom()允许将一个通道和另一个通道直接相连。<br/>
内存映射文件允许我们创建和修改那些因为太大而不能放入内存的文件。<br/>
文件加锁<br/>
文件锁对其他的操作系统进程是可见的，因为Java的文件加锁直接映射到了本地操作系统的加锁工具。对FileChannel调用tryLock()或lock()，就可以获得整个文件的FileLock。tryLock()是非阻塞式的，它设法获取锁，但是如果不能获得，它将直接从方法调用返回。lock是阻塞时的，它要阻塞进程直至所可以获得，或调用lock()的线程终端，或调用lock()的通道关闭。可以锁文件的某一区域。使用FileLock.release()可以释放锁。锁的类型（共享或独占）可以通过FileLock.isShared()进行查询。<br/>
`压缩`<br/>
压缩类库是按字节方式而不是字符方式处理的。<br/>
压缩类                         功能<br/>
CheckedInputStream      GetCheckSum()为任何InputStream产生校验和（不仅是解压缩）<br/>
CheckedOutputStream     GetCheckSum()为任何OutputStream产生校验和（不仅是压缩）<br/>
DeflaterOutputStream    压缩类的基类<br/>
ZipOutputStream         一个DeflaterOutputStream，用于将数据压缩成Zip文件格式<br/>
GZIPOutputStream        一个DeflaterOutputStream，用于将数据压缩成GZIP文件格式<br/>
InflaterInputStream     解压缩类的基类<br/>
ZipInputStream          一个InflaterInputStream，用于解压缩Zip文件格式的数据<br/>
GZIPInputStream         一个InflaterInputStream，用于解压缩GZIP文件格式的数据<br/>
有两种Checksum类型：Adler32（快一些）和CRC32（慢一些，但更准确）。<br/>
ZipEntry对象包含：名字、压缩的和未压缩的文件大小、日期、CRC校验和、额外字段数据、注释、压缩方法以及它是否是一个目录入口等等。<br/>
Zip格式也没应用于JAR（Java ARchive，Java档案文件）文件格式中。JAR文件中的每个条目都可以加上数字化签名。<br/>
不能够对已有的JAR文件进行添加或更新文件的操作，只能从头创建一个JAR文件。同时，也不能将文件移动至一个JAR文件，并在移动后将它们删除。<br/>
`对象序列化`<br/>
利用对象序列化可以实现轻量级持久性（lightweight persistence）。“持久性”意味着一个对象的生存周期并不取决与程序是否正在执行，它可以生存于程序的调用之间。<br/>
实现Serializable接口。<br/>
要序列化一个对象，首先要创建某些OutputStream对象，然后将其封装在一个ObjectOutputStream对象内。这时，只需调用writeObject()即可将对象序列化，并将其发送给OutputStream（对象序列化是基于字节的，因要使用InputStream和OutputStream继承层次结构）。<br/>
要反向进行该过程，将一个InputStream封装在ObjectInputStream内，再调用readObject()。<br/>
对象序列化能追踪对象内所包含的所有引用，并保存那些对象；接着又能对对象包含的每个这样的引用进行追踪；以此类推。<br/>
必须保证Java虚拟机能找到相关的.class文件。<br/>
Externalizable接口继承了Serializable接口，同时添加了两个方法：writeExternal()和readExternal()。这两个方法会在序列化和反序列化还原的过程中被自动调用，已被执行一些特殊操作。<br/>
Serializable对象，对象完全以它存储的二进制位为基础来构造，而不调用构造器。而对于一个Externalizable对象，所有普通的默认构造器都会被调用（包括在字段定义时的初始化），然后调用readExternal()。<br/>
transient（瞬时）关键字逐个字段地关闭序列化，它的意思是“不用麻烦你保存或回复数据——我自己会处理的”。transient关键字只能和Serializable对象一起使用。序列化会将private数据保存下来。<br/>
实现Serializable接口添加writeObject()和readObject()方法可以一定程度上替代Externalizable。<br/>
相同的流反序列化的对象有相同的地址，不同的流反序列化的对象有不同的地址。<br/>
Serializable接口不能直接序列化static值。<br/>
**枚举<br/>**
**注解<br/>**
