# 将 2N 位数之和减为一位数得到的数

> 原文:[https://www . geesforgeks . org/number-通过将 2n 位数之和减少为一位数获得/](https://www.geeksforgeeks.org/number-obtained-by-reducing-sum-of-digits-of-2n-into-a-single-digit/)

给定一个正整数 **N** ，任务是找到[递归](https://www.geeksforgeeks.org/recursion/)将 **2 <sup>N</sup>** 的位数相加后得到的一位数，直到剩下一位数。

**示例:**

> **输入:** N = 6
> **输出:** 1
> **解释:**
> 2 <sup>6</sup> = 64。位数之和= 10。
> 现在，位数之和= 10。因此，总和为 1。
> 
> **输入:** N = 10
> **输出:** 7
> **解释:** 2 <sup>10</sup> = 1024。位数之和= 7。

**天真法:**解决问题最简单的方法是计算 2 <sup>N</sup> 的值，然后，继续计算数字的[位数之和](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)，直到总和减少到一位数。

***时间复杂度:**O(log(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

对 **N** 的不同值进行运算后，可以观察到该值以如下方式每 6 个数重复一次:

*   如果 **N % 6 = 0，**则一位数之和等于 1。
*   如果 **N % 6 = 1，**则一位数之和等于 2。
*   如果 **N % 6 = 2，**则一位数之和等于 4。
*   如果 **N % 6 = 3，**则一位数之和等于 8。
*   如果 **N % 6 = 4，**则一位数之和等于 7。
*   如果 **N % 6 = 5，**则一位数之和等于 5。

按照以下步骤解决问题:

*   如果 **N % 6** 为 **0** ，则打印 **1** 。
*   否则，如果 **N % 6** 为 **1** ，则打印 **2** 。
*   否则，如果 **N % 6** 为 **2** ，则打印 **7** 。
*   否则，如果 **N % 6** 为 **3** ，则打印 **8** 。
*   否则，如果 **N % 6** 为 **4** ，则打印 **7** 。
*   否则，如果 **N % 6** 为 **5** ，则打印 **5** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number obtained
// by reducing sum of digits of 2 ^ N
// into a single digit
int findNumber(int N)
{
    // Stores answers for
    // different values of N
    int ans[6] = { 1, 2, 4, 8, 7, 5 };

    return ans[N % 6];
}

// Driver Code
int main()
{
    int N = 6;
    cout << findNumber(N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the number obtained
// by reducing sum of digits of 2 ^ N
// into a single digit
static int findNumber(int N)
{

    // Stores answers for
    // different values of N
    int []ans = {1, 2, 4, 8, 7, 5};

    return ans[N % 6];
}

// Driver Code
public static void main(String args[])
{
    int N = 6;

    System.out.println(findNumber(N));
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number obtained
# by reducing sum of digits of 2 ^ N
# into a single digit
def findNumber(N):

    # Stores answers for
    # different values of N
    ans = [ 1, 2, 4, 8, 7, 5 ]

    return ans[N % 6]

# Driver Code
if __name__ == "__main__":

    N = 6

    print (findNumber(N))

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the number obtained
// by reducing sum of digits of 2 ^ N
// into a single digit
static int findNumber(int N)
{

    // Stores answers for
    // different values of N
    int []ans = {1, 2, 4, 8, 7, 5};

    return ans[N % 6];
}

// Driver Code
public static void Main()
{
    int N = 6;

    Console.WriteLine(findNumber(N));
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the number obtained
// by reducing sum of digits of 2 ^ N
// into a single digit
function findNumber(N)
{

    // Stores answers for
    // different values of N
    let ans = [ 1, 2, 4, 8, 7, 5 ];
    return ans[N % 6];
}

// Driver Code
    let N = 6;
    document.write(findNumber(N) + "<br>");

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)