# 分配给元素的最小值，以便总和大于初始总和

> 原文:[https://www . geeksforgeeks . org/要分配给元素的最小值-因此总和变得大于初始总和/](https://www.geeksforgeeks.org/minimum-value-to-be-assigned-to-the-elements-so-that-sum-becomes-greater-than-initial-sum/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是将给定数组的所有元素更新为某个值 **X** ，使得所有更新后的数组元素之和严格大于初始数组的所有元素之和 **X** 是最小可能值。
**举例:**

> **输入:** arr[] = {4，2，1，10，6}
> **输出:** 5
> 原数组之和= 4 + 2 + 1 + 10 + 6 = 23
> 修改后数组之和= 5 + 5 + 5 + 5 + 5 = 25
> **输入:** arr[] = {9876，8654，5470，3567，7954}
> **输出:…**

**进场:**

*   找到原始数组元素的总和，并将其存储在变量**sumar**中
*   计算 **X = sumArr / n** ，其中 **n** 是数组中的元素数量。
*   现在，为了超过原始数组的总和，新数组的每个元素必须至少为 **X + 1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// required value
int findMinValue(int arr[], int n)
{

    // Find the sum of the
    // array elements
    long sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Return the required value
    return ((sum / n) + 1);
}

// Driver code
int main()
{
    int arr[] = { 4, 2, 1, 10, 6 };
    int n = sizeof(arr) / sizeof(int);

    cout << findMinValue(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the minimum
    // required value
    static int findMinValue(int arr[], int n)
    {

        // Find the sum of the
        // array elements
        long sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Return the required value
        return ((int)(sum / n) + 1);
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 4, 2, 1, 10, 6 };
        int n = arr.length;

        System.out.print(findMinValue(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# required value
def findMinValue(arr, n):

    # Find the sum of the
    # array elements
    sum = 0
    for i in range(n):
        sum += arr[i]

    # Return the required value
    return (sum // n) + 1

# Driver code
arr = [4, 2, 1, 10, 6]
n = len(arr)
print(findMinValue(arr, n))
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the minimum
    // required value
    static int findMinValue(int []arr, int n)
    {

        // Find the sum of the
        // array elements
        long sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Return the required value
        return ((int)(sum / n) + 1);
    }

    // Driver code
    static public void Main ()
    {
        int []arr = { 4, 2, 1, 10, 6 };
        int n = arr.Length;

        Console.WriteLine(findMinValue(arr, n));
    }
}       

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimum
// required value
function findMinValue(arr, n)
{

    // Find the sum of the
    // array elements
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += arr[i];

    // Return the required value
    return (parseInt(sum / n) + 1);
}

// Driver code
    let arr = [ 4, 2, 1, 10, 6 ];
    let n = arr.length;

    document.write(findMinValue(arr, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度** : O(N)。
**辅助空间** : O(1)。