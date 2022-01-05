# 求和最小的三元组

> 原文:[https://www . geeksforgeeks . org/find-triple-with-minimum-sum/](https://www.geeksforgeeks.org/find-triplet-with-minimum-sum/)

给定一组不同的整数 **arr[]** 。任务是找到具有最小和的三元组(一组 3 个元素)。
**注:**阵的大小总是大于两个。
**例:**

```
Input : arr[] = {1, 2, 3, 4, -1, 5, -2}
Output : -2
1 - 1 - 2 = -2
Input : arr[] = {5, 6, 0, 0, 1}
Output : 1
0 + 0 + 1.
```

**天真法:**想法是生成数组中所有可能的三元组，然后将一个三元组的和与其他三元组进行比较，然后找到最小和。
以下是上述办法的实施情况:

## C++

```
// C++ Program to find triplet with minimum sum
#include <bits/stdc++.h>
using namespace std;

// Function to find triplet with minimum sum
int getMinimumSum(int arr[] , int n)
{
    int ans = INT_MAX;

    // Generate all possible triplets
    for (int i = 0; i < n - 2; i++) {
        for (int j = i + 1; j < n - 1; j++) {
            for (int k = j + 1; k < n; k++) {
                // Calculate sum of each triplet
                // and update minimum
                ans = min(ans, arr[i] + arr[j] + arr[k]);
            }
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, -1, 5, -2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getMinimumSum(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find triplet with minimum sum
class GFG
{

// Function to find triplet with minimum sum
static int getMinimumSum(int arr[] , int n)
{
    int ans = Integer.MAX_VALUE;

    // Generate all possible triplets
    for (int i = 0; i < n - 2; i++)
    {
        for (int j = i + 1; j < n - 1; j++)
        {
            for (int k = j + 1; k < n; k++)
            {
                // Calculate sum of each triplet
                // and update minimum
                ans = Math.min(ans, arr[i] +
                                arr[j] + arr[k]);
            }
        }
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, -1, 5, -2 };
    int n = arr.length;

    System.out.print(getMinimumSum(arr, n) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Program to find triplet with minimum sum
import sys

# Function to find triplet with minimum sum
def getMinimumSum(arr, n):
    ans = sys.maxsize;

    # Generate all possible triplets
    for i in range(n - 2):
        for j in range(i + 1, n - 1):
            for k in range(j + 1, n):

                # Calculate sum of each triplet
                # and update minimum
                ans = min(ans, arr[i] + arr[j] + arr[k]);
    return ans;

# Driver Code
if __name__ == '__main__':
    arr = [ 1, 2, 3, 4, 5, -1, 5, -2 ];
    n = len(arr);

    print(getMinimumSum(arr, n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# Program to find triplet with minimum sum
using System;

class GFG
{

    // Function to find triplet with minimum sum
    static int getMinimumSum(int []arr, int n)
    {
        int ans = int.MaxValue;

        // Generate all possible triplets
        for (int i = 0; i < n - 2; i++)
        {
            for (int j = i + 1; j < n - 1; j++)
            {
                for (int k = j + 1; k < n; k++)
                {
                    // Calculate sum of each triplet
                    // and update minimum
                    ans = Math.Min(ans, arr[i] +
                                    arr[j] + arr[k]);
                }
            }
        }

        return ans;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4, 5, -1, 5, -2 };
        int n = arr.Length;

        Console.WriteLine(getMinimumSum(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript Program to find
// triplet with minimum sum

// Function to find triplet with minimum sum
function getMinimumSum(arr, n)
{
    let ans = Number.MAX_SAFE_INTEGER;

    // Generate all possible triplets
    for (let i = 0; i < n - 2; i++) {
        for (let j = i + 1; j < n - 1; j++)
        {
            for (let k = j + 1; k < n; k++)
            {
                // Calculate sum of each triplet
                // and update minimum
                ans = Math.min(ans, arr[i] +
                      arr[j] + arr[k]);
            }
        }
    }

    return ans;
}

// Driver Code
    let arr = [ 1, 2, 3, 4, 5, -1, 5, -2 ];
    let n = arr.length;

    document.write(getMinimumSum(arr, n) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
-2
```