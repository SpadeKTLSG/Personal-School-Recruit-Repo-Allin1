‍

OOM结合项目

‍

# 概念

‍

‍

## 零碎

‍

‍

‍

‍

‍

### static变量存储位置

在JDK 7之前，静态变量存储在永久代（PermGen）中。 永久代是方法区的一部分，用于存储类的元数据，包括类的静态变量、常量池、方法数据等。

从JDK 7->JDK 8 (8)完全移除了永久代，取而代之的是元空间（Metaspace），静态变量存储在其对应的Class对象中。而Class对象作为对象，和其他普通对象一样，都是存在java堆中的。

‍

‍

‍

### JVM 运行时数据区域 RDA 包含哪几部分?

> RDA从类加载子系统拿到目标, 在RDA这个大搅拌机里面处理 <-> 执行引擎

RuntimeDataArea

‍

* 堆 Heap
* 栈 Stack

  1. 本地方法栈 Native Method Stack
  2. 虚拟机栈 Java Virtual Machine Stack
* 程序计数器 Program Counter Register
* 方法区 Method Area

‍

‍

### JVM 执行流程极速版

JVM 的执行流程是，首先先把 Java 代码（.java）转化成字节码（.class），然后通过类加载器将字节码加载到内存中，所谓的内存也就是我们上面介绍的运行时数据区，但字节码并不是可以直接交给操作系统执行的机器码，而是一套 JVM 的指令集。这个时候需要使用特定的命令解析器也就是我们俗称的**执行引擎（Execution Engine）** 将字节码翻译成可以被底层操作系统执行的指令再去执行，这样就实现了整个 Java 程序的运行，这也是 JVM 的整体执行流程。

‍

#### Java 内存区域和 JMM 有何区别？

‍

完全不一样的两个东西：JVM / JUC

* JVM 内存结构 和 Java 虚拟机的运行时区域相关，定义了 JVM 在运行时如何分区存储程序数据，就比如说堆主要用于存放对象实例。
* Java 内存模型和 **Java 的并发编程**相关，抽象了线程和主内存之间的关系

  就比如说线程之间的**共享变量**必须存储在主内存中，规定了从 Java 源代码到 CPU 可执行指令的这个转化过程要遵守哪些和并发相关的原则和规范，其主要目的是为了简化多线程编程，增强程序可移植性的。

‍

‍

### 远程调试IDE原理

IDEA远程调试通过附加到JVM的原理主要涉及以下几个步骤：

1. **JVM启动参数**：在远程服务器上启动JVM时，需要添加特定的调试参数。这些参数允许JVM在特定的端口上监听调试请求。例如：

    ```sh
    java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 -jar your-application.jar
    ```
2. **JDWP协议**：IDEA使用Java Debug Wire Protocol (JDWP)与远程JVM进行通信。JDWP是Java平台调试架构（JPDA）的一部分，定义了调试器和被调试的JVM之间的通信协议。
3. **Socket连接**：IDEA通过网络套接字（Socket）连接到远程JVM的调试端口。IDEA作为客户端，远程JVM作为服务器，监听来自IDEA的调试请求。
4. **调试会话**：一旦连接建立，IDEA可以发送调试命令（如设置断点、单步执行、查看变量等）到远程JVM。JVM执行这些命令并返回结果。
5. **调试信息传输**：调试信息（如线程状态、变量值、堆栈跟踪等）通过JDWP协议在IDEA和远程JVM之间传输。

‍

### Synchronized 可以在静态代码块上加锁吗？

可以。静态代码块上的锁是类级别的锁，而不是对象级别的锁

‍

‍

### java的内存分配是什么样的，哪些在堆上，哪些在栈上？

在Java中，内存分配主要分为堆内存和栈内存：

1. **堆内存**：

    * 用于存储所有的对象实例和数组。
    * 由**垃圾回收器（Garbage Collector）管理**，负责回收不再使用的对象。
    * 所有通过`new`​关键字创建的对象都存储在堆内存中。
2. **栈内存**：

    * 用于存储方法调用的局部变量和方法调用的上下文（如方法参数、局部变量、返回地址等）。
    * 每个线程都有自己的栈内存，栈内存中的数据随着方法的调用和返回而自动分配和释放。
    * 基本数据类型的局部变量（如`int`​、`float`​等）和对象引用（即指向对象的指针）存储在栈内存中。

‍

以下是一个示例，展示了堆内存和栈内存的使用：

```java
public class MemoryAllocationExample {
    public static void main(String[] args) {
        int localVariable = 10; // 存储在栈内存中
        MyObject obj = new MyObject(); // obj引用存储在栈内存中，MyObject实例存储在堆内存中
        obj.setValue(20); // 修改堆内存中对象的值
    }
}

class MyObject {
    private int value; // 存储在堆内存中

    public void setValue(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }
}
```

在这个示例中：

* ​`localVariable`​是一个局部变量，存储在栈内存中。
* ​`obj`​是一个对象引用，存储在栈内存中。
* ​`new MyObject()`​创建的`MyObject`​实例存储在堆内存中。
* ​`MyObject`​实例的成员变量`value`​也存储在堆内存中。

‍

## **JVM由哪些部分组成，运行流程是什么？**

* ClassLoader（类加载器）
* Runtime Data Area（运行时数据区，即java内存）
* Execution Engine（执行引擎）
* Native Method Library（本地库接口）

‍

运行流程：

（1）类加载器（ClassLoader）把Java代码转换为字节码

（2）运行时数据区（Runtime Data Area）把字节码加载到内存中，而字节码文件只是JVM的一套指令集规范，并不能直接交给底层系统去执行，而是有执行引擎运行

（3）执行引擎（Execution Engine）将字节码翻译为底层系统指令，再交由CPU执行去执行，此时需要调用其他语言的本地库接口（Native Method Library）来实现整个程序的功能。

垃圾回收器：用于对JVM中的垃圾内容进行回收

‍

‍

## (运行时数据区) 整体内存模型 + 其运行原理

‍

先说JVM 的种类有很多，比如 HotSpot 虚拟机:  Sun/OracleJDK 和 OpenJDK 中的默认 JVM，也是目前使用范围最广的 JVM。

‍

JVM 其实泛指的是 HotSpot 虚拟机

无论是什么类型的虚拟机都必须遵守 Oracle 官方发布的《Java虚拟机规范》

:JVM 的内存布局分为以下几个部分

---

‍

==JVM内存布局==

‍

‍

* 线程独占 : 栈 (每个便签) + PC (指针)

  * 栈

    * ==虚拟机栈==
    * ==本地方法栈==
  * ==程序计数器==
* 共享内存 (线程) : 堆 (一堆零件) + 方法区 (扳手) 

  * ==堆== ( + 运行时常量池 )
  * ==方法区==

‍

5 个内存区域的主要用途如下

‍

‍

### 1. 堆 ( + 运行时常量池)

堆（Java Heap） 也叫 Java 堆或者是 GC 堆，它是一个线程共享的内存区域，也是 JVM 中占用内存最大的一块区域，Java 中"所有的对象"都存储在这里。垃圾收集器管理的主要区域

‍

运行时常量池：用于 存放class文件中的字面量（文本字符串、被final修饰的常量、基本数据类型值等）和符号引用（字段、方法描述符）。JDK1.7之后JVM将常量池从方法区中移除，直接放入堆中。

> 《Java虚拟机规范》对 Java 堆的描述是：“所有的对象实例以及数组都应当在堆上分配”。但这在技术日益发展的今天已经有点不那么“准确”了，比如 JIT（Just In Time Compilation，即时编译 ）优化中的**逃逸分析**，使得变量可以直接在栈上被分配。

堆大小的值可通过 -Xms 和 -Xmx 来设置（设置最小值和最大值），当堆超过最大值时就会抛出 OOM（OutOfMemoryError）异常。

‍

‍

当对象或者是变量在方法中被创建之后，其指针可能被线程所引用，而这个对象就被称作 指针逃逸或者是引用逃逸。

比如以下代码中的 sb 对象的逃逸：

```java
public static StringBuffer createString() {
    StringBuffer sb = new StringBuffer();
    sb.append("Java");
    return sb;
}
```

sb 虽然是一个局部变量，但上述代码可以看出，它被直接 return 出去了，因此可能被赋值给了其他变量，并且被完全修改，于是此 sb 就逃逸到了方法外部。

想要 sb 变量不逃逸也很简单，可以改return sb.toString();

> 小贴士：通过逃逸分析可以让变量或者是对象**直接在栈上分配**，从而极大地降低了垃圾回收的次数，以及堆分配对象的压力，进而提高了程序的整体运行效率。

‍

新生代细致划分为 Eden、From Survivor、To Survivor。老年代划分为tentired

‍

‍

### 2. 方法区

方法区也称为永久代或是说本地内存的元空间。JDK1.8后使用直接内存的元空间代替了永久代

方法区（Method Area） 也被称为非堆区，用于和“Java 堆”的概念进行区分，它也是线程共享的内存区域，用于存储已经被 JVM 加载的类型信息、常量、静态变量、代码缓存等数据。

‍

‍

> 说到方法区有人可能会联想到 “永久代”，但对于《Java虚拟机规范》来说并没有规定这样一个区域，同样它也只是 HotSpot 中特有的一个概念。这是因为 HotSpot 技术团队把垃圾收集器的分代设计扩展到方法区之后才有的一个概念，可以理解为 HotSpot 技术团队只是用永久代来实现方法区而已，但这会导致一个致命的问题，这样设计更容易造成内存溢出。
>
> 因为永久代有 -XX：MaxPermSize（方法区分配的最大内存）的上限，即使不设置也会有默认的大小。例如，32 位操作系统中的 4GB 内存限制等，并且这样设计导致了部分的方法在不同类型的 Java 虚拟机下的表现也不同，比如 String::intern() 方法。所以在 JDK 1.7 时 HotSpot 虚拟机已经把原本放在永久代的字符串常量池和静态变量等移出了方法区，并且在 JDK 1.8 中完全废弃了永久代的概念。

‍

‍

‍

### 3.程序计数器

我理解的PC, 每个线程都必须有一个私有的

程序计数器（Program Counter Register） 线程独有一块很小的内存区域，保存当前线程所执行字节码的位置，包括正在执行的指令、跳转、分支、循环、异常处理等

‍

‍

### 4.虚拟机栈

虚拟机栈也叫 Java 虚拟机栈（Java Virtual Machine Stack），和程序计数器相同它也是线程独享的，用来描述 Java 方法的执行，在每个方法被执行时就会同步创建一个==栈帧==，用来存储局部变量表、操作栈、动态链接、方法出口等信息。当调用方法时执行入栈，而方法返回时执行出栈。

‍

虚拟机栈由一个个的栈帧组成，每个栈帧包括局部变量表、操作数栈、动态链接、方法出口信息。

* 局部变量表: 存放方法内的局部变量
* 操作数栈：用来执行操作
* 动态链接：用来处理多态的引用
* 返回地址：用来处理返回

‍

‍

### 5.本地方法栈

‍

本地方法栈（Native Method Stacks）与虚拟机栈类似，它是线程独享的，并且作用也和虚拟机栈类似。只不过虚拟机栈是为虚拟机中执行的 Java 方法服务的，而本地方法栈则是为虚拟机使用到的本地（Native）方法服务。

> 小贴士：需要注意的是《Java虚拟机规范》只规定了有这么几个区域，但没有规定 JVM 的具体实现细节，因此对于不同的 JVM 来说，实现也是不同的。例如，“永久代”是 HotSpot 中的一个概念，而对于 JRockit 来说就没有这个概念。所以很多人说的 JDK 1.8 把永久代转移到了元空间，这其实只是 HotSpot 的实现，而非《Java虚拟机规范》的规定。

‍

‍

‍

## JVM 原理

你咋理解的JVM原理 (泛泛谈)

Key

1. 讲标准与实现
2. 跨平台问题
3. JMM内存管理
4. JVM模型
5. 不同的垃圾回收器

‍

> 一段答： jvm是java虚拟机，我们的class文件运行在虚拟机上，通过虚拟机解决了跨平台的问题，jvm中有jmm来管理java内存访问的方式，不同的jvm实现性能关注有差异，现在主流的实现是Hotspot，垃圾回收器是G1，jvm运行时内存中分为方法区，堆，栈，本地方法栈，执行代码时需要执行引擎

‍

‍

## JIT

‍

Java JIT（Just-In-Time）编译器是Java虚拟机（JVM）的一部分，它在程序运行时将字节码（Bytecode）编译为本地机器码，从而提高程序的执行效率。

‍

### 特点：

1. **即时编译**：JIT编译器在程序运行时动态地将字节码编译为机器码，而不是在程序启动前进行编译。
2. **性能优化**：JIT编译器可以进行各种优化，如内联、逃逸分析等，以提高程序的执行效率。
3. **热点代码**：JIT编译器会重点优化那些被频繁执行的代码段（热点代码），以最大化性能提升。

‍

### 工作流程：

1. **字节码加载**：JVM加载Java类文件并将其转换为字节码。
2. **解释执行**：JVM开始解释执行字节码。
3. **热点检测**：JIT编译器监测到某些方法或代码段被频繁执行时，将其标记为热点代码。
4. **即时编译**：JIT编译器将热点代码编译为本地机器码，并替换原来的字节码。
5. **执行优化后的代码**：JVM执行编译后的本地机器码，从而提高执行效率。

‍

### 优点：

* **提高性能**：通过将字节码编译为本地机器码，减少了解释执行的开销。
* **动态优化**：JIT编译器可以根据运行时的实际情况进行优化，适应不同的执行环境。

‍

### 缺点：

* **启动时间较长**：由于需要进行即时编译，程序启动时可能会有一定的延迟。
* **内存占用增加**：编译后的本地机器码需要额外的内存空间。

总结来说，Java JIT编译器通过在运行时将字节码编译为本地机器码，显著提高了Java程序的执行效率。

‍

‍

## 写的代码在CPU怎么跑起来的

‍

1. **编译**：Java 源代码（.java 文件）首先被编译成字节码（.class 文件）。这个过程由 Java 编译器（javac）完成。
2. **类加载**：Java 虚拟机（JVM）启动时，会通过类加载器（ClassLoader）将字节码加载到内存中。
3. **字节码解释**：JVM 内部有一个解释器（Interpreter），它逐行解释字节码并将其转换为机器码，供 CPU 执行。
4. **即时编译（JIT）** ：为了提高性能，JVM 还包含一个即时编译器（Just-In-Time Compiler, JIT）。JIT 会将热点代码（频繁执行的代码）编译成本地机器码，以提高执行效率。
5. **执行**：最终，编译后的机器码在 CPU 上执行。

‍

以下是一个简单的示意图，展示了 Java 代码从编写到在 CPU 上执行的过程：

```plaintext
Java 源代码 (.java)  -->  编译 (javac)  -->  字节码 (.class)  -->  类加载 (ClassLoader)  -->  字节码解释 (Interpreter)  -->  即时编译 (JIT)  -->  机器码  -->  CPU 执行
```

这个过程确保了 Java 代码可以在不同的平台上运行，而无需修改源代码。

‍

‍

## 栈帧是什么

栈帧是函数调用时在栈上分配的一块内存区域，用于存储函数的局部变量、参数、返回地址和其他信息。每次函数调用都会创建一个新的栈帧，函数返回时栈帧会被销毁。

‍

主要组成部分

1. **返回地址**：调用函数后，程序需要知道返回到哪里继续执行。
2. **参数**：传递给函数的参数。
3. **局部变量**：函数内部定义的变量。
4. **保存的寄存器**：保存调用者的寄存器状态，以便函数返回时恢复。

栈帧的结构因编译器和处理器架构而异，但基本原理相同。以下是一个简化的栈帧示意图：

```plaintext
+-----------------+
| 返回地址        |
+-----------------+
| 参数1           |
+-----------------+
| 参数2           |
+-----------------+
| ...             |
+-----------------+
| 局部变量1       |
+-----------------+
| 局部变量2       |
+-----------------+
| ...             |
+-----------------+
| 保存的寄存器状态|
+-----------------+
```

这个结构确保了 函数调用和返回时能够正确管理和恢复程序的执行状态。

‍

‍

## 弱引用啥时候会被回收

1. **没有强引用**：当一个对象只有弱引用指向它时，垃圾回收器会认为该对象是可回收的。
2. **垃圾回收**：在下一次垃圾回收时，垃圾回收器会回收所有只有弱引用指向的对象。

‍

弱引用的主要特点是它不会阻止垃圾回收器回收对象，因此在内存不足时，这些对象会被优先回收。

‍

‍

‍

## java是编译型语言还是解释型语言？.java编译完之后是编译模式还是解释？为什么java要这样设计？为什么不直接设计成解释型语言呢？（因为这样就得每个系统构建单独的解释器）

Java 是一种编译型和解释型相结合的语言。

‍

### 编译和解释过程

1. **编译**：Java 源代码（.java 文件）首先被编译器（javac）编译成字节码（.class 文件）。字节码是一种中间表示形式，与具体的硬件平台无关。
2. **解释**：编译后的字节码由 Java 虚拟机（JVM）解释执行。JVM 是一个解释器，它将字节码逐行解释成机器码并执行。

‍

### 设计原因

1. **跨平台性**：Java 设计成编译和解释相结合的模式，主要是为了实现“一次编写，到处运行”的跨平台特性。字节码与平台无关，可以在任何安装了 JVM 的系统上运行。
2. **性能优化**：JVM 可以在运行时进行各种优化，如即时编译（JIT），将热点代码编译成机器码，提高执行效率。
3. **安全性**：字节码可以在 JVM 中运行，JVM 提供了沙箱机制，可以有效地隔离和保护系统资源，增强安全性。

‍

### 为什么不直接设计成解释型语言

1. **性能**：纯解释型语言的执行效率较低，因为每次执行都需要逐行解释代码。Java 通过编译成字节码并结合 JIT 编译，可以在保持跨平台性的同时提高性能。
2. **优化**：编译成字节码后，JVM 可以在运行时进行各种优化，提高代码执行效率。
3. **开发效率**：编译型语言可以在编译时发现语法和类型错误，提高开发效率和代码质量。

总之，Java 通过编译和解释相结合的设计，实现了跨平台性、性能优化和安全性等多方面的平衡。

‍

‍

‍

## jvm - string都在元空间吗？

字符串并不都在元空间（Metaspace）中

‍

### 1. 字符串常量池

字符串常量池（String Constant Pool）是一个特殊的内存区域，用于存储字符串字面量和通过 `String.intern()`​ 方法创建的字符串。自 Java 7 起，字符串常量池从永久代（PermGen）移到了**堆**（Heap）中。

‍

### 2. 堆内存

**大多数字符串对象是在堆内存中分配的**。每当你使用 `new String()`​ 创建一个新的字符串对象时，它会在堆内存中分配。

‍

### 3. 元空间

元空间（Metaspace）是 Java 8 之后取代永久代的内存区域，用于存储类的元数据（如类的结构、方法、字段等）。字符串对象本身并不存储在元空间中，但类的元数据（如 `java.lang.String`​ 类的定义）会存储在元空间中。

‍

‍

‍

# 大块

‍

### 程序计数器

‍

#### 程序计数器为什么私有

程序计数器主要有下面两个作用：

1. **字节码解释器**通过改变程序计数器来依次**读取指令**，从而实现代码的流程控制，如：顺序执行、选择、循环、异常处理。
2. 在多线程的情况下，程序计数器用于记录当前线程执行的位置，从而当线程被切换回来的时候能够知道该线程上次运行到哪儿了。

‍

需要注意的是，如果执行的是 native 方法，那么程序计数器记录的是 undefined 地址，只有执行的是 Java 代码时程序计数器记录的才是下一条指令的地址。

所以，程序计数器私有主要是为了**线程切换后能恢复到正确的执行位置, 就是保证其正常功能的进行**

‍

‍

#### 虚拟机栈和本地方法栈为什么是私有的?

* **虚拟机栈：**  每个 Java 方法在执行的同时会创建一个栈帧用于存储局部变量表、操作数栈、常量池引用等信息。从方法调用直至执行完成的过程，就对应着一个栈帧在 Java 虚拟机栈中入栈和出栈的过程。
* **本地方法栈：**  和虚拟机栈所发挥的作用非常相似，区别是： **虚拟机栈为虚拟机执行 Java 方法 （也就是字节码）服务，而本地方法栈则为虚拟机使用到的 Native 方法服务。**  在 HotSpot 虚拟机中和 Java 虚拟机栈合二为一。

所以，为了**保证线程中的局部变量不被别的线程访问到**，虚拟机栈和本地方法栈是线程私有的。

‍

‍

## 类加载

‍

类的生命周期会经历以下 7 个阶段：

1. **加载** （Loading）
2. **连接** （Linking）

    1. 验证 （Verification）
    2. 准备 （Preparation）
    3. 解析 （Resolution）
3. **初始化**（Initialization）

    ---
4. 使用阶段（Using）
5. 卸载阶段（Unloading）

‍

平常所说的 JVM 类加载通常指的就是前五个阶段：加载、验证、准备、解析、初始化等

‍

> * 加载：第一步通过全类名获取定义此类的二进制字节流。第二步将字节流所代表的静态存储结构转换为方法区的数据结构。第二部在内存中生成一个代表该类的Class对象，作为方法区这些数据访问的入口。加载阶段需要用到类加载器。
> * 验证：校验一下.class文件是否正确，比如文件格式、语义方面、符号方面等。
> * 准备：主要为类变量分配内存并设置初始值（数据类型的默认值而不是被赋与的默认值）。类变量主要是在方法区中操作。其中类变量会分配内存，而实例变量不会，实例变量随着对象实例化分配到堆内存中。
> * 解析：将常量池中符号引用转化为直接引用。主要针对类、接口、字段、方法、方法类型等的引用。
> * 初始化：主要为类的静态变量赋值，可以通过类变量指定初始值或者静态代码块指定初始值。（类的初始化触发条件：new一个类/调用类的静态变量或方法/反射/初始化类的子类）。

‍

‍

### 1. 加载阶段

此阶段用于查到相应的类（通过类名进行查找）并将此类的字节流转换为方法区运行时的数据结构，然后再在内存中生成一个能代表此类的 `java.lang.Class`​ 对象，作为其他数据访问的入口。

> 小贴士：需要注意的是加载阶段和连接阶段的部分动作有可能是**交叉执行**的，比如一部分字节码文件格式的验证，在加载阶段还未完成时就已经开始验证了。

‍

---

连接

---

### 2. 验证阶段

校验 + 拆包

此步骤主要是为了验证字节码的安全性，如果不做安全校验的话可能会载入非安全或有错误的字节码，从而导致系统崩溃，它是 JVM 自我保护的一项重要举措。

验证的主要动作大概有以下几个：

* **文件格式校验**包括常量池中的常量类型、Class 文件的各个部分是否被删除或被追加了其他信息等； 检查类文件的魔数 0xCAFEBABE 以确保文件格式正确
* **元数据校验**包括父类正确性校验（检查父类是否有被 final 修饰）、抽象类校验等；
* **字节码校验**，此步骤最为关键和复杂，主要用于校验程序中的语义是否合法且符合逻辑；
* **符号引用校验**，对类自身以外比如常量池中的各种符号引用的信息进行匹配性校验。

‍

‍

### 3. 准备阶段

初始化 + 分配内存

此阶段是用来**初始化**并为类中定义的**静态变量分配内存**的，这些**静态变量会被分配到方法区**上 -> HotSpot 虚拟机在 JDK 1.7 之前都在方法区，而 JDK 1.8 之后此变量会随着类对象一起存放到 Java 堆中。

‍

‍

### 4. 解析阶段

翻译 + 连接

此阶段主要是用来解析类、接口、字段及方法的，解析时会把符号引用替换成直接引用。

所谓的符号引用是指以一组符号来描述所引用的目标，符号可以是任何形式的字面量，只要使用时能无歧义地定位到目标即可；而直接引用是可以直接指向目标的指针、相对偏移量或者是一个能间接定位到目标的句柄。

符号引用和直接引用有一个重要的区别：使用符号引用时被引用的目标不一定已经加载到内存中；而**使用直接引用时，引用的目标必定已经存在虚拟机的内存中了**。

‍

‍

### 5. 初始化

初始化阶段 JVM 就正式开始执行类中编写的 Java 业务代码了。到这一步骤之后，类的加载过程就算正式完成了。

‍

‍

‍

### 加载 class 文件原理

‍

关键点：

1. 类加载器
2. 魔数
3. 元空间

负责加载class文件，class文件在文件开头有特定的文件标示，并且ClassLoader只负责class文件的加载，至于它是否可以运行，则由Execution Engine决定。

‍

‍

#### **魔数 0xCAFEBABE**

* Class文件开头的四个字节的无符号整数称为魔数(Magic Number)
* 魔数是Class文件的标识。值是固定的，为**0xCAFEBABE**
* 如果一个Class文件的头四个字节不是0xCAFEBABE，虚拟机在进行文件校验的时候会报错。使用魔数而不是扩展名来识别Class文件，主要是基于安全方面的考虑，因为文件扩展名可以随意更改。

‍

‍

#### 类加载器

分为四种：前三种为虚拟机自带的加载器。

* 启动类加载器（Bootstrap）C++

  负责加载$JAVA_HOME中jre/lib/**rt.jar**里所有的class，由C++实现，不是ClassLoader子类

  也叫系统类加载器，负责加载**classpath**中指定的jar包及目录中class
* 扩展类加载器（Extension）Java

  负责加载java平台中**扩展功能**的一些jar包，包括$JAVA_HOME中jre/lib/*.jar或-Djava.ext.dirs指定目录下的jar包
* 应用程序类加载器（AppClassLoader）Java
* 用户自定义加载器  Java.lang.ClassLoader的子类，用户可以定制类的加载方式

‍

简洁

* BootStrap ClassLoader：最顶层加载器，主要加载核心类库。
* Extention ClassLoader：扩展的类加载器，加载扩展包的类库。
* App classLoader：加载当前应用的根目录下所有类。
* 自定义类加载器，继承ClassLoader。

‍

‍

#### 类加载器工作过程

* 1、当AppClassLoader加载一个class时，它首先不会自己去尝试加载这个类，而是把类加载请求委派给父类加载器ExtClassLoader去完成。
* 2、当ExtClassLoader加载一个class时，它首先也不会自己去尝试加载这个类，而是把类加载请求委派给BootStrapClassLoader去完成。
* 3、如果BootStrapClassLoader加载失败（例如在$JAVA_HOME/jre/lib里未查找到该class），会使用ExtClassLoader来尝试加载；
* 4、若ExtClassLoader也加载失败，则会使用AppClassLoader来加载
* 5、如果AppClassLoader也加载失败，则会报出异常ClassNotFoundException

其实这就是所谓的**双亲委派模型**。简单来说：如果一个类加载器收到了类加载的请求，它首先不会自己去尝试加载这个类，而是把**请求委托给父加载器去完成，依次向上**。

‍

好处：**防止内存中出现多份同样的字节码**(安全性角度)  
比如加载位于 rt.jar 包中的类 java.lang.Object，不管是哪个加载器加载这个类，最终都是委托给顶层的启动类加载器进行加载，这样就保证了使用不同的类加载器最终得到的都是同样一个 Object对象。

‍

‍

### 类加载的双亲委派机制

‍

‍

‍

## 垃圾回收

‍

### GC触发类型

* young GC：当新生代中的eden区内存满时会触发young GC，GC过后新生代一部分存活对象可能会升级到老年代中，导致老年代占用量上升。
* full GC：每次触发young GC时会判断GC后升级到老年代的对象占用内存是否大于老年代剩余的内存，如果大于，那么就不触发young GC转而触发full GC。如果老年代或者持久代被写满时也会触发full GC。调用System.gc()方法时也会触发full GC（一般GC由虚拟机决定，不会手动调用，即使调用了也不一定会触发）

‍

‍

### 类引用类型

1. 强引用：常用的普通对象的引用，**当JVM内存不足时会抛出OutOfMemoryError错误使程序停止**，也不会去回收强引用的对象。**被赋值为null**后可以被垃圾收集器回收。
2. 软引用：通过SoftReference类实现，当JVM**内存不足时，才会去回收软引用的对象**，以防止出现OutOfMemoryError错误，可以调用ReferenceQueue的poll()方法来检查指定对象是否被回收，软引用可以用于内存不足的缓存中。
3. 弱引用：通过WeakReference类实现，当垃圾收集器发现了弱引用的对象，**不管当前内存空间是否足够，都会回收对象**，因为垃圾回收器是一个优先级很低的线程，因此弱引用可能会存活很长一段时间，弱引用被回收时，会把弱引用假如到与之关联的引用队列ReferenceQueue中。
4. 虚引用：通过PhantomReference类实现，我们无法通过虚引用访问对象，垃圾收集器随时可以回收它。当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会在回收对象的内存之前，把这个虚引用加入到与之关联的引用队列中。可以通过判断是否加入了引用对象来判断对象是否被回收。

‍

‍

## 垃圾回收算法

垃圾回收器首先要做的就是，判断一个对象是存活状态还是死亡状态，死亡的对象将会被标识为垃圾数据并等待收集器进行清除。

判断一个对象是否为死亡状态的常用算法有两个：引用计数器算法和可达性分析算法。

‍

### 死亡确认

(找到垃圾才能进行)

‍

#### **引用计数算法（Reference Counting）**

属于垃圾收集器最早的实现算法了，它是指在创建对象时关联一个与之相对应的计数器，当此对象被使用时加 1，相反销毁时 -1。当此计数器为 0 时，则表示此对象未使用，可以被垃圾收集器回收。

‍

优点是垃圾回收比较及时，实时性比较高，只要对象计数器为 0，则可以直接进行回收操作

缺点是无法解决循环引用的问题

‍

‍

‍

#### **可达性分析算法（Reachability Analysis）**

是目前商业系统中所采用的判断对象死亡的常用算法，它是指从对象的起点（GC Roots）开始向下搜索，如果对象到 GC Roots 没有任何引用链相连时，也就是说此对象到 GC Roots 不可达时，则表示此对象可以被垃圾回收器所回收

‍

‍

**GC Roots**

在 Java 中可以作为 GC Roots 的对象，主要包含以下几个：

* 所有被**同步锁**持有的对象，比如被 synchronize 持有的对象

  > 这些对象在多线程环境中被锁定，确保它们在同步块或方法执行期间不会被垃圾回收
  >
* **字符串常量池**里的引用（String Table）

  > 字符串常量池中的字符串是全局共享的，JVM 会确保这些字符串在整个程序运行期间都存在，因此它们不会被垃圾回收。
  >
* 类型为引用类型的静态变量；

  > 静态变量属于类本身，而不是类的实例。只要类被加载，静态变量就会存在，因此它们不会被垃圾回收。
  >
* **栈**中的对象

  * 虚拟机栈中引用对象；

    > 方法执行时，局部变量表中的引用对象是活动的，JVM 会确保这些对象在方法执行期间不会被垃圾回收。
    >
  * 本地方法栈中的引用对象。

    > 本地方法栈中的引用对象是本地方法调用时使用的，JVM 会确保这些对象在本地方法执行期间不会被垃圾回收。
    >

‍

主要就是不会被垃圾回收的玩意

‍

‍

‍

#### 死亡对象判断

‍

当使用可达性分析判断一个对象不可达时，并不会直接标识这个对象为死亡状态，而是先将它标记为“待死亡”状态再进行一次校验。校验的内容就是此对象**是否重写了 finalize() 方法**

如果该对象重写了 finalize() 方法，那么这个对象将会被存入到 F-Queue 队列中，等待 JVM 的 Finalizer 线程去执行重写的 finalize() 方法，在这个方法中如果此对象将自己赋值给某个类变量时，则表示此对象已经被引用了。因此不能被标识为死亡状态，其他情况则会被标识为死亡状态。

‍

```java
public class FinalizeTest {
    // 需要状态判断的对象
    public static FinalizeTest Hook = null;

    @Override
    protected void finalize() throws Throwable {
        super.finalize();
        System.out.println("执行了 finalize 方法");
        Fi nalizeTest.Hook = this;
    }

    public static void main(String[] args) throws InterruptedException {
        Hook = new FinalizeTest();
        // 卸载对象，第一次执行 finalize()
        Hook = null;
        System.gc();
        Thread.sleep(500); // 等待 finalize() 执行
        if (Hook != null) {
            System.out.println("存活状态");
        } else {
            System.out.println("死亡状态");
        }
        // 卸载对象，与上一次代码完全相同
        Hook = null;
        System.gc();
        Thread.sleep(500); // 等待 finalize() 执行
        if (Hook != null) {
            System.out.println("存活状态");
        } else {
            System.out.println("死亡状态");
        }
    }
}
```

上述代码的执行结果为：

```text
执行了 finalize 方法
存活状态
死亡状态
```

‍

从结果可以看出，卸载了两次对象，第一次执行了 finalize() 方法，成功地把自己从待死亡状态拉了回来；而第二次同样的代码却没有执行 finalize() 方法，从而被确认为了死亡状态，这是因为**任何对象的 finalize() 方法都只会被系统调用一次**。

虽然可以从 finalize() 方法中把自己从死亡状态“拯救”出来，但是不建议这样做，因为所有对象的 finalize() 方法只会执行一次。因此同样的代码可能产生的结果是不同的，这样就给程序的执行带来了很大的不确定性。

‍

‍

‍

‍

### 垃圾回收算法

(狭义)

当确定了对象的状态之后（存活还是死亡）接下来就是进行垃圾回收了，垃圾回收的常见算法有以下几个：

* 标记-清除算法；
* 标记-复制算法；
* 标记-整理算法。

‍

‍

#### **标记-清除**

(搜寻并歼灭 Search and destroy)

 **（Mark-Sweep）**

算法属于最早的垃圾回收算法，它是由标记阶段和清除阶段构成的。标记阶段会给所有的存活对象做上标记，而清除阶段会把没有被标记的死亡对象进行回收。而标记的判断方法就是前面讲的引用计数算法和可达性分析算法。 会产生内存空间的碎片化问题

‍

#### **标记-复制**

(两半)

是标记-清除算法的一个升级，使用它可以有效地解决内存碎片化的问题。它是指将内存分为大小相同的两块区域，每次只使用其中的一块区域，这样在进行垃圾回收时就可以直接将存活的东西复制到新的内存上，然后再把另一块内存全部清理掉。这样就不会产生内存碎片的问题了

‍

#### **标记-整理**

(紧凑

诞生晚于标记-清除算法和标记-复制算法，它也是由两个阶段组成的：标记阶段和整理阶段。

其中标记阶段和标记-清除算法的标记阶段一样，不同的是后面的一个阶段，标记-整理算法的后一个阶段不是直接对内存进行清除，而是把所有存活的对象移动到内存的一端紧密排列好，然后把另一端的所有死亡对象全部清除 (将所有存活的对象往左端空闲空间移动，并更新对应指针)

‍

‍

#### 分代收集模型

目前商用虚拟机的垃圾收集器都是基于分代收集的理论进行设计的

指将**不同“年龄”** 的数据**分配到不同的内存区域**中进行存储，所谓的“年龄”指的是**经历过垃圾收集的次数**。一般(JAVA堆)分为老年代、新生代和永久代。

这样就可以把那些朝生暮死的对象集中分配到一起，把不容易消亡的对象分配到一起，对于不容易死亡的对象我们就可以设置较短的垃圾收集频率，这样就能消耗更少的资源来实现更理想的功能了

‍

通常情况下分代收集算法会分为两个区域：新生代（Young Generation）和老年代（Old Generation），其中新生代用于存储刚刚创建的对象，这个区域内的对象存活率不高，而对于经过了一定次数的 GC 之后还存活下来的对象，就可以成功晋级到老生代了。

> 说一下对于不同的实现有表述上的区别, 各自的具体结构也有不同

‍

可以根据不同代采用不同收集算法，提高了垃圾回收效率:

* 老年代特点是每次垃圾收集时只有少量对象被回收，所以适合采用**标记整理**算法
* 新生代特点是每次垃圾回收时都有大量的对象需要被回收，所以适合采用**复制算法**，每次只需要复制少量存活对象

‍

### 讲一下新生代、老年代、永久代的区别？

**新生代**主要用来存放新生的对象。新生代又被进一步划分为 **Eden区** 和 **Survivor区**，Survivor 区由 **From Survivor** 和 **To Survivor** 组成

**老年代**主要存放应用中生命周期长的内存对象。

**永久代**指的是永久保存区域。主要存放Class和Meta（元数据）的信息。在Java8中，永久代已经被移除，取而代之的是一个称之为“元数据区”（**元空间**）的区域。元空间和永久代类似，不过元空间与永久代之间最大的区别在于：元空间并不在虚拟机中，而是使用本地内存。因此，默认情况下，元空间的大小仅受本地内存的限制。

‍

‍

## 垃圾回收器

‍

### 哪些?

用过哪些垃圾回收器？它们有什么区别？(最简单)

‍

先讲比较常用的虚拟机是 OracleJDK 中自带的 HotSpot 虚拟机, 然后介绍 HotSpot 中使用的垃圾收集器主要包括 7 个：

**Serial、ParNew、Parallel Scavenge、|| Serial Old、Parallel Old、CMS 和 G1（Garbage First）收集器**

‍

‍

#### **Serial 收集器**

(默认新生代)

最早期的垃圾收集器，也是 JDK 1.3 版本之前唯一的垃圾收集器。

单线程运行的垃圾收集器，其单线程是指在进行垃圾回收时所有的工作线程必须暂停 STW ，直到垃圾回收结束为止.

简单和高效，并且本身的运行对内存要求不高，因此它在客户端模式下使用的比较多

‍

‍

#### **ParNew 收集器**

(默认新生代)

Serial 收集器的多线程并行版本

‍

‍

#### **Parallel Scavenge 收集器**

(默认新生代)

和 ParNew 收集器类似，它也是一个并行运行的垃圾回收器；

不同的是，该收集器关注的侧重点是**实现一个可以控制的吞吐量**。

而这个吞吐量计算的也很奇怪，它的计算公式是：用户运行代码的时间 / （用户运行代码的时间 + 垃圾回收执行的时间）。比如用户运行的时间是 8 分钟，垃圾回收运行的时间是 2 分钟，那么吞吐量就是 80%。Parallel Scavenge 收集器追求的目标就是将这个吞吐量的值，控制在一定的范围内。

‍

Parallel Scavenge 收集器有两个重要的参数：

* -XX:MaxGCPauseMillis 参数：它是用来控制垃圾回收的最大停顿时间；
* -XX:GCTimeRatio 参数：它是用来直接设置吞吐量的值的。

‍

‍

#### **Serial Old 收集器**

Serial GC 老年代版本

‍

#### Parallel Old 收集器

Parallel Scavenge GC 老年代版本

‍

‍

#### **CMS（Concurrent Mark Sweep）收集器**

(默认老年代)

与以吞吐量为目标的 Parallel Scavenge 收集器不同，它强调的是提供**最短的停顿时间**，因此可能会**牺牲一定的吞吐量**

主要应用在 Java Web 项目中，以此来提高用户的交互体验。

‍

‍

##### 具体执行流程: Why 停顿时间短

> 加分项

CMS 收集器是基于**标记-清除**算法实现的 (最呆的一个)

‍

整个过程可以分为四个阶段：

* 初始标记（CMS initial mark）
* 并发标记（CMS concurrent mark）
* 重新标记（CMS remark）
* 并发清除（CMS concurrent sweep）

**初始标记**阶段的执行时间很短，它只是标记一下 GC Roots 的关联对象；

**并发标记**​阶段是从 GC Roots 关联的对象进行遍历判断并标识死亡对象，这个过程比较慢，但不需要停止用户线程，用户的线程可以和垃圾收集线程并发执行；

**重新标记**阶段则是为了判断并标记，刚刚并发阶段用户**继续运行**的那一部分对象，所以此阶段的执行时间也比较短；(回首掏)

**并发清除**阶段，也就是清除上面标记的死亡对象，由于 CMS 使用的是**标记-清除**算法，而非**标记-整理**算法，因此无须移动存活的对象，这个阶段垃圾收集线程也可以和用户线程并发执行。

CMS 的整个执行过程中只有执行时间很短的==初始标记==和==重新标记==需要 Stop The World（全局停顿）的

‍

**执行过程**

```java
用户线程组->     |               | 用户线程组->  |                | 用户线程组->      |
               |    STW初始标记->   | 并发标记->   |   STW重新标记->    | 并发清理->        |
```

‍

##### 碎片处理 : **标记-清除的处理方案**

因为 CMS 是一款基于标记清除算法实现的垃圾收集器，因此会在收集时产生**大量的空间碎片**，为了解决这个问题，CMS 收集器提供了一个 `-XX:+UseCMS-CompactAtFullCollection`​ 的参数（默认是开启的，此参数从 JDK9 开始废弃），用于在 CMS 收集器**进行 Full GC 时开启内存碎片的合并和整理。**

但又因为碎片整理的过程必须移动存活的对象，所以它和用户线程是无法并发执行的，为了解决这个问题 CMS 收集器又提供了另外一个参数`<span> </span>-XX:CMSFullGCsBefore-Compaction`​，用于规定多少次（根据此参数的值决定）之后再进行一次碎片整理。

‍

‍

‍

‍

#### **Garbage First（简称 G1）收集器**

(整堆收集 - 新 + 老) 混合型

是历史发展的产物，也是一款更先进的垃圾收集器，主要面向服务端应用的垃圾收集器。

将内存划分为多个 **Region 分区**，回收时则**以分区为单位**进行回收，这样它就可以用相对较少的时间**优先回收包含垃圾最多区块**。

从 JDK 9 之后也成了官方默认的垃圾收集器

‍

‍

‍

## OOM综合

当JVM因为没有足够的内存来为对象分配空间并且垃圾回收器也已经没有空间可回收时，就会抛出这个error（注：非exception，因为这个问题已经严重到不足以被应用处理）

> 可以对照我的项目进行处理: 业务场景下发生了什么, 做了什么, 取得了什么结果.

‍

‍

### 为什么

原因不外乎有两点：

* 1）分配的少了：比如虚拟机本身可使用的内存（一般通过启动时的VM参数指定）太少。
* 2）应用用的太多，并且用完没释放，浪费了。此时就会造成内存泄露或者内存溢出。

‍

**内存泄露**：申请使用完的**内存没有释放**，导致虚拟机不能再次使用该内存，此时这段内存就泄露了，因为申请者不用了，而又不能被虚拟机分配给别人用。

**内存溢出**：申请的内存超出了JVM能提供的内存大小，此时称之为溢出。

‍

‍

### OOM类型

‍

**JVM内存模型**

‍

按照JVM规范，JAVA虚拟机在运行时会管理以下的内存区域：

* 程序计数器：当前线程执行的字节码的行号指示器，线程私有
* JAVA虚拟机栈：Java方法执行的内存模型，每个Java方法的执行对应着一个栈帧的进栈和出栈的操作。
* 本地方法栈：类似“ JAVA虚拟机栈 ”，但是为native方法的运行提供内存环境。
* JAVA堆：对象内存分配的地方，内存垃圾回收的主要区域，所有线程共享。可分为新生代，老生代。
* 方法区：用于存储已经被JVM加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。Hotspot中的“永久代”。
* 运行时常量池：方法区的一部分，存储常量信息，如各种字面量、符号引用等。
* **直接内存**：并不是JVM运行时数据区的一部分， 可直接访问的内存， 比如NIO会用到这部分。

‍

按照JVM规范，除了程序计数器不会抛出OOM外，其他各个内存区域都可能会抛出OOM

‍

最常见的OOM情况有以下三种：

**堆内存OOM, 永久代OOM, SOF**

* java.lang.OutOfMemoryError: Java heap space ------>java**堆内存溢出**，此种情况最常见，一般由于内存泄露或者堆的大小设置不当引起。对于内存泄露，需要通过内存监控软件查找程序中的泄露代码，而堆大小可以通过虚拟机参数 ==-Xms, -Xmx== 等修改。
* java.lang.OutOfMemoryError: PermGen space ------>java永久代溢出，即**方法区溢出了**，一般出现于大量Class或者jsp页面，或者采用cglib等反射机制的情况，因为上述情况会产生大量的Class信息存储于方法区。此种情况可以通过更改方法区的大小来解决，使用类似 ==-XX:PermSize=64m -XX:MaxPermSize=256m== 的形式修改。另外，过多的常量尤其是字符串也会导致方法区溢出。
* java.lang.StackOverflowError ------> 不会抛OOM error，但也是比较常见的Java内存溢出: JAVA虚拟机栈溢出，一般是由于程序中存在死循环或者深度递归调用造成的，栈大小设置太小也会出现此种溢出。可以通过虚拟机参数 ==-Xss== 来设置栈的大小。

‍

‍

## heapdump分析

转储堆内存镜像来进行故障排查

‍

要dump(转储)堆的内存镜像，可以采用如下两种方式：

* 设置JVM参数-XX:+HeapDumpOnOutOfMemoryError，设定当发生OOM时自动dump出堆信息 (JDK5以上版本)
* 使用JDK自带的jmap命令。"jmap -dump:format=b,file=heap.bin " 其中pid可以通过jps获取。

‍

dump堆内存信息后，需要对dump出的文件进行分析，从而找到OOM的原因。常用的工具有：

* mat: eclipse memory analyzer, 基于 eclipse RCP 的内存分析工具。详细信息参见：[http://www.eclipse.org/mat/](http://www.eclipse.org/mat/%EF%BC%8C%E6%8E%A8%E8%8D%90%E4%BD%BF%E7%94%A8%E3%80%82) ，推荐使用
* jhat：JDK自带的java heap analyze tool，可以将堆中的对象以html的形式显示出来，包括对象的数量，大小等等，并支持对象查询语言OQL，分析相关的应用后，可以通过http://localhost:7000来访问分析结果。不推荐使用，因为在实际的排查过程中，一般是先在生产环境 dump出文件来，然后拉到自己的开发机器上分析，所以，不如采用高级的分析工具比如前面的mat来的高效。

采用mat分析的例子

‍

注意：因为JVM规范没有对dump出的文件的格式进行定义，所以不同的虚拟机产生的dump文件并不是一样的。在分析时，需要针对不同的虚拟机的输出采用不同的分析工具（当然，有的工具可以兼容多个虚拟机的格式）。IBM HeapAnalyzer也是分析heap的一个常用的工具。

‍

‍

### jmap

​`jmap`​ 是 JDK 提供的一个命令行工具，用于生成 Java 虚拟机 (JVM) 的内存映像（heap dump）和查看内存使用情况。它可以帮助开发者分析内存泄漏、对象分布等问题。

‍

常用的 `jmap`​ 命令

1. **生成堆转储文件**

    ```sh
    jmap -dump:format=b,file=heapdump.hprof <pid>
    ```

    这条命令会生成一个堆转储文件 `heapdump.hprof`​，其中 `<pid>`​ 是目标 JVM 进程的进程 ID。
2. **查看堆内存摘要**

    ```sh
    jmap -heap <pid>
    ```

    这条命令会输出堆内存的使用情况摘要，包括堆配置、使用情况和垃圾收集器信息。
3. **查看对象的直方图**

    ```sh
    jmap -histo <pid>
    ```

    这条命令会输出 JVM 中所有对象的直方图，包括对象的数量和占用的内存。
4. **查看永久代（Metaspace）信息**

    ```sh
    jmap -permstat <pid>
    ```

    这条命令会输出永久代（或 Metaspace）的类加载器信息和类的内存使用情况。

‍

‍

# 高级

‍

## 逃逸分析

通过逃逸分析，Java Hotspot编译器能够分析出一个新的对象的引用的使用范围从而决定是否要将这个对象分配到堆上。

逃逸分析的基本行为就是分析对象动态作用域：当一个对象在方法中被定义后，它可能被外部方法所引用，例如作为调用参数传递到其他地方中，称为方法逃逸。

使用逃逸分析，编译器可以对代码做如下优化：

1. 同步省略。如果一个对象被发现只能从一个线程被访问到，那么对于这个对象的操作可以不考虑同步。
2. 将堆分配转化为栈分配。如果一个对象在子程序中被分配，要使指向该对象的指针永远不会逃逸，对象可能是栈分配的候选，而不是堆分配。
3. 分离对象或标量替换。有的对象可能不需要作为一个连续的内存结构存在也可以被访问到，那么对象的部分（或全部）可以不存储在内存，而是存储在CPU寄存器中。

‍

## 类加载器

启动类加载器：用C++语言实现，是虚拟机自身的一部分，它负责将 <JAVA_HOME>/lib路径下的核心类库，无法被Java程序直接引用  
扩展类加载器：用Java语言实现，它负责加载<JAVA_HOME>/lib/ext目录下或者由系统变量-Djava.ext.dir指定位路径中的类库，开发者可以直接使用  
系统类加载器：用Java语言实现，它负责加载系统类路径ClassPath指定路径下的类库，开发者可以直接使用

‍

## JVM调优

前提：在进行GC优化之前，需要确认项目的架构和代码等已经没有优化空间

目的：优化JVM垃圾收集性能从而增大吞吐量或减少停顿时间，让应用在某个业务场景上发挥最大的价值。吞吐量是指应用程序线程用时占程序总用时的比例。暂停时间是应用程序线程让与GC线程执行而完全暂停的时间段

对于交互性web应用来说，一般都是减少停顿时间，所以有以下方法：

1. 如果应用存在大量的短期对象，应该选择较大的年轻代；如果存在相对较多的持久对象，老年代应该适当增大
2. 让大对象进入年老代。可以使用参数-XX:PetenureSizeThreshold 设置大对象直接进入年老代的阈值。当对象的大小超过这个值时，将直接在年老代分配
3. 设置对象进入年老代的年龄。如果对象每经过一次 GC 依然存活，则年龄再加 1。当对象年龄达到阈值时，就移入年老代，成为老年对象
4. 使用关注系统停顿的 CMS 回收器

基础：[https://www.ibm.com/developerworks/cn/java/j-lo-jvm-optimize-experience/index.html](https://www.ibm.com/developerworks/cn/java/j-lo-jvm-optimize-experience/index.html)

案例：[https://www.wangtianyi.top/blog/2018/07/27/jvmdiao-you-ru-men-er-shi-zhan-diao-you-parallelshou-ji-qi/](https://www.wangtianyi.top/blog/2018/07/27/jvmdiao-you-ru-men-er-shi-zhan-diao-you-parallelshou-ji-qi/)
