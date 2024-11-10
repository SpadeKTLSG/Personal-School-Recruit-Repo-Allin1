‍

‍

### Header

‍

‍

‍

‍

# 概念

‍

## 零碎

‍

### 方法签名包含哪些部分? 如果两个方法的返回值不同其他的都一样，那就是可以形成重写或者重载吗？ 会有什么问题

‍

方法签名包含以下部分：

1. 方法名
2. 参数列表（参数的类型和顺序）

‍

方法签名不包括返回值类型和方法的修饰符（如 `public`​、`static`​ 等）。

‍

如果两个方法的返回值不同，但方法名和参数列表相同，这不会形成重载或重写。编译器会报错，因为它们的签名是相同的，无法区分这两个方法。

例如，以下代码会导致编译错误：

```java
public class Example {
    public int method(int a) {
        return a;
    }

    public double method(int a) { // 编译错误：方法签名相同
        return a;
    }
}
```

重载是指在同一个类中，方法名相同但参数列表不同的方法。重写是指子类重新定义父类中的方法，方法签名必须与父类方法相同。

‍

‍

### 快排时间复杂度和二分查找时间复杂度是什么?

快速排序（QuickSort）的时间复杂度和二分查找（Binary Search）的时间复杂度如下：

1. **快速排序（QuickSort）** ：

    * 最佳情况：O(n \* log n)
    * 平均情况：O(n \* log n)
    * 最坏情况：O(n^2)
2. **二分查找（Binary Search）** ：

    * 最佳情况：O(1)
    * 平均情况：O(log n)
    * 最坏情况：O(log n)

‍

### throw 在方法体内抛出具体异常对象，中断程序流程；throws 在方法签名抛出可能出现的异常类型，需要调用者处理。

‍

### ArrayList 的扩容机制

ArrayList list = new ArrayList(20)中的 list 扩充几次 : 有传参，没必要扩容，所以次数是0

ArrayList 的扩容机制是通过增加其内部数组的容量来实现的。每当需要添加元素且当前容量不足时，ArrayList 会创建一个更大的新数组，并将旧数组中的元素复制到新数组中。

‍

扩容机制的关键点：

* 初始容量：默认初始容量为10。
* 扩容因子：每次扩容时，新容量为旧容量的**1.5倍**（具体为oldCapacity + (oldCapacity >> 1)）。
* 复制元素：扩容时，会将旧数组中的元素**复制到新数组中**。

‍

‍

### 常用字符编码所占字节数？

‍

​`utf8`​ (UTF, 全部可用, 但是中文要处理) :英文占 1 字节，中文占 3 字节，`unicode`​ (统一码, 统一规格) ：任何字符都占2 个字节，`gbk`​ (中文专用码) ：英文占 1 字节，中文占 2 字节

‍

‍

### 哈希函数的关键特性包括：

* 高效率的计算过程

  * 高效使用
* 雪崩效应  

  * 输入的微小变化（例如一个比特的变化）会导致输出的哈希值有显著变化。这种特性确保了哈希值的均匀分布，增加了哈希函数的安全性和抗碰撞性。
* 输出长度固定

  * 无论输入数据的长度如何，哈希函数的输出长度都是固定的。这使得哈希值在存储和比较时更加方便和高效。

‍

‍

### **变量初始化是否是原子操作**

在Java中，变量初始化并不总是原子操作。具体情况取决于变量的类型和初始化的方式。

1. **基本数据类型**：

    * 对于基本数据类型（如`int`​、`float`​、`boolean`​等），变量的初始化是原子操作。例如：

      ```java
      int a = 5; // 原子操作
      ```
2. **引用类型**：

    * 对于引用类型，变量的初始化也是原子操作。例如：

      ```java
      String str = "Hello"; // 原子操作
      ```
3. **64位数据类型**：

    * 对于64位的数据类型（如`long`​和`double`​），在某些平台上，变量的初始化可能不是原子操作。例如：

      ```java
      long l = 123456789L; // 可能不是原子操作
      ```

      在32位的机器上，变量的读写操作可能需要分两次进行，因为32位机器一次只能处理32位的数据。这意味着在多线程环境中，可能会出现一个线程在读写64位数据时被另一个线程打断的情况，从而导致数据不一致。
4. **对象的初始化**：

    * 对于对象的初始化，构造函数的执行不是原子操作。例如：

      ```java
      MyObject obj = new MyObject(); // 不是原子操作
      ```

总结：基本数据类型和引用类型的变量初始化通常是原子操作，但对于**64位数据类型**和**对象的初始化**，可能不是原子操作。

‍

### HashMap变成红黑树之后还会不会变回链表

减少到一定程度（默认是6）以下, 会节省开销.

‍

‍

### Java反序列化的原理是什么? 为什么会有反序列化漏洞? 有哪些好用的反序列化工具吗？

Java反序列化的原理是将字节流转换回Java对象。反序列化的过程是通过读取字节流并重建对象的状态来实现的。以下是反序列化的基本步骤：

1. **读取字节流**：从输入流中读取字节数据。
2. **创建对象**：根据字节数据创建对象实例。
3. **恢复状态**：将对象的状态恢复到序列化时的状态。

‍

反序列化漏洞通常发生在不安全的反序列化过程中，攻击者可以通过构造恶意的字节流来执行任意代码或破坏系统。主要原因包括：

1. **不可信数据源**：从不可信的数据源反序列化数据，可能会导致恶意数据被执行。
2. **类加载机制**：Java的类加载机制允许在反序列化过程中加载任意类，这可能被攻击者利用。
3. **缺乏验证**：反序列化过程中缺乏对数据的验证和过滤，导致恶意数据被执行。

‍

为了防止反序列化漏洞，可以采取以下措施：

1. **避免反序列化不可信数据**：尽量避免从不可信的数据源反序列化数据。
2. **使用白名单**：使用白名单机制，只允许反序列化特定的类。
3. **使用安全的反序列化库**：使用安全的反序列化库，如Gson、Jackson等。

‍

以下是一些常用的反序列化工具：

1. **Java自带的反序列化工具**：使用`ObjectInputStream`​进行反序列化。
2. **Gson**：用于JSON格式的反序列化。
3. **Jackson**：用于JSON格式的反序列化。

‍

### 现在c继承b b继承a,a可以强转成b吗，c可以强转b吗? 你想想子类不是有父类没有的东西吗，我父类强转成子类，那么东西怎么办？

> 要分a实际指向的是是它自己这个老登还是小登.

父类强制转换成子类：这是不安全的，除非你确定这个对象实际上是子类的实例。否则会在运行时抛出ClassCastException。

子类强制转换成父类：这是安全的，因为子类对象总是包含父类的所有属性和方法。

‍

‍

### 异常种类

在Java中，异常分为两大类：受检异常（Checked Exception）和非受检异常（Unchecked Exception）

‍

1. **受检异常（Checked Exception）** ：  
    受检异常是==编译时异常==，必须在代码中显式地捕获或声明。常见的受检异常包括：

    * ​`IOException`​ IO经典
    * ​`SQLException`​ SQL
2. **非受检异常（Unchecked Exception）** ：  
    非受检异常是==运行时异常==，不需要显式地捕获或声明。常见的非受检异常包括：

    * ​`NullPointerException`​ 空指针一生之敌
    * ​`ArrayIndexOutOfBoundsException`​ 经典

对立的(特殊)的异常类型：**错误（Error）** ，它们表示应用程序无法处理的严重问题，例如内存不足（`OutOfMemoryError`​）

‍

‍

### 值传递与引用传递的区别

Java 的参数是以**==值传递==**的形式传入方法中

值传递和引用传递的区别在于传递后会不会影响实参的值：**值传递会创建副本**，引用传递不会创建副本

‍

* 基本数据类型：形式参数的改变，==不影响实际参数==

  每个方法在栈内存中，都会有独立的栈空间，方法运行结束后就会弹栈消失
* 引用类型：形式参数的改变，==影响实际参数的值==

  **引用数据类型的传参，本质上是将对象的地址以值的方式传递到形参中**，内存中会造成两个引用指向同一个内存的效果，所以即使方法弹栈，堆内存中的数据也已经是改变后的结果

‍

‍

## Object常用方法

‍

**toString**

‍

**equals**

默认比较两个引用变量是否指向同一个对象（内存地址）。可以重写equals方法，按照age和name是否相等来判断

‍

**hashCode**

将与对象相关的信息映射成一个哈希值，默认的实现hashCode值是根据内存地址换算的

‍

**clone**

Java赋值是复制对象引用，如果我们想要得到一个对象的副本，使用赋值操作是无法达到目的的。Object对象有个clone()方法，实现了对象中各个属性的复制，但它的可见范围是protected的。

所以实体类使用克隆的前提是：

* 实现Cloneable接口，这是一个标记接口，自身没有方法，这应该是一种约定。调用clone方法时，会判断有没有实现Cloneable接口，没有实现Cloneable的话会抛异常CloneNotSupportedException。
* 覆盖clone()方法，可见性提升为public。

‍

---

​`Object`​ 类是 Java 中所有类的超类，它提供了一些基本的方法，这些方法可以被所有类继承和使用。以下是 `Object`​ 类的主要方法：

1. ​`public final Class<?> getClass()`​
2. ​`hashCode()`​
3. ​`equals(Object obj)`​
4. ​`clone()`​
5. ​`toString()`​
6. ​`notify()`​
7. ​`notifyAll()`​
8. ​`wait() `​
9. ​`protected void finalize() throws Throwable`​

这些方法提供了对象的基本操作，如获取类信息、比较对象、生成对象的字符串表示、线程间通信等。

‍

## Comparable和Comparator有什么区别

1. 它们出自不同的包，Comparator在 java.util 包下，Comparable在 java.lang 包下。
2. Comparator 使用比较灵活，不需要修改实体类源码，但是需要实现一个比较器。
3. Comparable 使用简单，但是对代码有侵入性，需要修改实体类源码。
4. 都是接口

‍

## super()和this()不能同时在一个构造函数中出现

this()方法可以调用本类的无参构造函数。如果本类继承的有父类，那么无参构造函数会有一个隐式的super()的存在

同一个构造函数里面如果this()之后再调用super()，那么就相当于调用了两次super()，也就是调用了两次父类的无参构造，就失去了语句的意义，编译器也不会通过

‍

‍

## 理性分析ArrayList和LinkedList时间复杂度

**头部插入**：由于ArrayList头部插入需要移动后面所有元素，所以必然导致效率低。LinkedList不用移动后面元素，自然会快一些。  
**中间插入**：查看源码会注意到LinkedList的中间插入其实是先判断插入位置距离头尾哪边更接近，然后从近的一端遍历找到对应位置，而ArrayList是需要将后半部分的数据复制重排，所以两种方式其实都逃不过遍历的操作，相对效率都很低，但是从实验结果还是ArrayList更胜一筹，我猜测这与数组在内存中是连续存储有关。  
**尾部插入**：ArrayList并不需要复制重排数据，所以效率很高，这也应该是我们日常写代码时的首选操作，而LinkedList由于还需要new对象和变换指针，所以效率反而低于ArrayList。

删除操作和添加操作没有什么区别。所以笼统的说LinkedList插入删除效率比ArrayList高是不对的，有时候反而还低。之所以笼统的说LinkedList插入删除效率比ArrayList高，我猜测是ArrayList复制数组需要时间，也占一定的时间复杂度。而因为数据量太少，这种效果就体现不出来。

‍

‍

## 变量等

‍

### i+1比i小的

基础数据类型的最大值 + 1 会变负数

‍

‍

### Integer和int的区别

1. Integer是int的包装类，int则是java的一种基本的数据类型；
2. Integer实际是对象的引用，当new一个Integer时，实际上生成一个指针指向对象，而int则直接存储数值
3. Integer的默认值是null，而int的默认值是0
4. Integer 值大小在 -128到127之内 会使用IntegerCache
5. 值比对的时候走自动拆箱机制, Integer转化为int进行比较

‍

‍

### 字符型常量和字符串常量的区别?

* **形式** : 字符常量是单引号引起的一个字符，字符串常量是双引号引起的 0 个或若干个字符。
* **含义** : 字符常量相当于一个整型值( ASCII 值),可以参加表达式运算; 字符串常量代表一个地址值(该字符串在内存中存放位置)。
* **占内存大小**：字符常量只占 2 个字节; 字符串常量占若干个字节。

注意 `char`​ 在 Java 中占两个字节。

‍

‍

‍

### 静态方法为什么不能调用非静态成员?

‍

* 静态方法是属于类的，在类加载的时候就会分配内存，可以通过类名直接访问。而非静态成员属于实例对象，只有在对象实例化之后才存在，需要通过类的实例对象去访问。
* 在类的非静态成员不存在的时候静态方法就已经存在了，此时调用在内存中还不存在的非静态成员，属于非法操作。

‍

### String 为什么是不可变的?

真正不可变有下面几点原因：

1. ==保存字符串的数组==被 `final`​ 修饰且为私有的，并且`String`​ 类没有提供/暴露修改这个字符串的方法。
2. ​`String`​ 类被 `final`​ 修饰导致其不能被==继承==，进而避免了子类破坏 `String`​ 不可变

‍

### 字符串拼接用“+” 还是 StringBuilder?

在循环内使用“+”进行字符串的拼接的话，存在比较明显的缺陷：**编译器不会创建单个** **​`StringBuilder`​**​ **以复用，会导致创建过多的** **​`StringBuilder`​**​ **对象**。

在 JDK9 当中，字符串相加 “+” 改为了用动态方法 `makeConcatWithConstants()`​ 来实现，而不是大量的 `StringBuilder`​ 了

JDK 9 之后，你可以放心使用“+” 进行字符串拼接了

‍

‍

## 重载重写

‍

‍

|区别点|重载方法|重写方法|
| ------------| ----------| ------------------------------------------------------------------|
|发生范围|同一个类|子类|
|参数列表|必须修改|一定不能修改|
|返回类型|可修改|子类方法返回值类型应比父类方法返回值类型更小或相等|
|异常|可修改|子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等；|
|访问修饰符|可修改|一定不能做更严格的限制（可以降低限制）|
|发生阶段|编译期|运行期|

**方法的重写要遵循“两同两小一大”** （以下内容摘录自《疯狂 Java 讲义》，[issue#892open in new window](https://github.com/Snailclimb/JavaGuide/issues/892) ）：

* “两同”即方法名相同、形参列表相同；
* “两小”指的是子类方法返回值类型应比父类方法返回值类型更小或相等，子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等；
* “一大”指的是子类方法的访问权限应比父类方法的访问权限更大或相等。

‍

**重写的返回值类型** 这里需要额外多说明一下，上面的表述不太清晰准确：如果方法的返回类型是 void 和基本数据类型，则返回值重写时不可修改。但是如果方法的返回值是引用类型，重写时是可以返回该引用类型的子类的。

‍

### 浅拷贝、深拷贝、引用拷贝

​![](https://oss.javaguide.cn/github/javaguide/java/basis/shallow&deep-copy.png)​

‍

‍

### HashMap 和 Hashtable 的区别

* **线程是否安全：**​`HashMap`​ 是非线程安全的，`Hashtable`​ 是线程安全的,因为 `Hashtable`​ 内部的方法基本都经过`synchronized`​ 修饰。（如果你要保证线程安全的话就使用 `ConcurrentHashMap`​ ）
* **效率：**  因为线程安全的问题，`HashMap`​ 要比 `Hashtable`​ 效率高一点。另外，`Hashtable`​ 基本被淘汰，不要在代码中使用它；
* **对 Null key 和 Null value 的支持：**​`HashMap`​ 可以存储 null 的 key 和 value，但 null 作为键只能有一个，null 作为值可以有多个；Hashtable 不允许有 null 键和 null 值，否则会抛出 `NullPointerException`​。
* **初始容量大小和每次扩充容量大小的不同：**  

  ① 创建时如果不指定容量初始值，`Hashtable`​ 默认的初始大小为 11，之后每次扩充，容量变为原来的 2n+1。`HashMap`​ 默认的初始化大小为 16。之后每次扩充，容量变为**原来的 2 倍**。

  ② 创建时如果给定了容量初始值，那么 `Hashtable`​ 会直接使用你给定的大小，而 `HashMap`​ 会将其扩充为 2 的幂次方大小（`HashMap`​ 中的`tableSizeFor()`​方法保证，下面给出了源代码）。也就是说 `HashMap`​ 总是使用 2 的幂作为哈希表的大小
* **底层数据结构：**  JDK1.8 以后的 `HashMap`​ 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）时，将链表转化为红黑树（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树），以减少搜索时间（后文中我会结合源码对这一过程进行分析）。`Hashtable`​ 没有这样的机制。

‍

‍

## 浅谈 ReentrantLock 的设计

‍

1. ReentrantLock 是在**多线程竞争资源**时使用的锁，他是一个独占锁、可重入锁，也是悲观锁
2. ReentrantLock 支持公平锁，对公平和非公平锁有不同的实现逻辑
3. ReentrantLock 使用 aqs（AbstractQueuedSynchronizer）来实现的获取锁的线程队列等待的过程
4. 内部使用了原子操作类 cas 比较线程与对应的锁关系
5. 内部支持newCondition来灵活的控制获取到锁的线程的阻塞与释放

‍

‍

## JAVA特性(优势)

> 区分面向对象的封装, 继承, 多态

广泛使用

简单易懂

平台无关

面向对象

高效性

多线程

解释型

安全 (JRE隔离)

动态

‍

## JAVA版本特性

‍

### JDK 7 2011 MC 3年级初始化

1. 第一次接触的(MC)使用的玩意
2. try-with-resources语句
3. 多重catch
4. 钻石操作符（<>）

‍

‍

### JDK 8 2014 MC热门

1. **==Lambda==** **表达式**：神中神
2. **==Stream==** **API**：神中神
3. **==LocalDateTime==**：更好的日期和时间处理
4. **==Optional 类==**：用于避免空指针异常

‍

### JDK 11 2018 高中

LTS

1. **局部变量类型推断**：使用 ==​`var`​== ==关键字==简化局部变量的声明。
2. **新的**​**==字符串方法==**：如 ==​`isBlank`​==​`()`​, `lines()`​, `strip()`​, `repeat()`​

‍

### JDK 17 2021 大学

LTS

1. **Sealed Classes**：==密封类==. 允许类或接口限制其子类
2. **Pattern Matching for** **​`switch`​**​：==Switch增强==. 增强了 `switch`​ 语句的模式匹配能力。
3. **文本块**：简化==多行字符串==的编写

‍

‍

‍

‍

## 什么是fail fast快速失败机制？

快速失败（fail-fast）是Java集合框架中的一种**错误检测机制**。

当多个线程对同一个ArrayList进行操作时，如果一个线程在遍历该集合的过程中，另一个线程同时尝试修改它（例如添加、删除元素），那么遍历线程会抛出`ConcurrentModificationException`​异常。这种机制旨在防止并发修改导致的数据不一致问题。

‍

## 什么是fail safe安全失败机制？

采用安全失败机制的集合容器，在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历。java.util.concurrent包下的容器都是安全失败，可以在多线程下并发使用，并发修改。

**原理**：由于迭代时是对原集合的拷贝进行遍历，所以在遍历过程中对原集合所作的修改并不能被迭代器检测到，所以不会触发Concurrent Modification Exception。

**缺点**：基于拷贝内容的优点是避免了Concurrent Modification Exception，但同样地，迭代器并不能访问到修改后的内容，即：迭代器遍历的是开始遍历那一刻拿到的集合拷贝，在遍历期间原集合发生的修改迭代器是不知道的。

‍

## 如何让一个集合不能被修改？

可以采用Collections包下的unmodifiableMap/unmodifiableList/unmodifiableSet方法，通过这个方法返回的集合，是不可以修改的。如果修改的话，会抛出 java.lang.UnsupportedOperationException异常。

```
List<String> list = new ArrayList<>();
list.add("x");
Collection<String> clist = Collections.unmodifiableCollection(list);
clist.add("y"); // 运行时此行报错
System.out.println(list. size());

```

对于List/Set/Map集合，Collections包都有相应的支持。

**那使用final关键字进行修饰可以实现吗？**

答案是不可以。

**final关键字修饰的成员变量如果是是引用类型的话，则表示这个引用的地址值是不能改变的，但是这个引用所指向的对象里面的内容还是可以改变的。**

而集合类都是引用类型，用final修饰的话，集合里面的内容还是可以修改的。

‍

‍

‍

# 大块

‍

## String、StringBuilder、StringBuffer的区别？

‍

* 使用 `String`​ 处理不可变字符串。
* 使用 `StringBuilder`​ 处理可变字符串，适用于单线程环境。
* 使用 `StringBuffer`​ 处理可变字符串，适用于多线程环境。

‍

1. ​**​`String`​**​:

    * **不可变**：`String`​ 对象是不可变的，一旦创建就不能修改。如果对 `String`​ 进行任何修改操作，都会生成一个新的 `String`​ 对象。
    * **线程安全**：由于 `String`​ 是不可变的，因此是**线程安全**的。
    * **性能**：由于每次修改都会创建新的对象，因此在频繁修改字符串的场景下，性能较差。

    ```java
    String str = "Hello";
    str = str + " World"; // 生成了一个新的 String 对象
    ```
2. ​**​`StringBuilder`​**​:

    * **可变**：`StringBuilder`​ 对象是可变的，可以直接对其内容进行修改，而不会生成新的对象。
    * **非线程安全**：`StringBuilder`​ **不是线程安全**的，因此在多线程环境下不推荐使用。
    * **性能**：由于不需要创建新的对象，因此在频繁修改字符串的场景下，性能较好。

    ```java
    StringBuilder sb = new StringBuilder("Hello");
    sb.append(" World"); // 直接修改了原有对象
    ```
3. ​**​`StringBuffer`​**​:

    * **可变**：`StringBuffer`​ 对象也是可变的，可以直接对其内容进行修改。 (buffer意味着缓存)
    * **线程安全**：`StringBuffer`​ 是**线程安全**的，所有的方法都是同步的，因此在多线程环境下可以安全使用。
    * **性能**：由于方法是同步的，因此在单线程环境下性能不如 `StringBuilder`​。

    ```java
    StringBuffer sbf = new StringBuffer("Hello");
    sbf.append(" World"); // 直接修改了原有对象
    ```

总结：

* 使用 `String`​ 处理不可变的字符串。
* 使用 `StringBuilder`​ 处理单线程环境下频繁修改的字符串。
* 使用 `StringBuffer`​ 处理多线程环境下频繁修改的字符串。

‍

‍

‍

### 为什么StringBuilder可以变？底层是怎么实现的？

底层实现使用了一个可变的字符数组来存储字符串数据。每次对 StringBuilder 进行修改时，实际上是对这个字符数组进行操作，而不是创建新的对象。

‍

‍

## 浮点数精度问题

浮点数精度丢失问题考虑过吗？  
浮点数为什么会精度丢失，讲讲底层  
如何解决精度丢失问题

‍

## 集合相关

‍

### List

‍

#### ArrayList?

​`ArrayList`​ 的底层是动态数组，它的容量能动态增长。在添加大量元素前，应用可以使用`ensureCapacity`​操作增加 `ArrayList`​ 实例的容量。ArrayList 继承了 AbstractList ，并实现了 List 接口

‍

#### ArrayList 和 Array（数组）的区别？

​`ArrayList`​ 内部基于动态数组实现，比 `Array`​（静态数组） 使用起来更加灵活：

* ​`ArrayList`​会根据实际存储的元素动态地扩容或缩容，而 `Array`​ 被创建之后就不能改变它的长度了。
* ​`ArrayList`​ 允许你使用泛型来确保类型安全，`Array`​ 则不可以。
* ​`ArrayList`​ 中只能存储对象。对于基本类型数据，需要使用其对应的包装类（如 Integer、Double 等）。`Array`​ 可以直接存储基本类型数据，也可以存储对象。
* ​`ArrayList`​ 支持插入、删除、遍历等常见操作，并且提供了丰富的 API 操作方法，比如 `add()`​、`remove()`​等。`Array`​ 只是一个固定长度的数组，只能按照下标访问其中的元素，不具备动态添加、删除元素的能力。
* ​`ArrayList`​创建时不需要指定大小，而`Array`​创建时必须指定大小

‍

#### ArrayList 和 Vector 的区别?

* ​`ArrayList`​ 是 `List`​ 的主要实现类，底层使用 `Object[]`​存储，适用于频繁的查找工作，线程不安全 。
* ​`Vector`​ 是 `List`​ 的古老实现类，底层使用`Object[]`​ 存储，线程安全。
* ArrayList在内存不够时扩容为原来的1.5倍，Vector是扩容为原来的2倍。

‍

#### ArrayList 可以添加 null 值吗？

​`ArrayList`​ 中可以存储任何类型的对象，包括 `null`​ 值。

‍

#### Arraylist 与 LinkedList的区别

1，从操作数据效率来说

ArrayList按照下标查询的时间复杂度O(1)【内存是连续的，根据寻址公式】， LinkedList不支持下标查询

查找（未知索引）： ArrayList需要遍历，链表也需要链表，时间复杂度都是O(n)

新增和删除

* ArrayList尾部插入和删除，时间复杂度是O(1)；其他部分增删需要挪动数组，时间复杂度是O(n)
* LinkedList头尾节点增删时间复杂度是O(1)，其他都需要遍历链表，时间复杂度是O(n)

2，从内存空间占用来说

ArrayList底层是数组，内存连续，节省内存

LinkedList 是双向链表需要存储数据，和两个指针，更占用内存

3，从线程安全来说，ArrayList和LinkedList都不是线程安全的

‍

‍

#### ArrayList扩容原理

当调用add方法添加一个元素时，首先会确保当前ArrayList维护的数组具有存储新元素的能力。如果数组的容量不足以存储新元素，那么就会通过grow方法进行扩容。扩容的方式是将数组的容量扩大到原来的1.5倍，然后将原数组的数据复制到新的数组中。最后，将新元素添加到数组的末尾

‍

#### Arrays.asList转List后，如果修改了数组内容，list受影响吗？List用toArray转数组后，如果修改了List内容，数组受影响吗

Arrays.asList转换list之后，如果修改了数组的内容，list会受影响，因为它的底层使用的Arrays类中的一个内部类ArrayList来构造的集合，在这个集合的构造器中，把我们传入的这个集合进行了包装而已，最终指向的都是同一个内存地址

list用了toArray转数组后，如果修改了list内容，数组不会影响，当调用了toArray以后，在底层是它是进行了数组的拷贝，跟原来的元素就没啥关系了，所以即使list修改了以后，数组也不受影响。

‍

#### ArrayList 和 LinkedList 不是线程安全的，你们在项目中是如何解决这个的线程安全问题的？

嗯，是这样的，主要有两种解决方案：

第一：我们使用这个集合，优先在方法内使用，定义为局部变量，这样的话，就不会出现线程安全问题。

第二：如果非要在成员变量中使用的话，可以使用线程安全的集合来替代

ArrayList可以通过Collections 的 synchronizedList 方法将 ArrayList 转换成线程安全的容器后再使用。

LinkedList 换成ConcurrentLinkedQueue来使用

‍

‍

#### 实现数组和List之间的转换

数组转list，可以使用jdk17自动的一个工具类Arrays，里面有一个asList方法可以转换为数组

List 转数组，可以直接调用list中的toArray方法、，需要给一个参数，指定数组的类型，需要指定数组的长度。

‍

#### ArrayList的快速失败fail fast机制

ArrayList的快速失败（fail-fast）是Java集合框架中的一种**错误检测机制**。

当多个线程对同一个ArrayList进行操作时，如果一个线程在遍历该集合的过程中，另一个线程同时尝试修改它（例如添加、删除元素），那么遍历线程会抛出`ConcurrentModificationException`​异常。这种机制旨在防止并发修改导致的数据不一致问题。

‍

‍

### Map

‍

#### Map有哪些类？

Map接口有很多实现类，其中比较常用的有HashMap、LinkedHashMap、TreeMap、ConcurrentHashMap。

对于不需要排序的场景，优先考虑使用HashMap，因为它是性能最好的Map实现。如果需要保证线程安全，则可以使用ConcurrentHashMap。它的性能好于Hashtable，因为它在put时采用分段锁/CAS的加锁机制，而不是像Hashtable那样，无论是put还是get都做同步处理。对于需要排序的场景，如果需要按插入顺序排序则可以使用LinkedHashMap，如果需要将key按自然顺序排列甚至是自定义顺序排列，则可以选择TreeMap。如果需要保证线程安全，则可以使用Collections工具类将上述实现类包装成线程安全的Map。

​`TreeMap`​ 基于红黑树实现。

​`HashMap`​ 1.7基于哈希表实现，1.8基于数组+链表+红黑树。

​`HashTable`​ 和 HashMap 类似，但它是线程安全的，这意味着同一时刻多个线程可以同时写入 HashTable 并且不会导致数据不一致。它是遗留类，不应该去使用它。现在可以使用 ConcurrentHashMap 来支持线程安全，并且 ConcurrentHashMap 的效率会更高(1.7 ConcurrentHashMap 引入了分段锁, 1.8 引入了红黑树)。

​`LinkedHashMap`​ 使用双向链表来维护元素的顺序，顺序为插入顺序或者最近最少使用(LRU)顺序。

‍

‍

#### 集合转 Map

**在使用** **​`java.util.stream.Collectors`​**​ **类的** **​`toMap()`​** ​ **方法转为** **​`Map`​**​ **集合时，一定要注意当 value 为 null 时会抛 NPE 异常。**

[Java集合使用注意事项总结 | JavaGuide](https://javaguide.cn/java/collection/java-collection-precautions-for-use.html#%E9%9B%86%E5%90%88%E8%BD%AC-map)

‍

‍

#### 集合遍历方法

**不要在 foreach 循环里进行元素的** **​`remove/add`​**​ **操作。remove 元素请使用** **​`Iterator`​**​ **方式，如果并发操作，需要对** **​`Iterator`​**​ **对象加锁。**

> 通过反编译你会发现 foreach 语法底层其实还是依赖 `Iterator`​ 。不过， `remove/add`​ 操作直接调用的是集合自己的方法，而不是 `Iterator`​ 的 `remove/add`​方法
>
> 这就导致 `Iterator`​ 莫名其妙地发现自己有元素被 `remove/add`​ ，然后，它就会抛出一个 `ConcurrentModificationException`​ 来提示用户发生了并发修改异常。这就是单线程状态下产生的 **fail-fast 机制**

‍

推荐

* 使用普通 for 循环比对. 要复制个新的直接双指针拷贝也可以
* 使用 fail-safe 的集合类。`java.util`​包下面的所有的集合类都是 fail-fast 的，而`java.util.concurrent`​包下面的所有的类都是 fail-safe 的
* List自己的 `Collection  removeIf()`​方法删除满足特定条件的元素,如

  ```java
  list.removeIf(filter -> filter % 2 == 0); /* 删除list中的所有偶数 *
  ```

‍

‍

#### 数组转集合

使用工具类 `Arrays.asList()`​ 把数组转换成集合时，不能使用其修改集合相关的方法， 它的 `add/remove/clear`​ 方法会抛出 `UnsupportedOperationException`​ 异常。

‍

​`Arrays.asList()`​是临时的的将一个数组转换为一个 `List`​ 集合, 只能当做一个快照使用

```java
String[] myArray = {"Apple", "Banana", "Orange"};
List<String> myList = Arrays.asList(myArray);
```

‍

下面我们来总结一下使用注意事项。

**1、**​**​`Arrays.asList()`​** ​**是泛型方法，传递的数组必须是对象数组，而不是基本类型。**

传入一个原生数据类型数组时，`Arrays.asList()`​ 的真正得到的参数就不是数组中的元素，而是数组对象本身(指针)！此时 `List`​ 的唯一元素就是这个数组，使用包装类型数组! 

```java
Integer[] myArray = {1, 2, 3}; //true
```

‍

**2、使用集合的修改方法:**  **​`add()`​** ​ **、**​**​`remove()`​** ​ **、**​**​`clear()`​** ​**会抛出异常。**

​`Arrays.asList()`​ 方法返回的并不是 `java.util.ArrayList`​ ，而是 `java.util.Arrays`​ 的一个内部类,这个内部类并没有实现集合的修改方法或者说并没有重写这些方法

‍

**如何正确的将数组转换为** **​`ArrayList`​**​  **?**

1、手动实现工具类, 一个一个拷贝

2、最简便的方法, 但是使用了new来指定对象类型

```java
List list = new ArrayList<>(Arrays.asList("a", "b", "c"))
```

3、使用`Stream`​(最推荐)

```java
Integer [] myArray = { 1, 2, 3 };
List myList = Arrays.stream(myArray).collect(Collectors.toList());

//基本类型也可以实现转换（依赖boxed的装箱操作）
int [] myArray2 = { 1, 2, 3 };
List myList = Arrays.stream(myArray2).boxed().collect(Collectors.toList());
```

4、使用 Guava 工具类实现拷贝

‍

5.使用 Java9 的 `List.of()`​方法 , JDK17我一般用这个就无损了

```java
Integer[] array = {1, 2, 3};
List<Integer> list = List.of(array);
```

‍

‍

‍

### 代码块执行顺序示例

```java


/**
 * 随从类
 */
class Code {
    public Code() {
        System.out.println("Code的构造方法1111");
    }

    {
        System.out.println("Code的构造代码块22222");
    }

    static {
        System.out.println("Code的静态代码块33333");
    }
}

public class CodeBlock03 {

    {
        System.out.println("CodeBlock03的构造代码块22222");
    }

    static {
        System.out.println("CodeBlock03的静态代码块33333");
    }

    public CodeBlock03() {
        System.out.println("CodeBlock03的构造方法33333");
    }


    public static void main(String[] args) {

        System.out.println("我是主类======");
        new Code();
        System.out.println("======");
        new Code();
        System.out.println("======");
        new CodeBlock03();
    }
}
```

```text
CodeBlock03的静态代码块33333
我是主类======
Code的静态代码块33333
Code的构造代码块22222
Code的构造方法1111
======
Code的构造代码块22222
Code的构造方法1111
======
CodeBlock03的构造代码块22222
CodeBlock03的构造方法33333
```

类被加载到内存的时候，首先需要执行的是静态方法

再次实例化的时候，因此该类已经在内存中，所以不再运行静态代码块了

‍

---

```java
class Father {
    {
        System.out.println("我是父亲代码块");
    }
    public Father() {
        System.out.println("我是父亲构造");
    }
    static {
        System.out.println("我是父亲静态代码块");
    }
}

class Son extends Father{
    public Son() {
        System.out.println("我是儿子构造");
    }
    {
        System.out.println("我是儿子代码块");
    }

    static {
        System.out.println("我是儿子静态代码块");
    }
}

public class CodeBlock04 {

    public static void main(String[] args) {

        System.out.println("我是主类======");
        new Son();
        System.out.println("======");
        new Son();
        System.out.println("======");
        new Father();
    }
}
```

输出结果

```text
我是主类======

我是父亲静态代码块
我是儿子静态代码块

我是父亲代码块
我是父亲构造

我是儿子代码块
我是儿子构造

======

我是父亲代码块
我是父亲构造
我是儿子代码块
我是儿子构造

======

我是父亲代码块
我是父亲构造
```

‍

任何一个类被加载，必须加载这个类的静态代码块

同时如果存在父子关系的时候，调用子类的构造方法，同时子类的构造方法，在最顶部会调用super()也就是**父类的构造方法**，一般这个是被省略的

所以在子类初始化之前，还需要调用父类构造，所以父类需要加载进内存，也就是从父到子，静态执行，并且只加载一次

然后父类在进行实例化，在调用构造方法之前，需要调用本类的代码块

最后父类初始化成功后，再调用子类的

在执行第二次的 new Son()的时候，因为该类已经被装载在内存中了，因此静态代码块不需要执行，我们只需要从父到子执行即可

‍

‍

‍

### 包装类型的缓存机制

‍

Java 基本数据类型的包装类型的大部分都用到了缓存机制来提升性能

‍

​`Byte`​,`Short`​,`Integer`​,`Long`​ 这 4 种包装类默认创建了数值  **[-128，127]**  的相应类型的缓存数据，`Character`​ 创建了数值在  **[0,127]**  范围的缓存数据，`Boolean`​ 直接返回 `True`​ or `False`​。

如果超出对应范围仍然会去创建新的对象，缓存的范围区间的大小只是在性能和资源之间的权衡。

**两种浮点数类型的包装类** **​`Float`​**​ **,**​**​`Double`​**​ **并没有实现缓存机制**

‍

```java
Integer i1 = 40;
Integer i2 = new Integer(40);
System.out.println(i1==i2);
```

​`Integer i1=40`​ 这一行代码会发生装箱，这行代码等价于 `Integer i1=Integer.valueOf(40)`​ 。因此，`i1`​ 直接使用的是缓存中的对象。而`Integer i2 = new Integer(40)`​ 会要求直接创建新的对象。

‍

因此：**所有整型包装类对象之间值的比较，全部使用 equals 方法比较**。

‍

### 线程安全集合类

**java.util包下的集合类大部分都是线程不安全的，例如我们常用的HashSet、TreeSet、ArrayList、LinkedList、ArrayDeque、HashMap、TreeMap，这些都是线程不安全的集合类，但是它们的优点是性能好。** 如果需要使用线程安全的集合类，则可以使用Collections工具类提供的synchronizedXxx()方法，将这些集合类包装成线程安全的集合类。**java.util包下也有线程安全的集合类，例如Vector、Hashtable。这些集合类都是比较古老的API，虽然实现了线程安全，但是性能很差。** 所以即便是需要使用线程安全的集合类，也建议将线程不安全的集合类包装成线程安全集合类的方式，而不是直接使用这些古老的API。从Java5开始，Java在java.util.concurrent包下提供了大量支持高效并发访问的集合类，它们既能包装良好的访问性能，有能包装线程安全。这些集合类可以分为两部分，它们的特征如下：

* 以Concurrent开头的集合类： 以Concurrent开头的集合类代表了支持并发访问的集合，它们可以支持多个线程并发写入访问， 这些写入线程的所有操作都是线程安全的，但读取操作不必锁定。以Concurrent开头的集合类采 用了更复杂的算法来保证永远不会锁住整个集合，因此在并发写入时有较好的性能。
* 以CopyOnWrite开头的集合类： 以CopyOnWrite开头的集合类采用复制底层数组的方式来实现写操作。当线程对此类集合执行读 取操作时，线程将会直接读取集合本身，无须加锁与阻塞。当线程对此类集合执行写入操作时，集 合会在底层复制一份新的数组，接下来对新的数组执行写入操作。由于对集合的写入操作都是对数 组的副本执行操作，因此它是线程安全的。

‍

# 高级

‍

## String

‍

### String final修饰的好处

‍

从 String 类的源码我们可以看出 String 是被 final 修饰的不可继承类

```java
public final class String implements java.io.Serializable,Comparable<String>,CharSequence{
    ...
}
```

‍

> Java 语言之父James Gosling的回答是，他会更倾向于使用final，因为它能够缓存结果，当你在传参时不需要考虑谁会修改它的值；如果是可变类的话，则有可能需要重新拷贝出来一个新值进行传参，这样在性能上就会有一定的损失。
>
> James Gosling 还说迫使String类设计成 不可变 的另一个原因是安全，当你在调用其他方法时，比如调用一些系统级操作指令之前，可能会有一系列校验，如果是可变类的话，可能在你校验过后，它的内部的值又被改变了，这样有可能会引起严重的系统崩溃问题，这是迫使String类设计成不可变类的一个重要原因。

**安全, 高效 - 实现字符串常量池**

‍

‍

### 创建

* 直接赋值的方式`"String s1="Java";"`​
* `"String s2=new String("Java");"`​

‍

两者在JVM的存储区域却截然不同，在JDK1.8中:

变量s1会先去字符串常量池中找字符串`"Java”`​，如果有相同的字符则**直接返回常量句柄**

如果没有此字符串则会先在常量池中创建此字符串，然后再返回常量句柄；而变量s2是直接在堆上创建一个变量，如果调用`intern`​方法才会把此字符串保存到常量池中 intern: 逮捕

‍

```java
String s1 = new String("Java"); // 存入堆
String s2 = s1.intern();     //s1存入常量池后提取引用
String s3 = "Java";    //直接从常量池获取引用
System.out.println(s1 == s2); // false
System.out.println(s2 == s3); // true
```

它们在 JVM 存储的位置，如下所示

> Stack    s1    s2    s3
>
> |        ||
>
> Heap   "java" -> [常量池]

‍

‍

#### new String("dabin")会创建几个对象？

使用这种方式会创建两个字符串对象（前提是字符串常量池中没有 "dabin" 这个字符串对象）。

* "dabin" 属于字符串字面量，因此编译时期会在字符串常量池中创建一个字符串对象，指向这个 "dabin" 字符串字面量；
* 使用 new 的方式会在堆中创建一个字符串对象。

‍

‍

### String最大长度是多少？

length方法返回值为int类型，取值上限为2^31 -1。 (32位)

所以理论上String的最大长度为此

‍

**达到这个长度的话需要多大的内存吗**？

String内部是使用一个char数组来维护字符序列的，一个char占用两个字节。如果说String最大长度是2^31 -1的话，那么最大的字符串占用内存空间约等于4GB。-> 2^30

‍

‍

**那String一般都存储在JVM的哪块区域呢**？

字符串在JVM中的存储分两种情况，一种是String对象，存储在JVM的堆栈中(引用 -> 实体)。一种是字符串常量，存储在常量池(独立)里面。当**通过字面量进行字符串声明时**，比如String s = "程序新大彬";，这个字符串在编译之后会以常量的形式进入到常量池。

‍

‍

**那常量池中的字符串最大长度是2^31-1吗**？

不是的，常量池对String的长度是有另外限制的。。Java中的UTF-8编码的Unicode字符串在常量池中以CONSTANT_Utf8类型表示。

```java
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
```

length在这里就是代表字符串的长度，length的类型是u2，u2是无符号的16位整数，也就是说最大长度可以做到2^16-1 即 65535。

不过javac编译器做了限制，需要length < 65535。所以字符串常量在常量池中的最大长度是65535 - 1 = 65534。

‍

最后总结一下：

String在不同的状态下，具有不同的长度限制。

* 字符串常量长度不能超过65534
* 堆内字符串的长度不超过2^31-1

‍

‍

### String 是如何实现的？它有哪些重要的方法

以主流的 JDK 版本 1.8 来说，String 内部实际存储结构为 ==char 数组==

```java
public final class String implements java.io.Serializable,Comparable<String>,CharSequence{
    //用于存储字符串的值
    private final charvalue[];
    //缓存字符串的 hash code
    private int hash; //Default to 0
    //......其他内容
}
```

‍

**Stirng中的几个重要方法**

‍

‍

#### 多构造方法

String字符串中4个重要的构造方法:

```java
// String 为参数的构造方法
public String(String original) {
        this.value = original.value;
        this.hash = original.hash;
    }

// char[] 为参数的构造方法
public String(char value[]) {
        this.value = Arrays.copyOf(value, value.length);
    }

// StringBuffer 为参数的构造方法
  public String(StringBuffer buffer) {
        synchronized(buffer) {
            this.value = Arrays.copyOf(buffer.getValue(), buffer.length());
        }
    }

// StringBuilder 为参数的构造方法
public String(StringBuilder builder) {
        this.value = Arrays.copyOf(builder.getValue(), builder.length());
    }
```

‍

#### equals()比较两个字符串是否相等

源码

```java
public boolean equals(Object anObject) {
    // 对象引用相同直接返回true
    if (this == anObject) {
        return true;
    }
    // 判断需要对比的值是否为 String 类型，如果不是则直接返回 false
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            // 把两个字符串转化为 char 数组对比
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            // 循环比对两个字符串的每一字符
            while (n-- != 0) {
                // 如果其中一个字符不相等就返回false 若相等就继续比对
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}
```

​`String`​类型重写了`Object`​中的`equals()`​方法，`equals()`​方法需要传递一个`Object`​类型的参数值，在比较时会先通过`instanceof`​判断是否为`String`​类型，如果不是则会直接返回`false`​

当判断参数为`String`​类型之后，会循环对比两个字符串中的每一个字符，当所有字符都相等时返回`true`​，否则则返回`false`​

‍

‍

#### compareTo()比较两个字符串

compareTo() 方法用于比较两个字符串，返回的结果为 int 类型的值

```java
public int compareTo(String anotherString) {
        int len1 = value.length;
        int len2 = anotherString.value.length;
        // 获取两个字符串长度最短的那个 int 值
        int lim = Math.min(len1, len2);
        char v1[] = value;
        char v2[] = anotherString.value;

        int k = 0;
    	// 对比每个字符串
        while (k < lim) {
            char c1 = v1[k];
            char c2 = v2[k];
            if (c1 != c2) {
                // 有字符不相等就返回差值
                return c1 - c2;
            }
            k++;
        }
        return len1 - len2;
    }
```

‍

‍

## HashMap

> 含金量高

‍

‍

### 底层实现

‍

在JDK1.7中`HashMap`​是以数组加链表的形式组成的，JDK1.8之后新增了红黑树的组成结构，当链表大于8时，链表结构会转换成红黑树结构

可以看出每个哈希桶中包含了四个字段：hash、key、value、next，其中next 表示链表的下一个节点。

JDK 1.8之所以添加红黑树是因为一旦链表过长，会严重影响`HashMap`​的性能，而红黑树具有快速增删改查的特点，这样就可以有效的解决链表过长时操作比较慢的问题

‍

数组中的元素我们称之为==哈希桶==，定义如下：

```java
static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;
        final K key;
        V value;
        Node<K,V> next;

        Node(int hash, K key, V value, Node<K,V> next) {
            this.hash = hash;
            this.key = key;
            this.value = value;
            this.next = next;
        }

        public final int hashCode() {
            return Objects.hashCode(key) ^ Objects.hashCode(value);
        }

        public final boolean equals(Object o) {
            if (o == this)
                return true;
            if (o instanceof Map.Entry) {
                Map.Entry<?,?> e = (Map.Entry<?,?>)o;
                if (Objects.equals(key, e.getKey()) &&
                    Objects.equals(value, e.getValue()))
                    return true;
            }
            return false;
        }
    }
```

‍

​`HashMap`​ 是 Java 中常用的集合类，其底层实现是基于数组和链表的哈希表。以下是 `HashMap`​ 的一些关键点：

1. **数组**：`HashMap`​ 使用一个数组来存储键值对。数组中的每个位置称为一个桶（bucket）。
2. **链表**：当多个键的哈希值相同时，这些键值对会存储在同一个桶中，并以链表的形式链接在一起。
3. **红黑树**：在 Java 8 及以后的版本中，当链表长度超过一定阈值（默认是 8）时，链表会转换为红黑树，以提高查找效率。
4. **哈希函数**：`HashMap`​ 使用键的 `hashCode()`​ 方法来计算哈希值，并通过哈希值确定键值对在数组中的位置。

‍

以下是一个简化的 `HashMap`​ 底层结构示意：

```java
class HashMap<K, V> {
    // 默认初始容量
    static final int DEFAULT_INITIAL_CAPACITY = 16;
    // 默认负载因子
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
  
    // 数组，存储链表或红黑树的头节点
    Node<K, V>[] table;
  
    // 链表节点
    static class Node<K, V> {
        final int hash;
        final K key;
        V value;
        Node<K, V> next;
    
        Node(int hash, K key, V value, Node<K, V> next) {
            this.hash = hash;
            this.key = key;
            this.value = value;
            this.next = next;
        }
    }
  
    // 其他方法和成员变量省略...
}
```

‍

‍

### 加载因子是0.75？

加载因子也叫扩容因子或负载因子，用来判断什么时候进行扩容的，假如加载因子是0.5，`HashMap`​的初始化容量是16，那么当`HashMap`​中有16*0.5=8个元素时，`HashMap`​就会进行扩容。

这个数字是出于容量和性能之间平衡的结果

> 和链表到容量了扩容不一样, Hash避免碰撞肯定是不能满了再来扩容的

‍

### 三个重要方法：**查询**、**新增**和**数据扩容**

‍

#### 查询

> SK口头描述: 首先对定位到的第一处地方进行非空判断, 然后始终判断第一个节点(非空, 哈希吗相同), 不是的话判断下面一个非空, 根据是不是树结构进行判断, 是的话就调用树操作进行获取, 不是的话循环向下遍历. 都找不到return null.

```java
public V get(Object key) {
        Node<K,V> e;
    	// 对key进行哈希操作
        return (e = getNode(hash(key), key)) == null ? null : e.value;
    }

final Node<K,V> getNode(int hash, Object key) {
        Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
    	// 非空判断
        if ((tab = table) != null && (n = tab.length) > 0 &&
            (first = tab[(n - 1) & hash]) != null) {
            // 判断第一个是否是要查询的元素
            if (first.hash == hash && // always check first node
                ((k = first.key) == key || (key != null && key.equals(k))))
                return first;
            // 判断下一个节点是否非空
            if ((e = first.next) != null) {
                // 如果第一节点时树结构，则使用getTreeNode获取相应的数据
                if (first instanceof TreeNode)
                    return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                do {
                    // 非树结构，循环判断
                    // hash相等并且key相等，返回此节点
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        return e;
                } while ((e = e.next) != null);
            }
        }
        return null;
    }
```

‍

‍

#### 新增

SK口头描述过程:

> 你准备往hash表里插入一个元素的时候, 首先查哈希表长度, 能不能放得下了或者是有没有这个表. 不满足resize扩容. 满足后根据key -Hash映射下找到对应的目标下标index -> 看看那个地方有没有被人占座了? 没有就直接插入(1). 有人了, 就要和他判断一下是不是同一个key值, 如果是, 把他傻乐直接插入(2). 不是, 那么就要挂载了. 首先看看是挂载的红黑树还是链表(要看JDK版本), 如果是就采用红黑树的流程插入(3). 不是就是链表插入, 链表插入还要考虑要不要立刻变成红黑树承载. 是的话转红黑树插入(4), 不是的话就还是链表插入(5), 最后5种插入结果都要判断一下需不需要resize扩容. 不要就结束.

```java
public V put(K key, V value) {
    	// 对key进行哈希操作
        return putVal(hash(key), key, value, false, true);
    }
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
    	// 哈希表为空则创建表
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
    	// 根据 key 的哈希值计算出要插入的数组索引 i
        if ((p = tab[i = (n - 1) & hash]) == null)
            // 如果table[i]等于nul1，则直接插入
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e; K k;
            // 如果key已经存在了，直接覆盖 value
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            // 如果key不存在，判断是否为红黑树
            else if (p instanceof TreeNode)
                // 红黑树直接插入键值对
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                // 为链表结构，循环准备插入
                for (int binCount = 0; ; ++binCount) {
                    // 下一个元素为空时
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        //链表长度大于8转换为红黑树进行处理
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    // key已经存在直接覆盖 value
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
    	// 超过最大容量，扩容
        if (++size > threshold)
            resize();
        afterNodeInsertion(evict);
        return null;
    }

```

‍

‍

#### 扩容

```java
final Node<K,V>[] resize() {
    	// 扩容前的数组
        Node<K,V>[] oldTab = table;
    	// 扩容前的数组的大小和阈值
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        int oldThr = threshold;

    	//预定义新数组的大小和阈值
        int newCap, newThr = 0;
        if (oldCap > 0) {
            //超过最大值就不再扩容了
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            //扩大容量为当前容量的两倍，但不能超过MAXIMUM_CAPACITY
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
    	//当前数组没有数据，使用初始化的值
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        else {               // zero initial threshold signifies using defaults
            //如果初始化的值为0，则使用默认的初始化容量
            newCap = DEFAULT_INITIAL_CAPACITY;
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
    	//如果新的容量等于0
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        @SuppressWarnings({"rawtypes","unchecked"})
            Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
    	//开始扩容，将新的容量赋值给 table
        table = newTab;
    	//原数据不为空，将原数据复制到新 table中
        if (oldTab != null) {
            //根据容量循环数组，复制非空元素到新 table
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    //如果链表只有一个，则进行直接赋值
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e;
                    else if (e instanceof TreeNode)
                        // 红黑树相关操作
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    else { // preserve order
                        //链表复制，JDK1.8扩容优化部分
                        Node<K,V> loHead = null, loTail = null;
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                            // 原索引
                            if ((e.hash & oldCap) == 0) {
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            // 原索引 + oldCap
                            else {
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        // 将原索引放到哈希桶中
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        // 将 原索引+oldCap 放到哈希桶中
                        if (hiTail != null) {
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }
```

‍

从以上源码可以看出，JDK1.8在扩容时并没有像JDK1.7那样，重新计算每个元素的哈希值，而是通过高位运算(`e.hash&oldCap`​)来确定元素是否需要移动，比如key1的信息如下：

* key1.hash = 10 0000 1010
* oldCap = 16 0001 0000

使用`e.hash&oldCap`​得到的结果高一位为0，当结果为0时表示元素在扩容时位置不会发生任何变化，而key 2信息如下：

* key2.hash = 10 0001 0001
* oldCap = 16 0001 0000

这时候得到的结果高一位为 1，当结果为 1 时，表示元素在扩容时位置发生了变化，新的下标位置等于原下标位置 + 原数组长度

‍

‍

‍

‍

## clone()

‍

Object 对 clone() 方法的约定有三条：

* 对于所有对象来说，x.clone() !=x 应当返回 true，因为克隆对象与原对象不是同一个对象；
* 对于所有对象来说，x.clone().getClass() == x.getClass() 应当返回 true，因为克隆对象与原对象的类型是一样的；
* 对于所有对象来说，x.clone().equals(x) 应当返回 true，因为使用 equals 比较时，它们的值都是相同的。

除了注释信息外，我们看 clone() 的实现方法，发现 clone() 是使用 native 修饰的本地方法，因此执行的性能会很高，并且它返回的类型为 Object，因此在调用克隆之后要把对象强转为目标类型才行。

---

Arrays.copyOf()

从结果可以看出，我们在修改克隆对象的第一个元素之后，原型对象的第一个元素也跟着被修改了，这说明 Arrays.copyOf() 其实是一个浅克隆。

因为数组比较特殊数组本身就是引用类型，因此在使用 Arrays.copyOf() 其实只是把引用地址复制了一份给克隆对象，如果修改了它的引用对象，那么指向它的（引用地址）所有对象都会发生改变

‍

‍

### 深克隆实现方式汇总

深克隆的实现方式有很多种，大体可以分为以下几类：

* 所有对象都实现克隆方法；
* 通过构造方法实现深克隆；
* 使用 JDK 自带的字节流实现深克隆；
* 使用第三方工具实现深克隆，比如 Apache Commons Lang；
* 使用 JSON 工具类实现深克隆，比如 Gson、FastJSON 等。

‍

‍

#### 1.所有对象都实现克隆

```java

        @Override
        protected People clone() throws CloneNotSupportedException {
            People people = (People) super.clone();
            people.setAddress(this.address.clone()); // 引用类型克隆赋值
            return people;
        }
        // 忽略构造方法、set、get 方法
```

‍

‍

#### 2.通过构造方法实现深克隆 - 直接new

推荐使用构造器（Copy Constructor）来实现深克隆，如果构造器的参数为基本数据类型或字符串类型则直接赋值，如果是对象类型，则需要重新 new 一个对象

就是直接new对象

```java
// 调用构造函数克隆对象
        People p2 = new People(p1.getId(), p1.getName(),
                new Address(p1.getAddress().getId(), p1.getAddress().getCity()));
```

‍

‍

#### 3.通过字节流实现深克隆

通过 JDK 自带的字节流实现深克隆的方式，是要先将原型对象写入到内存中的字节流，然后再从这个字节流中读出刚刚存储的信息，来作为一个新的对象返回，那么这个新对象和原型对象就不存在任何地址上的共享，这样就实现了深克隆

此方式需要注意的是，由于是通过字节流序列化实现的深克隆，因此每个对象必须能被序列化，必须实现 Serializable 接口，标识自己可以被序列化，否则会抛出异常 (java.io.NotSerializableException)

```java
// 通过字节流实现克隆
        People p2 = (People) StreamClone.clone(p1);


 /**
     * 通过字节流实现克隆
     */
    static class StreamClone {
        public static <T extends Serializable> T clone(People obj) {
            T cloneObj = null;
            try {
                // 写入字节流
                ByteArrayOutputStream bo = new ByteArrayOutputStream();
                ObjectOutputStream oos = new ObjectOutputStream(bo);
                oos.writeObject(obj);
                oos.close();
                // 分配内存,写入原始对象,生成新对象
                ByteArrayInputStream bi = new ByteArrayInputStream(bo.toByteArray());//获取上面的输出字节流
                ObjectInputStream oi = new ObjectInputStream(bi);
                // 返回生成的新对象
                cloneObj = (T) oi.readObject();
                oi.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
            return cloneObj;
        }
    }

```

‍

#### 4.通过第三方工具实现深克隆

Apache Commons Lang

此方法和第三种实现方式类似，都需要实现 Serializable 接口，都是通过字节流的方式实现的，只不过这种实现方式是第三方提供了现成的方法，让我们可以直接调用。

```java
import org.apache.commons.lang3.SerializationUtils;

import java.io.Serializable;

        // 调用 apache.commons.lang 克隆对象
        People p2 = (People) SerializationUtils.clone(p1);
```

‍

‍

#### 5.通过 JSON 工具类实现深克隆

使用 Google 提供的 JSON 转化工具 Gson 来实现，其他 JSON 转化工具类也是类似的

使用 JSON 工具类会先把对象转化成字符串，再从字符串转化成新的对象，因为新对象是从字符串转化而来的，因此不会和原型对象有任何的关联，这样就实现了深克隆，其他类似的 JSON 工具类实现方式也是一样的。

```java
// 调用 Gson 克隆对象
        Gson gson = new Gson();
        People p2 = gson.fromJson(gson.toJson(p1), People.class);

        // 修改原型对象
        p1.getAddress().setCity("西安");
```

‍

‍

从源码中可以看出，`compareTo()`​方法会循环对比所有的字符，当两个字符串中有任意一个字符不相同时，则`return char1-char2`​。比如，两个字符串分别存储的是1和2，返回的值是-1；如果存储的是1和1，则返回的值是0，如果存储的是2和1，则返回的值是1。

‍

​`compareTo()`​方法和`equals()`​方法都是用于比较两个字符串的，但它们有两点不同：

* ​`equals()`​可以接收一个`Object`​ 类型的参数，而`compareTo()`​只能接收一个`String`​类型的参数;
* ​`equals()`​返回值为`Boolean`​，而`compareTo()`​的返回值则为`int`​。

‍

‍

‍

## Java中HashMap的长度一般是2的整数次幂，为什么要这么做？

在 Java 中，`HashMap`​ 的长度（容量）通常是 2 的整数次幂，这是为了优化哈希表的性能。具体原因如下：

### 1. 高效的哈希计算

​`HashMap`​ 使用哈希值来确定键值对在数组中的位置。通过将哈希值与数组长度减 1 进行按位与运算（`hash & (length - 1)`​），可以快速计算出索引位置。当数组长度是 2 的整数次幂时，这种运算可以确保哈希值的每一位都能参与到索引计算中，从而减少哈希冲突。

### 2. 减少哈希冲突

当数组长度是 2 的整数次幂时，哈希值的低位和高位都能均匀地分布在数组的索引上，从而减少哈希冲突。如果数组长度不是 2 的整数次幂，某些位可能永远不会被使用，导致哈希冲突增加。

### 3. 高效的扩容机制

​`HashMap`​ 在扩容时，会将容量翻倍（仍然是 2 的整数次幂），并重新计算所有键值对的位置。由于新容量是旧容量的两倍，键值对的位置要么保持不变，要么移动到新位置。这种扩容机制非常高效。

### 示例

以下是 `HashMap`​ 计算索引位置的示例代码：

```java
public class HashMapExample {
    public static void main(String[] args) {
        int hash = "example".hashCode();
        int length = 16; // 2 的整数次幂
        int index = hash & (length - 1);
        System.out.println("Index: " + index);
    }
}
```

在这个示例中，`length`​ 是 2 的整数次幂，通过 `hash & (length - 1)`​ 计算索引位置，可以确保哈希值的每一位都能参与到索引计算中，从而减少哈希冲突。

‍

## HashMap中当链表长度超过阈值时优化为红黑树，红黑树是一个二叉比较树，需要比较key的大小，但HashMap中的key不要求实现comparable接口的，也不需要传比较器，那么它是如何把key放在红黑树中的

‍

在 `HashMap`​ 中，当链表长度超过阈值时，会将链表转换为红黑树，以提高查找效率。虽然 `HashMap`​ 中的键不要求实现 `Comparable`​ 接口，也不需要传入比较器，但 `HashMap`​ 通过以下方式来处理键的比较：

‍

### 1. 使用键的哈希值进行比较

​`HashMap`​ 首先使用键的哈希值进行比较。如果两个键的哈希值不同，则可以直接根据哈希值确定它们在红黑树中的位置。

‍

### 2. 当哈希值相同时，使用 `equals`​ 方法进行比较

如果两个键的哈希值相同，`HashMap`​ 会进一步使用键的 `equals`​ 方法进行比较，以确定它们是否相等。如果键相等，则认为是同一个键；如果键不相等，则需要在红黑树中进一步处理。

‍

### 3. 当哈希值相同且 `equals`​ 方法返回 `false`​ 时，使用系统标识符（`System.identityHashCode`​）进行比较

在极少数情况下，如果两个键的哈希值相同且 `equals`​ 方法返回 `false`​，`HashMap`​ 会使用系统标识符（`System.identityHashCode`​）进行比较，以确保键在红黑树中的唯一性和正确位置。

‍

## HashMap rehash过程

1.7：

1. 空间不够用了，所以需要分配一个大一点的空间，然后保存在里面的内容需要重新计算 hash
2. 在准备好新的数组后，map会遍历数组的每个“桶”，然后遍历桶中的每个Entity，重新计算其hash值（也有可能不计算），找到新数组中的对应位置，以头插法插入新的链表
3. 因为是头插法，因此新旧链表的元素位置会发生转置现象。元素迁移的过程中在多线程情境下有可能会触发死循环（无限进行链表反转），因此HashMap线程不安全

1.8：

1. 底层结构为：数组+单链表/红黑树。因此如果某个桶中的链表长度大于等于8了，则会判断当前的hashmap的容量是否大于64，如果小于64，则会进行扩容；如果大于64，则将链表转为红黑树
2. java1.8+在扩容时，不需要重新计算元素的hash进行元素迁移。而是用原先位置key的hash值与旧数组的长度（oldCap）进行"与"操作。
3. 如果结果是0，那么当前元素的桶位置不变。
4. 如果结果为1，那么桶的位置就是原位置+原数组 长度
5. 值得注意的是：为了防止java1.7之前元素迁移头插法在多线程是会造成死循环，java1.8+后使用尾插法

‍

‍
