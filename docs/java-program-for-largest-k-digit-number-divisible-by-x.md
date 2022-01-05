# 可被 X 整除的最大 K 位数的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-maximum-k 位数-可被 x 整除/](https://www.geeksforgeeks.org/java-program-for-largest-k-digit-number-divisible-by-x/)

给出了整数 X 和 K。任务是找到能被 x 整除的最高 K 位数。

示例:

```
Input : X = 30, K = 3
Output : 990
990 is the largest three digit 
number divisible by 30.

Input : X = 7, K = 2
Output : 98

```

一个**有效的解决方案**是使用下面的公式。

```
ans = MAX - (MAX % X)
where MAX is the largest K digit 
number which is  999...K-times
```

这个公式适用于简单的学校方法划分。我们去掉余数得到最大的可除数。

```
// Java code to find highest
// K-digit number divisible by X

import java.io.*;
import java.lang.*;

class GFG {
    public static double answer(double X, double K)
    {
        double i = 10;
        // Computing MAX
        double MAX = Math.pow(i, K) - 1;

        // returning ans
        return (MAX - (MAX % X));
    }

    public static void main(String[] args)
    {

        // Number whose divisible is to be found
        double X = 30;

        // Max K-digit divisible is to be found
        double K = 3;

        System.out.println((int)answer(X, K));
    }
}

// Code contributes by Mohit Gupta_OMG <(0_o)>
```

**Output:**

```
990

```

要了解 Math.pow()函数，请参考文章第 18 点:
[https://www . geeksforgeeks . org/Java-lang-math-class-Java-set-2/](https://www.geeksforgeeks.org/java-lang-math-class-java-set-2/)

更多详情请参考[整篇文章最大 K 位数可被 X 整除](https://www.geeksforgeeks.org/largest-k-digit-number-divisible-x/)！