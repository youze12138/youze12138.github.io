---
title: 面向对象-异常
date: 2022-09-02 14:34:00 +0800
categories: [面向对象-知识点3]
tags: [后端]
pin: true
author: BruceZhou

toc: true
comments: true
typora-root-url: ../../youze12138.github.io
math: false
mermaid: truey
---

# 面向对象-知识点3

## 4.异常

### 4.1 异常的体系结构和分类

1.什么是异常？

异常就是程序出现了不正常的情况

**注意：**语法错误不算在异常体系中

2.异常的体系结构

![01_](/github/assets/blog_res/2022-09-02-JavaSE_advanced5.assets/01.png)

  ```java
//除RuntimeException之外的异常
public class ExceptionDemo1 {
    public static void main(String[] args)  {
//        int [] arr = {1,2,3,4,5};
//        System.out.println(arr[10]);//ArrayIndexOutOfBoundsException


//        String s = null;
//        System.out.println(s.equals("嘿嘿"));//NullPointerException

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日");
        sdf.parse("2048-1月1日");//ParseException
    }
}
  ```

 3.编译时异常和运行时异常的区别

- 编译时异常

  - 都是Exception类及其子类
  - 必须显式处理(手动处理)，否则程序就会发生错误，无法通过编译

- 运行时异常

  - 都是RuntimeException类及其子类
  - 无需显式处理(手动处理)，也可以和编译时异常一样处理

- 图示

  ![02_](/github/assets/blog_res/2022-09-02-JavaSE_advanced5.assets/02.png)

### 4.2 JVM默认处理异常的方式

1.如果程序出现了问题，我们没有做任何处理，最终JVM 会做默认的处理，处理方式有如下两个步骤：

- 把异常的名称，错误原因及异常出现的位置等信息输出在了控制台

- 程序停止执行

  ![1595944550721](/github/assets/blog_res/2022-09-02-JavaSE_advanced5.assets/1595944550721.png)

```java
public class ExceptionDemo2 {
    public static void main(String[] args){
        //思考:控制台为什么会有这样的红色字体呢? 是谁打印的?
        int [] arr = {1,2,3,4,5};
        System.out.println(arr[10]);//当代码出现了异常,那么就在这里创建了一个异常对象.
                                    //new ArrayIndexOutOfBoundsException();
                                    //首先会看,程序中有没有自己处理异常的代码.
                                    //如果没有,交给本方法的调用者处理.
                                    //最终这个异常会交给虚拟机默认处理.
                                    //JVM默认处理异常做了哪几件事情:
                                    //1,将异常信息以红色字体展示在控制台上.
                                    //2,停止程序运行. --- 哪里出现了异常,那么程序就在哪里停止,下面的代码不执行了.
        System.out.println("嘿嘿嘿,我最帅");



    }
}
```



### 4.3throws方式处理异常

1.定义格式  声明异常->说明一下有异常

```java
public void 方法() throws 异常类名 {
    
}
```

示例代码

```java
public class ExceptionDemo6 {
    public static void main(String[] args) throws ParseException {
        method1(); //此时调用者也没有处理.还是会交给虚拟机处理.
        method2(); //还是继续交给调用者处理.而main方法的调用者是虚拟机还是会采取虚拟机默认处理异常的方法.
    }

    //告诉调用者,你调用我,有可能会出现这样的异常哦.
    //如果方法中没有出现异常,那么正常执行
    //如果方法中真的出现了异常,其实也是将这个异常交给了调用者处理.
    private static void method1() /*throws NullPointerException*/ {
        int [] arr = null;
        for (int i = 0; i < arr.length; i++) {//出现的空指针异常,还是由虚拟机创建出来的.
            System.out.println(arr[i]);
        }
    }

    //告诉调用者,你调用我,有可能会出现这样的异常哦.
    //如果方法中没有出现异常,那么正常执行
    //如果方法中真的出现了异常,其实也是将这个异常交给了调用者处理.
    private static void method2() throws ParseException {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日");
        sdf.parse("2048-10月10日");
    }
}
```

### 4.4 throws方式处理异常-注意事项

**简单来说:**编译时的异常，必须声明，谁调用谁处理，最后让jvm来处理，运行时异常可以不声明

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;

public class ExceptionDemo6 {
    public static void main(String[] args) throws ParseException {
        method1(); //此时调用者也没有处理.还是会交给虚拟机处理.
        method2(); //还是继续交给调用者处理.而main方法的调用者是虚拟机还是会采取虚拟机默认处理异常的方法.
    }

    //告诉调用者,你调用我,有可能会出现这样的异常哦.
    //如果方法中没有出现异常,那么正常执行
    //如果方法中真的出现了异常,其实也是将这个异常交给了调用者处理.
    //如果声明的异常是一个运行时异常,那么声明的代码可以省略
    private static void method1() /*throws NullPointerException*/ {
        int [] arr = null;
        for (int i = 0; i < arr.length; i++) {//出现的空指针异常,还是由虚拟机创建出来的.
            System.out.println(arr[i]);
        }
    }

    //告诉调用者,你调用我,有可能会出现这样的异常哦.
    //如果方法中没有出现异常,那么正常执行
    //如果方法中真的出现了异常,其实也是将这个异常交给了调用者处理.
    //如果声明的异常是一个编译时异常,那么声明的代码必须要手动写出.
    private static void method2() throws ParseException {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日");
        sdf.parse("2048-10月10日");
    }
}

```

### 4.5 throw抛出异常

  1.格式

​	throw new 异常();

  2.注意

​	这个格式是在**方法内**的，表示当前代码**手动抛出**一个异常，下面的代码无法再执行了

3.抛出处理异常的意义

   1.在方法中,当传递的参数有误时,没有继续运行的必要了，采取抛出处理,表示该方法结束

2. 告诉调用者方法中出现了问题

4.throws和throw的区别

| throws                                         | throw                                |
| ---------------------------------------------- | ------------------------------------ |
| 用在方法声明后面，跟的是异常类名               | 用在方法体内，跟的是异常对象名       |
| 表示声明异常，调用该方法有可能会出现这样的异常 | 表示手动抛出异常对象(百分百抛出异常) |
| 可以声明多个异常                               | 只能有一个                           |

示例代码

```java
public class ExceptionDemo7 {
    public static void main(String[] args) {
        System.out.println("家里有一个貌美如花的老婆");
      System.out.println("还有一个当官的兄弟");
        System.out.println("自己还有一个买卖");
        System.out.println("这样的生活你要不要?");
        throw new RuntimeException(); //当代码执行到这里,就创建一个异常对象
                                    //该异常创建之后,暂时没有手动处理.抛给了调用者处理
                                    //下面的代码不会再执行了.
        //System.out.println("武大郎的标准生活");
    }
}
```

```java
  public class ExceptionDemo8 {
      public static void main(String[] args) {
          //int [] arr = {1,2,3,4,5};
          int [] arr = null;
          printArr(arr);//就会 接收到一个异常.
                          //我们还需要自己处理一下异常.
      }
 private static void printArr(int[] arr) {
      if(arr == null){
          //调用者知道成功打印了吗?
          //System.out.println("参数不能为null");
          throw new NullPointerException(); //当参数为null的时候
                                              //手动创建了一个异常对象,抛给了调用者.
      }else{
          for (int i = 0; i < arr.length; i++) {
              System.out.println(arr[i]);
          }
      }
  }
}
```


### 4.6 try-catch自己处理异常

- 定义格式

  ```java
  try {
  	可能出现异常的代码;
  } catch(异常类名 变量名) {
  	异常的处理代码;
  }
  ```

- 执行流程

  - 程序从 try 里面的代码开始执行
  - 出现异常，就会跳转到对应的 catch 里面去执行
  - 执行完毕之后，程序还可以继续往下执行

- 示例代码

  ```java
  public class ExceptionDemo9 {
      public static void main(String[] args) {
  
          //好处:为了能让代码继续往下运行.
          int [] arr = null;
          try{
              //有肯能发现异常的代码
              printArr(arr);
          }catch (NullPointerException e){
              //如果出现了这样的异常,那么我们进行的操作
              System.out.println("参数不能为null");
          }
  
  
          System.out.println("嘿嘿嘿,我最帅!!!");
  
      }
  
      private static void printArr(int[] arr) {
          if(arr == null){
              throw new NullPointerException();
          }else{
              for (int i = 0; i < arr.length; i++) {
                  System.out.println(arr[i]);
              }
          }
      }
  }
  ```

  ### 4.7 try-catch常见问题

  1. 如果 try 中没有遇到问题，怎么执行？

     会把try中所有的代码全部执行完毕,不会执行catch里面的代码

  2. 如果 try 中遇到了问题，那么 try 下面的代码还会执行吗？

     那么直接跳转到对应的catch语句中,try下面的代码就不会再执行了
     当catch里面的语句全部执行完毕,表示整个体系全部执行完全,继续执行下面的代码

  3. 如果出现的问题没有被捕获，那么程序如何运行？

     那么try...catch就相当于没有写.那么也就是自己没有处理.
     默认交给虚拟机处理.

  4. 同时有可能出现多个异常怎么处理？

     出现多个异常,那么就写多个catch就可以了.
     注意点:如果多个异常之间存在子父类关系.那么父类一定要写在下面


```java
public class ExceptionDemo10 {
    public static void main(String[] args) {
        //1.如果 try 中没有遇到问题，怎么执行？ --- 会把try中所有的代码全部执行完毕,不会执行catch里面的代码
        //2.如果 try 中遇到了问题，那么 try 下面的代码还会执行吗？
                            //那么直接跳转到对应的catch语句中,try下面的代码就不会再执行了
                            //当catch里面的语句全部执行完毕,表示整个体系全部执行完全,继续执行下面的代码
        //3.如果出现的问题没有被捕获，那么程序如何运行？
                             //那么try...catch就相当于没有写.那么也就是自己没有处理.
                             //默认交给虚拟机处理.
        //4.同时有可能出现多个异常怎么处理？
                            //出现多个异常,那么就写多个catch就可以了.
                            //注意点:如果多个异常之间存在子父类关系.那么父类一定要写在下面
        // method1();
    try {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入你的年龄");
        String line = sc.nextLine();
        int age = Integer.parseInt(line);//格式化异常
        System.out.println(age);
        System.out.println(2 / 0); //数学异常
    } catch (Exception e) {
        //以后我们针对于每种不同的异常,有可能会有不同的处理结果.
    }
    System.out.println("测试456");
}

private static void method1() {
    try {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入你的年龄");
        String line = sc.nextLine();
        int age = Integer.parseInt(line);//格式化异常
        System.out.println(age);
        System.out.println(2 / 0); //数学异常
    } catch (NumberFormatException e) {
        System.out.println("格式化异常出现了");
    }catch (ArithmeticException e) {
        System.out.println("数学运算异常出现了");
    }
    System.out.println("测试456");
}
```

### 4.7 Throwable中的常见方法（重点）

- 常用方法

  | 方法名                            | 说明                              |
  | --------------------------------- | --------------------------------- |
  | public String getMessage()        | 返回此 throwable 的详细消息字符串 |
  | public String toString()          | 返回此可抛出的简短描述            |
  | **public void printStackTrace()** | **把异常的错误信息输出在控制台**  |

- 示例代码

  ```java
  public class ExceptionDemo11 {
      //public String getMessage​()    返回此 throwable 的详细消息字符串
      //public String toString​()      返回此可抛出的简短描述
    //public void printStackTrace​() 把异常的错误信息输出在控制台(字体为红色的)
      public static void main(String[] args) {
  
          try {
              int [] arr = {1,2,3,4,5};
              System.out.println(arr[10]);//虚拟机帮我们创建了一个异常对象 new ArrayIndexOutOfBoundsException();
          } catch (ArrayIndexOutOfBoundsException e) {
              /*String message = e.getMessage();
            System.out.println(message);*/
             /* String s = e.toString();
              System.out.println(s);*/
             e.printStackTrace();
        }
  
          System.out.println("嘿嘿嘿");
  
    }
  }
  ```

### 4.8 异常的练习

![1595865869495](/github/assets/blog_res/2022-09-02-JavaSE_advanced5.assets/1595865869495.png)

+ 需求

  键盘录入学生的姓名和年龄,其中年龄为18 - 25岁,超出这个范围是异常数据不能赋值.需要重新录入,一直录到正确为止

+ 实现步骤

  1. 创建学生对象
  2. 键盘录入姓名和年龄，并赋值给学生对象
  3. 如果是非法数据就再次录入

+ 代码实现

  学生类

  ```java
  package com.itheima.exce;
  
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
          if(age >= 18 && age <= 25){
              this.age = age;
          }else{
              throw new RuntimeException("年龄超出了范围");
            
          }
      }
  
      @Override
      public String toString() {
          return "Student{" +
                  "name='" + name + '\'' +
                  ", age=" + age +
                  '}';
    }
  }
  ```

```java
 package com.itheima.exce;

  
import java.util.Scanner;
  
  public class ExceptionDemo12 {
      public static void main(String[] args) {
          // 键盘录入学生的姓名和年龄,其中年龄为 18 - 25岁,
          // 超出这个范围是异常数据不能赋值.需要重新录入,一直录到正确为止。
  
          Student s = new Student();
  
          Scanner sc = new Scanner(System.in);
          System.out.println("请输入姓名");
          String name = sc.nextLine();
          s.setName(name);
         while(true){
             System.out.println("请输入年龄");
             String ageStr = sc.nextLine();
             try {
                 int age = Integer.parseInt(ageStr);
                 s.setAge(age);
                 break;
             } catch (NumberFormatException e) {
                 System.out.println("请输入一个整数");
                 continue;
             } catch (AgeOutOfBoundsException e) {
                 System.out.println(e.toString());
                 System.out.println("请输入一个符合范围的年龄");
                 continue;
             }
             /*if(age >= 18 && age <=25){
               s.setAge(age);
                 break;
             }else{
                 System.out.println("请输入符合要求的年龄");
                 continue;
             }*/
         }
          System.out.println(s);
  
      }
  }
```

### 4.9 自定义异常

1.什么是自定义异常？

当Java中提供的异常不能满足我们的需求时,我们可以自定义异常

2.为什么要 自定义异常？

   有一个原则 ：异常类要与业务相关

3.实现步骤

1. 定义异常类
2. 写继承关系
3. 提供空参构造
4. 提供带参构造

异常类

```java
public class AgeOutOfBoundsException extends RuntimeException {
    public AgeOutOfBoundsException() {
    }

    public AgeOutOfBoundsException(String message) {
        super(message);
    }
}
```

学生类

```java
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
        if(age >= 18 && age <= 25){
            this.age = age;
        }else{
            //如果Java中提供的异常不能满足我们的需求,我们可以使用自定义的异常
            throw new AgeOutOfBoundsException("年龄超出了范围");
        }
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

测试类

```java
public class ExceptionDemo12 {
    public static void main(String[] args) {
        // 键盘录入学生的姓名和年龄,其中年龄为 18 - 25岁,
        // 超出这个范围是异常数据不能赋值.需要重新录入,一直录到正确为止。

        Student s = new Student();

        Scanner sc = new Scanner(System.in);
        System.out.println("请输入姓名");
        String name = sc.nextLine();
        s.setName(name);
       while(true){
           System.out.println("请输入年龄");
           String ageStr = sc.nextLine();
           try {
               int age = Integer.parseInt(ageStr);
               s.setAge(age);
               break;
           } catch (NumberFormatException e) {
               System.out.println("请输入一个整数");
               continue;
           } catch (AgeOutOfBoundsException e) {
               System.out.println(e.toString());
               System.out.println("请输入一个符合范围的年龄");
               continue;
           }
           /*if(age >= 18 && age <=25){
               s.setAge(age);
               break;
           }else{
               System.out.println("请输入符合要求的年龄");
               continue;
           }*/
       }
        System.out.println(s);

    }
}
```

##      小结

​        **1.什么是异常**

​          程序中的不正常称为异常

​        **2.异常的分类**

​          编译期异常和运行时异常

​        **3.谁处理异常?**

​           原则上方谁调用谁处理，不想处理throws声明异常

​           实际开发过程中尽量不要让jvm来处理异常

​        **4.如何捕获异常**

​           通过try...catch来捕获

​        **5.如何手动抛出异常**

​           throw new 异常类()

​        **6.为什么要自定义异常**

​          在实际开发过程中有很多异常是jdk没有帮我们定义好的，比如age负数或超出范围异常，因此我们需要根据实际的业务自定义异常

​		**7.如何自定义异常**

​          继承RuntimeException，调用父类中的带参构造方法









 
