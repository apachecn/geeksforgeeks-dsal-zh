# 如果步数是 2 的幂

，则计算走完一段距离的步数

> 原文:[https://www . geeksforgeeks . org/count-步数-覆盖一段距离-如果步数-可以采取-2 的幂/](https://www.geeksforgeeks.org/count-number-of-steps-to-cover-a-distance-if-steps-can-be-taken-in-powers-of-2/)

给定要走的距离 K，任务是找到走完这段距离所需的最小步数，如果步数可以是 2 的幂，如 1，2，4，8，16……..
**例:**

```
Input : K = 9
Output : 2

Input : K = 343 
Output : 6
```

所需的最小步长可以通过在每个步长中将 K 减少 2 的最高幂来计算，这可以通过计数一个数的二进制表示中的设置位数来获得。
以下是上述方法的实现:

## C++

```
// C++ program to count the minimum number of steps

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number of steps
int getMinSteps(int K)
{
   // __builtin_popcount() is a C++ function to
   // count the number of set bits in a number
   return __builtin_popcount(k);
}

// Driver Code
int main()
{
    int n = 343;

    cout << getMinSteps(n)<< '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count minimum number of steps
import java.io.*;

class GFG
{

    // Function to count the minimum number of steps
    static int getMinSteps(int K)
    {
        // count the number of set bits in a number
        return Integer.bitCount(K);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 343;

        System.out.println(getMinSteps(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to count the minimum number of steps
def getMinSteps(K) :

    # bin(K).count("1") is a Python3 function to
    # count the number of set bits in a number
    return bin(K).count("1")

# Driver Code
n = 343
print(getMinSteps(n))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# program to count minimum number of steps
using System;

class GFG
{

    // Function to count the minimum number of steps
    static int getMinSteps(int K)
    {
        // count the number of set bits in a number
        return countSetBits(K);
    }

    static int countSetBits(int x)
    {
        int setBits = 0;
        while (x != 0)
        {
            x = x & (x - 1);
            setBits++;
        }
        return setBits;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int n = 343;

        Console.WriteLine(getMinSteps(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to count minimum number of steps

    // Function to count the minimum number of steps
    function getMinSteps(K)
    {
        // count the number of set bits in a number
        return countSetBits(K);
    }

    function countSetBits(x)
    {
        let setBits = 0;
        while (x != 0)
        {
            x = x & (x - 1);
            setBits++;
        }
        return setBits;
    }

    let n = 343;

      document.write(getMinSteps(n));

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
6
```

**时间复杂度:** ![O(log(n))   ](img/0afc139c057223500739387f9a0f3f61.png "Rendered by QuickLaTeX.com")

**辅助空间:** O(1)