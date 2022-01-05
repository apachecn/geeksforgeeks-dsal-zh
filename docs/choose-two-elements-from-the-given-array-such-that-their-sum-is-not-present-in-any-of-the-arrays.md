# 从给定的数组中选择两个元素，使得它们的和不出现在任何数组中

> 原文:[https://www . geeksforgeeks . org/从给定数组中选择两个元素，这样它们的总和就不会出现在任何数组中/](https://www.geeksforgeeks.org/choose-two-elements-from-the-given-array-such-that-their-sum-is-not-present-in-any-of-the-arrays/)

给定两个数组**A【】**和**B【】**，任务是选择两个元素 **X** 和 **Y** ，使得 **X** 属于**A【】**而 **Y** 属于**B【】**且 **(X + Y)** 不得出现在任何数组中。
**示例:**

> **输入:** A[] = {3，2，2}，B[] = {1，5，7，7，9}
> **输出:** 3 9
> 3 + 9 = 12 和 12 不存在于
> 任何给定的数组中。
> **输入:** A[] = {1，3，5，7}，B[] = {7，5，3，1}
> **输出:** 7 7

**进场:**从 **A[]** 中选择 **X** 作为最大元素，从 **B[]** 中选择 **Y** 作为最大元素。现在，很明显 **(X + Y)** 将大于两个阵列的最大值，即它不会出现在任何阵列中。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the numbers from
// the given arrays such that their
// sum is not present in any
// of the given array
void findNum(int a[], int n, int b[], int m)
{
    // Find the maximum element
    // from both the arrays
    int x = *max_element(a, a + n);
    int y = *max_element(b, b + m);
    cout << x << " " << y;
}

// Driver code
int main()
{
    int a[] = { 3, 2, 2 };
    int n = sizeof(a) / sizeof(int);
    int b[] = { 1, 5, 7, 7, 9 };
    int m = sizeof(b) / sizeof(int);

    findNum(a, n, b, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// find maximum element in an array
static int max_element(int a[], int n)
{
    int m = Integer.MIN_VALUE;

    for(int i = 0; i < n; i++)
        m = Math.max(m, a[i]);

    return m;
}

// Function to find the numbers from
// the given arrays such that their
// sum is not present in any
// of the given array
static void findNum(int a[], int n,
                    int b[], int m)
{
    // Find the maximum element
    // from both the arrays
    int x = max_element(a, n);
    int y = max_element(b, m);
    System.out.print(x + " " + y);
}

// Driver code
public static void main(String args[])
{
    int a[] = { 3, 2, 2 };
    int n = a.length;
    int b[] = { 1, 5, 7, 7, 9 };
    int m = b.length;

    findNum(a, n, b, m);
}
}

// This code is contributed by Arnub Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the numbers from
# the given arrays such that their
# sum is not present in any
# of the given array
def findNum(a, n, b, m) :

    # Find the maximum element
    # from both the arrays
    x = max(a);
    y = max(b);
    print(x, y);

# Driver code
if __name__ == "__main__" :

    a = [ 3, 2, 2 ];
    n = len(a);

    b = [ 1, 5, 7, 7, 9 ];
    m = len(b);

    findNum(a, n, b, m);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // find maximum element in an array
    static int max_element(int []a, int n)
    {
        int m = int.MinValue;

        for(int i = 0; i < n; i++)
            m = Math.Max(m, a[i]);

        return m;
    }

    // Function to find the numbers from
    // the given arrays such that their
    // sum is not present in any
    // of the given array
    static void findNum(int []a, int n,
                        int []b, int m)
    {
        // Find the maximum element
        // from both the arrays
        int x = max_element(a, n);
        int y = max_element(b, m);
        Console.Write(x + " " + y);
    }

    // Driver code
    public static void Main()
    {
        int []a = { 3, 2, 2 };
        int n = a.Length;
        int []b = { 1, 5, 7, 7, 9 };
        int m = b.Length;

        findNum(a, n, b, m);
    }
}

// This code is contributed by kanugargng
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the numbers from
// the given arrays such that their
// sum is not present in any
// of the given array
function findNum(a, n, b, m)
{
    // Find the maximum element
    // from both the arrays
    var x = a.reduce(function(a, b) { return Math.max(a, b); });
    var y = b.reduce(function(a, b) { return Math.max(a, b); });
    document.write(x + " " + y);
}

// Driver code
var a = [ 3, 2, 2 ];
var n = a.length;
var b = [ 1, 5, 7, 7, 9 ]
var m = b.length;
findNum(a, n, b, m);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
3 9
```

**时间复杂度:** O(n)