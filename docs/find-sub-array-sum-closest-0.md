# 找到和最接近 0 的子阵列

> 原文:[https://www.geeksforgeeks.org/find-sub-array-sum-closest-0/](https://www.geeksforgeeks.org/find-sub-array-sum-closest-0/)

给定一个由正数和负数组成的数组，任务是找出和最接近于 0 的子数组。
这样的子阵可以有多个，我们只需要输出其中的 1 个。
**例:**

```
Input : arr[] = {-1, 3, 2, -5, 4}
Output : 1, 3
Subarray from index 1 to 3 has sum closest to 0 i.e.
3 + 2 + -5 = 0

Input : {2, -5, 4, -6, 3} 
Output : 0, 2
2 + -5 + 4 = 1 closest to 0
```

问于:微软

一种**天真的方法**是逐个考虑所有子阵，用和最接近于 0 的值更新子阵的索引。

## C++

```
// C++ program to find subarray with
// sum closest to 0
#include <bits/stdc++.h>
using namespace std;

// Function to find the subarray
pair<int, int> findSubArray(int arr[], int n)
{

    int start, end, min_sum = INT_MAX;

    // Pick a starting point
    for (int i = 0; i < n; i++) {

        // Consider current starting point
        // as a subarray and update minimum
        // sum and subarray indexes
        int curr_sum = arr[i];
        if (min_sum > abs(curr_sum)) {
            min_sum = abs(curr_sum);
            start = i;
            end = i;
        }

        // Try all subarrays starting with i
        for (int j = i + 1; j < n; j++) {
            curr_sum = curr_sum + arr[j];

            // update minimum sum
            // and subarray indexes
            if (min_sum > abs(curr_sum)) {
                min_sum = abs(curr_sum);
                start = i;
                end = j;
            }
        }
    }

    // Return starting and ending indexes
    pair<int, int> p = make_pair(start, end);
    return p;
}

// Drivers code
int main()
{
    int arr[] = { 2, -5, 4, -6, -3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    pair<int, int> point = findSubArray(arr, n);
    cout << "Subarray starting from ";
    cout << point.first << " to " << point.second;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find subarray with
// sum closest to 0

class GFG
{

    static class Pair
    {

        int first, second;
        public Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }

    }

    // Function to find the subarray
    static Pair findSubArray(int arr[], int n)
    {

        int start = 0, end = 0, min_sum = Integer.MAX_VALUE;

        // Pick a starting point
        for (int i = 0; i < n; i++)
        {

            // Consider current starting point
            // as a subarray and update minimum
            // sum and subarray indexes
            int curr_sum = arr[i];
            if (min_sum > Math.abs(curr_sum))
            {
                min_sum = Math.abs(curr_sum);
                start = i;
                end = i;
            }

            // Try all subarrays starting with i
            for (int j = i + 1; j < n; j++)
            {
                curr_sum = curr_sum + arr[j];

                // update minimum sum
                // and subarray indexes
                if (min_sum > Math.abs(curr_sum))
                {
                    min_sum = Math.abs(curr_sum);
                    start = i;
                    end = j;
                }
            }
        }

        // Return starting and ending indexes
        Pair p = new Pair(start, end);
        return p;
    }

    // Drivers code
    public static void main(String[] args)
    {
        int arr[] = {2, -5, 4, -6, -3};
        int n = arr.length;

        Pair point = findSubArray(arr, n);
        System.out.println("Subarray starting from "
                + point.first + " to " + point.second);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find subarray with
# sum closest to 0
import sys

# Function to find the subarray
def findSubArray(arr, n):
    min_sum = sys.maxsize

    # Pick a starting point
    for i in range(n):

        # Consider current starting point
        # as a subarray and update minimum
        # sum and subarray indexes
        curr_sum = arr[i]
        if (min_sum > abs(curr_sum)):
            min_sum = abs(curr_sum)
            start = i
            end = i

        # Try all subarrays starting with i
        for j in range(i + 1, n, 1):
            curr_sum = curr_sum + arr[j]

            # update minimum sum
            # and subarray indexes
            if (min_sum > abs(curr_sum)):
                min_sum = abs(curr_sum)
                start = i
                end = j

    # Return starting and ending indexes
    p = [start, end]
    return p

# Driver Code
if __name__ == '__main__':
    arr = [2, -5, 4, -6, -3]
    n = len(arr)

    point = findSubArray(arr, n)
    print("Subarray starting from ", end = "")
    print(point[0], "to", point[1])

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find subarray with
// sum closest to 0
using System;

class GFG
{

    public class Pair
    {

        public int first, second;
        public Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }

    }

    // Function to find the subarray
    static Pair findSubArray(int []arr, int n)
    {

        int start = 0, end = 0, min_sum = int.MaxValue;

        // Pick a starting point
        for (int i = 0; i < n; i++)
        {

            // Consider current starting point
            // as a subarray and update minimum
            // sum and subarray indexes
            int curr_sum = arr[i];
            if (min_sum > Math.Abs(curr_sum))
            {
                min_sum = Math.Abs(curr_sum);
                start = i;
                end = i;
            }

            // Try all subarrays starting with i
            for (int j = i + 1; j < n; j++)
            {
                curr_sum = curr_sum + arr[j];

                // update minimum sum
                // and subarray indexes
                if (min_sum > Math.Abs(curr_sum))
                {
                    min_sum = Math.Abs(curr_sum);
                    start = i;
                    end = j;
                }
            }
        }

        // Return starting and ending indexes
        Pair p = new Pair(start, end);
        return p;
    }

    // Drivers code
    public static void Main(String[] args)
    {
        int []arr = {2, -5, 4, -6, -3};
        int n = arr.Length;

        Pair point = findSubArray(arr, n);
        Console.WriteLine("Subarray starting from "
                + point.first + " to " + point.second);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find subarray with
// sum closest to 0

// Function to find the subarray
function findSubArray(arr, n) {

    let start, end, min_sum = Number.MAX_SAFE_INTEGER;

    // Pick a starting point
    for (let i = 0; i < n; i++) {

        // Consider current starting point
        // as a subarray and update minimum
        // sum and subarray indexes
        let curr_sum = arr[i];
        if (min_sum > Math.abs(curr_sum)) {
            min_sum = Math.abs(curr_sum);
            start = i;
            end = i;
        }

        // Try all subarrays starting with i
        for (let j = i + 1; j < n; j++) {
            curr_sum = curr_sum + arr[j];

            // update minimum sum
            // and subarray indexes
            if (min_sum > Math.abs(curr_sum)) {
                min_sum = Math.abs(curr_sum);
                start = i;
                end = j;
            }
        }
    }

    // Return starting and ending indexes
    let p = [start, end];
    return p;
}

// Drivers code

let arr = [2, -5, 4, -6, -3];
let n = arr.length;

let point = findSubArray(arr, n);
document.write("Subarray starting from ");
document.write(point[0] + " to " + point[1]);

</script>
```

**输出:**

```
Subarray starting from 0 to 2
```

**时间复杂度:** O(n <sup>2</sup> )
一种高效的方法是执行以下步骤:-

1.  维护一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。还要维护前缀和数组中的索引。
2.  根据和对前缀和数组进行排序。
3.  找出前缀和数组中差异最小的两个元素。

```
i.e.  Find min(pre_sum[i] - pre_sum[i-1]) 
```

1.  用最小差返回预和的索引。
2.  Subarray with (lower_index+1，upper_index)的和最接近 0。
3.  取 lower_index+1，因为减去 lower_index 的值，我们得到最接近 0 的和。这就是为什么不需要包含 lower_index。

## C++

```
// C++ program to find subarray with sum
// closest to 0
#include <bits/stdc++.h>
using namespace std;

struct prefix {
    int sum;
    int index;
};

// Sort on the basis of sum
bool comparison(prefix a, prefix b)
{
    return a.sum < b.sum;
}

// Returns subarray with sum closest to 0.
pair<int, int> findSubArray(int arr[], int n)
{
    int start, end, min_diff = INT_MAX;

    prefix pre_sum[n + 1];

    // To consider the case of subarray starting
    // from beginning of the array
    pre_sum[0].sum = 0;
    pre_sum[0].index = -1;

    // Store prefix sum with index
    for (int i = 1; i <= n; i++) {
        pre_sum[i].sum = pre_sum[i-1].sum + arr[i-1];
        pre_sum[i].index = i - 1;
    }

    // Sort on the basis of sum
    sort(pre_sum, pre_sum + (n + 1), comparison);

    // Find two consecutive elements with minimum difference
    for (int i = 1; i <= n; i++) {
        int diff = pre_sum[i].sum - pre_sum[i-1].sum;

        // Update minimum difference
        // and starting and ending indexes
        if (min_diff > diff) {
            min_diff = diff;
            start = pre_sum[i-1].index;
            end = pre_sum[i].index;
        }
    }

    // Return starting and ending indexes
    pair<int, int> p = make_pair(start + 1, end);
    return p;
}

// Drivers code
int main()
{
    int arr[] = { 2, 3, -4, -1, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    pair<int, int> point = findSubArray(arr, n);
    cout << "Subarray starting from ";
    cout << point.first << " to " << point.second;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find subarray with sum
// closest to 0
import java.util.*;

class Prefix
{
    int sum, index;
}

class Pair
{
    int first, second;
    Pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

class GFG{

// Returns subarray with sum closest to 0.
static Pair findSubArray(int arr[], int n)
{
    int start = -1, end = -1,
     min_diff = Integer.MAX_VALUE;

    Prefix pre_sum[] = new Prefix[n + 1];
    for(int i = 0; i < n + 1; i++)
        pre_sum[i] = new Prefix();

    // To consider the case of subarray starting
    // from beginning of the array
    pre_sum[0].sum = 0;
    pre_sum[0].index = -1;

    // Store prefix sum with index
    for(int i = 1; i <= n; i++)
    {
        pre_sum[i].sum = pre_sum[i - 1].sum +
                             arr[i - 1];
        pre_sum[i].index = i - 1;
    }

    // Sort on the basis of sum
    Arrays.sort(pre_sum, ((a, b) -> a.sum - b.sum));

    // Find two consecutive elements with minimum
    // difference
    for(int i = 1; i <= n; i++)
    {
        int diff = pre_sum[i].sum -
                   pre_sum[i - 1].sum;

        // Update minimum difference
        // and starting and ending indexes
        if (min_diff > diff)
        {
            min_diff = diff;
            start = pre_sum[i - 1].index;
            end = pre_sum[i].index;
        }
    }

    // Return starting and ending indexes
    Pair p = new Pair(start + 1, end);
    return p;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, -4, -1, 6 };
    int n = arr.length;

    Pair point = findSubArray(arr, n);

    System.out.print("Subarray starting from ");
    System.out.println(point.first + " to " +
                       point.second);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 program to find subarray
# with sum closest to 0
class prefix:

    def __init__(self, sum, index):
        self.sum = sum
        self.index = index

# Returns subarray with sum closest to 0.
def findSubArray(arr, n):

    start, end, min_diff = None, None, float('inf')

    pre_sum = [None] * (n + 1)

    # To consider the case of subarray
    # starting from beginning of the array
    pre_sum[0] = prefix(0, -1)

    # Store prefix sum with index
    for i in range(1, n + 1):
        pre_sum[i] = prefix(pre_sum[i - 1].sum +
                                arr[i - 1], i - 1)

    # Sort on the basis of sum
    pre_sum.sort(key = lambda x: x.sum)

    # Find two consecutive elements
    # with minimum difference
    for i in range(1, n + 1):
        diff = pre_sum[i].sum - pre_sum[i - 1].sum

        # Update minimum difference
        # and starting and ending indexes
        if min_diff > diff:
            min_diff = diff
            start = pre_sum[i - 1].index
            end = pre_sum[i].index

    # Return starting and ending indexes
    return (start + 1, end)

# Driver code
if __name__ == "__main__":

    arr = [2, 3, -4, -1, 6]
    n = len(arr)

    point = findSubArray(arr, n)
    print("Subarray starting from",
           point[0], "to", point[1])

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find subarray with sum
// closest to 0
using System;

class Prefix : IComparable<Prefix>
{
    public int sum, index;
    public int CompareTo(Prefix p)
         {
             return this.sum-p.sum;
         }
}

class Pair
{
    public int first, second;
    public Pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

public class GFG{

// Returns subarray with sum closest to 0.
static Pair findSubArray(int []arr, int n)
{
    int start = -1, end = -1,
     min_diff = int.MaxValue;

    Prefix []pre_sum = new Prefix[n + 1];
    for(int i = 0; i < n + 1; i++)
        pre_sum[i] = new Prefix();

    // To consider the case of subarray starting
    // from beginning of the array
    pre_sum[0].sum = 0;
    pre_sum[0].index = -1;

    // Store prefix sum with index
    for(int i = 1; i <= n; i++)
    {
        pre_sum[i].sum = pre_sum[i - 1].sum +
                             arr[i - 1];
        pre_sum[i].index = i - 1;
    }

    // Sort on the basis of sum
    Array.Sort(pre_sum);

    // Find two consecutive elements with minimum
    // difference
    for(int i = 1; i <= n; i++)
    {
        int diff = pre_sum[i].sum -
                   pre_sum[i - 1].sum;

        // Update minimum difference
        // and starting and ending indexes
        if (min_diff > diff)
        {
            min_diff = diff;
            start = pre_sum[i - 1].index;
            end = pre_sum[i].index;
        }
    }

    // Return starting and ending indexes
    Pair p = new Pair(start + 1, end);
    return p;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 3, -4, -1, 6 };
    int n = arr.Length;

    Pair point = findSubArray(arr, n);

    Console.Write("Subarray starting from ");
    Console.WriteLine(point.first + " to " +
                       point.second);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find subarray with sum
// closest to 0
class Prefix
{
    constructor()
    {
        this.sum = 0;
        this.index = 0;
    }
}

class Pair
{
    constructor(a, b)
    {
        this.first = a;
        this.second = b;
    }
}

// Returns subarray with sum closest to 0.
function findSubArray(arr, n)
{
    let start = -1, end = -1,
     min_diff = Number.MAX_VALUE;

    let pre_sum = new Array(n + 1);
    for(let i = 0; i < n + 1; i++)
        pre_sum[i] = new Prefix();

    // To consider the case of subarray starting
    // from beginning of the array
    pre_sum[0].sum = 0;
    pre_sum[0].index = -1;

    // Store prefix sum with index
    for(let i = 1; i <= n; i++)
    {
        pre_sum[i].sum = pre_sum[i - 1].sum +
                             arr[i - 1];
        pre_sum[i].index = i - 1;
    }

    // Sort on the basis of sum
    pre_sum.sort(function(a, b) {return a.sum - b.sum});

    // Find two consecutive elements with minimum
    // difference
    for(let i = 1; i <= n; i++)
    {
        let diff = pre_sum[i].sum -
                   pre_sum[i - 1].sum;

        // Update minimum difference
        // and starting and ending indexes
        if (min_diff > diff)
        {
            min_diff = diff;
            start = pre_sum[i - 1].index;
            end = pre_sum[i].index;
        }
    }

    // Return starting and ending indexes
    let p = new Pair(start + 1, end);
    return p;
}

// Driver code
let arr = [2, 3, -4, -1, 6 ];
let n = arr.length;
let point = findSubArray(arr, n);
document.write("Subarray starting from ");
document.write(point.first + " to " +
                   point.second);

// This code is contributed by rag2127
</script>
```

**输出:**

```
Subarray starting from 0 to 3
```

**时间复杂度:** O(n log n)
参考:
[https://www.careercup.com/question?id=14583859](https://www.careercup.com/question?id=14583859)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。