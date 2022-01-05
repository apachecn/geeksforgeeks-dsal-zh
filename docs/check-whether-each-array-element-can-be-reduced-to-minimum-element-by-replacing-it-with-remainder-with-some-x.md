# 检查每个数组元素是否可以通过用一些 X 的余数替换来减少到最小元素

> 原文:[https://www . geesforgeks . org/check-每个数组元素是否可以通过用某些-x 的余数替换它来减少到最小元素/](https://www.geeksforgeeks.org/check-whether-each-array-element-can-be-reduced-to-minimum-element-by-replacing-it-with-remainder-with-some-x/)

给定一个非负整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过选择任意正整数 **X** 来检查是否所有数组元素都可以简化为数组中的[最小元素，并将一个数组元素 **arr[i]** 更新为 **arr[i]%X** 。如果可以，则打印**是**。否则，打印**否**。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

**示例:**

> **输入:** arr[] = {1，1，3，4}
> **输出:**是
> **解释:**
> 可以执行以下操作将所有数组元素减少到 1:
> 
> 1.  为数组元素 arr[3]选择 X = 2，并用 arr[3] % 2 替换它，将数组 arr[]修改为{1，1，1，4}。
> 2.  为数组元素 arr[4]选择 X = 3，并用 arr[4] % 3 替换它，将数组 arr[]修改为{1，1，1，1}。
> 
> 在上述操作之后，所有数组元素都被减少到 arr[]的最小元素。因此，打印“是”。
> 
> **输入:** arr[] = {1，2，3 }
> T3】输出:否

**方法:**通过观察任何非负整数，比如说**数**都可以通过选择 **X** 的值作为**数/2** 而变成以下整数**【0，ceil(num/2)–1】**来解决给定的问题。很明显，其余的 **X** 将具有比 **X** 更短的变化数量范围，等于**数量/2** 。按照以下步骤解决问题:

*   初始化一个变量，比如说 **mini** ，它存储数组的[最小元素 **arr[]** 。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)
*   [遍历给定数组 **arr[]**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) ，如果 **mini** 的值不在**【0】范围内，则任何数组元素 **arr[i]** 的 ceil(arr[I]/2)–1)**然后打印 **No** 。否则，打印**是**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if every integer
// in the array can be reduced to the
// minimum array element
string isPossible(int arr[], int n)
{
    // Stores the minimum array element
    int mini = INT_MAX;

    // Find the minimum element
    for (int i = 0; i < n; i++)
        mini = min(mini, arr[i]);

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {
        if (arr[i] == mini)
            continue;

        // Stores the maximum value
        // in the range
        int Max = (arr[i] + 1) / 2 - 1;

        // Check whether mini lies in
        // the range or not
        if (mini < 0 || mini > Max)
            return "No";
    }

    // Otherwise, return Yes
    return "Yes";
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << isPossible(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if every integer
// in the array can be reduced to the
// minimum array element
static String isPossible(int arr[], int n)
{
    // Stores the minimum array element
    int mini = Integer.MAX_VALUE;

    // Find the minimum element
    for (int i = 0; i < n; i++)
        mini = Math.min(mini, arr[i]);

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {
        if (arr[i] == mini)
            continue;

        // Stores the maximum value
        // in the range
        int Max = (arr[i] + 1) / 2 - 1;

        // Check whether mini lies in
        // the range or not
        if (mini < 0 || mini > Max)
            return "No";
    }

    // Otherwise, return Yes
    return "Yes";
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 1, 3, 4 };
    int N = arr.length;

    System.out.print(isPossible(arr, N));

}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

import sys
# Function to check if every integer
# in the array can be reduced to the
# minimum array element
def isPossible(arr, n):
    # Stores the minimum array element
    mini = sys.maxsize

    # Find the minimum element
    for i in range(n):
        mini = min(mini, arr[i])

    # Traverse the array arr[]
    for i in range(n):
        if (arr[i] == mini):
            continue

        # Stores the maximum value
        # in the range
        Max = (arr[i] + 1) // 2 - 1

        # Check whether mini lies in
        # the range or not
        if (mini < 0 or mini > Max):
            return "No"

    # Otherwise, return Yes
    return "Yes"

# Driver Code
if __name__ == '__main__':
    arr = [1, 1, 3, 4]
    N = len(arr)

    print(isPossible(arr, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to check if every integer
// in the array can be reduced to the
// minimum array element
static String isPossible(int []arr, int n)
{

    // Stores the minimum array element
    int mini = int.MaxValue;

    // Find the minimum element
    for (int i = 0; i < n; i++)
        mini = Math.Min(mini, arr[i]);

    // Traverse the array []arr
    for (int i = 0; i < n; i++) {
        if (arr[i] == mini)
            continue;

        // Stores the maximum value
        // in the range
        int Max = (arr[i] + 1) / 2 - 1;

        // Check whether mini lies in
        // the range or not
        if (mini < 0 || mini > Max)
            return "No";
    }

    // Otherwise, return Yes
    return "Yes";
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 1, 3, 4 };
    int N = arr.Length;

    Console.Write(isPossible(arr, N));

}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Function to check if every integer
// in the array can be reduced to the
// minimum array element
function isPossible(arr, n)
{
    // Stores the minimum array element
    var mini = Number.MAX_VALUE;

    // Find the minimum element
    for (var i = 0; i < n; i++)
        mini = Math.min(mini, arr[i]);

    // Traverse the array arr[]
    for (var i = 0; i < n; i++) {
        if (arr[i] == mini)
            continue;

        // Stores the maximum value
        // in the range
        var Max = (arr[i] + 1) / 2 - 1;

        // Check whether mini lies in
        // the range or not
        if (mini < 0 || mini > Max)
            return "No";
    }

    // Otherwise, return Yes
    return "Yes";
}

// Driver code

    var arr = [ 1, 1, 3, 4 ];
    var N = arr.length;

    document.write(isPossible(arr, N));

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)