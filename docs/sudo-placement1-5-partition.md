# Sudo 放置【1.5】|分区

> 原文:[https://www.geeksforgeeks.org/sudo-placement1-5-partition/](https://www.geeksforgeeks.org/sudo-placement1-5-partition/)

给定一组正数和负数。任务是找到一个分割点，使得左数组的元素都不在右数组中。如果有多个分区，则求左数组之和与右数组之和(|sum <sub>左</sub>–sum<sub>右</sub> |)相对于分区点的绝对差最小的分区。如果有多个点，打印从左数第一个分区点，即(左数组的最后一个索引和右数组的第一个索引)/2。考虑基于 1 的索引。分区上的左右数组必须至少有 1 个元素，最多有 n-1 个元素。如果没有分区，打印-1。
**例:**

> **输入:** a[] = {1，2，-1，2，3}
> **输出:** 1
> 左数组= {1，2，-1，2}
> 右数组= {3}
> Sumleft = 4，Sumright = 3
> 差值= 1 这是最小可能值
> **输入:** a[] = {1，2，3，1}
> **输出:** -1

一种简单的方法是从每个索引开始向左和向右遍历，并检查分区在该索引处是否可能。如果分区是可能的，那么检查左数组的一个元素和右数组的元素的和之间的绝对差是否小于之前在分区获得的值。找到分割点后，贪婪地找到 **|sum <sub>左</sub>–sum<sub>右</sub> |** 。
**时间复杂度:**O(N<sup>2</sup>)
**一种有效的解决方案**是将每个出现元素的最后一个索引存储在哈希映射中。因为元素值很大，所以不能使用直接索引。创建一个*前缀[]* 和*后缀[]* 数组，分别存储前缀和后缀和。将变量计数初始化为 0。迭代数组中的所有元素。一个常见的观察点是，当遍历时，如果当前元素(A <sub>i</sub> )的最后一次不出现不是 I 本身，那么我们不能在 I 和元素的最后一次出现之间有一个划分。遍历存储元素最后一次出现的最大值时，因为分区在此之前无法完成。
一旦计数是 I 本身，我们就可以有一个分区，现在如果有多个分区那么选择 min |sum <sub>左</sub>–sum<sub>右</sub> |。
注意:使用 map 代替无序 _map 可能会导致 TLE。
以下是上述办法的实施情况。

## C++

```
// C++ program for SP- partition
#include <bits/stdc++.h>
using namespace std;

// Function to find the partition
void partition(int a[], int n)
{
    unordered_map<long long, long long> mpp;

    // mark the last occurrence of every element
    for (int i = 0; i < n; i++)
        mpp[a[i]] = i;

    // calculate the prefix sum
    long long presum[n];
    presum[0] = a[0];
    for (int i = 1; i < n; i++)
        presum[i] = presum[i - 1] + a[i];

    // calculate the suffix sum
    long long sufsum[n];
    sufsum[n - 1] = a[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        sufsum[i] = sufsum[i + 1] + a[i];
    }

    // Check if partition is possible
    bool possible = false;

    // Stores the absolute difference
    long long ans = 1e18;

    // stores the last index till
    // which there can not be any partition
    long long count = 0;

    // Stores the partition
    long long index = -1;

    // Check if partition is possible or not
    // donot check for the last element
    // as partition is not possible
    for (int i = 0; i < n - 1; i++) {

        // takes an element and checks it last occurrence
        // stores the maximum of the last occurrence
        // where partition can be done
        count = max(count, mpp[a[i]]);

        // if partition is possible
        if (count == i) {

            // partition is possible
            possible = true;

            // stores the left array sum
            long long sumleft = presum[i];

            // stores the right array sum
            long long sumright = sufsum[i + 1];

            // check if the difference is minimum
            if ((abs(sumleft - sumright)) < ans) {
                ans = abs(sumleft - sumright);
                index = i + 1;
            }
        }
    }

    // is partition is possible or not
    if (possible)
        cout << index << ".5" << endl;
    else
        cout << -1 << endl;
}

// Driver Code-
int main()
{
    int a[] = { 1, 2, -1, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    partition(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for SP- partition
import java.util.*;

class GFG
{

    // Function to find the partition
    static void partition(int a[], int n)
    {
        Map<Integer,
            Integer> mpp = new HashMap<>();

        // mark the last occurrence of
        // every element
        for (int i = 0; i < n; i++)
            mpp.put(a[i], i);

        // calculate the prefix sum
        long[] presum = new long[n];
        presum[0] = a[0];
        for (int i = 1; i < n; i++)
            presum[i] = presum[i - 1] + a[i];

        // calculate the suffix sum
        long[] sufsum = new long[n];
        sufsum[n - 1] = a[n - 1];
        for (int i = n - 2; i >= 0; i--)
        {
            sufsum[i] = sufsum[i + 1] + a[i];
        }

        // Check if partition is possible
        boolean possible = false;

        // Stores the absolute difference
        long ans = (long) 1e18;

        // stores the last index till
        // which there can not be any partition
        long count = 0;

        // Stores the partition
        long index = -1;

        // Check if partition is possible or not
        // donot check for the last element
        // as partition is not possible
        for (int i = 0; i < n - 1; i++)
        {

            // takes an element and checks its
            // last occurrence, stores the maximum
            // of the last occurrence where
            // partition can be done
            count = Math.max(count, mpp.get(a[i]));

            // if partition is possible
            if (count == i)
            {

                // partition is possible
                possible = true;

                // stores the left array sum
                long sumleft = presum[i];

                // stores the right array sum
                long sumright = sufsum[i + 1];

                // check if the difference is minimum
                if ((Math.abs(sumleft - sumright)) < ans)
                {
                    ans = Math.abs(sumleft - sumright);
                    index = i + 1;
                }
            }
        }

        // is partition is possible or not
        if (possible)
            System.out.print(index + ".5" + "\n");
        else
            System.out.print(-1 + "\n");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[] = { 1, 2, -1, 2, 3 };
        int n = a.length;

        partition(a, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for SP- partition

# Function to find the partition
def partition(a: list, n: int):
    mpp = dict()

    # mark the last occurrence of every element
    for i in range(n):
        mpp[a[i]] = i

    # calculate the prefix sum
    preSum = [0] * n
    preSum[0] = a[0]
    for i in range(1, n):
        preSum[i] = preSum[i - 1] + a[i]

    # calculate the suffix sum
    sufSum = [0] * n
    sufSum[n - 1] = a[n - 1]
    for i in range(n - 2, -1, -1):
        sufSum[i] = sufSum[i + 1] + a[i]

    # Check if partition is possible
    possible = False

    # Stores the absolute difference
    ans = int(1e18)

    # stores the last index till
    # which there can not be any partition
    count = 0

    # Stores the partition
    index = -1

    # Check if partition is possible or not
    # donot check for the last element
    # as partition is not possible
    for i in range(n - 1):

        # takes an element and checks it last occurrence
        # stores the maximum of the last occurrence
        # where partition can be done
        count = max(count, mpp[a[i]])

        # if partition is possible
        if count == i:

            # partition is possible
            possible = True

            # stores the left array sum
            sumleft = preSum[i]

            # stores the right array sum
            sumright = sufSum[i + 1]

            # check if the difference is minimum
            if abs(sumleft - sumright) < ans:
                ans = abs(sumleft - sumright)
                index = i + 1

    # is partition is possible or not
    if possible:
        print("%d.5" % index)
    else:
        print("-1")

# Driver Code
if __name__ == "__main__":

    a = [1, 2, -1, 2, 3]
    n = len(a)

    partition(a, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program for SP- partition
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the partition
    static void partition(int []a, int n)
    {
        Dictionary<int,
                   int> mpp = new Dictionary<int,
                                             int>();

        // mark the last occurrence of
        // every element
        for (int i = 0; i < n; i++)
            if(mpp.ContainsKey(a[i]))
                mpp[a[i]] = i;
            else
                mpp.Add(a[i], i);

        // calculate the prefix sum
        long[] presum = new long[n];
        presum[0] = a[0];
        for (int i = 1; i < n; i++)
            presum[i] = presum[i - 1] + a[i];

        // calculate the suffix sum
        long[] sufsum = new long[n];
        sufsum[n - 1] = a[n - 1];
        for (int i = n - 2; i >= 0; i--)
        {
            sufsum[i] = sufsum[i + 1] + a[i];
        }

        // Check if partition is possible
        bool possible = false;

        // Stores the absolute difference
        long ans = (long) 1e18;

        // stores the last index till which
        // there can not be any partition
        long count = 0;

        // Stores the partition
        long index = -1;

        // Check if partition is possible or not
        // donot check for the last element
        // as partition is not possible
        for (int i = 0; i < n - 1; i++)
        {

            // takes an element and checks its
            // last occurrence, stores the maximum
            // of the last occurrence where
            // partition can be done
            count = Math.Max(count, mpp[a[i]]);

            // if partition is possible
            if (count == i)
            {

                // partition is possible
                possible = true;

                // stores the left array sum
                long sumleft = presum[i];

                // stores the right array sum
                long sumright = sufsum[i + 1];

                // check if the difference is minimum
                if ((Math.Abs(sumleft -
                              sumright)) < ans)
                {
                    ans = Math.Abs(sumleft - sumright);
                    index = i + 1;
                }
            }
        }

        // is partition is possible or not
        if (possible)
            Console.Write(index + ".5" + "\n");
        else
            Console.Write(-1 + "\n");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []a = { 1, 2, -1, 2, 3 };
        int n = a.Length;

        partition(a, n);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for SP- partition

// Function to find the partition
function partition(a, n) {
    let mpp = new Map();

    // mark the last occurrence of every element
    for (let i = 0; i < n; i++)
        mpp.set(a[i], i);

    // calculate the prefix sum
    let presum = new Array(n);
    presum[0] = a[0];
    for (let i = 1; i < n; i++)
        presum[i] = presum[i - 1] + a[i];

    // calculate the suffix sum
    let sufsum = new Array(n);
    sufsum[n - 1] = a[n - 1];
    for (let i = n - 2; i >= 0; i--) {
        sufsum[i] = sufsum[i + 1] + a[i];
    }

    // Check if partition is possible
    let possible = false;

    // Stores the absolute difference
    let ans = Number.MAX_SAFE_INTEGER;

    // stores the last index till
    // which there can not be any partition
    let count = 0;

    // Stores the partition
    let index = -1;

    // Check if partition is possible or not
    // donot check for the last element
    // as partition is not possible
    for (let i = 0; i < n - 1; i++) {

        // takes an element and checks it last occurrence
        // stores the maximum of the last occurrence
        // where partition can be done
        count = Math.max(count, mpp.get(a[i]));

        // if partition is possible
        if (count == i) {

            // partition is possible
            possible = true;

            // stores the left array sum
            let sumleft = presum[i];

            // stores the right array sum
            let sumright = sufsum[i + 1];

            // check if the difference is minimum
            if ((Math.abs(sumleft - sumright)) < ans) {
                ans = Math.abs(sumleft - sumright);
                index = i + 1;
            }
        }
    }

    // is partition is possible or not
    if (possible)
        document.write(index + ".5" + "<br>");
    else
        document.write(-1 + "<br>");
}

// Driver Code-

let a = [1, 2, -1, 2, 3];
let n = a.length;

partition(a, n);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
4.5
```

**时间复杂度:** O(n)假设无序 _ 地图搜索在 O(1)时间内工作。