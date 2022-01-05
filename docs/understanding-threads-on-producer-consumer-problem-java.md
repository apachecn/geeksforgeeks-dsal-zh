# 了解生产者消费者问题的线程| Java

> 原文:[https://www . geesforgeks . org/understanding-threads-on-producer-consumer-problem-Java/](https://www.geeksforgeeks.org/understanding-threads-on-producer-consumer-problem-java/)

线程是执行的一部分，即它是程序中独立的执行路径。一个程序可以有多个线程，这就产生了[多线程](https://www.geeksforgeeks.org/multithreading-in-java/)的概念。我们必须使用 [java.lang.Thread](https://www.geeksforgeeks.org/java-lang-thread-class-java/) 类才能使用一个线程来执行特定的任务。在本文中，让我们通过一个程序来看看线程的实现。
每当一个程序被执行时，JVM 首先检查“Main”方法的存在。如果方法存在，默认情况下它会创建一个线程，这个线程被称为“主线程”，因为它负责执行主方法中存在的语句。一个线程可以处于多种状态，本文对此进行了讨论。
创建线程有两种方式。它们是:

1.  通过为线程类创建一个对象。
2.  通过使用可运行接口。

**通过扩展 Thread 类来创建线程:**我们创建了一个扩展 java.lang.Thread 类的类。此类覆盖线程类中可用的 **run()** 方法。一根线在**运行()**方法中开始它的生命。我们创建一个线程类的对象，调用 **start()** 方法开始执行一个线程。 **Start()** 调用线程对象上的 **run()** 方法。让我们来看一个使用线程寻找阶乘的例子:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the factorial
// of a number by the implementation
// of threads using thread class

class ThreadImplement extends Thread {
    static int fact = 1;

    // Overriding the run method
    // to find the factorial of
    // a number 5
    public void run()
    {

        // Loop to compute the factorial
        for (int i = 1; i <= 5; i++)
            fact = fact * i;
        System.out.println(fact);
    }
}

// Class to create a thread and
// compute the factorial
public class GFG {
    public static void main(String[] args)
    {
        // Creating an object of the
        // thread class
        Thread t1
            = new Thread(new ThreadImplement());

        // Computing the above class
        t1.start();
    }
}
```

**Output:** 

```
120
```