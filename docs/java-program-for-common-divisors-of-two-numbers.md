# 两个数的公约数 Java 程序

> 原文:[https://www . geesforgeks . org/Java-二进制数的公约数程序/](https://www.geeksforgeeks.org/java-program-for-common-divisors-of-two-numbers/)

给定两个整数，任务是求给定数的所有公约数？

```
Input : a = 12, b = 24
Output: 6
// all common divisors are 1, 2, 3, 
// 4, 6 and 12

Input : a = 3, b = 17
Output: 1
// all common divisors are 1

Input : a = 20, b = 36
Output: 3
// all common divisors are 1, 2, 4

```

```
// Java implementation of program

class Test {
    // method to calculate gcd of two numbers
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }
    // method to calculate all common divisors
    // of two given numbers
    // a, b --> input integer numbers
    static int commDiv(int a, int b)
    {
        // find gcd of a, b
        int n = gcd(a, b);

        // Count divisors of n.
        int result = 0;
        for (int i = 1; i <= Math.sqrt(n); i++) {
            // if 'i' is factor of n
            if (n % i == 0) {
                // check if divisors are equal
                if (n / i == i)
                    result += 1;
                else
                    result += 2;
            }
        }
        return result;
    }

    // Driver method
    public static void main(String args[])
    {
        int a = 12, b = 24;
        System.out.println(commDiv(a, b));
    }
}
```

**输出:**

```
6

```

更多详情请参考完整的[两个数的公约数](https://www.geeksforgeeks.org/common-divisors-of-two-numbers/)一文！