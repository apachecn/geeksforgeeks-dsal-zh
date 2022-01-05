# 计算将一个数组分成两半且总和相同的方法数

> 原文:[https://www . geeksforgeeks . org/count-将一个数组用同一个和分成两半的方法数/](https://www.geeksforgeeks.org/count-number-of-ways-to-divide-an-array-into-two-halves-with-same-sum/)

给定 N 个元素的整数数组。任务是找到将数组拆分成两个非零长度的等份和子数组的方法。

**示例:**

> **输入:** arr[] = {0，0，0，0}
> **输出:** 3
> **解释:**
> 所有可能的方式有:{ {{0}、{0，0，0}}、{{0，0}、{0，0}}、{{0，0，0}、{0}}
> 因此，需要的输出为 3。
> 
> **输入:** {1，-1，1，-1}
> 输出: 1

**简单解法**:一个简单的解法是生成所有可能的连续子数组对，并在那里求和。如果它们的总和相同，我们将增加一个计数。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效方法:**想法是取一个辅助数组 say，aux【】来计算数组的假定，这样对于一个索引**I**aux【I】将存储从索引 0 到索引 I 的所有元素的和。
通过这样做，我们可以
所以，想法是:

1.  找出数组中所有数字的和，并存储在一个变量中，比如 s。如果和是奇数，那么答案将是 0。
2.  遍历数组并继续计算元素的总和。在第一步，我们将使用变量 S 来保持从索引 0 到 I 的所有元素的总和。
    *   计算第一个指数的总和。
    *   如果此总和等于 S/2，则将路的数量增加 1。
3.  从 i=0 到 i=N-2 做这个。

以下是上述方法的实现:

## C++

```
// C++ program to count the number of ways to
// divide an array into two halves
// with the same sum

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of ways to
// divide an array into two halves
// with same sum
int cntWays(int arr[], int n)
{
    // if length of array is 1
    // answer will be 0 as we have
    // to split it into two
    // non-empty halves
    if (n == 1)
        return 0;

    // variables to store total sum,
    // current sum and count
    int tot_sum = 0, sum = 0, ans = 0;

    // finding total sum
    for (int i = 0; i < n; i++)
        tot_sum += arr[i];

    // checking if sum equals total_sum/2
    for (int i = 0; i < n - 1; i++) {
        sum += arr[i];
        if (sum == tot_sum / 2)
            ans++;
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, -1, 1, -1, 1, -1 };

    int n = sizeof(arr) / sizeof(int);

    cout << cntWays(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of ways to
// divide an array into two halves
// with the same sum
class GFG
{

    // Function to count the number of ways to
    // divide an array into two halves
    // with same sum
    static int cntWays(int arr[], int n)
    {
        // if length of array is 1
        // answer will be 0 as we have
        // to split it into two
        // non-empty halves
        if (n == 1)
        {
            return 0;
        }

        // variables to store total sum,
        // current sum and count
        int tot_sum = 0, sum = 0, ans = 0;

        // finding total sum
        for (int i = 0; i < n; i++)
        {
            tot_sum += arr[i];
        }

        // checking if sum equals total_sum/2
        for (int i = 0; i < n - 1; i++)
        {
            sum += arr[i];
            if (sum == tot_sum / 2)
            {
                ans++;
            }
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {1, -1, 1, -1, 1, -1};

        int n = arr.length;

        System.out.println(cntWays(arr, n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to count the number of ways to
# divide an array into two halves
# with the same sum

# Function to count the number of ways to
# divide an array into two halves
# with same sum
def cntWays(arr, n):
    # if length of array is 1
    # answer will be 0 as we have
    # to split it into two
    # non-empty halves
    if (n == 1):
        return 0;

    # variables to store total sum,
    # current sum and count
    tot_sum = 0; sum = 0; ans = 0;

    # finding total sum
    for i in range(0,n):
        tot_sum += arr[i];

    # checking if sum equals total_sum/2
    for i in range(0,n-1):
        sum += arr[i];
        if (sum == tot_sum / 2):
            ans+=1;
    return ans;

# Driver Code
arr = [1, -1, 1, -1, 1, -1 ];

n = len(arr);

print(cntWays(arr, n));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to count the number of ways to
// divide an array into two halves with
// the same sum
using System;

class GFG
{

    // Function to count the number of ways to
    // divide an array into two halves
    // with same sum
    static int cntWays(int []arr, int n)
    {
        // if length of array is 1
        // answer will be 0 as we have
        // to split it into two
        // non-empty halves
        if (n == 1)
        {
            return 0;
        }

        // variables to store total sum,
        // current sum and count
        int tot_sum = 0, sum = 0, ans = 0;

        // finding total sum
        for (int i = 0; i < n; i++)
        {
            tot_sum += arr[i];
        }

        // checking if sum equals total_sum/2
        for (int i = 0; i < n - 1; i++)
        {
            sum += arr[i];
            if (sum == tot_sum / 2)
            {
                ans++;
            }
        }

        return ans;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, -1, 1, -1, 1, -1};

        int n = arr.Length;

        Console.WriteLine(cntWays(arr, n));
    }
}

// This code contributed by anuj_67..
```

## java 描述语言

```
<script>

      // JavaScript program to count the number of ways to
      // divide an array into two halves
      // with the same sum

      // Function to count the number of ways to
      // divide an array into two halves
      // with same sum
      function cntWays(arr, n)
      {
        // if length of array is 1
        // answer will be 0 as we have
        // to split it into two
        // non-empty halves
        if (n == 1) return 0;

        // variables to store total sum,
        // current sum and count
        var tot_sum = 0,
          sum = 0,
          ans = 0;

        // finding total sum
        for (var i = 0; i < n; i++) tot_sum += arr[i];

        // checking if sum equals total_sum/2
        for (var i = 0; i < n - 1; i++) {
          sum += arr[i];
          if (sum == tot_sum / 2)
          ans++;
        }

        return ans;
      }

      // Driver Code
      var arr = [1, -1, 1, -1, 1, -1];
      var n = arr.length;
      document.write(cntWays(arr, n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)