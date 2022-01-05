# 高效打印给定数字所有质因数的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-efficient-print-all-prime-factors-of-a-number/](https://www.geeksforgeeks.org/java-program-for-efficiently-print-all-prime-factors-of-a-given-number/)

给定一个数字 n，写一个高效的函数打印 n 的所有[质因数](http://en.wikipedia.org/wiki/Prime_factor)，比如输入数字是 12，那么输出应该是“2 2 3”。如果输入的数字是 315，那么输出应该是“3 3 5 7”。
以下是寻找所有主要因素的步骤。
**1)** 当 n 可被 2 整除时，打印 2，再将 n 除以 2。
**2)** 第 1 步后，n 必须为奇数。现在开始一个从 i = 3 到 n 的平方根的循环，当我除 n 时，打印 I，用 I 除 n，将 I 增加 2，然后继续。
**3)** 如果 n 是素数且大于 2，那么通过以上两步 n 不会变成 1。所以如果大于 2 就打印 n。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to print all prime factors
import java.io.*;
import java.lang.Math;

class GFG {
    // A function to print all prime factors
    // of a given number n
    public static void primeFactors(int n)
    {
        // Print the number of 2s that divide n
        while (n % 2 == 0) {
            System.out.print(2 + " ");
            n /= 2;
        }

        // n must be odd at this point.  So we can
        // skip one element (Note i = i +2)
        for (int i = 3; i <= Math.sqrt(n); i += 2) {
            // While i divides n, print i and divide n
            while (n % i == 0) {
                System.out.print(i + " ");
                n /= i;
            }
        }

        // This condition is to handle the case whien
        // n is a prime number greater than 2
        if (n > 2)
            System.out.print(n);
    }

    public static void main(String[] args)
    {
        int n = 315;
        primeFactors(n);
    }
}
```

**Output:** 

```
3 3 5 7
```

***时间复杂度:** O(n <sup>1/2</sup> )*

***辅助空间:** O(1)*

**这是如何工作的？**
步骤 1 和 2 处理复合数，步骤 3 处理素数。为了证明完整的算法是有效的，我们需要证明步骤 1 和 2 实际上处理了复合数。很明显，步骤 1 处理偶数。在步骤 1 之后，所有剩余的质因数必须是奇数(两个质因数之差必须至少为 2)，这解释了为什么 I 增加 2。
现在主要部分是，循环运行到 n 的平方根 not till。为了证明这种优化是有效的，让我们考虑复合数的以下性质。
*每个复合数至少有一个小于或等于其平方根的质因数。*
这个属性可以用 counter 语句来证明。设 a 和 b 是 n 的两个因子，使得 a*b = n，如果两者都大于√n，那么 a.b > √n，* √n，这与表达式“a * b = n”相矛盾。
在上述算法的第 2 步中，我们运行一个循环，并在循环中执行以下操作
a)找到最小质因数 I(必须小于√n，
b)通过重复将 n 除以 I 来从 n 中移除所有出现的 I。
c)对除以的 n 重复步骤 a 和 b，i = i + 2。重复步骤 a 和 b，直到 n 变成 1 或质数。
更多详情请参考[高效程序打印给定数字](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)所有质因数的完整文章！