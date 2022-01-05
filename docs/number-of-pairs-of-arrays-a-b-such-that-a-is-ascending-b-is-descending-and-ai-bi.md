# A 上升，B 下降，A[i] ≤ B[i]

的阵列对(A，B)的数量

> 原文:[https://www . geeksforgeeks . org/数组对数-a-B-这样-a 是升序-b 是降序-ai-bi/](https://www.geeksforgeeks.org/number-of-pairs-of-arrays-a-b-such-that-a-is-ascending-b-is-descending-and-ai-bi/)

给定两个整数 **N** 和 **M** ，任务是找到数组对 **(A，B)** 的数量，使得数组 **A** 和 **B** 都是大小为 **M** 的数组，其中 **A** 和 **B** 的每个条目都是介于 **1** 和 **N** 之间的整数并给出数组 **A** 按**非降序**排序， **B** 按**非升序**排序。由于答案可能很大，返回答案取模 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** N = 2，M = 2
> **输出:** 5
> 1: A= [1，1] B=[1，1]
> 2: A= [1，1] B=[1，2]
> 3: A= [1，1] B=[2，2]
> 4: A= [1，2] B=[2，2]
> 5: A= [2，2] B=[2，2]
> 
> **输入:** N = 5，M = 3
> T3】输出: 210

**方法:**请注意，如果有一对有效的数组 A 和 B，并且如果 B 连接在 A 之后，则得到的数组将总是大小为 2 * M 的升序或非降序数组。(A + B)的每个元素都将在 1 和 N 之间(不一定必须使用 1 和 N 之间的所有元素)。现在，这只是将给定的问题转化为寻找所有可能的大小组合 **2 * M** ，其中每个元素在 1 到 N 之间(允许重复)，其公式为**T5】2 * M+N–1C<sub>N–1</sub>T9】或(2 * M+N–1)！/ ((2 * M)！*(N–1)！).**

下面是上述方法的实现:

## C++

```
// C++ code of above approach
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

long long fact(long long n)
{
    if(n == 1)
        return 1;
    else
        return (fact(n - 1) * n) % mod;
}

// Function to return the count of pairs
long long countPairs(int m, int n)
{
    long long ans = fact(2 * m + n - 1) /
                    (fact(n - 1) * fact(2 * m));
    return (ans % mod);
}

// Driver code
int main()
{
    int n = 5, m = 3;
    cout << (countPairs(m, n));
    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code of above approach
class GFG
{
    final static long mod = 1000000007 ;

    static long fact(long n)
    {
        if(n == 1)
            return 1;
        else
            return (fact(n - 1) * n) % mod;
    }

    // Function to return the count of pairs
    static long countPairs(int m, int n)
    {
        long ans = fact(2 * m + n - 1) /
                   (fact(n - 1) * fact(2 * m));

        return (ans % mod);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5, m = 3;

        System.out.println(countPairs(m, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import factorial as fact

# Function to return the count of pairs
def countPairs(m, n):
    ans = fact(2 * m + n-1)//(fact(n-1)*fact(2 * m))
    return (ans %(10**9 + 7))

# Driver code
n, m = 5, 3
print(countPairs(m, n))
```

## C#

```
// C# code of above approach
using System;

class GFG
{
    static long mod = 1000000007 ;

    static long fact(long n)
    {
        if(n == 1)
            return 1;
        else
            return (fact(n - 1) * n) % mod;
    }

    // Function to return the count of pairs
    static long countPairs(int m, int n)
    {
        long ans = fact(2 * m + n - 1) /
                (fact(n - 1) * fact(2 * m));

        return (ans % mod);
    }

    // Driver code
    public static void Main()
    {
        int n = 5, m = 3;

        Console.WriteLine(countPairs(m, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript code of above approach
var mod = 1000000007

function fact(n)
{
    if (n == 1)
        return 1;
    else
        return(fact(n - 1) * n) % mod;
}

// Function to return the count of pairs
function countPairs(m, n)
{
    var ans = fact(2 * m + n - 1) /
            (fact(n - 1) * fact(2 * m));
    return (ans % mod);
}

// Driver code
var n = 5, m = 3;

document.write(countPairs(m, n));

// This code is contributed by famously

</script>
```

**Output:** 

```
210
```

**时间复杂度:**O(n+m)
T3】辅助空间 : O(max(n，m))。