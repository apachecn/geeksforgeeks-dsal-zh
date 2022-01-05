# 求 N 与自身异或的值 K 次

> 原文:[https://www . geeksforgeeks . org/find-n-xored-to-自身-k-times/](https://www.geeksforgeeks.org/find-the-value-of-n-xored-to-itself-k-times/)

给定两个整数 **N** 和 **K** ，任务是求 **N 异或 N 异或 N …异或 N (K 次)**的值。

**示例:**

> **输入:** N = 123，K = 3
> **输出:**123
> (123 ^ 123 ^ 123)= 123
> **输入:** N = 123，K = 2
> **输出:** 0
> (123 ^ 123) = 0

**天真的做法:**简单地运行一个 for 循环，并异或 N，K 次。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return n ^ n ^ ... k times
int xorK(int n, int k)
{

    // Find the result
    int res = n;
    for (int i = 1; i < k; i++)
        res = (res ^ n);
    return res;
}

// Driver code
int main()
{
    int n = 123, k = 3;

    cout << xorK(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return n ^ n ^ ... k times
static int xorK(int n, int k)
{

    // Find the result
    int res = n;
    for (int i = 1; i < k; i++)
        res = (res ^ n);
    return n;
}

// Driver code
public static void main(String[] args)
{
    int n = 123, k = 3;

    System.out.print(xorK(n, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return n ^ n ^ ... k times
def xorK(n, k):

    # Find the result
    res = n
    for i in range(1, k):
        res = (res ^ n)
    return n

# Driver code
n = 123
k = 3

print(xorK(n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return n ^ n ^ ... k times
static int xorK(int n, int k)
{

    // Find the result
    int res = n;
    for (int i = 1; i < k; i++)
        res = (res ^ n);
    return n;
}

// Driver code
static public void Main ()
{
    int n = 123, k = 3;

    Console.Write(xorK(n, k));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// JavaSCript implementation of the approach

// Function to return n ^ n ^ ... k times
function xorK(n, k)
{

    // Find the result
    let res = n;
    for (let i = 1; i < k; i++)
        res = (res ^ n);
    return n;
}

// Driver code

    let n = 123, k = 3;

    document.write(xorK(n, k));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
123
```

**时间复杂度:**O(K)
T3】空间复杂度: O(1)

**有效方法:**从属性 **X XOR X = 0** 和 **X ^ 0 = X** 可以观察到，当 **K 为奇数**时，答案将是 **N** 本身，否则答案将是 **0** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return n ^ n ^ ... k times
int xorK(int n, int k)
{

    // If k is odd the answer is
    // the number itself
    if (k % 2 == 1)
        return n;

    // Else the answer is 0
    return 0;
}

// Driver code
int main()
{
    int n = 123, k = 3;

    cout << xorK(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return n ^ n ^ ... k times
static int xorK(int n, int k)
{

    // If k is odd the answer is
    // the number itself
    if (k % 2 == 1)
        return n;

    // Else the answer is 0
    return 0;
}

// Driver code
public static void main(String[] args)
{
    int n = 123, k = 3;

    System.out.print(xorK(n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return n ^ n ^ ... k times
def xorK(n, k):

    # If k is odd the answer is
    # the number itself
    if (k % 2 == 1):
        return n

    # Else the answer is 0
    return 0

# Driver code
n = 123
k = 3

print(xorK(n, k))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return n ^ n ^ ... k times
static int xorK(int n, int k)
{

    // If k is odd the answer is
    // the number itself
    if (k % 2 == 1)
        return n;

    // Else the answer is 0
    return 0;
}

// Driver code
public static void Main(String[] args)
{
    int n = 123, k = 3;

    Console.Write(xorK(n, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return n ^ n ^ ... k times
    function xorK(n, k)
    {

        // If k is odd the answer is
        // the number itself
        if (k % 2 == 1)
            return n;

        // Else the answer is 0
        return 0;
    }

    let n = 123, k = 3;

    document.write(xorK(n, k));

</script>
```

**Output:** 

```
123
```

**时间复杂度:**O(1)
T3】空间复杂度: O(1)