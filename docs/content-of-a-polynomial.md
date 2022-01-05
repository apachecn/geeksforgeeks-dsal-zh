# 多项式的内容

> 原文:[https://www.geeksforgeeks.org/content-of-a-polynomial/](https://www.geeksforgeeks.org/content-of-a-polynomial/)

给定一个表示多项式整数系数的数组 **arr[]** ，任务是找到多项式的内容。

> 整系数多项式的内容定义为其整系数的最大公约数。
> 这是为了:
> 
> f(x)= a<sub>m</sub>x<sup>m</sup>+a<sub>m-1</sub>x<sup>m-1</sup>+……..+a <sub>1</sub> x + a <sub>0</sub>
> 然后，多项式的内容= gcd(a <sub>m</sub> ，a <sub>m-1</sub> ，a <sub>m-2</sub> …。，一个 <sub>1</sub> ，一个 <sub>0</sub>

**示例:**

> **输入:** arr[] = {9，30，12}
> **输出:** 3
> **解释:**
> 给定多项式可以是:9x <sup>2</sup> + 30x + 12
> 因此，Content = gcd(9，30，12) = 3
> 
> **输入:** arr[] = {2，4，6 }
> T3】输出: 2

**方法:**思路是寻找数组所有元素的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)，通过一次选择两个元素，反复寻找 GCD，就可以计算出来。那就是:

```
gcd(a, b, c)
 = gcd(gcd(a, b), c)
 = gcd(a, gcd(b, c))
 = gcd(gcd(a, c), b)
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// content of the polynomial

#include <bits/stdc++.h>
using namespace std;

#define newl "\n"
#define ll long long
#define pb push_back

// Function to find the content
// of the polynomial
int findContent(int arr[], int n)
{
    int content = arr[0];

    // Loop to iterate over the
    // elements of the array
    for (int i = 1; i < n; i++) {

        //__gcd(a, b) is a inbuilt
        // function for Greatest
        // Common Divisor
        content = __gcd(content, arr[i]);
    }

    return content;
}

// Driver Code
int main()
{
    int n = 3;
    int arr[] = { 9, 6, 12 };

    // Function call
    cout << findContent(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// content of the polynomial
class GFG{

// Function to find the content
// of the polynomial
static int findContent(int arr[], int n)
{
    int content = arr[0];

    // Loop to iterate over the
    // elements of the array
    for(int i = 1; i < n; i++)
    {

        //__gcd(a, b) is a inbuilt
        // function for Greatest
        // Common Divisor
        content = __gcd(content, arr[i]);
    }
    return content;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    int n = 3;
    int arr[] = { 9, 6, 12 };

    // Function call
    System.out.print(findContent(arr, n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to find the
# content of the polynomial
from math import gcd

# Function to find the content
# of the polynomial
def findContent(arr, n):

    content = arr[0]

    # Loop to iterate over the
    # elements of the array
    for i in range(1, n):

        # __gcd(a, b) is a inbuilt
        # function for Greatest
        # Common Divisor
        content = gcd(content, arr[i])

    return content

# Driver Code
if __name__ == '__main__':

    n = 3
    arr = [ 9, 6, 12 ]

    # Function call
    print(findContent(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// content of the polynomial
using System;

class GFG{

// Function to find the content
// of the polynomial
static int findContent(int []arr, int n)
{
    int content = arr[0];

    // Loop to iterate over the
    // elements of the array
    for(int i = 1; i < n; i++)
    {

        //__gcd(a, b) is a inbuilt
        // function for Greatest
        // Common Divisor
        content = __gcd(content, arr[i]);
    }
    return content;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
    int n = 3;
    int []arr = { 9, 6, 12 };

    // Function call
    Console.Write(findContent(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// content of the polynomial

// Function to find the content
// of the polynomial
function findContent(arr, n)
{
    var content = arr[0];

    // Loop to iterate over the
    // elements of the array
    for(var i = 1; i < n; i++)
    {

        //__gcd(a, b) is a inbuilt
        // function for Greatest
        // Common Divisor
        content = __gcd(content, arr[i]);
    }
    return content;
}

function __gcd(a, b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
var n = 3;
var arr = [ 9, 6, 12 ];

// Function call
document.write(findContent(arr, n));

// This code is contributed by kirti

</script>
```

**Output:** 

```
3
```