---
title: 面向对象-继承
date: 2022-09-02 14:34:00 +0800
categories: [面向对象-继承]
tags: [后端]
pin: true
author: BruceZhou

toc: true
comments: true
typora-root-url: ../../youze12138.github.io
math: false
mermaid: truey
---

# 面向对象-继承

## 继承

### 1.2 继承概述

- 继承是面向对象三大特征之一。(封装，**继承**，多态)
- **可以使得子类具有父类的属性和方法，还可以在子类中重新定义，追加属性和方法。**



**继承的格式：**

- 格式：public class 子类名 **extends** 父类名 { }
- 范例：public class Zi **extends** Fu { }
- Fu：是父类，也被称为基类、超类
- Zi：是子类，也被称为派生类

**示例代码:**

```java
public class Fu {
    public void show() {
        System.out.println("show方法被调用");
    }
}
```

```java
public class Zi extends Fu {
    public void method() {
        System.out.println("method方法被调用");
    }
}
```

```java
//测试类
public class Demo {
    public static void main(String[] args) {
        //创建对象，调用方法
        Fu f = new Fu();
        f.show();

        Zi z = new Zi();
        z.method();
        z.show();
    }
}
```

**继承中子类的特点：**

- 子类可以有父类的内容
- 子类还可以有自己特有的内容

### 1.3 好处和弊端

**继承的好处：**

- 提高了代码的**复用性**(多个类相同的成员可以放到同一个类中)
- 提高了代码的**维护性**(如果方法的代码需要修改，修改一处即可)

**继承的弊端：**

- 继承让类与类之间产生了关系，类的耦合性增强了，当父类发生变化时子类实现也不得不跟着变化，削弱了子类的独立性



**什么时候使用继承：**

- 继承体现的关系：**is a**
- 假设法：我有两个类A和B，如果他们满足A是B的一种，或者B是A的一种，就说明他们存在继承关系，这个时候就可以考虑使用继承来体现，否则就不能滥用继承



### 1.4 继承中成员访问特点

#### 1.4.1 成员变量访问特点

**在子类方法中访问一个变量：**

- 子类局部范围找
- 子类成员范围找
- 父类成员范围找
- 如果都没有就报错(不考虑父亲的父亲…)

```java
public class Fu {
    //年龄
    public int age = 40;
}
```

```java
public class Zi extends Fu {
    //身高
    public int height = 175;

    //年龄
    public int age = 20;

    public void show() {
        int age = 30;
        System.out.println(age);
        System.out.println(height);
        //报错
//        System.out.println(weight);
    }
}
```

```java
//测试类
public class Demo {
    public static void main(String[] args) {
        //创建对象，调用方法
        Zi z = new Zi();
        z.show();
    }
}
```



#### 1.4.2 super关键字



**super** 关键字的用法和 **this** 关键字的用法相似

- **this：**代表调用该方法的对象(一般我们是在当前类中使用this，所以我们常说this代表本类对象的引用)
- **super**：代表父类存储空间的标识(可以理解为父类对象引用)

![1640591159377](/github/assets/blog_res/2022-09-02-JavaSE_advanced1.assets/1640591159377.png)



```java
public class Fu {
    public int age = 40;
}
```

```java
public class Zi extends Fu {
    public int age = 20;

    public void show() {
        int age = 30;
        System.out.println(age);
        //我要访问本类的成员变量age，怎么办呢？
        System.out.println(this.age);
        //我要访问父类的成员变量age，怎么办呢？
        System.out.println(super.age);
    }
}
```

```java
//测试类
public class Demo {
    public static void main(String[] args) {
        //创建对象，调用方法
        Zi z = new Zi();
        z.show();
    }
}
```



#### 1.4.3 构造方法访问特点

- 子类中所有的构造方法默认都会访问父类中无参的构造方法

- 因为子类会继承父类中的数据，可能还会使用父类的数据。所以，子类初始化之前，一定要先完成父类数据的初始化

- 每一个子类构造方法的第一条语句默认都是：**super()**

- 如果父类没有无参构造方法：

  ① 通过使用super关键字去显示的调用父类的带参构造方法

  ② 在父类中自己提供一个无参构造方法

**推荐：自己给出无参构造方法**



#### 1.4.4 成员方法访问特点

**通过子类对象访问一个方法：**

- 子类成员范围找
- 父类成员范围找
- 如果都没有就报错(不考虑父亲的父亲…)



### 1.5 方法重写

**什么是方法重写**

- 子类中出现了和父类中一模一样的方法声明(返回值类型,方法名,参数列表)

**方法重写的应用场景：**如果说父类满足不了子类当前的需求了,那么就应该使用重写

- 当子类需要父类的功能，而功能主体子类有自己特有内容时，可以重写父类中的方法，这样，即沿袭了父类的功能，又定义了子类特有的内容
- 练习：手机类和新手机类

```java
/*
    手机类
 */
public class Phone {
    public void call(String name) {
        System.out.println("给" + name + "打电话");
    }
}
```

```java
/*
    新手机
 */
public class NewPhone extends Phone {

    /*
    public void call(String name) {
        System.out.println("开启视频功能");
//        System.out.println("给" + name + "打电话");
        super.call(name);
    }
    */

    @Override
    public void call(String name) {
        System.out.println("开启视频功能");
//        System.out.println("给" + name + "打电话");
        super.call(name);
    }

}
```

```java
/*
    测试类
 */
public class PhoneDemo {
    public static void main(String[] args) {
        //创建对象，调用方法
        Phone p = new Phone();
        p.call("林青霞");
        System.out.println("--------");

        NewPhone np = new NewPhone();
        np.call("林青霞");
    }
}
```



### 1.6 继承的注意事项

- Java中类只支持单继承，不支持多继承
- Java中类支持多层继承

```java
public class Granddad {

    public void drink() {
        System.out.println("爷爷爱喝酒");
    }

}
```

```java
public class Father extends Granddad {

    public void smoke() {
        System.out.println("爸爸爱抽烟");
    }

}
```

```java
public class Mother {

    public void dance() {
        System.out.println("妈妈爱跳舞");
    }

}
```

```java
/*
public class Son extends Father, Mother {

}
*/

public class Son extends Father {

}
```



![1640593511560](/github/assets/blog_res/2022-09-02-JavaSE_advanced1.assets/1640593511560.png)

### 1.7 继承案例

#### 1.7.1 老师和学生

需求：定义老师类和学生类，然后写代码测试；最后找到老师类和学生类当中的共性内容，抽取出一个父类，用继承的方式改写代码，并进行测试

看完需求后，我们先简单的说一下思路：

**思路：**

①定义老师类(姓名，年龄，教书())

②定义学生类(姓名，年龄，学习())

③定义测试类，写代码测试

```java
/*
    老师类
 */
public class Teacher {
    private String name;
    private int age;

    public Teacher() {
    }

    public Teacher(String name, int age) {
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

    public void teach() {
        System.out.println("用爱成就每一位学员");
    }
}
```

```java
/*
    学生类
 */
public class Student {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
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

    public void study() {
        System.out.println("好好学习天天向上");
    }
}
```

```java
/*
    测试类
 */
public class Demo {
    public static void main(String[] args) {
        //创建老师类对象进行测试
        Teacher t1 = new Teacher();
        t1.setName("林青霞");
        t1.setAge(30);
        System.out.println(t1.getName() + "," + t1.getAge());
        t1.teach();

        Teacher t2 = new Teacher("风清扬", 33);
        System.out.println(t2.getName() + "," + t2.getAge());
        t2.teach();

        //学生类的测试，留给大家自己练习
    }
}
```

④共性抽取父类，定义人类(姓名，年龄)

⑤定义老师类，继承人类，并给出自己特有方法：教书()

⑥定义学生类，继承人类，并给出自己特有方法：学习()

⑦定义测试类，写代码测试

```java
/*
    人类
 */
public class Person {
    private String name;
    private int age;

    public Person() {
    }

    public Person(String name, int age) {
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
}
```

```java
/*
    老师类
 */
public class Teacher extends Person {

    public Teacher() {
    }

    public Teacher(String name, int age) {
//        this.name = name;
//        this.age = age;
        super(name, age);
    }

    public void teach() {
        System.out.println("用爱成就每一位学员");
    }

}

```

```java
/*
    测试类
 */
public class PersonDemo {
    public static void main(String[] args) {
        //创建老师类对象并进行测试
        Teacher t1 = new Teacher();
        t1.setName("林青霞");
        t1.setAge(33);
        System.out.println(t1.getName() + "," + t1.getAge());
        t1.teach();


        Teacher t2 = new Teacher("风清扬", 36);
        System.out.println(t2.getName() + "," + t2.getAge());
        t2.teach();

        //学生类的定义和测试，留给大家自学练习
    }
}
```



#### 1.7.2 项目经理和程序员

需求：请使用继承的思想设计出项目经理类和程序员类，并进行测试。

看完这个需求后，我们首先得知道项目经理和程序员都有哪些属性和行为，这样我们才能够设计这两个类，通过这两个类的共性特性，设计出一个父类。

这里呢，我们给出项目经理和程序员的成员变量和成员方法：

**项目经理：**

​	成员变量：工号，姓名，工资，奖金

​	成员方法：工作

**程序员：**

​	成员变量：工号，姓名，工资

​	成员方法：工作

通过分析，我们可以找到它们的共性内容，设计出一个父类：员工类

**员工类：**

​	成员变量：工号，姓名，工资

​	成员方法：工作

程序员类继承自员工类，没有新的成员需要添加。

而项目经理类继承自员工类，需要添加一个成员变量：奖金。

下面给出实现思路：

**思路：**

①定义员工类(工号，姓名，工资，工作())

②定义项目经理类，继承自员工类，添加一个新的成员变量奖金

③定义程序员类，不需要添加新的成员

④定义测试类，进行测试

分析完毕后，我们到IDEA中去实现一下：

```java
/*
    员工类
 */
public class Employee {
    //工号
    private String id;
    //姓名
    private String name;
    //薪水
    private double salary;

    public Employee() {
    }

    public Employee(String id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public void work() {
        System.out.println("员工需要工作");
    }
}
```

```java
/*
    项目经理类
 */
public class Manager extends Employee {
    //奖金
    private double bonus;

    public Manager() {
    }

    public Manager(String id, String name, double salary, double bonus) {
        super(id, name, salary);
        this.bonus = bonus;
    }

    public double getBonus() {
        return bonus;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    @Override
    public void work() {
        System.out.println("项目经理和客户谈需求");
    }
}
```

```java
/*
    程序员类
 */
public class Programmer extends Employee {

    public Programmer() {
    }

    public Programmer(String id, String name, double salary) {
        super(id, name, salary);
    }

    @Override
    public void work() {
        System.out.println("程序员根据需求编写代码");
    }
}
```

```java
/*
    测试类
 */
public class EmployeeDemo {
    public static void main(String[] args) {
        //创建项目经理类对象，并进行测试
        Manager m1 = new Manager();
        m1.setId("itheima001");
        m1.setName("林青霞");
        m1.setSalary(10000.00);
        m1.setBonus(20000.00);
        System.out.println(m1.getId() + "," + m1.getName() + "," + m1.getSalary() + "," + m1.getBonus());

        Manager m2 = new Manager("itheima001", "林青霞", 10000.00, 20000.00);
        System.out.println(m2.getId() + "," + m2.getName() + "," + m2.getSalary() + "," + m2.getBonus());
        System.out.println("-------------------------------");

        //创建程序员类对象，并进行测试
        Programmer p1 = new Programmer();
        p1.setId("itheima520");
        p1.setName("风清扬");
        p1.setSalary(20000.00);
        System.out.println(p1.getId() + "," + p1.getName() + "," + p1.getSalary());

        Programmer p2 = new Programmer("itheima520", "风清扬", 20000.00);
        System.out.println(p2.getId() + "," + p2.getName() + "," + p2.getSalary());
    }
}
```



## 修饰符

### 2.1 权限修饰符

**修饰符的分类：**

- 权限修饰符
- 状态修饰符

```java
package com.itheima_01;

public class Fu {
    private void show1() {
        System.out.println("private");
    }

    void show2() {
        System.out.println("默认");
    }

    protected void show3() {
        System.out.println("protected");
    }

    public void show4() {
        System.out.println("public");
    }

    public static void main(String[] args) {
        //创建Fu的对象，测试看有哪些方法可以使用
        Fu f = new Fu();
        f.show1();
        f.show2();
        f.show3();
        f.show4();
    }

}
```

```java
package com.itheima_01;

public class Zi extends Fu {

    public static void main(String[] args) {
        //创建Zi的对象，测试看有哪些方法可以使用
        Zi z = new Zi();
        z.show2();
        z.show3();
        z.show4();
    }

}
```

```java
package com.itheima_01;

public class Demo {

    public static void main(String[] args) {
        //创建Fu的对象，测试看有哪些方法可以使用
        Fu f = new Fu();
        f.show2();
        f.show3();
        f.show4();
    }

}
```

```java
package com.itheima_02;

import com.itheima_01.Fu;

public class Zi extends Fu {

    public static void main(String[] args) {
        //创建Zi的对象，测试看有哪些方法可以使用
        Zi z = new Zi();
        z.show3();
        z.show4();
    }

}
```

```java
package com.itheima_02;

import com.itheima_01.Fu;

public class Demo {

    public static void main(String[] args) {
        //创建Fu的对象，测试看有哪些方法可以使用
        Fu f = new Fu();
        f.show4();
    }

}
```

总结：

![1640609223048](/github/assets/blog_res/2022-09-02-JavaSE_advanced1.assets/1640609223048.png)

public（公众） > protected > 默认 > private（私有）

### 2.2 final

#### 2.2.1 final关键字

**状态修饰符的分类：**

- **final**(最终态) 
- **static**(静态)

- **final** 关键字是最终的意思，可以修饰成员方法，成员变量，类

**final** 修饰的特点

- 修饰方法：表明该方法是最终方法，**不能被重写**
- 修饰变量：表明该变量是常量，**不能再次被赋值**
- 修饰类：表明该类是最终类，**不能被继承**



#### 2.2.2 final修饰局部变量

**final修饰局部变量：**

- 变量是基本类型：final 修饰指的是基本类型的**数据值**不能发生改变

- 变量是引用类型：final 修饰指的是引用类型的**地址值**不能发生改变，但是地址里面的内容是可以发生改变的

  

### 2.3 static

#### 2.3.1 static关键字

- **static**关键字是静态的意思，可以修饰成员方法，成员变量

**static 修饰的特点**

- 被类的所有对象共享，这也是我们判断是否使用静态关键字的条件

- 可以通过类名调用，当然，也可以通过对象名调用，**推荐使用类名调用**

  

#### 2.3.2 static访问特点

**非静态的成员方法**

- 能访问静态的成员变量
- 能访问非静态的成员变量
- 能访问静态的成员方法
- 能访问非静态的成员方法

**静态的成员方法**

- 能访问静态的成员变量
- 能访问静态的成员方法

**总结成一句话就是：静态成员方法只能访问静态成员**



#### 2.3.3 main方法详细说明

main方法的声明：

public static void main(String[] args) { }

- public   被jvm调用，访问权限足够大
- static   被jvm调用，不用创建对象，直接类名访问
- void   被jvm调用，不需要给jvm返回值
- main   一个通用的名称，虽然不是关键字，但是被jvm识别
- String[] args   以前用于接收键盘录入的

通过args接收数据，参数的配置：

第一步：选择HelloWorld下面的Edit Configurations...

![1640610960632](/../github/assets/blog_res/2022-09-02-JavaSE_advanced1.assets/1640610960632.png)

第二步：配置参数，数据之间用空格隔开

![1640611036250](/../github/assets/blog_res/2022-09-02-JavaSE_advanced1.assets/1640611036250.png)

但极少人用了。



#### 2.3.4 static应用：工具类

static的应用有很多，这里我们讲解其中的一个，就是static关键字在工具类中的使用。

```java
/*
    工具类：
        构造方法私有
        成员静态修饰
 */
public class ArrayTool {

    //构造方法私有
    private ArrayTool() {
    }

    public static int getMax(int[] arr) {
        int max = arr[0];

        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }

        return max;
    }
}
```

```java
public class ArrayDemo {
    public static void main(String[] args) {
        //定义一个数组
        int[] arr = {12, 56, 78, 93, 40};

        //需求：获取数组中最大值
//        int max = arr[0];
//
//        for (int i = 1; i < arr.length; i++) {
//            if (arr[i] > max) {
//                max = arr[i];
//            }
//        }

        //创建对象调用
//        ArrayTool at = new ArrayTool();
//        int max = at.getMax(arr);

        //调用类的静态方法
        int max = ArrayTool.getMax(arr);

        System.out.println("数组中最大值是：" + max);
    }
}
```

**工具类的特点：**

- 构造方法私有
- 成员用static修饰



#### 2.3.5 Math类使用(自学)

- Math类是：数学工具类，包含对数学运算的方法
- 帮助文档中，没有看到构造方法，因为成员都用static修饰了，可以通过类名直接访问

示例：

```java
/*
    Math类的使用
 */
public class MathDemo {
    public static void main(String[] args) {
        //public static int abs(int a):返回int值的绝对值
        System.out.println(Math.abs(10));
        System.out.println(Math.abs(-10));
        System.out.println("-----------");

        //public static int max(int a, int b):返回两个int值中较大的int
        System.out.println(Math.max(10, 20));
        System.out.println("-----------");

        //public static double pow(double a, double b):返回第一个参数的值，该值是第二个参数的幂
        System.out.println(Math.pow(2, 3));
        System.out.println("-----------");

        //public static long round(double a):返回与参数最接近的long
        System.out.println(Math.round(15.4));
        System.out.println(Math.round(15.5));
    }
}
```
