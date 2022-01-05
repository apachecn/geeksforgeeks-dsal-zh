# 三个随机选择的数字出现在 AP 中的概率

> 原文:[https://www . geesforgeks . org/概率-三-随机选择-数字-ap/](https://www.geeksforgeeks.org/probability-three-randomly-chosen-numbers-ap/)

给定一个数字 **n** 和一个包含 1 到(2n+1)个连续数字的数组。随机选择三个元素。找出所选元素出现在
**中的概率** :

```
Input : n = 2
Output : 0.4
The array would be {1, 2, 3, 4, 5}
Out of all elements, triplets which 
are in AP: {1, 2, 3}, {2, 3, 4}, 
{3, 4, 5}, {1, 3, 5}
No of ways to choose elements from 
the array: 10 (5C3) 
So, probability = 4/10 = 0.4

Input : n = 5
Output : 0.1515
```

从(2n+1)个数字中选择任意 3 个数字的方法有:**<sup>(2n+1)</sup>C<sub>3</sub>**
现在，对于要在 AP 中的数字:
同差 1—{1，2，3}、{2，3，4}、{3，4，5}……{2n-1，2n，2n+1}
同差 2—{1，3，5 }、{ 2，4，6}、{3，5 (2n + 1)数中 3 个数的 AP 组总数为:
(2n–1)+(2n–3)+(2n–5)+…+3+1 =**n * n**([前 n 个奇数之和为 n * n](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/) )
所以，(2n+1)连续数中 3 个随机选择的数在 AP 中的概率= (n * n) / <sup>(2n + 1)</sup> C <sub>3</sub>

## C++

```
// CPP program to find probability that
// 3 randomly chosen numbers form AP.
#include <bits/stdc++.h>
using namespace std;

// function to calculate probability
double procal(int n)
{
    return (3.0 * n) / (4.0 * (n * n) - 1);
}

// Driver code to run above function
int main()
{
    int a[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(a)/sizeof(a[0]);
    cout << procal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find probability that
// 3 randomly chosen numbers form AP.

class GFG {

    // function to calculate probability
    static double procal(int n)
    {
        return (3.0 * n) / (4.0 * (n * n) - 1);
    }

    // Driver code to run above function
    public static void main(String arg[])
    {
        int a[] = { 1, 2, 3, 4, 5 };
        int n = a.length;
        System.out.print(Math.round(procal(n) * 1000000.0) / 1000000.0);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find probability that
# 3 randomly chosen numbers form AP.

# Function to calculate probability
def procal(n):

    return (3.0 * n) / (4.0 * (n * n) - 1)

# Driver code
a = [1, 2, 3, 4, 5]
n = len(a)
print(round(procal(n), 6))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find probability that
// 3 randomly chosen numbers form AP.
using System;

class GFG {

    // function to calculate probability
    static double procal(int n)
    {
        return (3.0 * n) / (4.0 * (n * n) - 1);
    }

    // Driver code
    public static void Main()
    {
        int []a = { 1, 2, 3, 4, 5 };
        int n = a.Length;
        Console.Write(Math.Round(procal(n) *
                    1000000.0) / 1000000.0);
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find probability that
// 3 randomly chosen numbers form AP.

// function to calculate probability
function procal($n)
{
    return (3.0 * $n) /
           (4.0 * ($n *
              $n) - 1);
}

    // Driver code
    $a = array(1, 2, 3, 4, 5);
    $n = sizeof($a);
    echo procal($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// Javascript program to find probability that
// 3 randomly chosen numbers form AP.

// function to calculate probability
function procal(n)
{
    return (3.0 * n) /
           (4.0 * (n *
              n) - 1);
}

    // Driver code
    let a = [1, 2, 3, 4, 5];
    let n = a.length;
    document.write(procal(n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
0.151515
```

时间复杂度:O(1)