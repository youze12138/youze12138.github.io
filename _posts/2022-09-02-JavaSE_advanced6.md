---
title: 面向对象-包数递时
date: 2022-09-02 14:34:00 +0800
categories: [面向对象-知识点4]
tags: [后端]
pin: true
author: BruceZhou

toc: true
comments: true
typora-root-url: ../../youze12138.github.io
math: false
mermaid: truey
---

# 面向对象-包数递时

## 1.包装类

### 1.1 基本类型包装类

- 基本类型包装类的作用

  将基本数据类型封装成对象的好处在于可以在对象中定义更多的功能方法操作该数据

  常用的操作之一：用于基本数据类型与字符串之间的转换

- 基本类型对应的包装类

  | 基本数据类型 | 包装类    |
  | ------------ | --------- |
  | byte         | Byte      |
  | short        | Short     |
  | int          | Integer   |
  | long         | Long      |
  | float        | Float     |
  | double       | Double    |
  | char         | Character |
  | boolean      | Boolean   |

### 1.2 Integer类

- Integer类概述

  包装一个对象中的原始类型 int 的值

- Integer类构造方法

  | 方法名                                  | 说明                                     |
  | --------------------------------------- | ---------------------------------------- |
  | public Integer(int   value)             | 根据 int 值创建 Integer 对象(过时)       |
  | public Integer(String s)                | 根据 String 值创建 Integer 对象(过时)    |
  | public static Integer valueOf(int i)    | 返回表示指定的 int 值的 Integer   实例   |
  | public static Integer valueOf(String s) | 返回一个保存指定值的 Integer 对象 String |

- 示例代码

  ```java
  public class IntegerDemo {
      public static void main(String[] args) {
          //public Integer(int value)：根据 int 值创建 Integer 对象(过时)
          Integer i1 = new Integer(100);
          System.out.println(i1);
  
          //public Integer(String s)：根据 String 值创建 Integer 对象(过时)
          Integer i2 = new Integer("100");
  //        Integer i2 = new Integer("abc"); //NumberFormatException
          System.out.println(i2);
          System.out.println("--------");
  
          //public static Integer valueOf(int i)：返回表示指定的 int 值的 Integer 实例
          Integer i3 = Integer.valueOf(100);
          System.out.println(i3);
  
          //public static Integer valueOf(String s)：返回一个保存指定值的Integer对象 String
          Integer i4 = Integer.valueOf("100");
          System.out.println(i4);
      }
  }
  ```

### 1.3 自动拆箱和自动装箱

- 自动装箱

  ​	把基本数据类型转换为对应的包装类类型

- 自动拆箱

  ​	把包装类类型转换为对应的基本数据类型

- 示例代码

  ```java
  Integer i = 100;  // 自动装箱
  i += 200;         // i = i + 200;  i + 200 自动拆箱；i = i + 200; 是自动装箱
  ```

### 1.4 int和String类型的相互转换

- int转换为String

  - 转换方式

    - 方式一：直接在数字后加一个空字符串
    - 方式二：通过String类静态方法valueOf()

  - 示例代码

    ```java
    public class IntegerDemo {
        public static void main(String[] args) {
            //int --- String
            int number = 100;
            //方式1
            String s1 = number + "";
            System.out.println(s1);
            //方式2
            //public static String valueOf(int i)
            String s2 = String.valueOf(number);
            System.out.println(s2);
            System.out.println("--------");
        }
    }
    ```

- String转换为int

  - 转换方式

    - 方式一：先将字符串数字转成Integer，再调用valueOf()方法
    - 方式二：通过Integer静态方法parseInt()进行转换

  - 示例代码

    ```java
    public class IntegerDemo {
        public static void main(String[] args) {
            //String --- int
            String s = "100";
            //方式1：String --- Integer --- int
            Integer i = Integer.valueOf(s);
            //public int intValue()
            int x = i.intValue();
            System.out.println(x);
            //方式2
            //public static int parseInt(String s)
            int y = Integer.parseInt(s);
            System.out.println(y);
        }
    }
    ```

## 2.数组的高级操作 

### 2.1 二分查找

+ 二分查找概述

  查找指定元素在数组中的位置时,以前的方式是通过遍历,逐个获取每个元素,看是否是要查找的元素,这种方式当数组元素较多时,查找的效率很低

  二分查找也叫折半查找,每次可以去掉一半的查找范围,从而提高查找的效率


+ 需求

  在数组{1,2,3,4,5,6,7,8,9,10}中,查找某个元素的位置

+ 实现步骤

  1. 定义两个变量，表示要查找的范围。默认min = 0 ，max = 最大索引
  2. 循环查找，但是min <= max
  3. 计算出mid的值
  4. 判断mid位置的元素是否为要查找的元素，如果是直接返回对应索引
  5. 如果要查找的值在mid的左半边，那么min值不变，max = mid -1.继续下次循环查找
  6. 如果要查找的值在mid的右半边，那么max值不变，min = mid + 1.继续下次循环查找
  7. 当min > max 时，表示要查找的元素在数组中不存在，返回-1.

+ 代码实现

  ```java
  public class MyBinarySearchDemo {
      public static void main(String[] args) {
          int [] arr = {1,2,3,4,5,6,7,8,9,10};
          int number = 11;
  
          //1,我现在要干嘛? --- 二分查找
          //2.我干这件事情需要什么? --- 数组 元素
          //3,我干完了,要不要把结果返回调用者 --- 把索引返回给调用者
          int index = binarySearchForIndex(arr,number);
          System.out.println(index);
      }
  
      private static int binarySearchForIndex(int[] arr, int number) {
          //1,定义查找的范围
          int min = 0;
          int max = arr.length - 1;
          //2.循环查找 min <= max
          while(min <= max){
              //3.计算出中间位置 mid
              int mid = (min + max) >> 1;
              //mid指向的元素 > number
              if(arr[mid] > number){
                  //表示要查找的元素在左边.
                  max = mid -1;
              }else if(arr[mid] < number){
                  //mid指向的元素 < number
                  //表示要查找的元素在右边.
                  min = mid + 1;
              }else{
                  //mid指向的元素 == number
                  return mid;
              }
          }
          //如果min大于了max就表示元素不存在,返回-1.
          return -1;
      }
    
  }
  ```

+ 注意事项

  有一个前提条件，数组内的元素一定要按照大小顺序排列，如果没有大小顺序，是不能使用二分查找法的

### 2.2 冒泡排序 

+ 冒泡排序概述

  一种排序的方式，对要进行排序的数据中相邻的数据进行两两比较，将较大的数据放在后面，依次对所有的数据进行操作，直至所有数据按要求完成排序

  如果有n个数据进行排序，总共需要比较n-1次

  每一次比较完毕，下一次的比较就会少一个数据参与

+ 代码实现

  ```java
  public class MyBubbleSortDemo2 {
      public static void main(String[] args) {
          int[] arr = {3, 5, 2, 1, 4};
          //1 2 3 4 5
          bubbleSort(arr);
      }
  
      private static void bubbleSort(int[] arr) {
          //外层循环控制的是次数 比数组的长度少一次.
          for (int i = 0; i < arr.length -1; i++) {
              //内存循环就是实际循环比较的
              //-1 是为了让数组不要越界
              //-i 每一轮结束之后,我们就会少比一个数字.
              for (int j = 0; j < arr.length - 1 - i; j++) {
                  if (arr[j] > arr[j + 1]) {
                      int temp = arr[j];
                      arr[j] = arr[j + 1];
                      arr[j + 1] = temp;
                  }
              }
          }
  
          printArr(arr);
      }
  
      private static void printArr(int[] arr) {
          for (int i = 0; i < arr.length; i++) {
              System.out.print(arr[i] + " ");
          }
          System.out.println();
      }
    
  }
  ```

## 3.递归

### 3.1 递归

- 递归的介绍

  - 以编程的角度来看，递归指的是方法定义中调用方法本身的现象
  - 把一个复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解
  - 递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算

- 递归的基本使用

  ```java
  public class MyFactorialDemo2 {
      public static void main(String[] args) {
          int sum = getSum(100);
          System.out.println(sum);
      }
  
      private static int getSum(int i) {
          //1- 100之间的和
              //100 + (1-99之间的和)
                      // 99 + (1- 98之间的和)
                          //....
                              //1
          //方法的作用: 求 1- i 之间和
          if(i == 1){
              return 1;
          }else{
              return i + getSum(i -1);
          }
      }
  }    
  ```

- 注意事项

  - 递归一定要有出口。否则内存溢出
  - 递归虽然有出口，但是递归的次数也不宜过多。否则内存溢出

### 3.2 递归求阶乘

- 案例需求

  ​	用递归求5的阶乘，并把结果在控制台输出

- 代码实现

  ```java
  public class DiGuiDemo01 {
      public static void main(String[] args) {
          //调用方法
          int result = jc(5);
          //输出结果
          System.out.println("5的阶乘是：" + result);
      }
  
      //定义一个方法，用于递归求阶乘，参数为一个int类型的变量
      public static int jc(int n) {
          //在方法内部判断该变量的值是否是1
          if(n == 1) {
              //是：返回1
              return 1;
          } else {
              //不是：返回n*(n-1)!
              return n*jc(n-1);
          }
      }
  }
  ```

- 内存图

  ![08_递归内存图](/assets/blog_res/2022-09-02-JavaSE_advanced6.assets/08_.png)

## 

### 3.3 Arrays

- Arrays的常用方法

  | 方法名                                           | 说明                               |
  | ------------------------------------------------ | ---------------------------------- |
  | public static String toString(int[] a)           | 返回指定数组的内容的字符串表示形式 |
  | public static void sort(int[] a)                 | 按照数字顺序排列指定的数组         |
  | public static int binarySearch(int[] a, int key) | 利用二分查找返回指定元素的索引     |

- 示例代码

  ```java
  public class MyArraysDemo {
        public static void main(String[] args) {
    //        public static String toString(int[] a)    返回指定数组的内容的字符串表示形式
    //        int [] arr = {3,2,4,6,7};
    //        System.out.println(Arrays.toString(arr));
  
    //        public static void sort(int[] a)	  按照数字顺序排列指定的数组
    //        int [] arr = {3,2,4,6,7};
    //        Arrays.sort(arr);
    //        System.out.println(Arrays.toString(arr));
  
    //        public static int binarySearch(int[] a, int key) 利用二分查找返回指定元素的索引
            int [] arr = {1,2,3,4,5,6,7,8,9,10};
            int index = Arrays.binarySearch(arr, 0);
            System.out.println(index);
            //1,数组必须有序
            //2.如果要查找的元素存在,那么返回的是这个元素实际的索引
            //3.如果要查找的元素不存在,那么返回的是 (-插入点-1)
                //插入点:如果这个元素在数组中,他应该在哪个索引上.
        }
    }
  ```

- 工具类设计思想

  1. 构造方法用 private 修饰
  2. 成员用 public static 修饰

## 4.时间日期类

### 4.1 时间概述

1. 北京时间需要在世界标准时间加上8小时

2. 计算机中时间原点（UNIX操作系统,C语言的诞生日）

   ![image-20201015005659191](/assets/blog_res/2022-09-02-JavaSE_advanced6.assets/time-c.png)

​      1970年1月1日 00:00:00

  3.时间换算单位

​    1秒 = 1000毫秒

### 4.2 时间日期类-Date构造方法

1. 什么是Date类

   Date 代表了一个特定的时间，精确到毫秒

  2.Date类构造方法

| 方法名                 | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| public Date()          | 创建 Date对象，默认存储当前时间，单位毫秒                    |
| public Date(long date) | 创建 Date对象，并将其初始化为表示从**标准基准时间**起指定的毫秒数 |

示例代码

```java
import java.util.Date;

public class DateDemo1 {
    public static void main(String[] args) {
//        public Date()		创建一个Date对象，表示默认时间
//public Date(long date)	创建一个Date对象，表示指定时间

        //那么这个时间就表示电脑中的当前时间。
        Date date1 = new Date();
        System.out.println(date1);

        //从计算机的时间原点开始，过了指定毫秒的那个时间。
        Date date2 = new Date(0L);
        System.out.println(date2);//Thu Jan 01 08:00:00 CST 1970
        //从时间原点开始，过了0毫秒。
        //因为我们是在中国，我们是在东八区需要+8小时。

        //1970年1月1日 上午的10点
        Date date3 = new Date(2*3600L * 1000);
        System.out.println(date3);
    }
}
```

### 4.3 时间日期类-Date成员方法

- 常用方法

  | 方法名                         | 说明                                                  |
  | ------------------------------ | ----------------------------------------------------- |
  | public long getTime()          | 获取的是日期对象从1970年1月1日 00:00:00到现在的毫秒值 |
  | public void setTime(long time) | 设置时间，给的是毫秒值                                |

- 示例代码

  ```java
  public class DateDemo2 {
      public static void main(String[] args) {
  //        public long getTime()			获取时间对象的毫秒值
  //        public void setTime(long time)		设置时间，传递毫秒值
  
          //method1();
          //method2();
  
    }
  
      private static void method2() {
          Date date1 = new Date();
          date1.setTime(0L);
          System.out.println(date1);
      }
  
      private static void method1() {
          //把当前时间封装成一个date对象
          Date date1 = new Date();
          //获取这个date对象的毫秒值 --- 获取当前时间的毫秒值
          long time = date1.getTime();
          System.out.println(time);
  		
          long time2 = System.currentTimeMillis();
          System.out.println(time2);
      }
  }
  ```

### 4.4 SimpleDateFormat类

1.SimpleDateFormat类有什么作用？

​	SimpleDateFormat可以对Date对象和日期字符串,进行格式化和解析

2.如何使用？

1.常用的模式字母及应对关系如下:

 HH：24小制,hh:12小时制

![1595820776762](/assets/blog_res/2022-09-02-JavaSE_advanced6.assets/1595820776762.png)

2.SimpleDateFormat类构造方法

| 方法名                                   | 说明                                             |
| ---------------------------------------- | ------------------------------------------------ |
| public   SimpleDateFormat()              | 构造一个SimpleDateFormat，使用默认模式和日期格式 |
| public  SimpleDateFormat(String pattern) | 构造一个SimpleDateFormat使用给定的模式           |

3.SimpleDateFormat类的常用方法

- 格式化(从Date到String)

​		public final String format(Date date)：将日期格式化成日期/时间字符串

- 解析(从日期/时间字符串String到Date)

​		public Date parse(String source)：从给定字符串的开始解析文本以生成日期      

示例代码（公历日期标准格式为；2007年2月6日；或：2007-02-06）

```java
public class DateDemo4 {
    public static void main(String[] args) throws ParseException {
        String s = "2048-01-01";

        //SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");

        Date date = sdf.parse(s);

        System.out.println(date);
    }
}
```

## 小结

1. 北京时间需要在世界标准时间加上8小时
2. 计算机中时间原点

​      1970年1月1日 00:00:00

  3.时间换算单位

​    1秒 = 1000毫秒

  4.Date类概述

​     Date 代表了一个特定的时间，精确到**毫秒**

  5.如何创建时间对象?

​    通过Date的构造方法，空参构造和带参构造，带参构造参数：是自1970年7月1日00:00:00经过的毫秒数

6.如何格式化和解析日期

   通过SimpleDateFormat，创建SimpleDateFormat类:new SimpleDateFormat("日期模式")

   格式化:format(Date string)

   解析: parse(String date)
