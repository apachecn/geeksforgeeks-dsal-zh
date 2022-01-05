# 服从数字

> 原文:[https://www.geeksforgeeks.org/amenable-numbers/](https://www.geeksforgeeks.org/amenable-numbers/)

给定一个数字 **N** ，任务是检查 N 是否是一个**服从数字**。如果 N 是一个服从的数字，那么打印**“是”**否则打印**“否”**。

> 如果存在大小、总和和乘积等于数的多组整数，则服从数就是数。
> 例如，8 是一个顺从数，因为有一组整数{-1，-1，1，1，1，1，2，4}的大小、和与积是 8。

**例:**

> **输入:** N = 8
> **输出:**是
> **解释:**
> 8 是一个服从数，因为有一组整数{-1，-1，1，1，1，1，2，4}的大小，和与积是 8。
> **输入:** N = 30
> **输出:**否
> **说明:**
> 30 不是一个顺从数，因为不存在大小、和、积为 30 的多组整数。

**方法:**
前几个服从的数字是 **1，5，8，9，12，13，16，17，20，21…..**可表示为形式 **4K 或 4K + 1** 。
因此，任何形式的数字 N**4K 或 4K + 1** 都是服从的数字。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N
// is Amenable number
bool isAmenableNum(int N)
{

    // Return true if N is of the form
    // 4K or 4K + 1
    return (N % 4 == 0
            || (N - 1) % 4 == 0);
}

// Driver Code
int main()
{
    // Given Number
    int n = 8;

    // Function Call
    if (isAmenableNum(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if N
// is Amenable number
static boolean isAmenableNum(int N)
{

    // Return true if N is of the form
    // 4K or 4K + 1
    return (N % 4 == 0 || (N - 1) % 4 == 0);
}

// Driver code
public static void main(String[] args)
{
    int n = 8;

    if (isAmenableNum(n))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if N
# is Amenable number
def isAmenableNum(N):

    # Return true if N is of the
    # form 4K or 4K + 1
    return (N % 4 == 0 or
           (N - 1) % 4 == 0);

# Driver code

# Given number
N = 8;

# Function call
if (isAmenableNum(N)):
    print("Yes");
else:
    print("No");

# This code is contributed by rock_cool
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if N
// is Amenable number
static bool isAmenableNum(int N)
{

    // Return true if N is of the form
    // 4K or 4K + 1
    return (N % 4 == 0 || (N - 1) % 4 == 0);
}

// Driver code
public static void Main(String[] args)
{
    int n = 8;

    if (isAmenableNum(n))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    // Function to check if N
    // is Amenable number
    function isAmenableNum( N)
    {

        // Return true if N is of the form
        // 4K or 4K + 1
        return (N % 4 == 0 || (N - 1) % 4 == 0);
    }

    // Driver code
    let n = 8;

    if (isAmenableNum(n)) {
        document.write("Yes");
    } else {
        document.write("No");
    }

// This code is contributed by Rajput-Ji.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*