# 生成勾股三元组

> 原文:[https://www . geesforgeks . org/generate-毕达哥拉斯-三胞胎/](https://www.geeksforgeeks.org/generate-pythagorean-triplets/)

毕达哥拉斯三元组是一组三个正整数 a、b 和 c，使得 a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>。给定一个极限，生成所有值小于给定极限的毕达哥拉斯三元组。

```
Input : limit = 20
Output : 3 4 5
         8 6 10
         5 12 13
         15 8 17
         12 16 20
```

一个**简单的解决方案**是使用三个嵌套循环生成这些小于给定限制的三元组。对于每个三元组，检查毕达哥拉斯条件是否为真，如果为真，则打印该三元组。该解的时间复杂度为 O(极限 <sup>3</sup> )，其中“极限”为给定极限。

一个**高效的解决方案**可以在 O(k)时间内打印所有的三胞胎，其中 k 是打印的三胞胎数量。其思想是利用毕达哥拉斯三元组的平方和关系，即 a 和 b 的平方之和等于 c 的平方，我们可以用 m 和 n 来写这些数，这样，

```
       a = m2 - n2
       b = 2 * m * n
       c  = m2 + n2
because,
       a2 = m4 + n4 – 2 * m2 * n2
       b2 = 4 * m2 * n2
       c2 = m4 + n4 + 2* m2 * n2
```

我们可以看到 a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>，所以我们可以迭代 m 和 n 来生成这些三元组，而不是迭代 a、b 和 c。

以下是上述想法的实现:

## C++

```
// C++ program to generate pythagorean
// triplets smaller than a given limit
#include <bits/stdc++.h>

// Function to generate pythagorean
// triplets smaller than limit
void pythagoreanTriplets(int limit)
{

    // triplet: a^2 + b^2 = c^2
    int a, b, c = 0;

    // loop from 2 to max_limitit
    int m = 2;

    // Limiting c would limit
    // all a, b and c
    while (c < limit) {

        // now loop on j from 1 to i-1
        for (int n = 1; n < m; ++n) {

            // Evaluate and print triplets using
            // the relation between a, b and c
            a = m * m - n * n;
            b = 2 * m * n;
            c = m * m + n * n;

            if (c > limit)
                break;

            printf("%d %d %d\n", a, b, c);
        }
        m++;
    }
}

// Driver Code
int main()
{
    int limit = 20;
    pythagoreanTriplets(limit);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate pythagorean
// triplets smaller than a given limit
import java.io.*;
import java.util.*;

class GFG {

    // Function to generate pythagorean
    // triplets smaller than limit
    static void pythagoreanTriplets(int limit)
    {

        // triplet: a^2 + b^2 = c^2
        int a, b, c = 0;

        // loop from 2 to max_limitit
        int m = 2;

        // Limiting c would limit
        // all a, b and c
        while (c < limit) {

            // now loop on j from 1 to i-1
            for (int n = 1; n < m; ++n) {
                // Evaluate and print
                // triplets using
                // the relation between
                // a, b and c
                a = m * m - n * n;
                b = 2 * m * n;
                c = m * m + n * n;

                if (c > limit)
                    break;

                System.out.println(a + " " + b + " " + c);
            }
            m++;
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int limit = 20;
        pythagoreanTriplets(limit);
    }
}

// This code is contributed by Manish.
```

## 蟒蛇 3

```
# Python3 program to generate pythagorean
# triplets smaller than a given limit

# Function to generate pythagorean
# triplets smaller than limit
def pythagoreanTriplets(limits) :
    c, m = 0, 2

    # Limiting c would limit
    # all a, b and c
    while c < limits :

        # Now loop on n from 1 to m-1
        for n in range(1, m) :
            a = m * m - n * n
            b = 2 * m * n
            c = m * m + n * n

            # if c is greater than
            # limit then break it
            if c > limits :
                break

            print(a, b, c)

        m = m + 1

# Driver Code
if __name__ == '__main__' :

    limit = 20
    pythagoreanTriplets(limit)

# This code is contributed by Shrikant13.
```

## C#

```
// C# program to generate pythagorean
// triplets smaller than a given limit
using System;

class GFG {

    // Function to generate pythagorean
    // triplets smaller than limit
    static void pythagoreanTriplets(int limit)
    {

        // triplet: a^2 + b^2 = c^2
        int a, b, c = 0;

        // loop from 2 to max_limitit
        int m = 2;

        // Limiting c would limit
        // all a, b and c
        while (c < limit) {

            // now loop on j from 1 to i-1
            for (int n = 1; n < m; ++n)
            {

                // Evaluate and print
                // triplets using
                // the relation between
                // a, b and c
                a = m * m - n * n;
                b = 2 * m * n;
                c = m * m + n * n;

                if (c > limit)
                    break;

                Console.WriteLine(a + " "
                            + b + " " + c);
            }
            m++;
        }
    }

    // Driver Code
    public static void Main()
    {
        int limit = 20;
        pythagoreanTriplets(limit);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate pythagorean
// triplets smaller than a given limit

// Function to generate pythagorean
// triplets smaller than limit
function pythagoreanTriplets($limit)
{

    // triplet: a^2 + b^2 = c^2
    $a;
    $b;
    $c=0;

    // loop from 2 to max_limitit
    $m = 2;

    // Limiting c would limit
    // all a, b and c
    while ($c < $limit)
    {

        // now loop on j from 1 to i-1
        for ($n = 1; $n < $m; ++$n)
        {

            // Evaluate and print
            // triplets using the
            // relation between a,
            // b and c
            $a = $m *$m - $n * $n;
            $b = 2 * $m * $n;
            $c = $m * $m + $n * $n;

            if ($c > $limit)
                break;

            echo $a, " ", $b, " ", $c, "\n";
        }
        $m++;
    }
}

    // Driver Code
    $limit = 20;
    pythagoreanTriplets($limit);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to generate pythagorean
// triplets smaller than a given limit

// Function to generate pythagorean
// triplets smaller than limit
function pythagoreanTriplets(limit)
{

    // Triplet: a^2 + b^2 = c^2
    let a, b, c = 0;

    // Loop from 2 to max_limitit
    let m = 2;

    // Limiting c would limit
    // all a, b and c
    while (c < limit)
    {

        // Now loop on j from 1 to i-1
        for(let n = 1; n < m; ++n)
        {

            // Evaluate and print
            // triplets using
            // the relation between
            // a, b and c
            a = m * m - n * n;
            b = 2 * m * n;
            c = m * m + n * n;

            if (c > limit)
                break;

            document.write(a + " " + b +
                               " " + c + "</br>");
        }
        m++;
    }
}

// Driver code
let limit = 20;
pythagoreanTriplets(limit);

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
3 4 5
8 6 10
5 12 13
15 8 17
12 16 20
```

这种方法的时间复杂度是 O(k)，其中 k 是给定限制下打印的三元组的数量(我们只迭代 m 和 n，每次迭代打印一个三元组)

**注意:**上述方法不会生成所有小于给定限制的三胞胎。例如“9 12 15”是一个有效的三元组，用上述方法不能打印。感谢希德·阿格沃尔指出这一点。
**参考文献:**

本文由 [**乌卡什·特里维迪**](https://www.linkedin.com/pub/utkarsh-trivedi/a7/69/253) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息