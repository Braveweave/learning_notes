# JAVA SE 初步



---

 1. 类： class 类是模板
 
 2. 对象： object \instance 对象是实例
 
  * 类是对象的模板，对象是类的实例，可以有一个或多个
  * 面向对象的程序设计 ：写一个程序时，程序员有两种角色： **写类的人，用类的人**
  
 3. 面对对象的类组成部分： 静态特征属性、动态特征行为（函数、方法）


------------------------

- 三个顶级元素，若干其他

0/1 package  类属于哪个package 
  
        package com.microsoft.hr 域名的反写


 0/n import 导入
 
        import java.lang.* 全部的类都要导入
        import java.util.*
        import javax.sql.connection
        

 java 类声明 写class
 
        访问修饰符 public default protect private
        如果用在类声明中修饰class ,只能用public 或 default
        当有多个class时可至多有一个public class,类名必须与当前文件名同名
        

* [google编码规范](http://www.hawstein.com/posts/google-java-style.html)

* [阿里巴巴编码规范](https://www.ibm.com/developerworks/cn/java/deconding-code-specification-part-1/index.html)

        public class testoo{
        {代码块}s
        属性s
        构造方法s
        方法s
        //内部类
        }
        

finalize():垃圾回收器准备释放内存时，相先调用finalize()

垃圾回收不是析构函数，对象不一定会被回收

垃圾回收与finalize()都是靠不住的，只有JVM还没快到耗尽内存的底部，是不会浪费时间进行垃圾回收的



    


 
