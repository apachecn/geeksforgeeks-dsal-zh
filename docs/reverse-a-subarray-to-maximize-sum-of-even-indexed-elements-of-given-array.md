# 反转子阵列，使给定阵列的偶数索引元素之和最大化

> 原文:[https://www . geesforgeks . org/reverse-a-subarray-to-max-sum-of-even-indexed-elements-of-the-of-the-给定数组/](https://www.geeksforgeeks.org/reverse-a-subarray-to-maximize-sum-of-even-indexed-elements-of-given-array/)

给定一个数组 **arr[]** ，任务是通过反转一个子数组来最大化偶数索引元素的和，并打印得到的最大和。

**示例:**

> **输入:** arr[] = {1，2，1，2，1}
> **输出:** 5
> **解释:**
> 初始偶数索引元素之和= a[0] + a[2] + a[4] = 1 + 1 + 1 = 3
> 反转子阵列{1，2，1，2}将数组修改为{2，1，2，1，1}。
> 因此，最大和= 2 + 2 + 1 = 5
> 
> **输入:** arr[] = {7，8，4，5，7，6，8，9，7，3}
> **输出:** 37

**天真方法:**
解决这个问题最简单的方法是通过逐个反转元素来生成所有可能的排列，并计算每个排列在偶数索引处的和。打印所有排列中最大可能的总和。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**高效方法:**
通过使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)检查数组旋转的最大差异，上述方法可以进一步优化为 ***O(N)计算复杂度*** 。
按照以下步骤解决问题:

*   比较奇数索引和偶数索引的元素，并跟踪它们。
*   初始化两个数组 **leftDP[]** 和 **rightDP[]** 。
*   对于每一个奇数索引， **leftDP[]** 存储当前索引处的元素与其左侧元素的差值，而 rightDP[]存储右侧元素的差值。
*   如果为上一个指数计算的差值为正，将其添加到当前差值中:

> if(DP[I–1]> 0)
> DP[I]= DP[I-1]+curr _ diff

*   否则，存储当前差值:

> S7-1200 可编程控制器：

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return maximized sum
// at even indices
int maximizeSum(int arr[], int n)
{
    int sum = 0;
    for(int i = 0; i < n; i = i + 2)
        sum += arr[i];

    // Stores difference with
    // element on the left
    int leftDP[n / 2];

    // Stores difference with
    // element on the right
    int rightDP[n / 2];

    int c = 0;

    for(int i = 1; i < n; i = i + 2)
    {

        // Compute and store
        // left difference
        int leftDiff = arr[i] - arr[i - 1];

        // For first index
        if (c - 1 < 0)
            leftDP = leftDiff;

        else
        {

            // If previous difference
            // is positive
            if (leftDP > 0)
                leftDP = leftDiff + leftDP;

            // Otherwise
            else
                leftDP[i] = leftDiff;
        }

        int rightDiff;

        // For the last index
        if (i + 1 >= n)
            rightDiff = 0;

        // Otherwise
        else
            rightDiff = arr[i] - arr[i + 1];

        // For first index
        if (c - 1 < 0)
            rightDP = rightDiff;
        else
        {

            // If the previous difference
            // is positive
            if (rightDP > 0)
                rightDP = rightDiff +
                             rightDP;
            else
                rightDP = rightDiff;
        }
        c++;
    }
    int maxi = 0;
    for(int i = 0; i < n / 2; i++)
    {
        maxi = max(maxi, max(leftDP[i],
                            rightDP[i]));
    }
    return maxi + sum;
}

// Driver Code
int main()
{
    int arr[] = { 7, 8, 4, 5, 7,
                  6, 8, 9, 7, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int ans = maximizeSum(arr, n);

    cout << (ans);
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;

class GFG {

    // Function to return maximized sum
    // at even indices
    public static int maximizeSum(int[] arr)
    {

        int n = arr.length;
        int sum = 0;
        for (int i = 0; i < n; i = i + 2)
            sum += arr[i];

        // Stores difference with
        // element on the left
        int leftDP[] = new int[n / 2];

        // Stores difference with
        // element on the right
        int rightDP[] = new int[n / 2];

        int c = 0;

        for (int i = 1; i < n; i = i + 2) {

            // Compute and store
            // left difference
            int leftDiff = arr[i]
                           - arr[i - 1];

            // For first index
            if (c - 1 < 0)
                leftDP = leftDiff;

            else {

                // If previous difference
                // is positive
                if (leftDP > 0)
                    leftDP = leftDiff
                                + leftDP;

                // Otherwise
                else
                    leftDP[i] = leftDiff;
            }

            int rightDiff;

            // For the last index
            if (i + 1 >= arr.length)
                rightDiff = 0;

            // Otherwise
            else
                rightDiff = arr[i]
                            - arr[i + 1];

            // For first index
            if (c - 1 < 0)
                rightDP = rightDiff;
            else {

                // If the previous difference
                // is positive
                if (rightDP > 0)
                    rightDP = rightDiff
                                 + rightDP;
                else
                    rightDP = rightDiff;
            }
            c++;
        }
        int max = 0;
        for (int i = 0; i < n / 2; i++) {
            max = Math.max(max,
                           Math.max(
                               leftDP[i],
                               rightDP[i]));
        }

        return max + sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 7, 8, 4, 5, 7, 6,
                      8, 9, 7, 3 };
        int ans = maximizeSum(arr);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return maximized sum
# at even indices
def maximizeSum(arr):

    n = len(arr)
    sum = 0

    for i in range(0, n, 2):
        sum += arr[i]

    # Stores difference with
    # element on the left
    leftDP = [0] * (n)

    # Stores difference with
    # element on the right
    rightDP = [0] * (n)

    c = 0
    for i in range(1, n, 2):

        # Compute and store
        # left difference
        leftDiff = arr[i] - arr[i - 1]

        # For first index
        if (c - 1 < 0):
            leftDP[i] = leftDiff
        else:

            # If previous difference
            # is positive
            if (leftDP[i] > 0):
                leftDP[i] = (leftDiff +
                             leftDP[i - 1])

            # Otherwise
            else:
                leftDP[i] = leftDiff

        rightDiff = 0

        # For the last index
        if (i + 1 >= len(arr)):
            rightDiff = 0

        # Otherwise
        else:
            rightDiff = arr[i] - arr[i + 1]

        # For first index
        if (c - 1 < 0):
            rightDP[i] = rightDiff
        else:

            # If the previous difference
            # is positive
            if (rightDP[i] > 0):
                rightDP[i] = (rightDiff +
                              rightDP[i - 1])
            else:
                rightDP[i] = rightDiff

        c += 1

    maxm = 0

    for i in range(n // 2):
        maxm = max(maxm, max(leftDP[i],
                            rightDP[i]))

    return maxm + sum

# Driver Code
if __name__ == '__main__':

    arr = [ 7, 8, 4, 5, 7,
            6, 8, 9, 7, 3 ]
    ans = maximizeSum(arr)

    print(ans)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return maximized sum
// at even indices
public static int maximizeSum(int[] arr)
{
    int n = arr.Length;
    int sum = 0;

    for(int i = 0; i < n; i = i + 2)
        sum += arr[i];

    // Stores difference with
    // element on the left
    int []leftDP = new int[n / 2];

    // Stores difference with
    // element on the right
    int []rightDP = new int[n / 2];

    int c = 0;

    for(int i = 1; i < n; i = i + 2)
    {

        // Compute and store
        // left difference
        int leftDiff = arr[i] - arr[i - 1];

        // For first index
        if (c - 1 < 0)
            leftDP = leftDiff;

        else
        {

            // If previous difference
            // is positive
            if (leftDP > 0)
                leftDP = leftDiff +
                            leftDP;

            // Otherwise
            else
                leftDP = leftDiff;
        }

        int rightDiff;

        // For the last index
        if (i + 1 >= arr.Length)
            rightDiff = 0;

        // Otherwise
        else
            rightDiff = arr[i] - arr[i + 1];

        // For first index
        if (c - 1 < 0)
            rightDP = rightDiff;

        else
        {

            // If the previous difference
            // is positive
            if (rightDP > 0)
                rightDP = rightDiff +
                             rightDP;
            else
                rightDP = rightDiff;
        }
        c++;
    }

    int max = 0;

    for(int i = 0; i < n / 2; i++)
    {
        max = Math.Max(max,
                       Math.Max(leftDP[i],
                               rightDP[i]));
    }
    return max + sum;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 7, 8, 4, 5, 7, 6,
                  8, 9, 7, 3 };
    int ans = maximizeSum(arr);

    Console.WriteLine(ans);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to return maximized sum
    // at even indices
function maximizeSum(arr)
{
    let n = arr.length;
        let sum = 0;
        for (let i = 0; i < n; i = i + 2)
            sum += arr[i];

        // Stores difference with
        // element on the left
        let leftDP = new Array(Math.floor(n / 2));

        // Stores difference with
        // element on the right
        let rightDP = new Array(Math.floor(n / 2));

         for(let i=0;i<n/2;i++)
        {
            leftDP[i]=0;
            rightDP[i]=0;
        }

        let c = 0;

        for (let i = 1; i < n; i = i + 2) {

            // Compute and store
            // left difference
            let leftDiff = arr[i]
                           - arr[i - 1];

            // For first index
            if (c - 1 < 0)
                leftDP[i] = leftDiff;

            else {

                // If previous difference
                // is positive
                if (leftDP[i] > 0)
                    leftDP[i] = leftDiff
                                + leftDP[i-1];

                // Otherwise
                else
                    leftDP[i] = leftDiff;
            }

            let rightDiff;

            // For the last index
            if (i + 1 >= arr.length)
                rightDiff = 0;

            // Otherwise
            else
                rightDiff = arr[i]
                            - arr[i + 1];

            // For first index
            if (c - 1 < 0)
                rightDP[i] = rightDiff;
            else {

                // If the previous difference
                // is positive
                if (rightDP[i] > 0)
                    rightDP[i] = rightDiff
                                 + rightDP[i-1];
                else
                    rightDP[i] = rightDiff;
            }
            c++;
        }
        let max = 0;
        for (let i = 0; i < n / 2; i++) {
            max = Math.max(max,
                           Math.max(
                               leftDP[i],
                               rightDP[i]));
        }

        return max + sum;
}

// Driver Code
let arr=[7, 8, 4, 5, 7, 6,
                      8, 9, 7, 3];
let ans = maximizeSum(arr);
document.write(ans);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
37
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*