# Java 中的大斐波那契数

> 原文:[https://www.geeksforgeeks.org/large-fibonacci-numbers-java/](https://www.geeksforgeeks.org/large-fibonacci-numbers-java/)

给定一个数 n，求第 n 个斐波那契数。请注意，n 可能很大。

**示例:**

```
Input : 100
Output : 354224848179261915075

Input : 500
Output : 139423224561697880139724382870
         407283950070256587697307264108962948325571622
         863290691557658876222521294125 

```

**先决条件:**[Java 中的 BigInteger 类](https://www.geeksforgeeks.org/biginteger-class-in-java/)、[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)
大数的斐波那契数可能包含 100 个以上的数字，用 Java 中的 BigInteger 可以轻松处理。BigInteger 类用于数学运算，它涉及非常大的整数计算，超出了所有可用的原始数据类型的限制。

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java program to compute n-th Fibonacci
// number where n may be large.
import java.io.*;
import java.util.*;
import java.math.*;

public class Fibonacci
{
    // Returns n-th Fibonacci number
    static BigInteger fib(int n)
    {
        BigInteger a = BigInteger.valueOf(0);
        BigInteger b = BigInteger.valueOf(1);
        BigInteger c = BigInteger.valueOf(1);
        for (int j=2 ; j<=n ; j++)
        {
            c =  a.add(b);
            a = b;
            b = c;
        }

        return (b);
    }

    public static void main(String[] args)
    {
        int n = 100;
        System.out.println("Fibonacci of " + n +
            "th term" + " " +"is" +" " + fib(n));
    }
}
```

**Output**

```
Fibonacci of 100th term is 354224848179261915075

```

注意上面的解需要 O(n)个时间，我们可以在 O( log [n)时间](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)中找到[第 n 个斐波那契数。作为练习，在 O(log n)时间内找到大 n 的第 n 个斐波那契数。
本文为来稿(1)；而是由**普拉莫德·库马尔**。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客的主页上，并帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。