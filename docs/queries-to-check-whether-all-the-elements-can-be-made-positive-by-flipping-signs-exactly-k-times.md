# 查询是否所有元素都可以通过将符号精确翻转 K 次

变成正的

> 原文:[https://www . geeksforgeeks . org/query-to-check-all-elements-是否可以通过翻转符号-确切地-k-times/](https://www.geeksforgeeks.org/queries-to-check-whether-all-the-elements-can-be-made-positive-by-flipping-signs-exactly-k-times/) 使所有元素都为正

给定一个整数数组 arr[]，以及一些由整数 **K** 组成的查询，任务是通过精确地翻转整数的符号 **K** 次来确定是否有可能使所有的整数都为正。我们可以多次翻转整数的符号。如果可能，则打印**是**否则打印**否**。
**举例:**

> **输入:** arr[] = {-1，2，-3，4，5}，q[] = {1，2}
> **输出:**
> 否
> 是
> 查询 1:只能更改-1 或-3 的符号
> ，不能同时更改。
> 查询 2:两个负数
> 的符号都可以改为正数。
> **输入:** arr[] = {-1，-1，0，6}，q[] = {1，2，3，4}
> **输出:**
> 否
> 是
> 是
> 是

**方法:**下面是我们将使用的算法:

1.  计算数组中负整数的个数，并将其存储在变量 **cnt** 中。
2.  如果数组中没有零:
    *   如果 **K ≥ cnt** ，则答案为**是**。
    *   如果 **K = cnt** 、**(K–CNT)% 2 = 0**，则答案为**是**。
    *   否则答案将是**否**。
3.  如果数组中有一个零，那么答案将只是**否**如果 **K < cnt** 否则答案总是**是**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// To store the count of
// negative integers
int cnt_neg;

// Check if zero exists
bool exists_zero;

// Function to find the count of
// negative integers and check
// if zero exists in the array
void preProcess(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        if (arr[i] < 0)
            cnt_neg++;
        if (arr[i] == 0)
            exists_zero = true;
    }
}

// Function that returns true if array
// elements can be made positive by
// changing signs exactly k times
bool isPossible(int k)
{
    if (!exists_zero) {
        if (k >= cnt_neg and (k - cnt_neg) % 2 == 0)
            return true;
        else
            return false;
    }
    else {
        if (k >= cnt_neg)
            return true;
        else
            return false;
    }
}

// Driver code
int main()
{
    int arr[] = { -1, 2, -3, 4, 5 };
    int n = sizeof(arr) / sizeof(int);

    // Pre-processing
    preProcess(arr, n);

    int queries[] = { 1, 2, 3, 4 };
    int q = sizeof(queries) / sizeof(int);

    // Perform queries
    for (int i = 0; i < q; i++) {
        if (isPossible(queries[i]))
            cout << "Yes" << endl;
        else
            cout << "No" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// To store the count of
// negative integers
static int cnt_neg;

// Check if zero exists
static boolean exists_zero;

// Function to find the count of
// negative integers and check
// if zero exists in the array
static void preProcess(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        if (arr[i] < 0)
            cnt_neg++;
        if (arr[i] == 0)
            exists_zero = true;
    }
}

// Function that returns true if array
// elements can be made positive by
// changing signs exactly k times
static boolean isPossible(int k)
{
    if (!exists_zero)
    {
        if (k >= cnt_neg && (k - cnt_neg) % 2 == 0)
            return true;
        else
            return false;
    }
    else
    {
        if (k >= cnt_neg)
            return true;
        else
            return false;
    }
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { -1, 2, -3, 4, 5 };
    int n = arr.length;

    // Pre-processing
    preProcess(arr, n);

    int queries[] = { 1, 2, 3, 4 };
    int q = arr.length;

    // Perform queries
    for (int i = 0; i < q; i++)
    {
        if (isPossible(queries[i]))
            System.out.println( "Yes");
        else
            System.out.println( "No");
    }
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# To store the count of
# negative integers
cnt_neg = 0;

# Check if zero exists
exists_zero = None;

# Function to find the count of
# negative integers and check
# if zero exists in the array
def preProcess(arr, n) :
    global cnt_neg

    for i in range(n) :
        if (arr[i] < 0) :
            cnt_neg += 1;

        if (arr[i] == 0) :
            exists_zero = True;

# Function that returns true if array
# elements can be made positive by
# changing signs exactly k times
def isPossible(k) :

    if (not exists_zero) :
        if (k >= cnt_neg and (k - cnt_neg) % 2 == 0) :
            return True;
        else :
            return False;

    else :
        if (k >= cnt_neg) :
            return True;
        else :
            return False;

# Driver code
if __name__ == "__main__" :

    arr = [ -1, 2, -3, 4, 5 ];
    n = len(arr);

    # Pre-processing
    preProcess(arr, n);

    queries = [ 1, 2, 3, 4 ];
    q = len(queries);

    # Perform queries
    for i in range(q) :
        if (isPossible(queries[i])) :
            print("Yes");
        else :
            print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// To store the count of
// negative integers
static int cnt_neg;

// Check if zero exists
static bool exists_zero ;

// Function to find the count of
// negative integers and check
// if zero exists in the array
static void preProcess(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        if (arr[i] < 0)
            cnt_neg++;
        if (arr[i] == 0)
            exists_zero = true;
    }
}

// Function that returns true if array
// elements can be made positive by
// changing signs exactly k times
static bool isPossible(int k)
{
    if (!exists_zero)
    {
        if (k >= cnt_neg && (k - cnt_neg) % 2 == 0)
            return true;
        else
            return false;
    }
    else
    {
        if (k >= cnt_neg)
            return true;
        else
            return false;
    }
}

// Driver code
static public void Main ()
{

    int []arr = { -1, 2, -3, 4, 5 };
    int n = arr.Length;

    // Pre-processing
    preProcess(arr, n);

    int []queries = { 1, 2, 3, 4 };
    int q = arr.Length;

    // Perform queries
    for (int i = 0; i < q; i++)
    {
        if (isPossible(queries[i]))
            Console.WriteLine( "Yes");
        else
            Console.WriteLine( "No");
    }
}
}

// This code is contributed by ajit...
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// To store the count of
// negative integers
let cnt_neg = 0;

// Check if zero exists
let exists_zero = false;

// Function to find the count of
// negative integers and check
// if zero exists in the array
function preProcess(arr, n)
{
    for (let i = 0; i < n; i++) {
        if (arr[i] < 0)
            cnt_neg++;
        if (arr[i] == 0)
            exists_zero = true;
    }
}

// Function that returns true if array
// elements can be made positive by
// changing signs exactly k times
function isPossible(k)
{
    if (!exists_zero) {
        if (k >= cnt_neg && (k - cnt_neg) % 2 == 0)
            return true;
        else
            return false;
    }
    else {
        if (k >= cnt_neg)
            return true;
        else
            return false;
    }
}

// Driver code
    let arr = [ -1, 2, -3, 4, 5 ];
    let n = arr.length;

    // Pre-processing
    preProcess(arr, n);

    let queries = [ 1, 2, 3, 4 ];
    let q = queries.length;

    // Perform queries
    for (let i = 0; i < q; i++) {
        if (isPossible(queries[i]))
            document.write("Yes<br>");
        else
            document.write("No<br>");
    }

</script>
```

**Output:** 

```
No
Yes
No
Yes
```