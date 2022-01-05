# 从数组中移除一个数字而不改变其算术平均值

> 原文:[https://www . geeksforgeeks . org/从数组中移除数字而不改变其算术平均值/](https://www.geeksforgeeks.org/removing-a-number-from-array-without-changing-its-arithmetic-mean/)

给定一个大小为 **N** 的正整数数组**[]**。任务是从给定数组中移除一个元素，使数组的算术平均值保持不变。如果可以删除任何此类号码，则打印该号码。否则，打印-1。
**例:**

> **输入:** a[] = {1，2，3，4，5}
> **输出:** 3
> 给定数组的平均值为 3。移动第三个元素
> 后，数组变成{1，2，4，5}，其平均值也是 3。
> **输入:** a[] = {5，4，3，6}
> **输出:** -1

**进场:**

一种有效的方法是找到数组的平均值，并检查平均值是否存在于给定的数组中。我们只能移除值等于平均值的元素。

设原阵的均值为 **M** ，元素之和为**之和**。那么**总和= M * N** 。去掉 **M** 后，新的平均值为**((M * N)–M)/(N–1)= M**，保持不变。因此，只需使用任何[搜索](https://www.geeksforgeeks.org/searching-algorithms/)方法并打印元素。

以下是上述方法的实施:

## C++

```
// CPP program to remove a number from the
// array without changing its arithmetic mean
#include <bits/stdc++.h>
using namespace std;

// Function to remove a number from the
// array without changing its arithmetic mean
int FindElement(int a[], int n)
{
    // Find sum of all elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + a[i];

    // If mean is an integer
    if (sum % n == 0) {
        int m = sum / n;

        // Check if mean is present in the array or not
        for (int i = 0; i < n; i++)
            if (a[i] == m)
                return m;
    }

    return -1;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 4, 5 };

    int n = sizeof(a) / sizeof(int);

    cout << FindElement(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove a number from the
// array without changing its arithmetic mean
import java.io.*;

class GFG
{

// Function to remove a number from the
// array without changing its arithmetic mean
static int FindElement(int a[], int n)
{
    // Find sum of all elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + a[i];

    // If mean is an integer
    if (sum % n == 0)
    {
        int m = sum / n;

        // Check if mean is present in the array or not
        for (int i = 0; i < n; i++)
            if (a[i] == m)
                return m;
    }

    return -1;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 2, 3, 4, 5 };
    int n = a.length;

    System.out.print(FindElement(a, n));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to remove a number from the
# array without changing its arithmetic mean

# Function to remove a number from the
# array without changing its arithmetic mean
def FindElement(a, n):

    # Find sum of all elements
    s = 0
    for i in range(n):
        s = s + a[i]

    # If mean is an integer
    if s % n == 0:
        m = s // n

        # Check if mean is present
        # in the array or not
        for j in range(n):
            if a[j] == m:
                return m
    return -1

# Driver code
if __name__ == "__main__":
    a = [1, 2, 3, 4, 5]
    n = len(a)
    print(FindElement(a, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to remove a number from the
// array without changing its arithmetic mean
using System;

class GFG
{

// Function to remove a number from the
// array without changing its arithmetic mean
static int FindElement(int []a, int n)
{
    // Find sum of all elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + a[i];

    // If mean is an integer
    if (sum % n == 0)
    {
        int m = sum / n;

        // Check if mean is present in the array or not
        for (int i = 0; i < n; i++)
            if (a[i] == m)
                return m;
    }

    return -1;
}

// Driver code
public static void Main ()
{
    int []a = { 1, 2, 3, 4, 5 };
    int n = a.Length;

    Console.WriteLine(FindElement(a, n));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript program to remove a number from the
// array without changing its arithmetic mean

// Function to remove a number from the
// array without changing its arithmetic mean
function FindElement(a, n)
{
    // Find sum of all elements
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum = sum + a[i];

    // If mean is an integer
    if (sum % n == 0) {
        let m = parseInt(sum / n);

        // Check if mean is present in
        // the array or not
        for (let i = 0; i < n; i++)
            if (a[i] == m)
                return m;
    }

    return -1;
}

// Driver code
    let a = [ 1, 2, 3, 4, 5 ];

    let n = a.length;

    document.write(FindElement(a, n));

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(N)