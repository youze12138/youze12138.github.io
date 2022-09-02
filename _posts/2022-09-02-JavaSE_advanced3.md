---
title: 面向对象-知识点
date: 2022-09-02 14:34:00 +0800
categories: [面向对象-知识点]
tags: [后端]
pin: true
author: BruceZhou

toc: true
comments: true
typora-root-url: ../../youze12138.github.io
math: false
mermaid: truey
---

# 面向对象-知识点

## 内部类 

### 1.1 内部类-成员内部类

1.什么是内部类

在一个类中定义一个类。

举例：在一个类A的内部定义一个类B，类B就被称为内部类，像这样👇

```java
/*
	格式：
    class 外部类名{
    	修饰符 class 内部类名{
    	
    	}
    }
*/

class Outer {
    public class Inner {
        
    }
}
```

3 内部类的分类

- 在类的成员位置:成员内部类
- 在类方法内位置:局部内部类

4 外部如何使用普通成员内部类？

格式:外部类名.内部类名 对象名=new 外部对象().new 内部对象()

范例: Outer.Inner oi=new Outer().new Inter();

```java
package com.itheima.test1;
class Outer {

    private int a = 10;

    class Inner {
        int num = 10;

        public void show(){
            System.out.println("Inner..show");
            // 内部类, 访问外部类成员, 可以直接访问, 包括私有
            System.out.println(a);
        }
    }
}
```

5 成员内部类的访问非静态成员时的特点 

1. 内部类可以直接访问外部类的成员，包括私有
2. 外部类要访问内部类的成员，必须创建对象

### 1.2 私有成员内部类-静态成员内部类

1.私有成员内部类的访问特点

只能在自己所在的外部类中创建对象访问

2.如何创建静态成员内部类对象？

​	外部类名.内部类名 对象名 = new 外部类名.内部类名();

3.如何访问静态成员内部类中的静态方法？

​	外部类名.内部类名.方法名();

**示例代码**

### 1.3 局部内部类

1.什么是局部内部类

在方法中定义的类

2.局部内部类如何使用？

   局部内部类，外界是无法直接使用，需要在方法内部创建对象并使用

3.局部内部类的特点

1. 局部内部类是在方法中定义的类
2. 该类可以直接访问外部类的成员，也可以访问方法内的局部变量

### 1.4 匿名内部类【重点】

1.什么是匿名内部类？

​	特殊的局部内部类

2 匿名内部类的前提

 存在一个类或者接口，这里的类可以是具体类也可以是抽象类

3 如何使用匿名内部类？

- 格式：new 类名 ( ) {  重写方法 }   

- new  接口名 ( ) { 实现方法 }

- 举例： 

  ```java
  new Inter(){
      @Override
      public void method(){}
  } 
  ```

4 匿名内部类的本质

​    本质：是一个继承了该类或者实现了该接口的子类匿名对象

​    理解 :  匿名内部类是将(继承\实现)(方法重写)(创建对象)三个步骤,放在了一步进行

### 1.5 匿名内部类的应用场景【重点】

- 匿名内部类在开发中的使用

  当某个方法的参数类型是一个接口或抽象类 类型

  **示例代码：**

  ```java
  package com.itheima.test6;
  
  public class TestSwimming {
      public static void main(String[] args) {
          goSwimming(new Swimming() {
              @Override
              public void swim() {
                  System.out.println("铁汁, 我们去游泳吧");
              }
          });
      }
  
      /**
       * 使用接口的方法
       */
      public static void goSwimming(Swimming swimming){
          /*
              Swimming swim = new Swimming() {
                  @Override
                  public void swim() {
                      System.out.println("铁汁, 我们去游泳吧");
                  }
              }
           */
          swimming.swim();
      }
  }
  
  /*
      游泳接口
   */
  interface Swimming {
      void swim();
  }
  ```


## **小结**

**1.什么是内部类**

在一个类中定义一个类

**2.内部类的分类？**

   成员内部类和局部内部类

**3.如何使用成员内部类？**

格式:外部类名.内部类名 对象名=new 外部对象().new内部对象()

范例: Outer.Inner oi=new Outer().new Inter();

**4. 成员内部类的访问时有什么特点 ？** 

1. 内部类可以直接访问外部类的成员，包括私有
2. 外部类要访问内部类的非静态成员，必须创建对象

**5.私有成员内部类的访问特点？**

   只能在自己所在的外部类中创建对象访问

**6.如何创建静态成员内部类对象？**

​	外部类名.内部类名 对象名 = new 外部类名.内部类名();

**7.如何访问静态成员内部类中的静态方法？**

​	静态成员内部类中的静态方法：外部类名.内部类名.方法名();

**8.局部内部类的使用方式**

- 局部内部类，外界是无法直接使用，需要在方法内部创建对象并使用

**9.局部内部类的特点**

1. 局部内部类是在方法中定义的类
2. 该类可以直接访问外部类的成员，也可以访问方法内的局部变量

**10.什么是匿名内部类？**

​	没有显式的名字的内部类

**11 匿名内部类的前提**

 存在一个类或者接口，这里的类可以是具体类也可以是抽象类

**12 如何使用匿名内部类？**

格式：new 类名 ( ) {  重写方法 }    new  接口名 ( ) { 重写方法 }

**13. 匿名内部类的理解**

​    是一个继承了该类或者实现了该接口的子类匿名对象

**14.匿名内部类的应用场景？**

当发现某个方法需要，接口或抽象类的子类对象，我们就可以传递一个匿名内部类过去，来简化传统的代码

## Lambda表达式

### 2.1 Lambda表达式初体验和函数式编程思想

1.什么是函数式编程的思想？

在数学中，函数就是有输入量、输出量的一套计算方案，也就是“拿数据做操作”

函数式思想则尽量忽略面向对象的复杂语法：“强调做什么，而不是以什么形式去做”

2.面向对象思想和函数式编程思想对比

面向对象思想强调“必须通过对象的形式来做事情”

函数式思想则尽量忽略面向对象的复杂语法：“强调做什么，而不是以什么形式去做”



### 2.2Lambda表达式的格式说明和前提条件【重点】

1 Lambda表达式的前提条件

有一个接口，接口中只能有一个抽象方法

2 如何使用Lambda表达式？

- 组成Lambda表达式的三要素：

​       形式参数，箭头，代码块

​	  (形式参数) -> {代码块}

1. 形式参数：如果有多个参数，参数之间用逗号隔开；如果没有参数，留空即可
2. ->：由英文中画线和大于符号组成，固定写法。代表指向动作
3. 代码块：是我们具体要做的事情，也就是以前我们写的方法体内容

3 Lambda表达式练习

**示例代码**

```java
package com.itheima.test2;

public class TestLambda {
    /*
        Lambda表达式的使用前提
            1. 一个接口
            2. 接口中有且仅有一个抽象方法

        练习1：
            1. 编写一个接口（ShowHandler）
            2. 在该接口中存在一个抽象方法（show），该方法是无参数无返回值
            3. 在测试类（ShowHandlerDemo）中存在一个方法（useShowHandler）
                        方法的的参数是ShowHandler类型的
                        在方法内部调用了ShowHandler的show方法
     */
    public static void main(String[] args) {
        useShowHandler(new ShowHandler() {
            @Override
            public void show() {
                System.out.println("我是匿名内部类中的show方法");
            }
        });

        // Lambda实现
        useShowHandler( () -> System.out.println("我是Lambda中的show方法"));
    }

    public static void useShowHandler(ShowHandler showHandler){
        showHandler.show();
    }

}

interface ShowHandler {
    void show();
}
```

### 2.3  有参无返回值的Labmda表达式【应用】

```java
package com.itheima.test3;

public class StringHandlerDemo {
    /*
        1.首先存在一个接口（StringHandler）
        2.在该接口中存在一个抽象方法（printMessage），该方法是有参数无返回值
        3.在测试类（StringHandlerDemo）中存在一个方法（useStringHandler）
                方法的的参数是StringHandler类型的
                在方法内部调用了StringHandler的printMessage方法
     */
    public static void main(String[] args) {
        useStringHandler(new StringHandler() {
            @Override
            public void printMessage(String msg) {
                System.out.println("我是匿名内部类" + msg);
            }
        });

        // Lambda实现
        useStringHandler( msg -> System.out.println("我是Lambda表达式" + msg));
    }

    public static void useStringHandler(StringHandler stringHandler){
        stringHandler.printMessage("itheima");
    }
}

interface StringHandler {
    void printMessage(String msg);
}
```

### 2.4Labmda表达式-无参数有返回值【应用】

```java
package com.itheima.test4;
import java.util.Random;

public class RandomNumHandlerDemo {
    /*
        1. 首先存在一个接口（RandomNumHandler）
        2. 在该接口中存在一个抽象方法（getNumber），该方法是无参数但是有返回值
        3. 在测试类（RandomNumHandlerDemo）中存在一个方法（useRandomNumHandler）
                方法的的参数是RandomNumHandler类型的
                在方法内部调用了RandomNumHandler的getNumber方法
     */
    public static void main(String[] args) {
        useRandomNumHandler(new RandomNumHandler() {
            @Override
            public int getNumber() {
                Random r = new Random();
                int num = r.nextInt(10) + 1;
                return num;
            }
        });

        useRandomNumHandler( () -> {
                Random r = new Random();
                int num = r.nextInt(10) + 1;
                return num;
                // 注意: 如果lambda所操作的接口中的方法, 有返回值, 一定要通过return语句, 将结果返回
                // 否则会出现编译错误
        } );
    }

    public static void useRandomNumHandler(RandomNumHandler randomNumHandler){
        int result = randomNumHandler.getNumber();
        System.out.println(result);
    }
}

interface RandomNumHandler {
    int getNumber();
}
```

### 2.5Labmda表达式-带参数带返回值【应用】

```java
package com.itheima.test5;

public class CalculatorDemo {
    /*
        1. 首先存在一个接口（Calculator）
        2. 在该接口中存在一个抽象方法（calc），该方法是有参数也有返回值
        3. 在测试类（CalculatorDemo）中存在一个方法（useCalculator）
            方法的的参数是Calculator类型的
            在方法内部调用了Calculator的calc方法

     */
    public static void main(String[] args) {
        useCalculator(new Calculator() {
            @Override
            public int calc(int a, int b) {
                return a + b;
            }
        });

        useCalculator( ( a,  b) -> {
            return a + b;
        });
    }

    public static void useCalculator(Calculator calculator){
        int result = calculator.calc(10,20);
        System.out.println(result);
    }
}

interface Calculator {
    int calc(int a, int b);
}
```

### 2.6Lambda表达式的省略模式【应用】

1.省略的规则

- ​	参数类型可以省略。但是有多个参数的情况下，不能只省略一个
- ​	如果参数有且仅有一个，那么小括号可以省略
- ​	如果代码块的语句只有一条，可以省略大括号和分号，和return关键字

代码演示

```java
package com.itheima.test6;

public class Test6 {
  public static void main(String[] args) {
        /*useInter( (double a, double b) -> {
            return a + b;
        });*/

        useInter( (a,b) ->
                a + b
        );
    }

    public static void useInter(Inter i) {
        double result = i.method(12.3, 22.3);
        System.out.println(result);
    }

}

interface Inter {
    // 用于计算 a + b 的结果并返回
    double method(double a, double b);
}
```

### 2.7 Lambda表达式的应用场景

当某个方法的参数类型是一个接口或抽象类类型,并且接口或抽象类中只有一个抽象方法

### 2.8Lambda表达式和匿名内部类的区别

- 所需类型不同
  - 匿名内部类：可以是接口，也可以是抽象类，还可以是具体类
  - Lambda表达式：只能是接口
- 使用限制不同
  - 如果接口中有且仅有一个抽象方法，可以使用Lambda表达式，也可以使用匿名内部类
  - 如果接口中多于一个抽象方法，只能使用匿名内部类，而不能使用Lambda表达式
- 实现原理不同
  - 匿名内部类：编译之后，产生一个单独的.class字节码文件
  - Lambda表达式：编译之后，没有一个单独的.class字节码文件。对应的字节码会在运行的时候动态生成

## **小结**

**1.什么是函数式编程思想**

函数式思想则尽量忽略面向对象的复杂语法：“强调做什么，而不是以什么形式去做”

**2.如何使用Lambda表达式？**

- 组成Lambda表达式的三要素：

​       形式参数，箭头，代码块

​	  (形式参数) -> {代码块}

1. 形式参数：如果有多个参数，参数之间用逗号隔开；如果没有参数，留空即可
2. ->：由英文中画线和大于符号组成，固定写法。代表指向动作
3. 代码块：是我们具体要做的事情，也就是以前我们写的方法体内容

**3. Lambda表达式的前提条件**

有一个接口，接口中只能有一个抽象方法

**4.匿名内部类应用场景**

当某个方法的参数类型是一个接口或抽象类类型,并且接口或抽象类中只有一个抽象方法

**5.Lambda表达式和匿名内部类的区别**

- 所需类型不同
  - 匿名内部类：可以是接口，也可以是抽象类，还可以是具体类
  - Lambda表达式：只能是接口
- 使用限制不同
  - 如果接口中有且仅有一个抽象方法，可以使用Lambda表达式，也可以使用匿名内部类
  - 如果接口中多于一个抽象方法，只能使用匿名内部类，而不能使用Lambda表达式
- 实现原理不同
  - 匿名内部类：编译之后，产生一个单独的.class字节码文件
  - Lambda表达式：编译之后，没有一个单独的.class字节码文件。对应的字节码会在运行的时候动态生成







