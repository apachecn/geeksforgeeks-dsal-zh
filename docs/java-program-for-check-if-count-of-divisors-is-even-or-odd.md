# 检查除数是偶数还是奇数的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序检查除数是偶数还是奇数/](https://www.geeksforgeeks.org/java-program-for-check-if-count-of-divisors-is-even-or-odd/)

给定一个数“n”，求它的除数总数是偶数还是奇数。

示例:

```
Input: n = 10      
Output: Even

Input: n = 100
Output: Odd

Input:  n = 125
Output: Even
```

一种天真的方法是[找到所有的除数](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)，然后看看除数的总数是偶数还是奇数。

这种解决方案的时间复杂度为 0(平方英尺(n))

```
// Naive Solution to
// find if count of
// divisors is even
// or odd
import java.io.*;
import java.math.*;

class GFG {

    // Function to count
    // the divisors
    static void countDivisors(int n)
    {
        // Initialize count
        // of divisors
        int count = 0;

        // Note that this
        // loop runs till
        // square root
        for (int i = 1; i <= Math.sqrt(n) + 1; i++) {
            if (n % i == 0)

                // If divisors are
                // equal increment
                // count by one
                // Otherwise increment
                // count by 2
                count += (n / i == i) ? 1 : 2;
        }

        if (count % 2 == 0)
            System.out.println("Even");

        else
            System.out.println("Odd");
    }

    // Driver program
    public static void main(String args[])
    {
        System.out.println("The count of divisor:");
        countDivisors(10);
    }
}
/* This code is contributed by Nikita Tiwari.*/
```

**Output:**

```
The count of divisor:
Even

```

**有效解:**
我们可以观察到除数只有在完美平方的情况下才是奇数。因此，最好的解决办法是检查给定的数字是否是完美的正方形。如果它是一个完美的正方形，那么除数将是奇数，否则它将是偶数。

```
// Java program for
// Efficient Solution to find
// if count of divisors is
// even or odd
import java.io.*;
import java.math.*;

class GFG {

    // Function to find if count
    // of divisors is even or
    // odd
    static void countDivisors(int n)
    {
        int root_n = (int)(Math.sqrt(n));

        // If n is a perfect square,
        // then, it has odd divisors
        if (root_n * root_n == n)
            System.out.println("Odd");

        else
            System.out.println("Even");
    }

    /* Driver program to test above function */
    public static void main(String args[])
        throws IOException
    {
        System.out.println("The count of "
                           + "divisors of 10 is: ");

        countDivisors(10);
    }
}

/* This code is contributed by Nikita Tiwari. */
```

**Output:**

```
The count of divisors of 10 is: 
Even

```

详情请参考[查看除数是偶数还是奇数](https://www.geeksforgeeks.org/check-if-total-number-of-divisors-are-even-or-odd/)整篇文章！