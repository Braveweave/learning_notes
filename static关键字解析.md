# static关键字解析

---

##static 关键字用途

>static方法就是没有this 的方法，在static 方法内部不能调用非静态方法，反过来是可以的，而且可以在没有创建任何对象的前提下，仅仅**通过类本身来调用static方法**

java中所有东西都可以理解为对象，在不考虑权限的情况下，类通常需要先实例化，然后通过对象的引用，访问成员变量或方法。然而有一种情况是例外的：static 修饰符修饰的变量或方法

一个变量或方法用static 修饰时，已经分配了内存空间，JVM不需要创建类实例就可以找到该内存区域调用相应的方法或属性

- 限制：
 - 仅能调用其他static 方法
 - 只能访问static 数据
 - 不能以其他方式引用this 或super



static 关键字修饰的方法或变量不需要依赖于对象进行访问，类被加载了就可以通过类名访问

- static 方法
 
由于静态方法不依赖于任何对象就可以进行访问，因此**对于静态方法来说，是没有this的**，因为它不依附于任何对象，既然都没有对象，就谈不上this了。

静态方法中**不能访问非静态成员方法和非静态成员变量**

- static变量

静态变量被所有的对象所共享，在内存中只有一个副本，它当且仅当在类初次加载时会被初始化。
　　
-----------------

##static 息息相关的单例模式

创建类的对象，即调用类的无参构造方法； 因为要创建一个人和情况都只有一个类实例，所以我们就要先控制这个无参构造方法的访问权限为私有，只有在类内部能调用这个构造方法。然而，类不创建，又如何调用无参的构造方法来创建对象呢？

那么就是凭借单例模式的核心：static。写一个静态方法（不需要创建对象，再类加载之后就可以调用），在这个静态方法内部，调用构造方法，来创建对象。方法返回值为这个类对象。

```
public class Singleton {

    private Singleton(){

    }
    public static Singleton getInstance(){
        return new Singleton();
    }
}
```

可能出现并发问题，修改后:在类加载的时候就产生了类实例，所以就保证了线程安全
```
public class Singleton {
    private static Singleton singleton =new Singleton();
    private Singleton(){

    }
    public static Singleton getInstance(){
            return singleton;
    }
}
```

缺点：失去了延迟加载特性，如果有1w个单例，不管有用没有产生所有实例造成冗余。

改进：使用synchronized的时候，一个线程在执行synchronized中的代码的时候如果别的线程也要执行其中的代码就要等到之前的线程运行完之后在才能够进入。
```
public class Singleton {
    private static Singleton singleton ;
    private Singleton(){

    }
    public static Singleton getInstance(){
        if(singleton==null){
            synchronized (Singleton.class) {
                if(singleton==null){
                    singleton=new Singleton();
                }
            }
        }
            return singleton;
    }
}
```

判断对象是否已经创建，如果没有创建，则进入同步代码中，进入之后再判断是否已经创建，排除第一次创建时就发生并发的问题，如果已经创建则结束同步代码，如果为创建，则创建对象。其中同步锁用类的字节码也就是Singleton.class。实现单例模式的时候，只有第一次创建类实例的时候进入了同步锁中。极大的避免了同步所带来的等待问题。锁内和锁外两次判断也确保了类实例的唯一性。


