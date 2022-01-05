# 执行给定操作后找到数组的最终序列

> 原文:[https://www . geeksforgeeks . org/在执行给定操作后找到阵列的最终序列/](https://www.geeksforgeeks.org/find-the-final-sequence-of-the-array-after-performing-given-operations/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是精确地执行以下操作 **N** 次，
创建一个整数的空列表 **b[]** ，在 **i <sup>th</sup>** 操作中，

1.  将**arr【I】**追加到**b【】**的末尾。
2.  反转 **b[]** 中的元素。

最后，在所有操作结束后，打印列表 **b[]** 的内容。
**例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:**4 2 1 3
> T6】
> 
> | 操作 | [b] |
> | --- | --- |
> | one | {1} |
> | Two | {2, 1} |
> | three | {3, 1, 2} |
> | four | {4, 2, 1, 3} |
> 
> **输入:** arr[] = {1，2，3 }
> T3】输出: 3 1 2

**方法:**我们需要一些观察来解决这个问题。假设数组中的元素数是偶数。假设我们的数组是{4，8，6，1，7，9}。
T3】

| 操作 | [b] |
| --- | --- |
| one | {4} |
| Two | {8, 4} |
| three | {6, 4, 8} |
| four | {1, 8, 4, 6} |
| five | {7, 6, 4, 8, 1} |
| six | {9, 1, 8, 4, 6, 7} |

仔细观察后，我们得出结论，对于数组中偶数大小的元素，位于偶数位置的数字(基于索引 1)在开始时反转并相加，而位于奇数位置的数字保持相同的顺序并在最后相加。
对于奇数大小的数组，奇数位置的元素在开始时反转并相加，而偶数位置的数组中的元素保持不变并在最后相加。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that generates the
// array b[] when n is even
void solveEven(int n, int* arr, int* b)
{
    int left = n - 1;

    // Fill the first half of the final array
    // with reversed sequence
    for (int i = 0; i < (n / 2); ++i) {
        b[i] = arr[left];
        left = left - 2;
        if (left < 0)
            break;
    }

    // Fill the second half
    int right = 0;
    for (int i = n / 2; i <= n - 1; ++i) {
        b[i] = arr[right];
        right = right + 2;
        if (right > n - 2)
            break;
    }
}

// Function that generates the
// array b[] when n is odd
void solveOdd(int n, int* arr, int* b)
{

    // Fill the first half of the final array
    // with reversed sequence
    int left = n - 1;
    for (int i = 0; i < (n / 2) + 1; ++i) {
        b[i] = arr[left];
        left = left - 2;
        if (left < 0)
            break;
    }

    // Fill the second half
    int right = 1;
    for (int i = (n / 2) + 1; i <= n - 1; ++i) {
        b[i] = arr[right];
        right = right + 2;
        if (right > n - 2)
            break;
    }
}

// Function to find the final array b[]
// after n operations of given type
void solve(int n, int* arr)
{

    // Create the array b
    int b[n];

    // If the array size is even
    if (n % 2 == 0)
        solveEven(n, arr, b);
    else
        solveOdd(n, arr, b);

    // Print the final array elements
    for (int i = 0; i <= n - 1; ++i) {
        cout << b[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    solve(n, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function that generates the
// array b[] when n is even
static void solveEven(int n, int arr[], int b[])
{
    int left = n - 1;

    // Fill the first half of the final array
    // with reversed sequence
    for (int i = 0; i < (n / 2); ++i)
    {
        b[i] = arr[left];
        left = left - 2;
        if (left < 0)
            break;
    }

    // Fill the second half
    int right = 0;
    for (int i = n / 2; i <= n - 1; ++i)
    {
        b[i] = arr[right];
        right = right + 2;
        if (right > n - 2)
            break;
    }
}

// Function that generates the
// array b[] when n is odd
static void solveOdd(int n, int arr[], int b[])
{

    // Fill the first half of the final array
    // with reversed sequence
    int left = n - 1;
    for (int i = 0; i < (n / 2) + 1; ++i)
    {
        b[i] = arr[left];
        left = left - 2;
        if (left < 0)
            break;
    }

    // Fill the second half
    int right = 1;
    for (int i = (n / 2) + 1; i <= n - 1; ++i)
    {
        b[i] = arr[right];
        right = right + 2;
        if (right > n - 2)
            break;
    }
}

// Function to find the final array b[]
// after n operations of given type
static void solve(int n, int arr[])
{

    // Create the array b
    int b[] = new int[n];

    // If the array size is even
    if (n % 2 == 0)
        solveEven(n, arr, b);
    else
        solveOdd(n, arr, b);

    // Print the final array elements
    for (int i = 0; i <= n - 1; ++i)
    {
        System.out.print( b[i] + " ");
    }
}

// Driver code
public static void main (String[] args)
{
    int []arr = { 1, 2, 3, 4 };
    int n = arr.length;

    solve(n, arr);
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that generates the
# array b[] when n is even
def solveEven(n, arr, b):
    left = n - 1

    # Fill the first half of the final array
    # with reversed sequence
    for i in range((n // 2)):
        b[i] = arr[left]
        left = left - 2
        if (left < 0):
            break

    # Fill the second half
    right = 0
    for i in range(n // 2, n, 1):
        b[i] = arr[right]
        right = right + 2
        if (right > n - 2):
            break

# Function that generates the
# array b[] when n is odd
def solveOdd(n, arr, b):

    # Fill the first half of the final array
    # with reversed sequence
    left = n - 1
    for i in range(n // 2 + 1):
        b[i] = arr[left]
        left = left - 2
        if (left < 0):
            break

    # Fill the second half
    right = 1
    for i in range(n // 2 + 1, n, 1):
        b[i] = arr[right]
        right = right + 2
        if (right > n - 2):
            break

# Function to find the final array b[]
# after n operations of given type
def solve(n, arr):

    # Create the array b
    b = [0 for i in range(n)]

    # If the array size is even
    if (n % 2 == 0):
        solveEven(n, arr, b)
    else:
        solveOdd(n, arr, b)

    # Print the final array elements
    for i in range(n):
        print(b[i], end = " ")

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 4]
    n = len(arr)

    solve(n, arr)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that generates the
// array b[] when n is even
static void solveEven(int n, int []arr,
                             int []b)
{
    int left = n - 1;

    // Fill the first half of the final array
    // with reversed sequence
    for (int i = 0; i < (n / 2); ++i)
    {
        b[i] = arr[left];
        left = left - 2;
        if (left < 0)
            break;
    }

    // Fill the second half
    int right = 0;
    for (int i = n / 2; i <= n - 1; ++i)
    {
        b[i] = arr[right];
        right = right + 2;
        if (right > n - 2)
            break;
    }
}

// Function that generates the
// array b[] when n is odd
static void solveOdd(int n, int []arr, int []b)
{

    // Fill the first half of the final array
    // with reversed sequence
    int left = n - 1;
    for (int i = 0; i < (n / 2) + 1; ++i)
    {
        b[i] = arr[left];
        left = left - 2;
        if (left < 0)
            break;
    }

    // Fill the second half
    int right = 1;
    for (int i = (n / 2) + 1; i <= n - 1; ++i)
    {
        b[i] = arr[right];
        right = right + 2;
        if (right > n - 2)
            break;
    }
}

// Function to find the final array b[]
// after n operations of given type
static void solve(int n, int []arr)
{

    // Create the array b
    int []b = new int[n];

    // If the array size is even
    if (n % 2 == 0)
        solveEven(n, arr, b);
    else
        solveOdd(n, arr, b);

    // Print the final array elements
    for (int i = 0; i <= n - 1; ++i)
    {
        Console.Write( b[i] + " ");
    }
}

// Driver code
public static void Main ()
{
    int []arr = { 1, 2, 3, 4 };
    int n = arr.Length;

    solve(n, arr);
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function that generates the
    // array b[] when n is even
    function solveEven(n, arr, b)
    {
        let left = n - 1;

        // Fill the first half of the final array
        // with reversed sequence
        for (let i = 0; i < parseInt(n / 2, 10); ++i)
        {
            b[i] = arr[left];
            left = left - 2;
            if (left < 0)
                break;
        }

        // Fill the second half
        let right = 0;
        for (let i = parseInt(n / 2, 10); i <= n - 1; ++i)
        {
            b[i] = arr[right];
            right = right + 2;
            if (right > n - 2)
                break;
        }
    }

    // Function that generates the
    // array b[] when n is odd
    function solveOdd(n, arr, b)
    {

        // Fill the first half of the final array
        // with reversed sequence
        let left = n - 1;
        for (let i = 0; i < parseInt(n / 2, 10) + 1; ++i)
        {
            b[i] = arr[left];
            left = left - 2;
            if (left < 0)
                break;
        }

        // Fill the second half
        let right = 1;
        for (let i = parseInt(n / 2, 10) + 1; i <= n - 1; ++i)
        {
            b[i] = arr[right];
            right = right + 2;
            if (right > n - 2)
                break;
        }
    }

    // Function to find the final array b[]
    // after n operations of given type
    function solve(n, arr)
    {

        // Create the array b
        let b = new Array(n);

        // If the array size is even
        if (n % 2 == 0)
            solveEven(n, arr, b);
        else
            solveOdd(n, arr, b);

        // Print the final array elements
        for (let i = 0; i <= n - 1; ++i)
        {
            document.write( b[i] + " ");
        }
    }

    let arr = [ 1, 2, 3, 4 ];
    let n = arr.length;

    solve(n, arr);

</script>
```

**Output:** 

```
4 2 1 3
```

**高效进场:**
阵的最后一个元素只会反转一次。倒数第二个元素将被反转两次。因此，它到达最终结果数组 ie b 中的最后一个位置。因此，我们可以通过从头到尾迭代原始数组，并将元素放在未填充的第一个索引和未填充的最后一个索引处来填充 b 数组。下面实现了同样的想法。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

int* solve(int arr[], int n)
{
    static int b[4];
    int p = 0;
    for (int i = n - 1; i >= 0; i--)
    {
        b[p] = arr[i--];
        if (i >= 0)
            b[n - 1 - p] = arr[i];
        p++;
    }
    return b;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr)/sizeof(arr[0]);

    int *b ;
    b = solve(arr, n);
    for(int i = 0; i < n; i++)
    cout << b[i] << " ";
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    static int[] solve(int[] arr, int n) {
        int[] b = new int[n];
        int p = 0;
        for (int i = n - 1; i >= 0; i--) {
            b[p] = arr[i--];
            if (i >= 0)
                b[n - 1 - p] = arr[i];
            p++;
        }
        return b;
    }

    public static void main(String[] args)
    {
        int []arr = { 1, 2, 3, 4 };
        int n = arr.length;

        int[] b = solve(arr, n);

        System.out.println(Arrays.toString(b));
    }
}

// This code is contributed by Pramod Hosahalli
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int[] solve(int[] arr, int n)
    {
        int[] b = new int[n];
        int p = 0;
        for (int i = n - 1; i >= 0; i--)
        {
            b[p] = arr[i--];
            if (i >= 0)
                b[n - 1 - p] = arr[i];
            p++;
        }
        return b;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 1, 2, 3, 4 };
        int n = arr.Length;

        int[] b = solve(arr, n);

        Console.WriteLine("[" + String.Join(",", b) + "]");
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach
def solve(arr, n):
    b = [0 for i in range(n)]
    p = 0
    i = n - 1
    while i >= 0:
        b[p] = arr[i]
        i -= 1
        if (i >= 0):
            b[n - 1 - p] = arr[i]
        p += 1
        i -= 1
    return b

# Driver Code
arr = [1, 2, 3, 4]
n = len(arr)

b = solve(arr, n)

print(b)

# This code is contributed by Mohit kumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach
    function solve(arr , n) {
        var b = Array(n).fill(0);
        var p = 0;
        for (i = n - 1; i >= 0; i--) {
            b[p] = arr[i--];
            if (i >= 0)
                b[n - 1 - p] = arr[i];
            p++;
        }
        return b;
    }

        var arr = [ 1, 2, 3, 4 ];
        var n = arr.length;

        var b = solve(arr, n);

        document.write("["+ b.toString()+ "]");

// This code contributed by aashish1995
</script>
```

**Output:** 

```
[4, 2, 1, 3]
```