# 蛋糕分配问题

> 原文:[https://www.geeksforgeeks.org/cake-distribution-problem/](https://www.geeksforgeeks.org/cake-distribution-problem/)

给定两个整数 **N** 和 **M** ，其中 N 是以顺时针方式坐在一个圈里的朋友数，M 是蛋糕数。任务是计算将 **i** 蛋糕分发给**I**朋友后剩下的蛋糕数量。如果蛋糕的数量少于所需数量，蛋糕的分发将停止。
**举例:**

> **输入:** N = 4，M = 11
> **输出:** 0
> 第一轮:
> 第一个朋友得到 1 个蛋糕，第二个得到 2 个蛋糕，
> 第三个得到 3 个，第四个得到 4 个蛋糕。
> 剩余蛋糕= 11 –( 1+2+3+4)= 1
> 第二轮:
> 这次只有 1 号朋友拿到剩下的 1 个蛋糕。
> 剩余蛋糕= 1–1 = 0
> **输入:** N = 3，M = 8
> **输出:** 1
> 第一轮:
> 第一个朋友得到 1 个蛋糕，第二个得到 2 个蛋糕，
> 第三个得到 3 个蛋糕。
> 剩余蛋糕= 8 –( 1+2+3)= 2
> 第二轮:
> 这次只有第一个朋友拿到剩下的 1 个蛋糕，
> 然后第二个朋友就没有蛋糕了。
> 剩余蛋糕= 2–1 = 1

**进场:**

*   从 m 个蛋糕中检查蛋糕的分发周期。
*   计算 1 个周期的蛋糕数量

```
sum = n * (n + 1) / 2
```

*   现在通过求和得到循环数+一些余数。
*   现在检查还有多少剩余的蛋糕可以分发给 x 个朋友。
*   通过求解二次方程
    可以很容易地得到 x 的值

```
remainder = x * (x + 1) / 2
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the
// remaining count of cakes
int cntCakes(int n, int m)
{

    // Sum for 1 cycle
    int sum = (n * (n + 1)) / 2;

    // no. of full cycle and remainder
    int quo = m/sum ;
    int rem = m % sum ;
    double ans = m - quo * sum ;

    double x = (-1 + pow((8 * rem) + 1, 0.5)) / 2;

    ans = ans - x * (x + 1) / 2;

    return int(ans);
}

// Driver Code
int main ()
{
    int n = 3;
    int m = 8;
    int ans = cntCakes(n, m);
    cout << (ans);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the
    // remaining count of cakes
    static int cntCakes(int n, int m)
    {

        // Sum for 1 cycle
        int sum = (n * (n + 1)) / 2;

        // no. of full cycle and remainder
        int quo = m/sum ;
        int rem = m % sum ;
        double ans = m - quo * sum ;

        double x = (-1 + Math.pow((8 * rem) + 1, 0.5)) / 2;

        ans = ans - x * (x + 1) / 2;

        return (int)ans;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 3;
        int m = 8;
        int ans = cntCakes(n, m);
        System.out.println(ans);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# remaining count of cakes
def cntCakes(n, m):

    # Sum for 1 cycle
    sum = (n*(n + 1))//2

    # no. of full cycle and remainder
    quo, rem = m//sum, m % sum
    ans = m - quo * sum

    x = int((-1 + (8 * rem + 1)**0.5)/2)
    ans = ans - x*(x + 1)//2

    return ans

# Driver code
def main():
  n = 4
  m = 11
  ans = cntCakes(n, m)
  print(ans)

main()
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the
    // remaining count of cakes
    static int cntCakes(int n, int m)
    {

        // Sum for 1 cycle
        int sum = (n * (n + 1)) / 2;

        // no. of full cycle and remainder
        int quo = m/sum ;
        int rem = m % sum ;
        double ans = m - quo * sum ;

        double x = (-1 + Math.Pow((8 * rem) + 1, 0.5)) / 2;

        ans = ans - x * (x + 1) / 2;

        return (int)ans;
    }

    // Driver Code
    static public void Main ()
    {
        int n = 3;
        int m = 8;
        int ans = cntCakes(n, m);
        Console.Write(ans);
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the
    // remaining count of cakes
    function cntCakes(n, m)
    {

        // Sum for 1 cycle
        let sum = (n * (n + 1)) / 2;

        // no. of full cycle and remainder
        let quo = m/sum;
        let rem = m % sum ;
        let ans = m - quo * sum + 6;

        let x = (-1 + Math.pow((8 * rem) + 1, 0.5));

        ans = ans - x * (x + 1) / 2;

        return parseInt(ans, 10);
    }

    let n = 3;
    let m = 8;
    let ans = cntCakes(n, m);
    document.write(ans);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(1)