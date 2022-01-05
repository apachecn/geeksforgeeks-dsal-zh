# 给定和的毕达哥拉斯三元组

> 原文:[https://www . geesforgeks . org/毕达哥拉斯-三元组-给定-总和/](https://www.geeksforgeeks.org/pythagorean-triplet-given-sum/)

A [毕达哥拉斯三元组](https://www.geeksforgeeks.org/find-pythagorean-triplet-in-an-unsorted-array/)是一组自然数，如 a < b < c，其中 **a^2 + b^2 = c^2** 。例如，3^2 + 4^2 = 5^2.
给定一个数 n，求一个和为 n 的勾股三元组
**例:**

```
Input : n = 12
Output : 3, 4, 5
Note that 3, 4 and 5 is a Pythagorean Triplet
with sum equal to 12.

Input : n = 4.
Output : No Triplet
There does not exist a Pythagorean Triplet
with sum equal to 4.
```

一个**简单的解决方案**是运行三个嵌套循环来生成所有可能的三元组，并且对于每个三元组，检查它是否是毕达哥拉斯三元组并且已经给出了总和。这个解的时间复杂度为 O(n <sup>3</sup> )。
一个**有效的解决方案**是运行两个循环，其中第一个循环从 i = 1 运行到 n/3，第二个循环从 j = i+1 运行到 n/2。在第二个循环中，我们检查(n–I–j)是否等于 i * i + j * j.

## C++

```
// C++ program to find Pythagorean
// Triplet of given sum.
#include <bits/stdc++.h>
using namespace std;

void pythagoreanTriplet(int n)
{
    // Considering triplets in
    // sorted order. The value
    // of first element in sorted
    // triplet can be at-most n/3.
    for (int i = 1; i <= n / 3; i++)
    {

        // The value of second
        // element must be less
        // than equal to n/2
        for (int j = i + 1; j <= n / 2; j++)
        {
            int k = n - i - j;
            if (i * i + j * j == k * k)
            {
                cout << i << ", "
                     << j << ", "
                     << k;
                return;
            }
        }
    }

    cout << "No Triplet";
}

// Driver Code
int main()
{
    int n = 12;
    pythagoreanTriplet(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Pythagorean 
// Triplet of given sum.
class GFG
{
    static void pythagoreanTriplet(int n)
    {

        // Considering triplets in
        // sorted order. The value
        // of first element in sorted
        // triplet can be at-most n/3.
        for (int i = 1; i <= n / 3; i++)
        {

            // The value of second element
            // must be less than equal to n/2
            for (int j = i + 1; j <= n / 2; j++)
            {
                int k = n - i - j;
                if (i * i + j * j == k * k)
                {
                    System.out.print(i + ", "+
                                j + ", " + k);
                    return;
                }
            }
        }

        System.out.print("No Triplet");
    }

    // Driver Code
    public static void main(String arg[])
    {
        int n = 12;

        pythagoreanTriplet(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# Pythagorean Triplet of
# given sum.

def pythagoreanTriplet(n):

    # Considering triplets in
    # sorted order. The value
    # of first element in sorted
    # triplet can be at-most n/3.
    for i in range(1, int(n / 3) + 1):

        # The value of second element
        # must be less than equal to n/2
        for j in range(i + 1,
                       int(n / 2) + 1):

            k = n - i - j
            if (i * i + j * j == k * k):
                print(i, ", ", j, ", ",
                               k, sep = "")
                return

    print("No Triplet")

# Driver Code
n = 12
pythagoreanTriplet(n)

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// C# program to find 
// Pythagorean Triplet
// of given sum.
using System;

class GFG
{
    static void pythagoreanTriplet(int n)
    {

        // Considering triplets in
        // sorted order. The value
        // of first element in sorted
        // triplet can be at-most n/3.
        for (int i = 1; i <= n / 3; i++)
        {

            // The value of second element
            // must be less than equal to n/2
            for (int j = i + 1;
                     j <= n / 2; j++)
            {
                int k = n - i - j;
                if (i * i + j * j == k * k)
                {
                    Console.Write(i + ", "+
                                  j + ", " + k);
                    return;
                }
            }
        }

        Console.Write("No Triplet");
    }

    // Driver Code
    public static void Main()
    {
        int n = 12;

        pythagoreanTriplet(n);
    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find 
// Pythagorean Triplet
// of given sum.

function pythagoreanTriplet($n)
{
    // Considering triplets in
    // sorted order. The value
    // of first element in sorted
    // triplet can be at-most n/3.
    for ( $i = 1; $i <= $n / 3; $i++)
    {

        // The value of second
        // element must be less
        // than equal to n/2
        for ( $j = $i + 1; $j <= $n / 2; $j++)
        {
            $k = $n - $i - $j;
            if ($i * $i + $j * $j == $k * $k)
            {
                echo $i , ", ", $j ,", ", $k;
                return;
            }
        }
    }

    echo "No Triplet";
}

// Driver Code
$n = 12;
pythagoreanTriplet($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find Pythagorean 
// Triplet of given sum.

    function pythagoreanTriplet(n)
    {

        // Considering triplets in
        // sorted order. The value
        // of first element in sorted
        // triplet can be at-most n/3.
        for (let i = 1; i <= n / 3; i++)
        {

            // The value of second element
            // must be less than equal to n/2
            for (let j = i + 1; j <= n / 2; j++)
            {
                let k = n - i - j;
                if (i * i + j * j == k * k)
                {
                    document.write(i + ", "+
                                j + ", " + k);
                    return;
                }
            }
        }

        document.write("No Triplet");
    }

// Driver Code
        let n = 12;
        pythagoreanTriplet(n);

// This code is contributed by avijitmondal1998.
</script>
```

**Output :** 

```
3, 4, 5
```