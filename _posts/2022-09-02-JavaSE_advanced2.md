---
title: 面向对象-多态
date: 2022-09-02 14:34:00 +0800
categories: [面向对象-多态]
tags: [后端]
pin: true
author: BruceZhou

toc: true
comments: true
typora-root-url: ../../youze12138.github.io
math: false
mermaid: truey
---

# 面向对象-多态

## 多态

### 1.1 多态概述

- **多态：**指的是同一个对象，在不同时刻表现出来的多种形态

- 我们可以说猫是猫：**猫** **cat = new** **猫**();
- 我们也可以说猫是动物：**动物** **animal = new** **猫**();
- 这里猫在不同的时刻表现出来了多种形态，这就是多态

了解了什么是多态后，我们再来说一下多态的前提和体现：

- 有继承/实现关系
- 有方法重写
- 有父类引用指向子类对象

```java
public class Animal {

    public void eat() {
        System.out.println("动物吃东西");
    }

}
```

```java
public class Cat extends Animal {

    @Override
    public void eat() {
        System.out.println("猫吃鱼");
    }

}
```

```java
/*
    多态的前提和体现
        有继承/实现关系
        有方法重写
        有父类引用指向子类对象
 */
public class AnimalDemo {
    public static void main(String[] args) {
        //有父类引用指向子类对象
        Animal a = new Cat();
    }
}
```

### 1.2 多态中成员访问特点

**成员变量**：编译看左边，执行看左边

**成员方法**：编译看左边，执行看右边

为什么成员变量和成员方法的访问不一样呢？

因为成员方法有重写，而成员变量没有

### 1.3 多态的好处和弊端

**多态的好处：**提高了程序的扩展性

具体体现：定义方法的时候，使用父类型作为参数，将来在使用的时候，使用具体的子类型参与操作

**多态的弊端：**不能使用子类的特有功能

### 1.4 多态中的转型

多态的弊端是不能访问子类的特有功能，而通过转型就可以访问子类特有功能了。

多态中的转型分为如下两种情况：

- 向上转型
  - 从子到父
  - 父类引用指向子类对象
- 向下转型
  - 从父到子
  - 父类引用转为子类对象
  - 虽然我们通过向下转型解决了多态中的访问弊端，但是一般来说，我们使用多态的时候，主要还是使用父类中定义的通用功能。



### 1.5 多态转型内存图解

![1640769395233](/github/assets/blog_res/2022-09-02-JavaSE_advanced2.assets/1640769395233.png)



### 1.6 案例：猫和狗(多态版)

需求：请采用多态的思想实现猫和狗的案例，并在测试类中进行测试

**思路：**

① 定义动物类(Animal)

- 成员变量：姓名，年龄
- 构造方法：无参，带参
- 成员方法：get/set，吃(){}

② 定义猫类(Cat)，继承动物类，重写吃的方法

- 构造方法：无参，带参
- 成员方法：吃(){}

③ 定义狗类(Dog)，继承动物类，重写吃的方法

- 构造方法：无参，带参
- 成员方法：吃(){}

④ 定义测试类(AnimalDemo)，写代码测试

实现代码:

```java
public class Animal {
    private String name;
    private int age;

    public Animal() {
    }

    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void eat() {
        System.out.println("动物吃东西");
    }
}
```

```java
public class Cat extends Animal {

    public Cat() {
    }

    public Cat(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println("猫吃鱼");
    }
}
```

```java
public class Dog extends Animal {

    public Dog() {
    }

    public Dog(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println("狗吃骨头");
    }
}
```

```java
/*
    测试类
 */
public class AnimalDemo {
    public static void main(String[] args) {
        //按照多态的方式创建对象并进行测试
        Animal a = new Cat();
        a.setName("加菲");
        a.setAge(5);
        System.out.println(a.getName() + "," + a.getAge());
        a.eat();

        a = new Cat("加菲", 5);
        System.out.println(a.getName() + "," + a.getAge());
        a.eat();

    }
}
```

创建狗类的对象进行测试同上。



## 抽象类

### 2.1 抽象类概述

- 在Java中，一个**没有方法体**的方法应该定义为**抽象方法**，而类中如果有**抽象方法**，该类必须定义为**抽象类**

### 2.2 抽象类特点

**抽象类的特点：**

- 抽象类和抽象方法必须使用 **abstract** 关键字修饰

  - public **abstract** class 类名 {}
  - public **abstract** void eat();

- 抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类

- 抽象类不能实例化

  - 抽象类如何实例化呢？参照多态的方式，通过子类对象实例化，这叫抽象类多态

- 抽象类的子类

  - 要么重写抽象类中的所有抽象方法

  - 要么是抽象类

    抽象类和普通类的区别: 普通类所拥有的的,抽象类都有,而且还多了一个抽象方法

### 2.3 抽象类的成员特点

**抽象类的成员特点：**

- 成员变量
  - 可以是变量
  - 也可以是常量
- 构造方法
  - 有构造方法，但是不能实例化
  - 那么，构造方法的作用是什么呢？用于子类访问父类数据的初始化
- 成员方法
  - 可以有抽象方法：限定子类必须完成某些动作
  - 也可以有非抽象方法：提高代码复用性

### 2.4 案例：猫和狗(抽象类版)

需求：请采用抽象类的思想实现猫和狗的案例，并在测试类中进行测试

**思路：**

① 定义动物类(Animal)

- 成员变量：姓名，年龄
- 构造方法：无参，带参
- 成员方法：get/set，吃();

② 定义猫类(Cat)，继承动物类，重写吃的方法

- 构造方法：无参，带参
- 成员方法：吃(){…}

③ 定义狗类(Dog)，继承动物类，重写吃的方法

- 构造方法：无参，带参
- 成员方法：吃(){…}

④ 定义测试类(AnimalDemo)，写代码测试

```java
public abstract class Animal {
    private String name;
    private int age;

    public Animal() {
    }

    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public abstract void eat();
}
```

```java
public class Cat extends Animal {

    public Cat() {
    }

    public Cat(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println("猫吃鱼");
    }
}
```

```java
public class Dog extends Animal {

    public Dog() {
    }

    public Dog(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println("狗吃骨头");
    }
}
```

```java
/*
    测试类
 */
public class AnimalDemo {
    public static void main(String[] args) {
        //创建对象，按照多态的方式
        Animal a = new Cat();
        a.setName("加菲");
        a.setAge(5);
        System.out.println(a.getName()+","+a.getAge());
        a.eat();
        System.out.println("--------");

        a = new Cat("加菲",5);
        System.out.println(a.getName()+","+a.getAge());
        a.eat();
    }
}
```

## 接口

### 3.1 接口概述

接口很好理解，举例子这是我们生活当中的，其实与计算机相关的接口。

![1640785329296](/../github/assets/blog_res/2022-09-02-JavaSE_advanced2.assets/1640785329296.png)

键盘的USB插口、U盘的USB插口、鼠标的USB插口为什么是一摸一样的？

因为电脑只提供了USB插口这种方式，如果说键盘的接口是Type-C的，那它就用不来哦。

最后呢，我们来说一下：

- 接口就是一种**公共的规范标准**，只要符合规范标准，大家都可以通用
- Java中的接口更多的体现在**对行为的抽象**



### 3.2 接口特点

**接口的特点：**

- 接口用关键字interface修饰
  - public **interface** 接口名 {} 
- 类实现接口用implements表示
  - public class 类名 **implements** 接口名 {}
- 接口不能实例化
  - 接口如何实例化呢？参照多态的方式，通过实现类对象实例化，这叫接口多态
  - 多态的形式：具体类多态，**抽象类多态，接口多态**
  - 多态的前提：有继承或者实现关系；有方法重写；有父(类/接口)引用指向(子/实现)类对象
- 接口的实现类
  - 要么重写接口中的所有抽象方法
  - 要么是抽象类



### 3.3 接口的成员特点

**接口的成员特点：**

- 成员变量
  - 只能是常量
  - 默认修饰符：**public static final**
- 构造方法
  - 没有，因为接口主要是扩展功能的，而没有具体存在
  - 一个类如果没有父类，默认继承自Object类
- 成员方法
  - 只能是抽象方法
  - 默认修饰符：**public abstract**



### 3.4 类和接口的关系

- 类和类的关系
  - 继承关系，只能单继承，但是可以多层继承
- 类和接口的关系
  - 实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时实现多个接口
- 接口和接口的关系
  - 继承关系，可以单继承，也可以多继承



### 3.5 抽象类和接口的区别

- 成员区别
  - 抽象类   变量,常量；有构造方法；有抽象方法,也有非抽象方法
  - 接口   常量；抽象方法
- 关系区别
  - 类与类   继承，单继承
  - 类与接口   实现，可以单实现，也可以多实现
  - 接口与接口   继承，单继承，多继承
- 设计理念区别
  - 抽象类   对类抽象，包括属性、行为
  - 接口   对行为抽象，主要是行为

### 3.6 案例：木门和电动报警门

需求：请采用面向对象的思想实现木门和电动报警门的案例，并在测试类中进行测试

分析：

![1641276207662](/../github/assets/blog_res/2022-09-02-JavaSE_advanced2.assets/1641276207662.png)

**分析：**

①木门

- 成员变量：宽，高，品牌
- 成员方法：开门，关门

②电动报警门：

- 成员变量：宽，高，品牌
- 成员方法：开门，关门，报警

**思路：**

①定义报警 (Alarm)接口

- 成员方法：报警

②定义门 (Door)抽象类

- 成员变量：宽，高，品牌
- 构造方法：无参，带参
- 成员方法：get/set方法，开门，关门

③定义木门类(WoodDoor)，继承门类

- 构造方法：无参，带参
- 成员方法：开门，关门

④定义电动报警门类(ElectricAlarmDoor),继承门类,实现报警接口

- 构造方法：无参，带参
- 成员方法：开门，关门，报警

⑤定义测试类(DoorDemo)，创建对象进行测试

实现代码：

```java
/*
    报警接口
 */
public interface Alarm {
    void alarm();
}
```

```java
/*
    抽象门类
 */
public abstract class Door {
    //宽
    private double width;
    //高
    private double height;
    //品牌
    private String brand;

    public Door() {
    }

    public Door(double width, double height, String brand) {
        this.width = width;
        this.height = height;
        this.brand = brand;
    }

    public double getWidth() {
        return width;
    }

    public void setWidth(double width) {
        this.width = width;
    }

    public double getHeight() {
        return height;
    }

    public void setHeight(double height) {
        this.height = height;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    //开门
    public abstract void open();

    //关门
    public abstract void close();
}
```

```java
/*
    木门
 */
public class WoodDoor extends Door {

    public WoodDoor() {
    }

    public WoodDoor(double width, double height, String brand) {
        super(width, height, brand);
    }

    @Override
    public void open() {
        System.out.println("手动开门");
    }

    @Override
    public void close() {
        System.out.println("手动关门");
    }
}
```

```java
/*
    电动报警门
 */
public class ElectricAlarmDoor extends Door implements Alarm {
    public ElectricAlarmDoor() {
    }

    public ElectricAlarmDoor(double width, double height, String brand) {
        super(width, height, brand);
    }

    @Override
    public void open() {
        System.out.println("自动开门");
    }

    @Override
    public void close() {
        System.out.println("自动关门");
    }


    @Override
    public void alarm() {
        System.out.println("具有报警功能");
    }
}
```

```java
/*
    测试类
 */
public class DoorDemo {
    public static void main(String[] args) {
        //木门
        WoodDoor wd = new WoodDoor();
        wd.open();
        wd.close();
//        wd.alarm();
        System.out.println("--------");

        //电动报警门
        ElectricAlarmDoor ed = new ElectricAlarmDoor();
        ed.open();
        ed.close();
        ed.alarm();
        System.out.println("--------");

        //多态用法
        Door d = new WoodDoor();
        d.open();
        d.close();
        System.out.println("--------");

        d = new ElectricAlarmDoor();
        d.open();
        d.close();
//        d.alarm();
        System.out.println("--------");

        Alarm a = new ElectricAlarmDoor();
//        a.open();
//        a.close();
        a.alarm();
    }
}
```

### 3.7 接口新增的方法

接口组成：

- 常量
  - public static final
- 抽象方法
  - public abstract
- 默认方法(Java 8)
- 静态方法(Java 8)
- 私有方法(Java 9)

但是呢，在Java 8 以后，我们可以在接口中添加默认方法和静态方法了。在Java 9以后，我们可以在接口中添加私有方法了。

这里新增的3类方法我们自己在开发中很少使用，通常是Java源码中涉及到，对我们来说，能够识别语法，知道调用关系即可。

先来看第一个**默认方法**：

**接口中默认方法的定义格式：**

- 格式：public **default** 返回值类型 方法名(参数列表) {   }
- 范例：public **default** void show1() {   }

**接口中默认方法的注意事项：**

- public可以省略，default不能省略



再来看第二个**静态方法**：

**接口中静态方法的定义格式：**

- 格式：public **static** 返回值类型 方法名(参数列表) {   }
- 范例：public **static** void show2() {   }

**接口中静态方法的注意事项：**

- 静态方法只能通过接口名调用，不能通过实现类名或者对象名调用

- public可以省略，static不能省略



最后来看第三个**私有方法**：

**接口中私有方法的定义格式：**

- 格式1：**private** 返回值类型 方法名(参数列表) {   }
- 范例1：**private** void show3() {   }
- 格式2：**private** static 返回值类型 方法名(参数列表) {   }
- 范例2：**private** static void show4() {   }

**接口中私有方法的注意事项：**

- 默认方法可以调用私有的静态方法和非静态方法
- 静态方法只能调用私有的静态方法







