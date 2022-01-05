# 使所有数组元素等于 1 所需的成本

> 原文:[https://www . geeksforgeeks . org/cost-制作所有数组元素所需的成本-等于 1/](https://www.geeksforgeeks.org/cost-required-to-make-all-array-elements-equal-to-1/)

给定大小为 **N** 的二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到使所有数组元素等于 **1** 所需的总成本，其中将任何 **0** 转换为 **1** 的成本等于在此之前存在的 **1s** 的[计数。](https://www.geeksforgeeks.org/count-1s-sorted-binary-array/)

**示例:**

> **输入:** arr[] = {1，0，1，0，1，0}
> **输出:** 9
> **解释:**
> 执行以下操作:
> 
> 1.  将 arr[1]转换为 1 会将 arr[]修改为{1，1，1，0，1，0}。成本= 1。
> 2.  将 arr[3]转换为 1 会将 arr[]修改为{1，1，1，1，0}。成本= 3。
> 3.  将 arr[5]转换为 1 会将 arr[]修改为{1，1，1，1，5}。成本= 5。
> 
> 因此，总成本为 1 + 3 + 5 = 9。
> 
> **输入:** arr[] = {1，1，1 }
> T3】输出: 0

**天真法:**解决给定问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并统计每个包含 **0** 的索引前出现的 **1** 的个数，打印得到的所有代价的总和。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**通过观察以下事实可以优化上述方法:在将每个 **0** 转换为 **1** 之后，在每个 **0** 之前存在的 **1** 的计数由出现 **0** 的指数给出。因此，任务是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并打印数组**arr【】**中所有具有 **0** s 的索引的总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the cost required
// to make all array elements equal to 1
int findCost(int A[], int N)
{
    // Stores the total cost
    int totalCost = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If current element is 0
        if (A[i] == 0) {

            // Convert 0 to 1
            A[i] = 1;

            // Add the cost
            totalCost += i;
        }
    }

    // Return the total cost
    return totalCost;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 1, 0, 1, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findCost(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG{

// Function to calculate the cost required
// to make all array elements equal to 1
static int findCost(int[] A, int N)
{

    // Stores the total cost
    int totalCost = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If current element is 0
        if (A[i] == 0)
        {

            // Convert 0 to 1
            A[i] = 1;

            // Add the cost
            totalCost += i;
        }
    }

    // Return the total cost
    return totalCost;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 0, 1, 0, 1, 0 };
    int N = arr.length;

    System.out.println(findCost(arr, N));
}
}

// This code is contributed by ukasp
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the cost required
# to make all array elements equal to 1
def findCost(A, N):

    # Stores the total cost
    totalCost = 0

    # Traverse the array arr[]
    for i in range(N):

        # If current element is 0
        if (A[i] == 0):

            # Convert 0 to 1
            A[i] = 1

            # Add the cost
            totalCost += i

    # Return the total cost
    return totalCost

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 0, 1, 0, 1, 0 ]
    N = len(arr)

    print(findCost(arr, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate the cost required
// to make all array elements equal to 1
static int findCost(int []A, int N)
{

    // Stores the total cost
    int totalCost = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If current element is 0
        if (A[i] == 0)
        {

            // Convert 0 to 1
            A[i] = 1;

            // Add the cost
            totalCost += i;
        }
    }

    // Return the total cost
    return totalCost;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 0, 1, 0, 1, 0 };
    int N = arr.Length;

    Console.Write(findCost(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate the cost required
// to make all array elements equal to 1
function findCost(A, N)
{
    // Stores the total cost
    var totalCost = 0;

    var i;
    // Traverse the array arr[]
    for (i = 0; i < N; i++) {

        // If current element is 0
        if (A[i] == 0) {

            // Convert 0 to 1
            A[i] = 1;

            // Add the cost
            totalCost += i;
        }
    }

    // Return the total cost
    return totalCost;
}

// Driver Code
    var arr = [1, 0, 1, 0, 1, 0]
    var N = arr.length
    document.write(findCost(arr, N));

</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)