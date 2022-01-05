# 生成正有理数的算法

> 原文:[https://www . geeksforgeeks . org/算法生成正有理数/](https://www.geeksforgeeks.org/algorithm-to-generate-positive-rational-numbers/)

有理数的形式是 p/q，其中 p 和 q 是整数。问题陈述是生成有理数，从而在有限的时间内生成任何特定的数。对于给定的 n，我们生成所有有理数，其中 1 <= p <= n，1 <= q <= n

示例:

```
Input : 5
Output : 1, 1/2, 2, 1/3, 2/3, 3/2, 3, 1/4,
         3/4, 4/3, 4, 1/5, 2/5, 3/5, 4/5,
         5/4, 5/3, 5/2, 5

Input : 7
Output :1, 1/2, 2, 1/3, 2/3, 3/2, 3, 1/4, 3/4,
        4/3, 4, 1/5, 2/5, 3/5, 4/5, 5/4, 5/3, 
        5/2, 5, 1/6, 5/6, 6/5, 6, 1/7, 2/7, 3/7,
        4/7, 5/7, 6/7, 7/6, 7/5, 7/4, 7/3, 7/2, 7

```

用数学术语来说，如果一个集合的元素可以与自然数的集合一一对应，那么这个集合就是无限的。

这里的问题陈述是生成 p/q 的组合，其中 p 和 q 都是整数，p 和 q 的任何特定组合都将在有限步数内达到。如果 p 增加 1，2，3…等，保持 q 不变，反之亦然，所有的组合都不能在有限的时间内达到。处理这个问题的方法是把自然数想象成矩阵的行、列

(1，1) (1，2) (1，3) (1，4)
(2，1) (2，2) (2，3) (2，4)
(3，1) (3，2) (3，3) (3，4)
(4，1) (4，2) (4，3) (4，4)

这些元素在每次迭代中以**倒** L 形状遍历

(1，1)
(1，2)、(2，2) (2，1)
(1，3)、(2，3)、(3，3)、(3，2)、(3，1)

生产的

1/1
1/2，2/2，2/1
1/3，2/3，3/3，3/2，3/1

显然，这将产生 2/1 和 4/2 等副本，但可以通过使用最大公约数约束来消除这些副本。

```
// Java program 
import java.util.ArrayList;
import java.util.List;

class Rational {

    private static class RationalNumber {

        private int numerator;
        private int denominator;

        public RationalNumber(int numerator, int denominator)
        {
            this.numerator = numerator;
            this.denominator = denominator;
        }

        @Override
        public String toString()
        {
            if (denominator == 1) {
                return Integer.toString(numerator);
            }
            else {
                return Integer.toString(numerator) + '/' + 
                       Integer.toString(denominator);
            }
        }
    }

    /**
     * Greatest common divisor
     * @param num1
     * @param num2
     * @return
     */
    private static int gcd(int num1, int num2)
    {
        int n1 = num1;
        int n2 = num2;

        while (n1 != n2) {
            if (n1 > n2)
                n1 -= n2;
            else
                n2 -= n1;
        }
        return n1;
    }

    private static List<RationalNumber> generate(int n)
    {

        List<RationalNumber> list = new ArrayList<>();

        if (n > 1) {
            RationalNumber rational = new RationalNumber(1, 1);
            list.add(rational);
        }

        for (int loop = 1; loop <= n; loop++) {

            int jump = 1;

            // Handle even case
            if (loop % 2 == 0)
                jump = 2;
            else
                jump = 1;

            for (int row = 1; row <= loop - 1; row += jump) {

                // Add only if there are no common divisors other than 1
                if (gcd(row, loop) == 1) {
                    RationalNumber rational = new RationalNumber(row, loop);
                    list.add(rational);
                }
            }

            for (int col = loop - 1; col >= 1; col -= jump) {

                // Add only if there are no common divisors other than 1
                if (gcd(col, loop) == 1) {
                    RationalNumber rational = new RationalNumber(loop, col);
                    list.add(rational);
                }
            }
        }

        return list;
    }

    public static void main(String[] args)
    {
        List<RationalNumber> rationals = generate(7);
        System.out.println(rationals.stream().
                  map(RationalNumber::toString).
                  reduce((x, y) -> x + ", " + y).get());
    }
}
```

**Output:**

```
1, 1/2, 2, 1/3, 2/3, 3/2, 3, 1/4, 3/4, 4/3, 4, 1/5, 2/5, 3/5, 4/5, 5/4, 5/3, 5/2, 5, 1/6, 5/6, 6/5, 6, 1/7, 2/7, 3/7, 4/7, 5/7, 6/7, 7/6, 7/5, 7/4, 7/3, 7/2, 7

```