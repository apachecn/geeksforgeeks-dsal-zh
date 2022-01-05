# 检查是否可以通过恰好替换一个元素

使数组和等于数组乘积

> 原文:[https://www . geeksforgeeks . org/check-如果可能，通过替换恰好一个元素来使数组和等于数组积/](https://www.geeksforgeeks.org/check-if-possible-to-make-array-sum-equal-to-array-product-by-replacing-exactly-one-element/)

给定一个由非负整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过用任何非负整数恰好替换一个数组元素来检查是否有可能使[数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的和等于数组元素的[乘积。](https://www.geeksforgeeks.org/program-for-product-of-array/)

**示例:**

> **输入:** arr[] = {1，3，4}
> **输出:**是
> **解释:**
> 用 2 替换数组的最后一个元素将数组修改为{1，3，2}。数组元素的和= 6，数组元素的积是 1*2*3 = 6。因此，打印“是”。
> 
> **输入:** arr[] = {1，2，3 }
> T3】输出:否

**方法:**给定的问题可以通过使用以下数学观察来解决:

> 将阵元之和视为 **S** 阵元之积视为 **P** ，将任意阵元 **X** 替换为 **Y** 阵元之和与积必须相同，方程为:
> 
> **=>S–X+Y = P * Y/X**
> **=>Y =(S–X)/(P/X–1)**

从上面的观察来看，想法是找到数组元素的和与积作为 **S** 和 **P** ，然后迭代数组元素(比如说 **X** )并使用上面的等式找到 **Y** 的值，如果有任何数组元素的值为 **Y** 作为一个完整的非负整数，那么打印 **Yes** 。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to check if it is possible
// to form an array whose sum and the
// product is the same or not
int canPossibleReplacement(int N, int arr[])
{

    // Find the sum of the array
    // initialize sum
    int S = 0;
    int i;

    // Iterate through all elements and
    // add them to sum
    for (i = 0; i < N; i++)
        S += arr[i];

    // Find the product of the array
    int P = 1;

    for (i = 0; i < N; i++)
    {
        P *= i;
    }

    // Check a complete integer y
    // for every x
    for (int i = 0; i < N; i++)
    {
        int x = arr[i];
        int y = (S - x) / (P / x - 1);

        // If got such y
        if ((S - x + y) == (P * y) / x)
            return 1;
    }

    // If no such y exist
    return 0;
}

// Driver Code
int main()
{
    int N = 3;
    int arr[] = {1, 3, 4};

    if (canPossibleReplacement(N, arr) == 1)
        cout << ("Yes");
    else
        cout << ("No");
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if it is possible
// to form an array whose sum and the
// product is the same or not
static int canPossibleReplacement(int N, int[] arr)
{

    // Find the sum of the array
    // initialize sum
    int S = 0;
    int i;

    // Iterate through all elements and
    // add them to sum
    for(i = 0; i < arr.length; i++)
        S +=  arr[i];

    // Find the product of the array
    int P = 1;

    for(i = 0; i < arr.length; i++)
    {
        P *= i;
    }

    // Check a complete integer y
    // for every x
    for(int x : arr)
    {
        int y = (S - x)/(P / x - 1);

        // If got such y
        if ((S - x + y) == (P * y) / x)
            return 1;
    }

    // If no such y exist
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    int arr[] = { 1, 3, 4 };

    if (canPossibleReplacement(N, arr) == 1)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if it is possible
# to form an array whose sum and the
# product is the same or not
def canPossibleReplacement(N, arr):

    # Find the sum of the array
    S = sum(arr)

    # Find the product of the array
    P = 1

    for i in arr:
        P *= i

    # Check a complete integer y
    # for every x
    for x in arr:

        y = (S-x)//(P / x-1)

        # If got such y
        if (S-x + y) == (P * y)/x:

            return 'Yes'

    # If no such y exist
    return 'No'

# Driver Code
N, arr = 3, [1, 3, 4]
print(canPossibleReplacement(N, arr))
```

## C#

```
// C# program for the above approach

using System;

class GFG{

// Function to check if it is possible
// to form an array whose sum and the
// product is the same or not
static int canPossibleReplacement(int N, int[] arr)
{

    // Find the sum of the array
    // initialize sum
    int S = 0;
    int i;

    // Iterate through all elements and
    // add them to sum
    for(i = 0; i < arr.Length; i++)
        S +=  arr[i];

    // Find the product of the array
    int P = 1;

    for(i = 0; i < arr.Length; i++)
    {
        P *= i;
    }

    // Check a complete integer y
    // for every x
    foreach(int x in arr)
    {
        int y = (S - x)/(P / x - 1);

        // If got such y
        if ((S - x + y) == (P * y) / x)
            return 1;
    }

    // If no such y exist
    return 0;
}

// Driver Code
public static void Main(string[] args)
{
    int N = 3;
    int []arr = { 1, 3, 4 };

    if (canPossibleReplacement(N, arr) == 1)
        Console.Write("Yes");
    else
         Console.Write("No");
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// javascript Program to implement
// the above approach

// Function to check if it is possible
// to form an array whose sum and the
// product is the same or not
function canPossibleReplacement(N, arr)
{

    // Find the sum of the array
    // initialize sum
    var S = 0;
    var i;

    // Iterate through all elements and
    // add them to sum
    for (i = 0; i < N; i++)
        S += arr[i];

    // Find the product of the array
    var P = 1;

    for (i = 0; i < N; i++)
    {
        P *= i;
    }

    // Check a complete integer y
    // for every x
    for (i = 0; i < N; i++)
    {
        var x = arr[i];
        var y = (S - x) / (P / x - 1);

        // If got such y
        if ((S - x + y) == (P * y) / x)
            return 1;
    }

    // If no such y exist
    return 0;
}

// Driver Code
    var N = 3;
    var arr = [1, 3, 4]

    if (canPossibleReplacement(N, arr) == 1)
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by ipg2016107.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)