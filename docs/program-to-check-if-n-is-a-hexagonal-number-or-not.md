# 程序检查 N 是否为六边形数字

> 原文:[https://www . geesforgeks . org/program-to-check-if-n-is-a-hexagon-number-or-not/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-hexagonal-number-or-not/)

给定一个**号 N** ，检查是否为[六边形](https://www.geeksforgeeks.org/hexagonal-number/)。如果是，则打印“是”，否则输出“否”。

**示例:**

> **输入:** N = 6
> **输出:**是
> **说明:**
> 6 是第二个六边形数。
> 
> **输入:** N = 14
> **输出:**否
> **说明:**
> 第二个六边形数为 6，第三个六边形数为 15。因此 14 不是一个六边形数字。

**方法:**为了解决上面提到的问题，我们必须注意到**第 n 个六边形数**由公式给出:**H(n)= n *(2n–1)**。公式表明，第 N 个六边形数二次依赖于 N，因此，求 N = H(n)方程的正整数根。

因此，H(n) =第 N 个六边形数，N 是给定的数。因此求解以下方程:

> 这里，H(N)= N
> =>N *(2n–1)= N
> =>2 * N * N–N–N = 0
> 这个方程的正根是:
> n = (1 + sqrt(8 N + 1)) / 4

获取 n 的值后，如果**n–floor(n)为 0，检查是否为整数，其中 n 为整数。**

下面是上述方法的实现:

## C++

```
// C++ Program to check
// if N is a Hexagonal Number

#include <bits/stdc++.h>
using namespace std;

// Function to check
// if number is hexagonal
bool isHexagonal(int N)
{
    float val = 8 * N + 1;

    float x = 1 + sqrt(val);

    // Calculate the value for n
    float n = (x) / 4;

    // Check if n - floor(n)
    // is equal to 0
    if ((n - (int)n) == 0)
        return true;

    else
        return false;
}

// Driver code
int main()
{
    int N = 14;

    if (isHexagonal(N) == true)
        cout << "Yes" << endl;

    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// if N is a hexagonal number
import java.util.*;

class GFG {

// Function to check
// if number is hexagonal
static boolean isHexagonal(int N)
{
    float val = 8 * N + 1;

    float x = 1 + (float)Math.sqrt(val);

    // Calculate the value for n
    float n = (x) / 4;

    // Check if n - floor(n)
    // is equal to 0
    if ((n - (int)n) == 0)
        return true;

    else
        return false;
}

// Driver code
public static void main(String[] args)
{
    int N = 14;

    if (isHexagonal(N) == true)
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to check
# if N is a hexagonal number
from math import sqrt

# Function to check
# if number is hexagonal
def isHexagonal(N):

    val = 8 * N + 1
    x = 1 + sqrt(val)

    # Calculate the value for n
    n = x / 4

    # Check if n - floor(n)
    # is equal to 0
    if ((n - int(n)) == 0):
        return True
    else:
        return False

# Driver code
if __name__ == '__main__':

    N = 14

    if (isHexagonal(N) == True):
        print("Yes")
    else:
        print("No")

# This code is contributed by BhupendraSingh
```

## C#

```
// C# program to check if
// N is a hexagonal number
using System;

class GFG{

// Function to check
// if number is hexagonal
static bool isHexagonal(int N)
{
    float val = 8 * N + 1;
    float x = 1 + (float)Math.Sqrt(val);

    // Calculate the value for n
    float n = (x) / 4;

    // Check if n - floor(n)
    // is equal to 0
    if ((n - (int)n) == 0)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver code
public static void Main(string[] args)
{
    int N = 14;

    if (isHexagonal(N) == true)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to check
// if N is a hexagonal number

// Function to check
// if number is hexagonal
function isHexagonal(N)
{
    let val = 8 * N + 1;
    let x = 1 + Math.sqrt(val);

    // Calculate the value for n
    let n = (x) / 4;

    // Check if n - floor(n)
    // is equal to 0
    if ((n - parseInt(n)) == 0)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver code
let N = 14;

if (isHexagonal(N) == true)
{
    document.write("Yes" + "</br>");
}
else
{
    document.write("No");
}

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
No
```

***时间复杂度:** O(1)*