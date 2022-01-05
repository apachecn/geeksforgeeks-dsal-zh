# 给定两个数组的最小总和

> 原文:[https://www . geeksforgeeks . org/给定两个数组的最小总和/](https://www.geeksforgeeks.org/minimum-total-sum-from-the-given-two-arrays/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** 的 **N** 正整数和一个成本 **C** 。我们可以从给定数组的每个索引中选择任何一个元素，即对于任何索引 **i** ，我们只能选择元素**A【I】**或**B【I】**。任务是找到从给定的两个数组中选择 **N** 元素的最小总和，如果我们在下一次迭代中选择从 **A[]** 到 **B[]** 或反之的任何元素，那么成本 **C** 也会被加到总和中。

**注:**按指数递增顺序选择元素，即 **0 ≤ i < N** 。

**示例:**

> **输入:** N = 9，A[] = {7，6，18，6，16，18，1，17，17}，B[] = {6，9，3，10，9，1，10，1，5}，C = 2
> **输出:** 49
> **解释:**
> 从数组 A 中取第一个元素时，求和= 7
> 从数组 A 中取第二个元素时，求和= 7 + 6 = 13 当我们从数组 A 进入数组 B 时，sum = 13 + 3 + 2 = 18
> 当我们从数组 A 中取出第 4 个元素时，当我们从数组 B 进入数组 A 时，sum = 18 + 6 + 2 = 26
> 当我们从数组 B 中取出第 5 个元素时，当我们从数组 A 进入数组 B 时， sum = 26 + 9 + 2 = 37
> 取数组 B 的第 6 个元素时，sum = 37 + 1 = 38
> 取数组 A 的第 7 个元素时，当我们从数组 B 进入到数组 A 时，sum = 38 + 1 + 2 = 41
> 取数组 B 的第 8 个元素时，当我们从数组 A 进入到数组 B 时，sum = 41 + 1 + 2 = 44
> 取数组 B 的第 9 个元素时，sum = 44 + 5 = 49。
> 
> **输入:** N = 9，A = {3，2，3，1，3，1，4，1}，B = {1，2，3，4，4，1，2，1，3}，C = 1
> **输出:** 18
> **解释:**
> 从数组 B 中取出第一个元素时，sum = 1
> 从数组 A 中取出第二个元素时，sum = 1 + 2 = 3
> 从数组 B 中取出第三个元素时 sum = 3 + 3 = 6
> 从数组 A 中取第 4 个元素时，sum = 6 + 1 = 7
> 从数组 A 中取第 5 个元素时，sum = 7 + 3 = 10
> 从数组 B 中取第 6 个元素时，当我们从数组 A 进入数组 B 时，sum = 10 + 1 + 1 = 12
> 从数组 A 中取第 7 个元素时， 当我们从数组 B 进入到数组 A 时，sum = 12 + 1 + 1 = 14
> 当我们从数组 A 进入到数组 B 时，sum = 14 + 1 + 1 = 16
> 当我们从数组 A 进入到数组 B 时，sum = 16 + 1 + 1 = 18。

**方法:**我们将使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决这个问题。以下是步骤:

1.  创建一个由 **N** 行和两列组成的 2D 数组 **dp[][]** ，并将 dp 的所有元素初始化为**无穷大**。
2.  从两个数组中添加元素可能有 4 种情况:
    *   当先前添加的元素来自数组 a[]时，从数组 a[]添加元素。
    *   当先前添加的元素来自数组 b[]时，从数组 a[]添加元素。在这种情况下，将整数 C 与结果相加是一种惩罚。
    *   当先前添加的元素来自数组 b[]时，从数组 b[]添加元素。
    *   当先前添加的元素来自数组 a[]时，从数组 b[]添加元素。在这种情况下，将整数 C 与结果相加是一种惩罚。
3.  每次用上述四个条件的最小值更新 dp 数组。
4.  **DP[N-1][0]****DP[N-1][1]**的最小值是选择 **N** 元素的最小总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that prints minimum sum
// after selecting N elements
void minimumSum(int a[], int b[],
                int c, int n)
{

    // Initialise the dp array
    vector<vector<int> > dp(n,
                            vector<int>(2,
                                        1e6));

    // Base Case
    dp[0][0] = a[0];
    dp[0][1] = b[0];

    for (int i = 1; i < n; i++) {

        // Adding the element of array a if
        // previous element is also from array a
        dp[i][0] = min(dp[i][0],
                    dp[i - 1][0] + a[i]);

        // Adding the element of array a if
        // previous element is from array b
        dp[i][0] = min(dp[i][0],
                    dp[i - 1][1] + a[i] + c);

        // Adding the element of array b if
        // previous element is from array a
        // with an extra penalty of integer C
        dp[i][1] = min(dp[i][1],
                    dp[i - 1][0] + b[i] + c);

        // Adding the element of array b if
        // previous element is also from array b
        dp[i][1] = min(dp[i][1],
                    dp[i - 1][1] + b[i]);
    }

    // Print the minimum sum
    cout << min(dp[n - 1][0],
                dp[n - 1][1])
        << "\n";
}

// Driver Code
int main()
{
    // Given array arr1[] and arr2[]
    int arr1[] = { 7, 6, 18, 6, 16,
                18, 1, 17, 17 };

    int arr2[] = { 6, 9, 3, 10, 9,
                1, 10, 1, 5 };

    // Given cost
    int C = 2;

    int N = sizeof(arr1) / sizeof(arr1[0]);

    // Function Call
    minimumSum(arr1, arr2, C, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that prints minimum sum
// after selecting N elements
static void minimumSum(int a[], int b[],
                       int c, int n)
{

    // Initialise the dp array
    int [][]dp = new int[n][2];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            dp[i][j] = (int) 1e6;
        }
    }

    // Base Case
    dp[0][0] = a[0];
    dp[0][1] = b[0];

    for(int i = 1; i < n; i++)
    {

        // Adding the element of array a if
        // previous element is also from array a
        dp[i][0] = Math.min(dp[i][0],
                            dp[i - 1][0] + a[i]);

        // Adding the element of array a if
        // previous element is from array b
        dp[i][0] = Math.min(dp[i][0],
                            dp[i - 1][1] + a[i] + c);

        // Adding the element of array b if
        // previous element is from array a
        // with an extra penalty of integer C
        dp[i][1] = Math.min(dp[i][1],
                            dp[i - 1][0] + b[i] + c);

        // Adding the element of array b if
        // previous element is also from array b
        dp[i][1] = Math.min(dp[i][1],
                            dp[i - 1][1] + b[i]);
    }

    // Print the minimum sum
    System.out.print(Math.min(dp[n - 1][0],
                              dp[n - 1][1]) + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr1[] and arr2[]
    int arr1[] = { 7, 6, 18, 6, 16,
                   18, 1, 17, 17 };

    int arr2[] = { 6, 9, 3, 10, 9,
                   1, 10, 1, 5 };

    // Given cost
    int C = 2;

    int N = arr1.length;

    // Function call
    minimumSum(arr1, arr2, C, N);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that prints minimum sum
# after selecting N elements
def minimumSum(a, b, c, n):

    # Initialise the dp array
    dp = [[1e6 for i in range(2)]
            for j in range(n)]

    # Base Case
    dp[0][0] = a[0]
    dp[0][1] = b[0]

    for i in range(1, n):

        # Adding the element of array a if
        # previous element is also from array a
        dp[i][0] = min(dp[i][0],
                    dp[i - 1][0] + a[i])

        # Adding the element of array a if
        # previous element is from array b
        dp[i][0] = min(dp[i][0],
                    dp[i - 1][1] + a[i] + c)

        # Adding the element of array b if
        # previous element is from array a
        # with an extra penalty of integer C
        dp[i][1] = min(dp[i][1],
                    dp[i - 1][0] + b[i] + c)

        # Adding the element of array b if
        # previous element is also from array b
        dp[i][1] = min(dp[i][1],
                    dp[i - 1][1] + b[i])

    # Print the minimum sum
    print(min(dp[n - 1][0], dp[n - 1][1]))

# Driver code
if __name__ == '__main__':

    # Given array arr[]
    arr1 = [ 7, 6, 18, 6, 16,
            18, 1, 17, 17 ]

    arr2 = [ 6, 9, 3, 10, 9,
            1, 10, 1, 5 ]

    # Given cost
    C = 2

    N = len(arr1)

    # Function Call
    minimumSum(arr1, arr2, C, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that prints minimum sum
// after selecting N elements
static void minimumSum(int []a, int []b,
                       int c, int n)
{

    // Initialise the dp array
    int [,]dp = new int[n, 2];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            dp[i, j] = (int)1e6;
        }
    }

    // Base Case
    dp[0, 0] = a[0];
    dp[0, 1] = b[0];

    for(int i = 1; i < n; i++)
    {

        // Adding the element of array a if
        // previous element is also from array a
        dp[i, 0] = Math.Min(dp[i, 0],
                            dp[i - 1, 0] + a[i]);

        // Adding the element of array a if
        // previous element is from array b
        dp[i, 0] = Math.Min(dp[i, 0],
                            dp[i - 1, 1] + a[i] + c);

        // Adding the element of array b if
        // previous element is from array a
        // with an extra penalty of integer C
        dp[i, 1] = Math.Min(dp[i, 1],
                            dp[i - 1, 0] + b[i] + c);

        // Adding the element of array b if
        // previous element is also from array b
        dp[i, 1] = Math.Min(dp[i, 1],
                            dp[i - 1, 1] + b[i]);
    }

    // Print the minimum sum
    Console.Write(Math.Min(dp[n - 1, 0],
                           dp[n - 1, 1]) + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array arr1[] and arr2[]
    int []arr1 = { 7, 6, 18, 6, 16,
                   18, 1, 17, 17 };

    int []arr2 = { 6, 9, 3, 10, 9,
                   1, 10, 1, 5 };

    // Given cost
    int C = 2;

    int N = arr1.Length;

    // Function call
    minimumSum(arr1, arr2, C, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that prints minimum sum
// after selecting N elements
function minimumSum(a, b, c, n)
{

    // Initialise the dp array
    let dp =  new Array(n);
    for (var i = 0; i < dp.length; i++) {
    dp[i] = new Array(2);
    }

    for(let i = 0; i < n; i++)
    {
        for(let j = 0; j < 2; j++)
        {
            dp[i][j] = 1e6;
        }
    }

    // Base Case
    dp[0][0] = a[0];
    dp[0][1] = b[0];

    for(let i = 1; i < n; i++)
    {

        // Adding the element of array a if
        // previous element is also from array a
        dp[i][0] = Math.min(dp[i][0],
                            dp[i - 1][0] + a[i]);

        // Adding the element of array a if
        // previous element is from array b
        dp[i][0] = Math.min(dp[i][0],
                            dp[i - 1][1] + a[i] + c);

        // Adding the element of array b if
        // previous element is from array a
        // with an extra penalty of integer C
        dp[i][1] = Math.min(dp[i][1],
                            dp[i - 1][0] + b[i] + c);

        // Adding the element of array b if
        // previous element is also from array b
        dp[i][1] = Math.min(dp[i][1],
                            dp[i - 1][1] + b[i]);
    }

    // Print the minimum sum
    document.write(Math.min(dp[n - 1][0],
                              dp[n - 1][1]) + "<br/>");
}

// Driver Code

    // Given array arr1[] and arr2[]
    let arr1 = [ 7, 6, 18, 6, 16,
                   18, 1, 17, 17 ];

    let arr2 = [ 6, 9, 3, 10, 9,
                   1, 10, 1, 5 ];

    // Given cost
    let C = 2;

    let N = arr1.length;

    // Function call
    minimumSum(arr1, arr2, C, N);

</script>
```

**Output:** 

```
49
```

**时间复杂度:**T2【O(N)T4】