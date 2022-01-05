# Java 程序求一个数列的和 1/1！+ 2/2!+ 3/3!+ 4/4!+…….+ n/n！

> 原文:[https://www . geesforgeks . org/Java-program-for-program-to-find-sum-a-series-11-22-33-44-nn/](https://www.geeksforgeeks.org/java-program-for-program-to-find-the-sum-of-a-series-11-22-33-44-nn/)

你已经得到了 1/1 系列！+ 2/2!+ 3/3!+ 4/4!+…….+ n/n！，求出直到第 n 项的级数和。
**例:**

```
Input :n = 5
Output : 2.70833

Input :n = 7
Output : 2.71806
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the sum of series

import java.io.*;
import java.lang.*;

class GFG {
    public static double sumOfSeries(double num)
    {
        double res = 0, fact = 1;
        for (int i = 1; i <= num; i++) {
            /*fact variable store factorial of the i.*/
            fact = fact * i;

            res = res + (i / fact);
        }
        return (res);
    }

    public static void main(String[] args)
    {
        double n = 5;
        System.out.println("Sum: " + sumOfSeries(n));
    }
}

// Code contributed by Mohit Gupta_OMG <(0_o)>
```

**Output:** 

```
Sum: 2.708333333333333
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

请参考[程序的完整文章，找到一个数列 1/1 的和！+ 2/2!+ 3/3!+ 4/4!+…….+ n/n！](https://www.geeksforgeeks.org/program-to-find-the-sum-of-a-series-11-22-33-44-nn/)了解更多详情！