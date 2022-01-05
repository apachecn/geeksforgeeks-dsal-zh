# 可被 X 整除的最小 K 位数的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-minist-k-digital-number-除尽-x/](https://www.geeksforgeeks.org/java-program-for-smallest-k-digit-number-divisible-by-x/)

给出了整数 X 和 K。任务是找到能被 x 整除的最小 K 位数。

示例:

```
Input : X = 83, K = 5
Output : 10043
10040 is the smallest 5 digit
number that is multiple of 83.

Input : X = 5, K = 2
Output : 10
```

一个有效的解决方案是:

```
Compute MIN : smallest K-digit number (1000...K-times)
If, MIN % X is 0, ans = MIN
else, ans = (MIN + X) - ((MIN + X) % X))
This is because there will be a number in 
range [MIN...MIN+X] divisible by X.

```

```
// Java code to find smallest K-digit
// number divisible by X

import java.io.*;
import java.lang.*;

class GFG {
    public static double answer(double X, double K)
    {
        double i = 10;
        // Computing MIN
        double MIN = Math.pow(i, K - 1);

        // returning ans
        if (MIN % X == 0)
            return (MIN);
        else
            return ((MIN + X) - ((MIN + X) % X));
    }

    public static void main(String[] args)
    {

        // Number whose divisible is to be found
        double X = 83;
        double K = 5;

        System.out.println((int)answer(X, K));
    }
}

// Code contributed by Mohit Gupta_OMG <(0_o)>
```

**Output:**

```
10043

```

要了解 Math.pow()函数，请参考文章第 18 点:
[https://www . geeksforgeeks . org/Java-lang-math-class-Java-set-2/](https://www.geeksforgeeks.org/java-lang-math-class-java-set-2/)

详情请参考[最小可被 X 整除的 K 位数](https://www.geeksforgeeks.org/smallest-k-digit-number-divisible-x/)整篇文章！