# N 个男孩围坐在圆桌旁的座位安排，两个特定的男孩坐在一起

> 原文:[https://www . geeksforgeeks . org/座位安排-n 个男孩围坐在圆桌旁-这样-两个特定的男孩坐在一起/](https://www.geeksforgeeks.org/seating-arrangement-of-n-boys-sitting-around-a-round-table-such-that-two-particular-boys-sit-together/)

有 **N** 个男孩围着一张圆桌坐着。任务是找到多少种方式让 **N** 男孩围坐在一张圆桌旁，让两个特别的男孩坐在一起。
**例:**

> **输入:** N = 5
> **输出:** 48
> 2 小子可以排成 2 个！方式和其他男生
> 可以排在(5–1)！(减去 1 是因为
> 之前选的两个男生现在会被认为是单身男生)
> 所以，合计方式是 2！* 4!= 48.
> **输入:** N = 9
> **输出:** 80640

**进场:**

*   第一，2 个男生可以排成 2 个！方法。
*   安排剩余男孩和前两个男孩配对的方法数量为(n–1)！。
*   所以，**总途径= 2！*(n–1)！**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the total count of ways
int Total_Ways(int n)
{

    // Find (n - 1) factorial
    int fac = 1;
    for (int i = 2; i <= n - 1; i++) {
        fac = fac * i;
    }

    // Return (n - 1)! * 2!
    return (fac * 2);
}

// Driver code
int main()
{
    int n = 5;

    cout << Total_Ways(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the total count of ways
static int Total_Ways(int n)
{

    // Find (n - 1) factorial
    int fac = 1;
    for (int i = 2; i <= n - 1; i++)
    {
        fac = fac * i;
    }

    // Return (n - 1)! * 2!
    return (fac * 2);
}

// Driver code
public static void main (String[] args)
{

    int n = 5;

    System.out.println (Total_Ways(n));
}
}

// This code is contributed by Tushil.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the total count of ways
def Total_Ways(n) :

    # Find (n - 1) factorial
    fac = 1;
    for i in range(2, n) :
        fac = fac * i;

    # Return (n - 1)! * 2!
    return (fac * 2);

# Driver code
if __name__ == "__main__" :

    n = 5;

    print(Total_Ways(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the total count of ways
static int Total_Ways(int n)
{

    // Find (n - 1) factorial
    int fac = 1;
    for (int i = 2; i <= n - 1; i++)
    {
        fac = fac * i;
    }

    // Return (n - 1)! * 2!
    return (fac * 2);
}

// Driver code
static public void Main ()
{
    int n = 5;

    Console.Write(Total_Ways(n));
}
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the total count of ways
    function Total_Ways(n)
    {

        // Find (n - 1) factorial
        var fac = 1;
        for (i = 2; i <= n - 1; i++)
        {
            fac = fac * i;
        }

        // Return (n - 1)! * 2!
        return (fac * 2);
    }

    // Driver code
        var n = 5;
        document.write(Total_Ways(n));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
48
```