# JVM

## 类的生命周期

类的生命周期分为加载、验证、准备、解析、初始化、使用、卸载七个阶段。加载读取字节码生成Class对象；验证确保格式安全；准备为静态变量分配内存并赋零值；解析将符号引用转为直接引用；初始化执行`<clinit>`，其后类进入使用阶段，最终被GC卸载。

```
  加载  →  验证  →  准备  →  解析  →  初始化  →  使用  →  卸载
  (Loading) (Verification) (Preparation) (Resolution) (Initialization) (Usage) (Unloading)
```

## JVM类加载机制

 **类加载器层级（三层 + 自定义）**

- **启动类加载器**（Bootstrap，C++实现）：加载 `<JAVA_HOME>/lib` 核心类，如 `rt.jar`，是其他加载器的最终父委托。
- **扩展类加载器**（Extension，`sun.misc.Launcher$ExtClassLoader`）：加载 `<JAVA_HOME>/lib/ext` 或 `java.ext.dirs` 下的类。
- **应用类加载器**（Application，`sun.misc.Launcher$AppClassLoader`）：加载 `classpath` 下用户类。
- **自定义类加载器**：继承 `ClassLoader`，可打破双亲委派实现隔离或热部署。

**双亲委派**：保证唯一，安全

**破坏双亲委派的典型案例**

- **Java SPI**（如 JDBC）：核心接口由启动类加载器加载，但实现类由第三方提供，双亲委派无法向上找到。于是引入**线程上下文类加载器**，保存应用类加载器，在核心类中通过该加载器去加载实现类。
- **OSGi、Tomcat等**：为实现模块化和类隔离，自定义类加载器平级依赖，打破层级委派。
- **热部署**：通过新类加载器重新加载类，旧类加载器和对应类一起被GC。

## JVM内存区域

```
 Thread A          Thread B
+-------------+   +-------------+
| PC Register |   | PC Register |   <- 线程私有
| Java Stack  |   | Java Stack  |
| Native Stack|   | Native Stack|
+-------------+   +-------------+
       |                 |
       v                 v
+------------------------------------+
|           Java Heap (共享)          |
|  -Xms / -Xmx                      |
|  +-----------+-------------------+ |
|  | Young Gen |   Old Gen         | |
|  | Eden S0 S1|   (Tenured)       | |
|  +-----------+-------------------+ |
+------------------------------------+

+------------------------------------+
|   Method Area / Metaspace (共享)   |
|  -XX:MaxMetaspaceSize (JDK8+)     |
|  +-------------------------------+|
|  |  Runtime Constant Pool       ||
|  |  Class Metadata, static vars ||
|  |  Method bytecodes, ...       ||
|  +-------------------------------+|
+------------------------------------+
 (使用本地内存，不再在堆中)

+------------------------------------+
| Direct Memory (NIO, 本地内存)     |
+------------------------------------+
```

**线程私有**

- **程序计数器**（线程私有）：记录当前线程执行的字节码行号，无OOM。
- **Java虚拟机栈**（线程私有）：方法的栈帧（局部变量表、操作数栈、动态链接、返回地址），会抛出 `StackOverflowError` / `OutOfMemoryError`。
- **本地方法栈**（线程私有）：为Native方法服务，类似虚拟机栈。

**线程共享**

- **Java堆**（线程共享）：存放对象实例，GC主战场，分新生代（Eden + Survivor）和老年代。
- **方法区（元空间）**（线程共享）：存储类信息、常量、静态变量、JIT编译后的代码。JDK8起用本地内存实现（Metaspace），取代永久代。
- **运行时常量池**（方法区一部分）：class文件常量池的运行时表示，存放字面量和符号引用。
- **直接内存**（非运行时数据区）：NIO的DirectBuffer使用，受 `-XX:MaxDirectMemorySize` 限制。