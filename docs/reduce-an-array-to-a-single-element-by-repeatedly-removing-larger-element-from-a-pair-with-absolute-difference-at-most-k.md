# 通过从绝对差最多为 K 的一对中重复移除较大的元素，将数组简化为单个元素

> 原文:[https://www . geesforgeks . org/通过从最多绝对差为 k 的对中重复移除较大的元素来将数组减少为单个元素/](https://www.geeksforgeeks.org/reduce-an-array-to-a-single-element-by-repeatedly-removing-larger-element-from-a-pair-with-absolute-difference-at-most-k/)

给定一个由 **N** 整数**T7】和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过重复移除绝对差最多为**K**的两个元素对中较大的一个来检查给定数组是否可以简化为单个元素。如果数组可以简化为单个元素，则打印**“是”**。否则，打印**“否”**。**

**示例:**

> **输入:** arr[] = {2，1，1，3}，K = 1
> **输出:**是
> **解释:**
> **操作 1:** 选择配对{arr[0]，arr[3]} ( = (2，3)，为| 3–2 |≤1。现在，从数组中移除 3。数组修改为{2，1，1}。
> **操作 2:** 选择对{arr[0]，arr[1]} ( = (2，1)，为| 2–1 |≤1。现在，从数组中移除 2。数组修改为{1，1}。
> **操作 3:** 从数组中移除 1。数组修改为{1}。
> 因此，最后剩余的数组元素为 1。
> 
> **输入:** arr[] = {1，4，3，6}，K = 1
> T3】输出:否

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。其思想是在每一个可能的移动中移除具有最大值的[元素。按照给定的步骤解决问题:](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

*   [按降序排列给定数组**arr[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [在指数**【0，N–2】**范围内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**【arr】**。如果**arr【I】**和**arr【I+1】**的绝对值大于 **K** ，则打印**“否”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   如果循环完全执行，则打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if an array can be
// reduced to single element by removing
// maximum element among any chosen pairs
void canReduceArray(int arr[], int N, int K)
{
    // Sort the array in descending order
    sort(arr, arr + N, greater<int>());

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // If the absolute difference
        // of 2 consecutive array
        // elements is greater than K
        if (arr[i] - arr[i + 1] > K) {

            cout << "No";
            return;
        }
    }

    // If the array can be reduced
    // to a single element
    cout << "Yes";
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 1, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 1;

    // Function Call to check
    // if an array can be reduced
    // to a single element
    canReduceArray(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to check if an array can be
// reduced to single element by removing
// maximum element among any chosen pairs
static void canReduceArray(int arr[], int N, int K)
{

    // Sort the array in descending order
    Arrays.sort(arr);
    int b[] = new int[N];
        int j = N;
        for (int i = 0; i < N; i++) {
            b[j - 1] = arr[i];
            j = j - 1;
        }
    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // If the absolute difference
        // of 2 consecutive array
        // elements is greater than K
        if (arr[i] - arr[i + 1] > K) {

            System.out.print("No");
            return;
        }
    }

    // If the array can be reduced
    // to a single element
    System.out.print("Yes");
}

// Driven Code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 1, 3 };
    int N = arr.length;
    int K = 1;

    // Function Call to check
    // if an array can be reduced
    // to a single element
    canReduceArray(arr, N, K);
}
}

// This code is contributed by splevel62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if an array can be
# reduced to single element by removing
# maximum element among any chosen pairs
def canReduceArray(arr, N, K):

    # Sort the array in descending order
    arr = sorted(arr)

    # Traverse the array
    for i in range(N - 1):

        # If the absolute difference
        # of 2 consecutive array
        # elements is greater than K
        if (arr[i] - arr[i + 1] > K):
            print ("No")
            return

    # If the array can be reduced
    # to a single element
    print ("Yes")

# Driver Code
if __name__ == '__main__':

    arr = [2, 1, 1, 3]
    N = len(arr)
    K = 1

    # Function Call to check
    # if an array can be reduced
    # to a single element
    canReduceArray(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if an array can be
// reduced to single element by removing
// maximum element among any chosen pairs
static void canReduceArray(int[] arr, int N,
                           int K)
{

    // Sort the array in descending order
    Array.Sort(arr);
    int[] b = new int[N];
    int j = N;

    for(int i = 0; i < N; i++)
    {
        b[j - 1] = arr[i];
        j = j - 1;
    }

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {

        // If the absolute difference
        // of 2 consecutive array
        // elements is greater than K
        if (arr[i] - arr[i + 1] > K)
        {
            Console.WriteLine("No");
            return;
        }
    }

    // If the array can be reduced
    // to a single element
    Console.WriteLine("Yes");
}

// Driver Code
public static void Main(String []args)
{
    int[] arr = { 2, 1, 1, 3 };
    int N = arr.Length;
    int K = 1;

    // Function Call to check
    // if an array can be reduced
    // to a single element
    canReduceArray(arr, N, K);
}
}

// This code is contributed by souravghosh0416
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to check if an array can be
// reduced to single element by removing
// maximum element among any chosen pairs
function canReduceArray(arr, N, K)
{

    // Sort the array in descending order
    arr.sort();
    let b = Array(N ).fill(0);
        let j = N;
        for (let i = 0; i < N; i++) {
            b[j - 1] = arr[i];
            j = j - 1;
        }
    // Traverse the array
    for (let i = 0; i < N - 1; i++) {

        // If the absolute difference
        // of 2 consecutive array
        // elements is greater than K
        if (arr[i] - arr[i + 1] > K) {

            document.write("No");
            return;
        }
    }

    // If the array can be reduced
    // to a single element
    document.write("Yes");
}

// Driver Code

    let arr = [ 2, 1, 1, 3 ];
    let N = arr.length;
    let K = 1;

    // Function Call to check
    // if an array can be reduced
    // to a single element
    canReduceArray(arr, N, K);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*