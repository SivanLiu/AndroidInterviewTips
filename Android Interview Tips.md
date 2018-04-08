---

title: Android/Java 面试锦囊

date:  2018-3-23 22:42:21

tags:  Android/Java

top: 30

---

# Android、Java 面试集锦

## 一、Android 面试
### 1. Intent 传值有大小限制吗，为什么，如何处理；
#### 1.1 限制：
Intent（包括Bundle一共）大小限制为不到 1MB(实测某些机型上 500k 左右也无法正常传递)，所以在超过这个限制之后，就会出现静默崩溃的现象

#### 1.2 解决方案：

* 写入临时文件或者数据库，通过 FileProvider 将该文件或者数据库通过 Uri 发送至目标。一般适用于不同进程，比如分离进程的 UI 和后台服务，或不同的 App 之间。之所以采用 FileProvider 是因为 7.0 以后，对分享本 App 文件存在着严格的权限检查。
* 通过设置静态类中的静态变量进行数据交换。一般适用于同一进程内，这样本质上数据在内存中只存在一份，通过静态类进行传递。需要注意的是进行数据校对，以防多线程Data Racer出现导致的数据显示混乱。

### 2. 自定义 View 流程，主要的方法及各自作用；如何防止过度绘制；对View中的onMesurse方法的详细介绍和使用；

### 3. 事件分发及举例说明；
### 4. LruCache和DisLruCache的原理；；
### 5. 谈谈内存优化；
### 6. 安卓中方法数不能超过 64k 的原因，及如何处理；
### 7. 如何实现圆形 ImageView；
### 8. 说说动态代理的作用；
### 9. 谈谈注解；
### 10. 如何自己实现RecyclerView的侧滑删除；
### 11. TabLayout中如何让当前标签永远位于屏幕中间；
### 12. Activity跳转时的生命周期问题；
### 13. Retrofit和EventBus的源码分析；
### 14. 对 js 互调如何使用，做过什么优化；
### 15. 遇到过哪些关于 Fragment 的问题；

### 16. 图片的处理、缓存和优化；
### 17. Android 实现异步的几种方式；
### 18. 如何对 Android 应用进行性能分析；
### 19. MVP的优点与确点；
### 20. 64k出现的原因及如何解决
### 21. 对 ART 的认识；
### 22. 动态代理的作用；
### 23. TextView调用setText方法的内部执行流程；
### 24. ClassLoader的双亲委派；ClassLoader
这个其实要是问起来其实是有很多东西的，如果是Java相关其实还好，会问你类加载机制，但是Android里面除了Java的类加载机制之外，还会引出插件化跟热修复。### 25. 虚拟机
JVM
对于Java，加载的是Class文件，一般会问到Java运行时的内存分配，类加载机制以及GC，实际上后面两个问地比较多，尤其是GC相关，往往结合四种引用出题，最后会通过这个来引出内存泄露相关的一些问题。

DVM&ART
Android的虚拟就DVM以及ART是对JVM做了一些优化，加载的是dex文件，对Class字节码做了一些优化，这个里面其实挺复杂的，我只知道一些基本的概念。


### 25. JNI
基本上稍微大点的公司都会问到，不过我的回答始终如一：我只能看懂C的代码，项目中没有用过JNI，当然这个属于加分项，因为我当时的选择是把我用过熟悉的东西研究地滚瓜烂熟，而不是在自己平时很少接触到的东西上面搞个一知半解。

### 26. Binder
Binder系列，各种AMS,WMS,PWS，常问到的有APP的启动流程，然后两个Activity相互跳转的时候的生命周期，Activity的生命周期。




## 二、Java 面试
### 1. Java 基础：
#### 1. 请简述下 java 中 ==，equals，hashCode 的区别
##### a. 概念
* == ：操作符，生成的是一个 boolean 结果，它计算的是操作数的值之间的关系，针对于原生类型的比较；
* equals ： Object 的实例方法，比较两个对象的内容是否相同；
* hashCode ： Object 的 native方法，获取对象的哈希值，用于确定该对象在哈希表中的索引位置，它实际上是一个 int 型整数；

##### b. 异同点：
* == 用来比较原生类型如：boolean、int、char 等等，而 equals() 则用来比较对象；
* 如果两个引用指向相同的对象，== 返回 true，equals() 的返回结果则依赖于具体的业务实现；
* 字符串的对比使用 equals() 代替 == 操作符；
* 如果两个对象 equals，则 hashcode 一定相等；
* 如果两个对象不 equals ，则 hashcode 可能相等；
* 如果两个对象 hashcode 相等，那么不一定 equals；
* 如果两个对象 hashcode 不相等，则一定不 equals

#### 2. int、char、long 各占多少字节数?

##### a. 基本数据类型：
| 类型 | 字节(byte) | bit 数 | 取值范围 | 封装类 |
| :---: | :---: | :---: | :---: | --- |
| int | 4 | 32 | -2147483648~2147483647 | Integer |
| short | 2 | 16 | -32768~32767 | Short |
| long | 8 | 64 | Long |
| byte | 1 | 8 | -128~127 | Byte |
| float | 4 | 32 | Float |
| double | 8 | 64 | Double |
| boolean | 1 | 8 | true、false | Boolean |
| char | 2 | 16 | Character |

##### b. int 与 integer 的区别（基本类型与其封装类的区别）：
* int 属于基本数据类型，放在栈中，直接存数值，而 integer 属于复杂数据类型对象；
* 在类进行初始化时 int 类的变量初始为 0，而 Integer 的变量则初始化为 null；
* 基本数据类型只能按值传递，而封装类按引用传递；
* 基本类型在堆栈中创建；而对于对象类型，对象在堆中创建，对象的引用在堆栈中创建。基本类型由于在堆栈中，效率会比较高，但是可能会存在内存泄漏的问题；

##### c. 有了基本类型，为什么还要使用封装类呢？
* 某些情况下，数据必须作为对象出现，此时必须使用封装类来将简单类型封装成对象。比如，如果想使用 List 来保存数值，由于 List 中只能添加对象，因此我们需要将数据封装到封装类中再加入 List。在 JDK5.0 以后可以自动封包，可以简写成 list.add(1) 的形式，但添加的数据依然是封装后的对象
* 某些情况下，自定义诸如 func(Object o) 的这种方法，它可以接受所有类型的对象数据，但对于简单数据类型，我们则必须使用封装类的对象
* 某些情况下，使用封装类使我们可以更加方便的操作数据。比如封装类具有一些基本类型不具备的方法，比如 valueOf()，toString()，以及方便的返回各种类型数据的方法，如 Integer 的 shortValue()，longValue()，intValue()等

#### 3. 谈谈你对 java 多态的理解
##### a. **多态的三个必要条件**：

* 继承
* 子类要重写父类的方法
* 父类引用指向子类对象

**下面看个例子：**

```java
//父类
public class Animal {
    int num = 10;
    static int age = 20;

    public void eat() {
        System.out.println("动物吃饭");
    }

    public static void sleep() {
        System.out.println("动物睡觉");
    }

    public void run() {
        System.out.println("动物奔跑");
    }
}

//子类
public class Dog extends Animal {
    int num = 100;
    static int age = 40;

    String name = "MyDog";

    public void eat() {
        System.out.println("小狗吃饭");
    }

    public static void sleep() {
        System.out.println("小狗睡觉");
    }

    public void playFootball() {
        System.out.println("小狗玩球");
    }
}

public class Polymorphism {
    public static void main(String[] args) {
        Animal animal = new Dog();
        animal.eat();
        animal.sleep();
        animal.run();
        System.out.println("num = " + animal.num);
        System.out.println("age = " + animal.age);
        
//        System.out.println("age = " + animal.name);
//        animal.playFootball();
    }
}
```
**上述三段代码充分体现了多态的三个前提：**

* 继承：Dog 类继承了 Animal 类
* 子类要重写父类的方法：Dog 类重写了父类的 eat()，sleep() 两个成员方法，其中 eat() 是非静态的，sleep() 是静态的
* 父类数据的类型的引用指向子类对象：Polymorphism 中 Animal animal = new Dog()；语句在堆内存中开辟了子类 Dog 的对象，并把栈内存中的父类 Animal 的引用指向了 Dog 对象

**下面看看结果是什么？**

```groovy
小狗吃饭
动物睡觉
动物奔跑
num = 10
age = 20

Process finished with exit code 0
```
**可以看出来：**

* 子类 Dog 重写了父类 Animal 的非静态成员方法 animal.eat()；的输出结果为：小狗吃饭
* 子类重写了父类 Animal 的静态成员方法 animal.sleep()；的输出结果为：动物睡觉
* 未被子类 Dog 重写的父类 Animal 方法 animal.run()；输出结果为：动物奔跑
* 子类 Dog 重新定义了父类中的成员变量 num，age，输出结果为：10，20

**从上述结果可知：**

* 成员变量：编译看父类，运行看父类
* 非静态成员方法：编译看父类，运行看子类
* 静态成员方法：编译看父类，运行看父类

##### b. **那么多态有什么缺点吗？**
Polymorphism 中最后两行代码会报错，找不到 Dog 中的 name 和 playFootball
从上述结果可知，**多态后不能使用子类特有的成员属性和子类特有的成员方法**

如果想要在多态中访问特有的成员属性和方法，该怎么做呢？
**将父类引用指向子类对象 animal 再强制转回 Dog 类型后就可以访问 Dog 类中的所有属性和方法了。**

**修改后的代码如下：**

```java
public class Polymorphism {
    public static void main(String[] args) {
        Animal animal = new Dog();
        animal.eat();
        animal.sleep();
        animal.run();
        System.out.println("num = " + animal.num);
        System.out.println("age = " + animal.age);

//        System.out.println("age = " + animal.name);
//        animal.playFootball();

        System.out.println("*****************************");
        Dog dog = (Dog) animal;
        dog.eat();
        dog.sleep();
        dog.run();
        System.out.println("num = " + dog.num);
        System.out.println("age = " + dog.age);

        System.out.println("age = " + dog.name);
        dog.playFootball();
    }
}
```

**结果：**

```groovy
小狗吃饭
动物睡觉
动物奔跑
num = 10
age = 20
*****************************
小狗吃饭
小狗睡觉
动物奔跑
num = 100
age = 40
age = MyDog
小狗玩球
```
现在 dog 就指向了最开始在堆内存中创建的 Dog 类型的对象了，尽管多态存在缺点，但优势十分明显。

##### c. **多态的优点主要有以下几个方面：**

- 消除类型之间的耦合关系 
- 可替换性：多态对已存在的代码具有可替换性。
- 可扩充性：多态对代码具有可扩充性，增加新的子类不影响已存在类的多态性、继承性，以及其他特性的运行和操作。
- 接口性：多态是超类通过方法签名，向子类提供了一个共同接口，由子类来完善或者覆盖它而实现的。
- 灵活性：它在应用中体现了灵活多样的操作，提高了使用效率。
- 简化性：多态简化了对应用软件的代码编写和修改过程，尤其在处理大量对象的运算和操作时，这个特点尤为突出和重要。值得注意的是，多态并不能够解决提高执行速度的问题，因为它基于动态装载和地址引用，或称动态绑定。 

#### 4. String、StringBuffer、StringBuilder 区别

##### a. 定义：

* String: 字符串常量，使用 char[] 保存字符串，有 final 修饰，其对象不可变，对 String 对象的任何改变都不影响到原对象，相关的任何改变操作都会生成新的对象；
* StringBuffer: 字符串变量（Synchronized，即线程安全），继承自 AbstractStringBuilder 类，AbstractStringBuilder 中也是使用 char[] 来保存字符串；
* StringBuilder: 字符串变量，线程不安全，继承自 AbstractStringBuilder 类；

##### b. 使用场景：

* String：操作少量数据的情况下
* StringBuffer：多线程情况下操作大量数据 
* StringBuilder：单线程情况下操作大量数据

#### 5. 什么是内部类？说说内部类的作用？

##### a. 定义：
内部类是指定义在类的内部的类，主要分为以下几种：

###### 1）成员内部类
在外部类内部直接定义（不在方法内部或代码块内部）的类就是成员内部类，它可以直接使用外部类的所有变量和方法，即使是 private 的。外部类要想访问内部类的成员变量和方法，则需要通过内部类的对象来获取。

* 静态内部类：使用 static 修饰的成员内部类，除了访问权限修饰符比外围类多以外, 和外围类没有区别, 只是代码上将静态内部类组织在了外围类里面. 如果在外围类外部引用静态内部类, 需要带上外围类的名字
* 非静态内部类：没有 static 修饰的成员内部类

###### 2）局部内部类
局部内部类是在某个作用域或方法体内定义的内部类，局部内部类不能有 private 等访问说明符

###### 3）匿名内部类
匿名内部类则用来创建一个继承自某个基类的匿名类的对象，并向上转型为该基类的引用。
* 匿名内部类不能是抽象类：匿名内部类创建时，会立即创建匿名内部类的对象
* 匿名内部类不能定义构造器：无类名，无法定义构造器，但可定义初始化块

###### 4）匿名内部类与 Lambda：

* Lambda 表达式的目标类型必须是明确的函数式接口
* Lambda 表达式只能为函数式接口创建对象

**Lambda 常见方式：**

* 将 Lambda 表达式赋值给函数式接口类型的变量
* 将 Lambda 表达式作为函数式接口类型的参数传给某个方法
* 使用函数式接口对 Lambda 表达式进行强制类型转换

**Lambda 表达式支持的方法引用和构造器引用**

| 种类 | 示例 | 说明 | 对应的 Lambda 表达式 |
| :-- | :-- | :-- | :-- |
| 引用类方法 | 类名::类方法 | 函数式接口中被实现方法的全部参数传给该类方法作为参数 | (a, b...)-> 类名.类方法(a, b...)  |
| 引用特定对象的实例方法 | 特定对象::实例方法 | 函数式接口中被实现方法的全部参数传给该方法作为参数 | (a, b...)-> 特定对象.实例方法(a, b,...) |
| 引用某类对象的实例方法 | 类型::实例方法 | 函数式接口中被实现方法的第一个参数作为调用者，后面的参数全部传给该方法作为采纳数 | (a, b...)-> a.实例方法(b,...) |
| 引用构造器 | 类名::new | 函数式接口中被实现方法的全部参数传给该构造器作为参数 | (a, b...)-> new 类名(a, b,...) |

**Lambda 表达式与匿名内部类的主要区别**：

* 匿名内部类可以为任意接口创建实例，但 Lambda 只能为函数式接口创建实例；
* 匿名内部类可以为抽象类甚至普通类创建实例，但 Lambda 表达式只能为函数式接口创建实例；
* 匿名内部类实现抽象方法的方法允许调用接口中定义的默认方法，但 Lambda 表达式的代码不允许调用接口中定义的默认方法

###### 6）内部类与外部类语法区别：

* 内部类比外部类可以多使用三个修饰符：private/protected/static
* 非静态内部类不能拥有静态成员

##### b. 作用：

* 可以用来实现“多重继承”，弥补了单继承的缺陷；
* 内部类可以有多个实例，每个对象都与外围类相互独立；
* 可以让多个内部类以不同的方式实现同一个接口，或继承同一个类；
* 创建内部类对象的时刻并不依赖于外围类对象的创建；
* 内部类可以直接或利用引用访问外部类的属性和方法，包括私有属性和方法（但静态内部类不能访问外部类的非静态成员变量和方法）
* 内部类提供了更好的封装，可以把内部类隐藏在外部类之内，不允许同一个包中的其他类访问该类
* 内容类成员可以直接访问外部类的私有数据，因为内部类被当做其外部类成员，同一个类的成员之间可以相互访问，但外部类不能访问内部类的实现细节，如内部类的成员变量
* 匿名内部类适合用于创建那些仅需要一次使用的类

#### 6. 抽象类和接口区别，抽象类的意义，抽象类是否可以没有方法和属性？
##### 6.1 抽象类、抽象方法：
* 抽象类必须使用 abstract 修饰符来修饰，抽象方法也必须使用 abstract 修饰符来修饰，抽象方法不能有方法体
* 抽象类不能被实例化，无法使用 new 关键字来调用抽象类的构造器创建抽象类的实例
* 抽象类可以包含成员变量、方法、构造器、初始化块、内部类(接口、枚举) 5 种成分。抽象类的构造器不能用于创建实例，主要用于被其子类调用
* 含有抽象方法的类只能被定义成抽象类

**意义：**
抽象类是从多个具体类中抽象出来的父类，它具有更高层次的抽象，从多个具有相同特征的类中抽象出一个抽象类，以这个抽象类作为其子类的模板，从而避免了子类设计的随意性

**模板模式：**
* 抽象父类可以只定义需要使用的某些方法，把不能实现的部分抽象成抽象方法，留给其子类去实现
* 父类中可能包含需要调用其他系列方法的方法，这些被调用方法可以由父类实现，也可以由其子类实现

##### 6.2 接口：
接口是从多个相似类中抽象出来的规范，接口不提供任何实现，接口体现的是规范和实现分离的设计哲学，降低模块间的耦合性，提供更好的扩展性和可维护性

##### 6.3 联系：

* 接口和抽象类都不能被实例化，它们都位于继承树的顶端，用于被其他类实现和继承
* 接口和抽象类都可以包含抽象方法，实现接口或者继承抽象类的普通子类都必须实现这些抽象方法
 
##### 6.4 区别：
* 接口体现的是一种规范，类似于整个系统的总纲，制定了系统各模块应该遵循的标准，因此一个系统中的接口不应该经常改变
* 抽象类体现的是一种模板式设计，作为多个子类的抽象父类，可以看作是系统实现过程中的中间产品
* 接口里只能包含抽象方法和默认方法，不能为普通方法提供方法实现；抽象类则完全可以包含普通方法
* 接口里不能定义静态方法；抽象类里可以定义静态方法
* 接口里只能定义静态常量，不能定义普通成员变量；抽象类里则既可以定义普通成员变量，也可以定义静态常量
* 接口里不包含构造器；抽象类里可以包含构造器，抽象类里的构造器并不是用于创建对象，而是让其子类调用这些构造器来完成属于抽象类的初始化操作
* 接口里不能包含初始化块；但抽象类里则完全可以包含初始化块
* 一个类最多只能有有一个直接父类，包括抽象类，但一个类可以直接实现多个接口，通过实现多个接口可以弥补 Java 单继承的不足
* 抽象类单继承，接口多实现

#### 7. Java 泛型中 extends 和 super 的区别
* <? extends T>：是指包括 T 在内的任何 T 的子类，称为“上界通配符”；频繁往外读取内容的，适合用上界 extends。
* <? super T>：是指包括 T 在内的任何 T 的父类，称为“下界通配符”；经常往里插入的，适合用下界 Super

#### 8. 父类的静态方法能否被子类重写

* 静态方法是在编译阶段使用了编译类型信息，进行静态绑定的
* 静态方法从程序开始运行后就已经分配了内存，子类中如果定义了相同名称的静态方法，并不会重写，而应该是在内存中又分配了一块给子类的静态方法
* 父类的静态方法可以被子类继承，但是不能重写

#### 9. 进程和线程的区别
##### 9.1 进程：
进程是处于运行过程中的程序，并且具有一定的独立功能，进程是系统进行资源分配和调度的一个独立单位

**三个特征**

* 独立性：进程是系统中独立存在的实体，拥有自己独立的资源，每一个进程都拥有自己私有的地址空间；
* 动态性：进程是一个正在系统中活动的指令集合，而程序只是一个静态的指令集合；进程包含了时间的概念，拥有自己的生命周期和各种不同的状态；
* 并发性：多个进程可以在单个处理器上并发执行，多个进程之间不会互相影响；

并发性和并行性的区别：并行指在同一个时刻，有多条指令在多个处理器上同时执行；并发指在同一个时刻只能有一条指令执行，但多个进程指令被快速地轮换执行，使得在宏观上具有多个进程同时执行的效果

##### 9.2 线程：
线程是进程的执行单元，线程在程序中是独立的、并发的执行流；线程可以拥有自己的堆栈、程序计数器、局部变量，但不拥有系统资源，与父进程的其它线程共享该进程所拥有的全部资源

###### a. 多线程优点：
* 进程之间不能共享内存，但线程之间共享内存非常容易；
* 系统创建进程时需要为该进程重新分配系统资源，但创建进程则代价小得多，因此使用多线程来实现多任务并发比多进程的效率高；

###### b. 线程的创建方式：
* 继承 Thread 类创建线程类；
* 实现 Runnable 接口创建线程类；
* 使用 Callable 和 Future 创建线程；
 
```java
//创建 Callable 接口的实现类，并实现 call() 方法，该 call() 方法将作为线程执行体，且该 call() 方法有返回值，再创建 Callable() 实现类的实例
//使用 FutureTask 类来包装 Callable 对象，该 FutureTask 对象封装了该 Callable 对象的 call() 方法的返回值
//调用 FutureTask 对象作为 Thread 对象的 target 创建并启动新线程
//调用 FutureTask 对象的 get() 方法来获得子线程执行结束后的返回值
Callable<Integer> callable = () -> {
            int i = 100;
            System.out.println("Callable thread : " + Thread.currentThread().getName() + " " + i);
            return i;
        };

FutureTask<Integer> task = new FutureTask<>(callable);
new Thread(task, "有返回值的线程").start();
try {
        System.out.println("Callable thread get = " + task.get());
    } catch (InterruptedException | ExecutionException e) {
        e.printStackTrace();
    }
```
###### c. 三种创建方式比较：
**采用实现 Runnable、Callable 接口的方式创建多线程的优缺点：**
**优点：**

* 线程类只是实现了 Runnable 接口或 Callable 接口，还可以继承其他类；
* 多个线程可以共享同一个 target 对象，非常适合多个相同线程来处理同一份资源的情况，从而可以将 CPU、代码和数据分开，形成清晰的模型，较好地体现了面向对象的思想

**缺点：**

* 编程稍微复杂，必须使用 ThreadCurrentThread 访问当前线程 

**采用继承 Thread 类的方式创建多线程的优缺点：**

**优点：**

* 编写简单，直接使用 this 可以获取当前线程

**缺点：**

* 线程类已经继承了 Thread 类，不能再继承其他父类

###### d. 线程的生命周期

* 新建：new 关键字创建线程之后；
* 就绪：调用了 start() 方法；
* 运行：获得了 CPU， 开始执行 run() 方法的线程执行体； 
* 阻塞：调用 sleep() 方法主动放弃所占用的处理器资源，调用了阻塞式 IO 方法，线程试图获取同步监视器，但监视器正被其他线程所持有，线程在等待某个通知(notify)，调用了线程的 suspend() 方法将线程挂起
* 死亡：run() 或者 call() 方法执行完成，线程正常结束；线程抛出一个未捕获的异常或者错误；直接调用线程的 stop() 方法来结束该线程，该方法易导致死锁；

###### e. 线程控制

* **join 线程**：当在某个程序执行流中调用其他线程的 join() 方法时，调用线程将被阻塞，直到被 join() 方法加入的 join 线程执行完为止；通常由使用线程的程序调用，以将大问题划分成许多小问题，每个小问题分配一个线程，当所有的小问题都得到处理后，再调用主线程来进一步操作

```java
public class ThreadTest {
    public static void main(String[] args) {
        new Thread1("第一个线程").start();
        for (int i = 0; i < 5; ++i) {
            if (i == 3) {
                Thread1 thread1 = new Thread1("被 Join 的线程");
                thread1.start();
                try {
                    thread1.join();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }

            System.out.println("主线程 = " + Thread.currentThread().getName() + " i = " + i);
        }
    }
}


class Thread1 extends Thread {
    Thread1(String name) {
        super(name);
    }

    @Override
    public void run() {
        for (int i = 0; i < 5; ++i) {
            System.out.println("thread1 name = " + this.getName() + " i =" + i);
        }
    }
}

结果：

thread1 name = 第一个线程 i =0
thread1 name = 第一个线程 i =1
thread1 name = 第一个线程 i =2
thread1 name = 第一个线程 i =3
thread1 name = 第一个线程 i =4
主线程 = main i = 0
主线程 = main i = 1
主线程 = main i = 2
thread1 name = 被 Join 的线程 i =0
thread1 name = 被 Join 的线程 i =1
thread1 name = 被 Join 的线程 i =2
thread1 name = 被 Join 的线程 i =3
thread1 name = 被 Join 的线程 i =4
主线程 = main i = 3
主线程 = main i = 4
Process finished with exit code 0
```

* **后台线程：** 在后台运行的线程，为其他线程提供服务，如 JVM 的垃圾回收线程；前台线程都结束，后台线程也会自动结束； Thread.setDaemon(true) 可将指定线程设置成后台线程，必须在 start 之前调用

```java
public class ThreadTest {
    public static void main(String[] args) {
        Thread t = new Thread1("第一个线程");

        t.setDaemon(true);
        t.start();

        for (int i = 0; i < 5; ++i) {
            System.out.println("主线程 = " + Thread.currentThread().getName() + " i = " + i);
            Thread.currentThread().stop();
        }

    }
}

class Thread1 extends Thread {
    Thread1(String name) {
        super(name);
    }

    @Override
    public void run() {
        for (int i = 0; i < 500; ++i) {
            System.out.println("SubThread name = " + this.getName() + " i =" + i);
        }
    }
}

结果：
主线程结束时，后台线程也随之结束了
```

**线程睡眠：sleep**
线程暂停一段时间，并进入阻塞状态。

**线程让步：yield**
yield 也可以让当前正在执行的线程暂停，但它不会阻塞该线程，只是将线程转入就绪状态；实际上当某个线程调用了 yield() 方法之后，只有优先级与该线程相同或者更高的处于就绪状态的线程才会获得执行的机会。

```java
public class ThreadTest {
    public static void main(String[] args) {
        Thread t1 = new Thread1("第一个线程");
        t1.start();

        Thread t2 = new Thread1("第二个线程");
        t2.start();
    }
}


class Thread1 extends Thread {
    Thread1(String name) {
        super(name);
    }

    @Override
    public void run() {
        for (int i = 0; i < 5; ++i) {

            System.out.println("SubThread name = " + this.getName() + " i =" + i);
            if (i == 2) {
                Thread.yield();
            }
        }
    }
}

结果：在多 cpu 并行的情况下，yield() 方法的功能并不明显
SubThread name = 第一个线程 i =0
SubThread name = 第一个线程 i =1
SubThread name = 第二个线程 i =0
SubThread name = 第一个线程 i =2
SubThread name = 第二个线程 i =1
SubThread name = 第二个线程 i =2
SubThread name = 第一个线程 i =3
SubThread name = 第一个线程 i =4
SubThread name = 第二个线程 i =3
SubThread name = 第二个线程 i =4

Process finished with exit code 0

设置优先级后的结果：
SubThread name = 第一个线程 i =0
SubThread name = 第二个线程 i =0
SubThread name = 第二个线程 i =1
SubThread name = 第一个线程 i =1
SubThread name = 第二个线程 i =2
SubThread name = 第一个线程 i =2
SubThread name = 第二个线程 i =3
SubThread name = 第二个线程 i =4
SubThread name = 第一个线程 i =3
SubThread name = 第一个线程 i =4

Process finished with exit code 0
```

**sleep() 和 yield() 区别：**

1. sleep() 暂停线程后，会给其他线程执行机会，跟优先级无关，但 yield() 只会给优先级相同或更高的线程的执行机会；
2. sleep() 会将线程转入阻塞状态，而 yield() 不会，只是强制线程进入就绪状态；
3. sleep() 抛出异常，而 yield() 不会抛出任何异常；
4. slee() 比 yield() 方法有更好的移植性，不建议使用 yield() 控制并发线程的执行；

###### f. 线程同步

1. 同步代码块： synchronized 修改是的代码块
2. 同步方法： synchronized 修饰的实例方法
3. 线程安全类：可以被多个线程安全地访问，每个线程调用该对象的任意方法之后都将得到正确结果，每个线程调用该对象的任意方法之后，该对象依然保持合理状态
4. 同步锁(ReadWriteLock/ReentrantLock/ReentrantReadWriteLock/StampedLock)：显式定义同步锁对象来实现同步
5. 死锁：两个线程互相等待对方释放同步监视器时就会发生死锁

###### g. 线程通信：

1) 传统的线程通信借助于 Object 类的 wait()、notify() 和 notifyAll() 方法：

* wait(): 导致当前线程等待，直到其他线程调用该同步监视器的 notify() 方法或 notifyAll() 方法来唤醒该线程；调用 wait() 方法的当前线程会释放对该同步监视器的锁定。
* notify(): 唤醒在此同步监视器上等待的单个线程。如果所有线程都在同步监视器上等待，则会选择唤醒其中的任意一个线程；只有当前线程放弃对该同步监视器的锁定后，才可以执行被唤醒的线程。
* notifyAll(): 唤醒在此同步监视器上等待的所有线程；只有当前线程放弃对该同步监视器的锁定后，才可以执行被唤醒的线程。

2) 如何调用？ 

* 对于使用 synchronized 修饰的同步方法，因为该类的默认实例(this)就是同步监视器，可以在同步方法中直接调用 wait()、notify() 和 notifyAll() 方法
* 对于使用 synchronized 修饰的同步代码块，同步监视器是 synchronized 后括号里的对象，所以必须使用该对象调用 wait()、notify() 和 notifyAll() 方法
   
3) 使用 Condition 控制线程通信

对于使用 Lock 对象来保证同步的情况，则系统中不存在隐式的同步监视器，就不能使用 wait()、notify() 和 notifyAll() 方法了；此时就需要 Condition 来保持协调，使用 Condition 可以让那些已经得到 Lock 对象却无法继续执行的线程释放 Lock 对象，Condition 对象也可以唤醒其他处于等待的线程

* await(): 类似于隐式监视器上的 wait() 方法，导致当前线程等待，直到其他线程调用该 Condition 的 signal() 或 signalAll() 方法来唤醒该线程；
* signal(): 唤醒在此 Lock 对象上等待的单个线程，如果所有的线程都在该 Lock 对象上等待，则会选择唤醒其中任意一个；只要当前线程放弃对该 Lock 对象的锁定后，才可以执行被唤醒的线程；
* signalAll(): 唤醒在此 Lock 对象上等待的所有个线程；只要当前线程放弃对该 Lock 对象的锁定后，才可以执行被唤醒的线程；

4) 使用阻塞队列(BlockingQueue)控制线程通信

BlockingQueue 主要作为线程同步的工具，当生产者线程试图向 BlockingQueue 中放入元素时，如果该队列已满，则该线程被阻塞；当消费者线程试图从 BlockingQueue 中取出元素时，如果该队列为空，则该线程被阻塞。

* put(E e): 尝试把 E 元素放入 BlockingQueue 中，如果该队列的元素已满，则阻塞该线程；
* take(): 尝试从 BlockingQueue 的头部取出元素，如果该队列的元素为空，则阻塞该线程；

###### h. 线程池(线程池的参数和工作原理；)
1) 创建线程池：

* newCachedThreadPool(): 创建一个具有缓存功能的线程池
* newFixedThreadPool(int nThreads): 创建一个可重用的，具有固定线程数的线程池
* newSingleThreadExecutor(): 创建一个只有单线程的线程池，相当于 newFixedThreadPool 方法时传入参数 1
* ExecutorService newWorkStealingPool(int parallelism): 创建持有足够的线程的线程池来支持给定的并行级别，该方法还会使用多个队列来减少竞争

ExecutorService 代表尽快执行线程的线程池，只要线程池中有空闲线程，就立即执行线程任务，程序只要将一个 Runnable 对象或 Callable 对象提交给该线程池，该线程池就会尽快执行该任务。

2) ExecutorService 创建线程池的步骤：

* 调用 Executors 类的静态方法创建一个 ExecutorService 对象，该对象代表一个线程池
* 调用 Runnable 实现类或 Callable 实现类的实例，作为线程执行任务
* 调用 ExecutorService 对象的 submit() 方法来提交 Runnable 实例或 Callable 实例
* 当不提交任何任务时，调用 ExecutorService 对象的 shutdown() 方法来关闭线程池

```java
public class ThreadPoolTest {
    public static void main(String[] args) {

        ExecutorService pool = Executors.newFixedThreadPool(5);
        Runnable runnable = () -> {
            for (int i = 0; i < 10; i++) {
                System.out.println("CurrentThreadName = " + Thread.currentThread().getName() +
                        " 的 i 的值为：" + i);
            }
        };


        pool.submit(runnable);
        pool.submit(runnable);

        pool.shutdown();
    }
}
```

#### 10. final，finally，finalize 的区别
* final(修饰符): 修饰类、成员变量和成员方法，类不可被继承，成员变量不可变，成员方法不可重写
* finally(异常处理):与 try...catch... 共同使用，确保无论是否出现异常都能被调用到
* finalize(垃圾回收): 类的方法，垃圾回收之前会调用此方法，子类可以重写finalize() 方法实现对资源的回收

#### 11. 谈谈序列化的方式，Serializable 和 Parcelable 的区别
##### 11.1 定义：
序列化就是将对象转为字节序列的过程；任何数据都是以二进制的形式存贮到硬盘或是在网络上传送，而 Java 为了能将 Java 对象存贮到硬盘上或在网络上传送，把 Java 对象转换成字节流进行传输，这个转换过程就称之为Java序列化。Java 对象 --> 二进制字节流。

##### 11.2 意义

* 持久化：将那些内存中的瞬时数据保存到存储设备中，保证在程序关闭的情况下，这些数据仍然不会丢失；保存在内存中的数据是处于瞬时状态的，而保存在存储设备中的数据是处于持久状态的；持久化技术则是提供了一种机制可以让数据在瞬时状态和持久状态之间进行转换。Android数据持久主要通过文件存储、SharedPreference 存储以及数据库存储来实现
* 进程间对象传递: 由于字节是两个进程都认可并能处理的方式；进程之间不共享内存，如果想要从 A 进程传递一个类对象到 B进程，那么就需要把 A 的类对象转换为字节序列，在 B 中接收字节并处理。

##### 11.3 Serializable 和 Parcelable 区别：

* 存储媒介：Serializable 使用 I/O 读写存储在硬盘上，而 Parcelable 是直接在内存中读写。很明显，内存的读写速度通常大于 IO 读写，所以在 Android 中传递数据优先选择 Parcelable。
* 效率：Serializable 会使用反射，序列化和反序列化过程需要大量 I/O 操作，适用于将对象存储到文件或网络传输；Parcelable 自已实现封送和解封操作不需要用反射，数据也存放在 Native 内存中，效率要快很多。

#### 12. 谈谈对 http 缓存的了解。

#### 13. ArrayList、Vector、LinkedList的区别；

#### 14. JVM垃圾回收机制；

## 三、算法
### 1. 电梯运行的算法分析；
### 2. 冒泡排序；
### 3. 
















