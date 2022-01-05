# 通过划分每个元素使数组和最多为 K 的最小数

> 原文:[https://www . geeksforgeeks . org/最小数字对最多 k 个元素进行数组求和/](https://www.geeksforgeeks.org/smallest-number-to-make-array-sum-at-most-k-by-dividing-each-element/)

给定一个大小为 **N** 的数组**arr【】**和一个数字 **K** ，任务是找到最小的数字 **M** ，这样当该数组的每个元素除以数字 **M** 时，该数组的和变得小于或等于数字 **K** 。
**注意:**除法的每个结果都被舍入到大于或等于该元素的最近整数。例如:10/3 = 4 和 6/2 = 3

**示例:**

> **输入:** arr[] = {2，3，4，9}，K = 6
> **输出:** 4
> **解释:**
> 当每个元素除以 4-2/4+3/4+4/4+9/4 = 1+1+3 = 6
> 当每个元素除以 3- 2/3 + 3/3 + 4/3 + 9/3 = 1 + 1 + 2 + 3 = 7 大于 K .【t10t
> **输入:** arr[] = {5，6，7，8}，K = 4
> **输出:** 8

**天真法:**这个问题的天真法是从 1 开始，对于每个数字，对数组中的每个元素进行除法运算，检查和是否小于等于 k，这个条件满足的第一个数字就是需要的答案。
**时间复杂度:** *O(N * M)* ，其中 M 为待寻数，N 为数组大小。

**高效途径:**想法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的概念。

1.  输入数组。
2.  假设最大可能答案为 10 <sup>9</sup> ，将最大值初始化为 10 <sup>9</sup> ，最小值初始化为 1。
3.  在此范围内执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，对于每个数字，检查总和是否小于或等于 k
4.  如果总和小于 K，那么对于小于 K 的数可能存在一个答案。所以，继续并检查小于该计数器的数字。
5.  如果总和大于 K，则数字 M 大于当前计数器。所以，继续并检查大于那个计数器的数字。

下面是上述方法的实现:

## C++

```
// C++ program to find the smallest
// number such that the sum of the
// array becomes less than or equal
// to K when every element of the
// array is divided by that number

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// number such that the sum of the
// array becomes less than or equal
// to K when every element of the
// array is divided by that number
int findMinDivisor(int arr[], int n, int limit)
{
    // Binary search between 1 and 10^9
    int low = 0, high = 1e9;
    while (low < high) {
        int mid = (low + high) / 2;
        int sum = 0;

        // Calculating the new sum after
        // dividing every element by mid
        for (int i = 0; i < n; i++) {
            sum += ceil((double)arr[i]
                        / (double)mid);
        }

        // If after dividing by mid,
        // if the new sum is less than or
        // equal to limit move low to mid+1
        if (sum <= limit)
            high = mid;
        else

            // Else, move mid + 1 to high
            low = mid + 1;
    }

    // Returning the minimum number
    return low;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 6;

    cout << findMinDivisor(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest
// number such that the sum of the
// array becomes less than or equal
// to K when every element of the
// array is divided by that number
import java.util.*;

class GFG{

// Function to find the smallest
// number such that the sum of the
// array becomes less than or equal
// to K when every element of the
// array is divided by that number
static int findMinDivisor(int arr[],
                          int n, int limit)
{

    // Binary search between 1 and 10^9
    int low = 0, high = 1000000000;

    while (low < high)
    {
        int mid = (low + high) / 2;
        int sum = 0;

        // Calculating the new sum after
        // dividing every element by mid
        for(int i = 0; i < n; i++)
        {
           sum += Math.ceil((double) arr[i] /
                            (double) mid);
        }

        // If after dividing by mid,
        // if the new sum is less than or
        // equal to limit move low to mid+1
        if (sum <= limit)
            high = mid;
        else

            // Else, move mid + 1 to high
            low = mid + 1;
    }

    // Returning the minimum number
    return low;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 2, 3, 4, 9 };
    int N = arr.length;
    int K = 6;

    System.out.println(
           findMinDivisor(arr, N, K));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to find the smallest
# number such that the sum of the
# array becomes less than or equal
# to K when every element of the
# array is divided by that number
from math import ceil

# Function to find the smallest
# number such that the sum of the
# array becomes less than or equal
# to K when every element of the
# array is divided by that number
def findMinDivisor(arr, n, limit):

    # Binary search between 1 and 10^9
    low = 0
    high = 10 ** 9

    while (low < high):
        mid = (low + high) // 2
        sum = 0

        # Calculating the new sum after
        # dividing every element by mid
        for i in range(n):
            sum += ceil(arr[i] / mid)

        # If after dividing by mid,
        # if the new sum is less than or
        # equal to limit move low to mid+1
        if (sum <= limit):
            high = mid
        else:

            # Else, move mid + 1 to high
            low = mid + 1

    # Returning the minimum number
    return low

# Driver code
if __name__ == '__main__':

    arr= [ 2, 3, 4, 9 ]
    N = len(arr)
    K = 6

    print(findMinDivisor(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the smallest
// number such that the sum of the
// array becomes less than or equal
// to K when every element of the
// array is divided by that number
using System;

class GFG{

// Function to find the smallest
// number such that the sum of the
// array becomes less than or equal
// to K when every element of the
// array is divided by that number
static int findMinDivisor(int []arr, int n,
                          int limit)
{

    // Binary search between 1 and 10^9
    int low = 0, high = 1000000000;

    while (low < high)
    {
        int mid = (low + high) / 2;
        int sum = 0;

        // Calculating the new sum after
        // dividing every element by mid
        for(int i = 0; i < n; i++)
        {
           sum += (int)Math.Ceiling((double) arr[i] /
                                    (double) mid);
        }

        // If after dividing by mid,
        // if the new sum is less than or
        // equal to limit move low to mid+1
        if (sum <= limit)
        {
            high = mid;
        }
        else
        {

            // Else, move mid + 1 to high
            low = mid + 1;
        }
    }

    // Returning the minimum number
    return low;
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 2, 3, 4, 9 };
    int N = arr.Length;
    int K = 6;

    Console.WriteLine(findMinDivisor(arr, N, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Program  program to find the smallest
// number such that the sum of the
// array becomes less than or equal
// to K when every element of the
// array is divided by that number

// Function to find the smallest
// number such that the sum of the
// array becomes less than or equal
// to K when every element of the
// array is divided by that number
function findMinDivisor(arr, n, limit)
{

    // Binary search between 1 and 10^9
    let low = 0, high = 1000000000;

    while (low < high)
    {
        let mid = Math.floor((low + high) / 2);
        let sum = 0;

        // Calculating the new sum after
        // dividing every element by mid
        for(let i = 0; i < n; i++)
        {
           sum += Math.ceil( arr[i] / mid);
        }

        // If after dividing by mid,
        // if the new sum is less than or
        // equal to limit move low to mid+1
        if (sum <= limit)
            high = mid;
        else

            // Else, move mid + 1 to high
            low = mid + 1;
    }

    // Returning the minimum number
    return low;
}

// Driver Code

       let arr = [ 2, 3, 4, 9 ];
    let N = arr.length;
    let K = 6;

    document.write(
           findMinDivisor(arr, N, K));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** *O(N * 30)* ，其中 N 是数组的大小，因为找到 1 到 10 之间的任意数字 <sup>9</sup> 在二分搜索法最多需要 30 次运算。
**辅助空间:** O(1)