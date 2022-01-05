# 检查两个给定的有理数是否相等

> 原文:[https://www . geesforgeks . org/check-如果两个给定的有理数相等或不相等/](https://www.geeksforgeeks.org/check-if-two-given-rational-numbers-are-equal-or-not/)

给定两个代表非负数[有理数](https://www.geeksforgeeks.org/rational-numbers/)的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **T** ，任务是检查 **S** 和 **T** 的值是否相等。如果发现为真，则打印**“是”**。否则，打印**“否”**。

**注:**任意有理数可以用以下三种方式之一表示:

*   **<整数部分>** (例如 0、12、123)
*   **<内部部分> <。> <非重复部分>** (例如 0.5，1。, 2.12, 2.0001)
*   **<内部部分> <。> <非重复部分> < ( > <重复部分> < ) >** (例如 0.1(6)、0.9(9)、0.00(1212))

**示例:**

> **输入:**S =“0”。(52)”、T =“0.5(25)”
> **输出:** YES
> **解释:**
> 有理数“0。(52)“可以表示为 0.52525252……”
> 有理数“0.5(25)”可以表示为 0.525252525……。
> 因此，要求的输出为“是”。
> 
> **输入:**S =“0.9(9)”，T =“1。”
> **输出:** YES
> **说明:**
> 有理数“0.9(9)”可以表示为 0.9999999999……，等于 1。
> 有理数“1”可以表示为数字 1。
> 因此，要求的输出为“是”。

**方法:**想法是将有理数转换成分数，然后[检查两个有理数的分数是否相等](https://www.geeksforgeeks.org/program-compare-two-fractions/)。如果发现属实，则打印**“是”**。否则，打印**“否”**。以下是观察结果:

> 十进制扩展的重复部分通常用一对圆括号表示。
> 例如:1 / 6 = 0.1666666…= 0.1(6)= 0.1666(6)= 0.166(66)
> 0.1(6)或 0.1666(6)或 0.166(66)都是 1/6 的正确表示。

基于以下观察，任何有理数都可以转换成分数:

> 设 x = 0.5(25) —> (1)
> 整数部分= 0，非重复部分= 5，重复部分= 25
> 将等式(1)的两边乘以 10 的非重复部分长度的幂，即 10 * x = 5。(25) — > (2)
> 将等式(1)的两边乘以 10 的幂(非重复部分的长度+重复部分的长度)，1000 * x = 525。(25) — > (3)
> 从方程式(3)
> 中减去方程式(2)1000 * x–10 * x = 525。(25)-5.(25)
> 990 * x = 520
> x = 520/990

按照以下步骤解决问题:

*   利用上面的观察将两个有理数转换成分数。
*   [检查两个数的分数是否相等](https://www.geeksforgeeks.org/program-compare-two-fractions/)。如果发现属实，则打印**“是”**。
*   否则，打印**“否”**。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to check if the string S and T
    // are equal or not
    public static boolean isRationalEqual(String s,
                                          String t)
    {

        // Stores the fractional part of s
        Fraction f1 = Rational.parse(s).toFraction();

        // Stores the fractional part of t
        Fraction f2 = Rational.parse(t).toFraction();

        // If the condition satisfies, returns true
        // otherwise return false
        return f1.p * f2.q == f2.p * f1.q;
    }

    // Rational class having integer, non-repeating
    // and repeating part of the number
    public static class Rational {
        private final String integer, nonRepeating,
            repeating;

        // Constructor function to initialize
        // the object of the class
        private Rational(String integer,
                         String nonRepeating,
                         String repeating)
        {

            // Stores integer part
            this.integer = integer;

            // Stores non repeating part
            this.nonRepeating = nonRepeating;

            // Stores repeating part
            this.repeating = repeating;
        }

        // Function to split the string into
        // integer, repeating & non-repeating part
        public static Rational parse(String s)
        {

            // Split s into parts
            String[] parts = s.split("[.()]");

            return new Rational(
                parts.length >= 1 ? parts[0] : "",
                parts.length >= 2 ? parts[1] : "",
                parts.length >= 3 ? parts[2] : "");
        }

        // Function to convert the string
        // into fraction
        public Fraction toFraction()
        {

            long a = tenpow(nonRepeating.length());
            long i = Long.parseLong(integer + nonRepeating);

            // If there is no repeating part, then
            // form a new fraction of the form i/a
            if (repeating.length() == 0) {
                return new Fraction(i, a);
            }

            // Otherwise
            else {
                long b = tenpow(nonRepeating.length()
                                + repeating.length());

                long j = Long.parseLong(
                    integer + nonRepeating + repeating);

                // Form the new Fraction and return
                return new Fraction(j - i, b - a);
            }
        }

        public String toString()
        {
            return String.format("%s.%s(%s)", integer,
                                 nonRepeating, repeating);
        }
    }

    // Fraction class having numerator as p
    // and denominator as q
    public static class Fraction {
        private final long p, q;

        // Constructor function to initialize
        // the object of the class
        private Fraction(long p, long q)
        {
            this.p = p;
            this.q = q;
        }

        public String toString()
        {
            return String.format("%d/%d", p, q);
        }
    }

    // Function to find 10 raised
    // to power of x
    public static long tenpow(int x)
    {
        assert x >= 0;
        long r = 1;
        while (--x >= 0) {
            r *= 10;
        }
        return r;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given S and T
        String S = "0.(52)", T = "0.5(25)";

        // Function Call
        if (isRationalEqual(S, T)) {
            System.out.println("YES");
        }
        else {

            System.out.println("NO");
        }

        // Print result
    }
}
```

**Output:**

```
YES

```

***时间复杂度:** O(N)，其中 N 是 S 和 T 的最大长度*
***辅助空间:** O(1)*