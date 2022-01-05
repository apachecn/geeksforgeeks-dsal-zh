# 检查浮点值是否等于整数值

> 原文:[https://www . geesforgeks . org/check-如果浮点值等于整数值/](https://www.geeksforgeeks.org/check-if-a-float-value-is-equivalent-to-an-integer-value/)

给定一个[浮点数](https://en.wikipedia.org/wiki/Floating-point_arithmetic) **N** ，任务是检查 **N** 的值是否等于一个[整数](https://en.wikipedia.org/wiki/Integer)。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**N = 1.5
> T3】输出:否
> 
> **输入:**N = 1.0
> T3】输出:是

**做法:**思路是采用[式铸造](https://www.geeksforgeeks.org/type-conversion-in-c/)的概念。按照以下步骤解决问题:

*   初始化一个变量，比如说 **X** ，来存储 **N** 的整数值。
*   [将 **N** 的数值浮点值转换为整数](https://www.geeksforgeeks.org/how-to-convert-float-to-int-in-python/)存储在 **X** 中。
*   最后，检查**(N–X)>0**是否存在。如果发现属实，则打印**“否”**。
*   否则，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if N is
// equivalent to an integer
bool isInteger(double N)
{

    // Convert float value
    // of N to integer
    int X = N;

    double temp2 = N - X;

    // If N is not equivalent
    // to any integer
    if (temp2 > 0) {
        return false;
    }
    return true;
}

// Driver Code
int main()
{
    double N = 1.5;

    if (isInteger(N)) {

        cout << "YES";
    }
    else {

        cout << "NO";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to check if N is
// equivalent to an integer
static boolean isInteger(double N)
{

    // Convert float value
    // of N to integer
    int X = (int)N;
    double temp2 = N - X;

    // If N is not equivalent
    // to any integer
    if (temp2 > 0)
    {
        return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    double N = 1.5;
    if (isInteger(N))
    {
        System.out.println("YES");
    }
    else
    {
        System.out.println("NO");
    }
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if N is
# equivalent to an integer
def isInteger(N):

    # Convert float value
    # of N to integer
    X = int(N)

    temp2 = N - X

    # If N is not equivalent
    # to any integer
    if (temp2 > 0):
        return False

    return True

# Driver Code
if __name__ == '__main__':

    N = 1.5

    if (isInteger(N)):
        print("YES")
    else:
        print("NO")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if N is
// equivalent to an integer
static bool isint(double N)
{

    // Convert float value
    // of N to integer
    int X = (int)N;

    double temp2 = N - X;

    // If N is not equivalent
    // to any integer
    if (temp2 > 0)
    {
        return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    double N = 1.5;

    if (isint(N))
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if N is
// equivalent to an integer
function isInteger(N)
{

    // Convert float value
    // of N to integer
    let X = Math.floor(N);
    let temp2 = N - X;

    // If N is not equivalent
    // to any integer
    if (temp2 > 0)
    {
        return false;
    }
    return true;
}

// driver function
    let N = 1.5;
    if (isInteger(N))
    {
        document.write("YES");
    }
    else
    {
        document.write("NO");
    }

 // This code is contributed by souravghosh0416.
</script>   
```

**Output:** 

```
NO
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)