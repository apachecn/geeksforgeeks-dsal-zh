# D 天内装运包裹的能力

> 原文:[https://www . geesforgeks . org/d 天内运送包裹的能力/](https://www.geeksforgeeks.org/capacity-to-ship-packages-within-d-days/)

给定一个由表示 N 个项目的重量的正整数和一个正整数组成的数组，任务是找到一艘船的最小载重量(比如说， **K** )以在 **D** 天内装运所有重量，从而使装载在船上的重量的顺序与数组元素在**arr【】**中的顺序一致

**示例:**

> **输入:** arr[] = {1，2，1}，D = 2
> **输出:** 3
> **解释:**
> 将船所需的最小重量考虑为 **3** ，那么下面是重量的顺序，这样所有的重量都可以在 D(= 2)天内装运:
> **第 1 天:**将第一天数值 1 和数值 2 的重量作为重量 1 + 2 = 3 的总和装运(【T18
> **第二天:**将第二天价值 1 的重量作为重量 1 的总和发货(< = 3)。
> 考虑最小重量为 3，D(= 2)天内装运全部重量。因此，打印 3。
> 
> **输入:** arr[] = {9，8，10}，D = 3
> T3】输出: 10

**方法:**给定的问题可以用[贪心法](https://www.geeksforgeeks.org/greedy-algorithms/)和[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决。问题的单调性可以观察到，如果所有的包裹都可以在 **D** 天内以 **K** 的容量成功发货，那么肯定可以以任何大于 **K** 的容量发货。按照以下步骤解决问题:

*   初始化一个变量，将**和**表示为 **-1** ，以存储所需船只的最小容量。
*   初始化两个变量，比如说 **s** 和 **e** ，给定数组中的[最大元素和数组](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的[总和分别表示搜索空间的下限和上限。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   [迭代直到](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)的值 **s** 小于或等于 **e** ，并执行以下步骤:
    *   初始化一个变量，说**中间**为 **(s + e)/2** 。
    *   检查是否有可能在 **D** 天内装运所有包裹，此时允许的最大容量为**中**。如果发现**为真**，则将**和**的值更新为**中间**，将 **e** 的值更新为**(中间–1)**。
    *   否则，将 **s** 的值更新为**(中间+ 1)** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the weights
// can be delivered in D days or not
bool isValid(int weight[], int n,
             int D, int mx)
{
    // Stores the count of days required
    // to ship all the weights if the
    // maximum capacity is mx
    int st = 1;
    int sum = 0;

    // Traverse all the weights
    for (int i = 0; i < n; i++) {
        sum += weight[i];

        // If total weight is more than
        // the maximum capacity
        if (sum > mx) {
            st++;
            sum = weight[i];
        }

        // If days are more than D,
        // then return false
        if (st > D)
            return false;
    }

    // Return true for the days < D
    return true;
}

// Function to find the least weight
// capacity of a boat to ship all the
// weights within D days
void shipWithinDays(int weight[], int D,
                    int n)
{
    // Stores the total weights to
    // be shipped
    int sum = 0;

    // Find the sum of weights
    for (int i = 0; i < n; i++)
        sum += weight[i];

    // Stores the maximum weight in the
    // array that has to be shipped
    int s = weight[0];
    for (int i = 1; i < n; i++) {
        s = max(s, weight[i]);
    }

    // Store the ending value for
    // the search space
    int e = sum;

    // Store the required result
    int res = -1;

    // Perform binary search
    while (s <= e) {

        // Store the middle value
        int mid = s + (e - s) / 2;

        // If mid can be shipped, then
        // update the result and end
        // value of the search space
        if (isValid(weight, n, D, mid)) {
            res = mid;
            e = mid - 1;
        }

        // Search for minimum value
        // in the right part
        else
            s = mid + 1;
    }

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    int weight[] = { 9, 8, 10 };
    int D = 3;
    int N = sizeof(weight) / sizeof(weight[0]);
    shipWithinDays(weight, D, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to check if the weights
// can be delivered in D days or not
static boolean isValid(int[] weight, int n,
                       int D, int mx)
{

    // Stores the count of days required
    // to ship all the weights if the
    // maximum capacity is mx
    int st = 1;
    int sum = 0;

    // Traverse all the weights
    for(int i = 0; i < n; i++)
    {
        sum += weight[i];

        // If total weight is more than
        // the maximum capacity
        if (sum > mx)
        {
            st++;
            sum = weight[i];
        }

        // If days are more than D,
        // then return false
        if (st > D)
            return false;
    }

    // Return true for the days < D
    return true;
}

// Function to find the least weight
// capacity of a boat to ship all the
// weights within D days
static void shipWithinDays(int[] weight, int D, int n)
{

    // Stores the total weights to
    // be shipped
    int sum = 0;

    // Find the sum of weights
    for(int i = 0; i < n; i++)
        sum += weight[i];

    // Stores the maximum weight in the
    // array that has to be shipped
    int s = weight[0];
    for(int i = 1; i < n; i++)
    {
        s = Math.max(s, weight[i]);
    }

    // Store the ending value for
    // the search space
    int e = sum;

    // Store the required result
    int res = -1;

    // Perform binary search
    while (s <= e)
    {

        // Store the middle value
        int mid = s + (e - s) / 2;

        // If mid can be shipped, then
        // update the result and end
        // value of the search space
        if (isValid(weight, n, D, mid))
        {
            res = mid;
            e = mid - 1;
        }

        // Search for minimum value
        // in the right part
        else
            s = mid + 1;
    }

    // Print the result
    System.out.println(res);
}

// Driver Code
public static void main(String[] args)
{

    int[] weight = { 9, 8, 10 };
    int D = 3;
    int N = weight.length;

    shipWithinDays(weight, D, N);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the weights
# can be delivered in D days or not
def isValid(weight, n, D, mx):

    # Stores the count of days required
    # to ship all the weights if the
    # maximum capacity is mx
    st = 1
    sum = 0

    # Traverse all the weights
    for i in range(n):
        sum += weight[i]

        # If total weight is more than
        # the maximum capacity
        if (sum > mx):
            st += 1
            sum = weight[i]

        # If days are more than D,
        # then return false
        if (st > D):
            return False

    # Return true for the days < D
    return True

# Function to find the least weight
# capacity of a boat to ship all the
# weights within D days
def shipWithinDays(weight, D, n):

    # Stores the total weights to
    # be shipped
    sum = 0

    # Find the sum of weights
    for i in range(n):
        sum += weight[i]

    # Stores the maximum weight in the
    # array that has to be shipped
    s = weight[0]
    for i in range(1, n):
        s = max(s, weight[i])

    # Store the ending value for
    # the search space
    e = sum

    # Store the required result
    res = -1

    # Perform binary search
    while (s <= e):

        # Store the middle value
        mid = s + (e - s) // 2

        # If mid can be shipped, then
        # update the result and end
        # value of the search space
        if (isValid(weight, n, D, mid)):
            res = mid
            e = mid - 1

        # Search for minimum value
        # in the right part
        else:
            s = mid + 1

    # Print the result
    print(res)

# Driver Code
if __name__ == '__main__':

    weight = [ 9, 8, 10 ]
    D = 3
    N = len(weight)

    shipWithinDays(weight, D, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the weights
// can be delivered in D days or not
static bool isValid(int[] weight, int n,
                    int D, int mx)
{

    // Stores the count of days required
    // to ship all the weights if the
    // maximum capacity is mx
    int st = 1;
    int sum = 0;

    // Traverse all the weights
    for(int i = 0; i < n; i++)
    {
        sum += weight[i];

        // If total weight is more than
        // the maximum capacity
        if (sum > mx)
        {
            st++;
            sum = weight[i];
        }

        // If days are more than D,
        // then return false
        if (st > D)
            return false;
    }

    // Return true for the days < D
    return true;
}

// Function to find the least weight
// capacity of a boat to ship all the
// weights within D days
static void shipWithinDays(int[] weight, int D, int n)
{

    // Stores the total weights to
    // be shipped
    int sum = 0;

    // Find the sum of weights
    for(int i = 0; i < n; i++)
        sum += weight[i];

    // Stores the maximum weight in the
    // array that has to be shipped
    int s = weight[0];
    for(int i = 1; i < n; i++)
    {
        s = Math.Max(s, weight[i]);
    }

    // Store the ending value for
    // the search space
    int e = sum;

    // Store the required result
    int res = -1;

    // Perform binary search
    while (s <= e)
    {

        // Store the middle value
        int mid = s + (e - s) / 2;

        // If mid can be shipped, then
        // update the result and end
        // value of the search space
        if (isValid(weight, n, D, mid))
        {
            res = mid;
            e = mid - 1;
        }

        // Search for minimum value
        // in the right part
        else
            s = mid + 1;
    }

    // Print the result
    Console.WriteLine(res);
}

// Driver Code
public static void Main()
{
    int[] weight = { 9, 8, 10 };
    int D = 3;
    int N = weight.Length;

    shipWithinDays(weight, D, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if the weights
// can be delivered in D days or not
function isValid(weight, n,
                       D, mx)
{

    // Stores the count of days required
    // to ship all the weights if the
    // maximum capacity is mx
    let st = 1;
    let sum = 0;

    // Traverse all the weights
    for(let i = 0; i < n; i++)
    {
        sum += weight[i];

        // If total weight is more than
        // the maximum capacity
        if (sum > mx)
        {
            st++;
            sum = weight[i];
        }

        // If days are more than D,
        // then return false
        if (st > D)
            return false;
    }

    // Return true for the days < D
    return true;
}

// Function to find the least weight
// capacity of a boat to ship all the
// weights within D days
function shipWithinDays(weight, D, n)
{

    // Stores the total weights to
    // be shipped
    let sum = 0;

    // Find the sum of weights
    for(let i = 0; i < n; i++)
        sum += weight[i];

    // Stores the maximum weight in the
    // array that has to be shipped
    let s = weight[0];
    for(let i = 1; i < n; i++)
    {
        s = Math.max(s, weight[i]);
    }

    // Store the ending value for
    // the search space
    let e = sum;

    // Store the required result
    let res = -1;

    // Perform binary search
    while (s <= e)
    {

        // Store the middle value
        let mid = s + Math.floor((e - s) / 2);

        // If mid can be shipped, then
        // update the result and end
        // value of the search space
        if (isValid(weight, n, D, mid))
        {
            res = mid;
            e = mid - 1;
        }

        // Search for minimum value
        // in the right part
        else
            s = mid + 1;
    }

    // Print the result
    document.write(res);
}

// Driver Code

    let weight = [ 9, 8, 10 ];
    let D = 3;
    let N = weight.length;

    shipWithinDays(weight, D, N);

</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N * log(S–M))，其中 **S** 为数组元素* *之和 **M** 为数组最大元素*[](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)**。*
***辅助空间:** O(1)**