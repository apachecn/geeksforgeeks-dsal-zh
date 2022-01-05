# 检查是否可以通过给定的运算从数组中获得和 Y

> 原文:[https://www . geeksforgeeks . org/check-if-sum-y-可以通过给定的操作从数组中获取/](https://www.geeksforgeeks.org/check-if-sum-y-can-be-obtained-from-the-array-by-the-given-operations/)

给定一个整数数组 **arr[]** 和两个整数 **X** 和 **Y** ，任务是检查是否有可能获得具有和 **X** 的序列，使得子序列的每个元素乘以一个数组元素的和等于 **Y** 。
**注意:**这里 X 总是小于 y。

**示例:**

> **输入:** arr[] = {1，2，7，9，10}，X = 11，Y = 13
> **输出:** Yes
> **解释:**
> X(= 11)的给定值可以拆分为序列{9，2}，使得 9 * 1(= arr[0]+2 * 2(= arr[1])= 13(= Y)
> **输入:** arr[] ={1，3，5，7

**方法:**按照以下步骤解决问题:

*   计算 **Y** 和 **X** 之间的**差**。
*   对于每个数组元素 **arr[i]** ，即 **> 1** ，更新**(Y–X)%(arr[I]–1)**。
*   如果**差值**减少 0，打印“**是**”。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to check if it is possible
// to obtain sum Y from a sequence of
// sum X from the array arr[]
void solve(int arr[], int n, int X, int Y)
{

    // Store the difference
    int diff = Y - X;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (arr[i] != 1) {
            diff = diff % (arr[i] - 1);
        }
    }

    // If diff reduced to 0
    if (diff == 0)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 7, 9, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int X = 11, Y = 13;
    solve(arr, n, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to check if it is possible
// to obtain sum Y from a sequence of
// sum X from the array arr[]
static void solve(int arr[], int n,
                  int X, int Y)
{

    // Store the difference
    int diff = Y - X;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] != 1)
        {
            diff = diff % (arr[i] - 1);
        }
    }

    // If diff reduced to 0
    if (diff == 0)
        System.out.print( "Yes");
    else
        System.out.print("No");
}

// Driver Code
public static void main (String []args)
{
    int arr[] = { 1, 2, 7, 9, 10 };
    int n = arr.length;
    int X = 11, Y = 13;

    solve(arr, n, X, Y);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if it is possible
# to obtain sum Y from a sequence of
# sum X from the array arr[]
def solve(arr, n, X, Y):

    # Store the difference
    diff = Y - X

    # Iterate over the array
    for i in range(n):
        if(arr[i] != 1):
            diff = diff % (arr[i] - 1)

    # If diff reduced to 0
    if(diff == 0):
        print("Yes")
    else:
        print("No")

# Driver Code
arr = [ 1, 2, 7, 9, 10 ]
n = len(arr)
X, Y = 11, 13

# Function call
solve(arr, n, X, Y)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if it is possible
// to obtain sum Y from a sequence of
// sum X from the array []arr
static void solve(int []arr, int n,
                  int X, int Y)
{

    // Store the difference
    int diff = Y - X;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] != 1)
        {
            diff = diff % (arr[i] - 1);
        }
    }

    // If diff reduced to 0
    if (diff == 0)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 1, 2, 7, 9, 10 };
    int n = arr.Length;
    int X = 11, Y = 13;

    solve(arr, n, X, Y);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if it is possible
// to obtain sum Y from a sequence of
// sum X from the array arr[]
function solve(arr, n, X, Y)
{

    // Store the difference
    var diff = Y - X;

    // Iterate over the array
    for(var i = 0; i < n; i++)
    {

        if (arr[i] != 1)
        {
            diff = diff % (arr[i] - 1);
        }
    }

    // If diff reduced to 0
    if (diff == 0)
        document.write("Yes");
    else
        document.write("No");
}

// Driver Code
var arr = [ 1, 2, 7, 9, 10 ];
var n = arr.length;
var X = 11, Y = 13;

solve(arr, n, X, Y);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)