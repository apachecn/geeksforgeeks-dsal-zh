# 根据给定的移除元素的规则找到最小可能的数组大小

> 原文:[https://www . geeksforgeeks . org/find-具有给定移除规则的最小可能阵列大小/](https://www.geeksforgeeks.org/find-minimum-possible-size-of-array-with-given-rules-for-removal/)

给定一个数字数组和一个常数 k，按照以下规则最小化数组的大小来移除元素。

*   正好三个元素可以一次去掉。
*   移除的三个元素必须在数组中相邻，即 arr[i]，arr[i+1]，arr[i+2]。第二个元素必须比第一个元素大 k，第三个元素必须比第二个元素大 k，即 arr[I+1]–arr[I]= k，arr[I+2]–arr[I+1]= k。

示例:

```
Input: arr[] = {2, 3, 4, 5, 6, 4}, k = 1
Output: 0
We can actually remove all elements. 
First remove 4, 5, 6 => We get {2, 3, 4}
Now remove 2, 3, 4   => We get empty array {}

Input:  arr[] = {2, 3, 4, 7, 6, 4}, k = 1
Output: 3
We can only remove 2 3 4
```

来源:[https://code . Google . com/codejam/contest/4214486/dashboard # s = p2](https://code.google.com/codejam/contest/4214486/dashboard#s=p2)
**我们强烈建议您尽量减少浏览器，先自己试试这个。**
对于每个元素 arr[i]有两种可能。
1)要么该元素未被移除。
2)或元素被移除(如果它遵循移除规则)。当一个元素被移除时，还有两种可能。
…..a)可以直接删除，即初始 arr[i+1]为 arr[i]+k，arr[i+2]为 arr[i] + 2*k.
…..b)存在 x 和 y，使得 arr[x]–arr[I]= k，arr[y]–arr[x]= k，且子阵列“arr[I+1…x-1]”&“arr[x+1…y-1]”可以被完全移除。

下面是基于上述思想的递归算法。

```
// Returns size of minimum possible size of arr[low..high]
// after removing elements according to given rules
findMinSize(arr[], low, high, k)

// If there are less than 3 elements in arr[low..high]
1) If high-low+1 < 3, return high-low+1

// Consider the case when 'arr[low]' is not considered as
// part of any triplet to be removed.  Initialize result 
// using this case
2) result = 1 + findMinSize(arr, low+1, high)

// Case when 'arr[low]' is part of some triplet and removed
// Try all possible triplets that have arr[low]
3) For all i from low+1 to high
    For all j from i+1 to high
      Update result if all of the following conditions are met
      a) arr[i] - arr[low] = k  
      b) arr[j] - arr[i]  = k
      c) findMinSize(arr, low+1, i-1, k) returns 0
      d) findMinSize(arr, i+1, j-1, k) also returns 0
      e) Result calculated for this triplet (low, i, j)
         is smaller than existing result.

4) Return result
```

上述解的时间复杂度是指数的。如果我们画出完整的递归树，我们可以观察到许多子问题被一次又一次地解决。由于相同的子问题被再次调用，这个问题具有重叠子问题的性质。像其他典型的[动态规划(DP)问题](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)一样，通过构造一个临时数组 dp[][]来存储子问题的结果，可以避免相同子问题的重新计算。下面是基于动态规划的解决方案

以下是上述想法的实现。该实现是基于记忆的，即它是递归的，并使用查找表 dp[][]来检查子问题是否已经解决。

## C++

```
// C++ program to find size of minimum possible array after
// removing elements according to given rules
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000

// dp[i][j] denotes the minimum number of elements left in
// the subarray arr[i..j].
int dp[MAX][MAX];

int minSizeRec(int arr[], int low, int high, int k)
{
    // If already evaluated
    if (dp[low][high] != -1)
        return dp[low][high];

    // If size of array is less than 3
    if ( (high-low + 1) < 3)
        return high-low +1;

    // Initialize result as the case when first element is
    // separated (not removed using given rules)
    int res = 1 + minSizeRec(arr, low+1, high, k);

    // Now consider all cases when first element forms a triplet
    // and removed. Check for all possible triplets (low, i, j)
    for (int i = low+1; i<=high-1; i++)
    {
        for (int j = i+1; j <= high; j++ )
        {
            // Check if this triplet follows the given rules of
            // removal. And elements between 'low' and 'i' , and
            //  between 'i' and 'j' can be recursively removed.
            if (arr[i] == (arr[low] + k) &&
                arr[j] == (arr[low] + 2*k) &&
                minSizeRec(arr, low+1, i-1, k) == 0 &&
                minSizeRec(arr, i+1, j-1, k) == 0)
            {
                 res = min(res, minSizeRec(arr, j+1, high, k));
            }
        }
    }

    // Insert value in table and return result
    return (dp[low][high] = res);
}

// This function mainly initializes dp table and calls
// recursive function minSizeRec
int minSize(int arr[], int n, int k)
{
    memset(dp, -1, sizeof(dp));
    return minSizeRec(arr, 0, n-1, k);
}

// Driver program to test above function
int main()
{
    int arr[] = {2, 3, 4, 5, 6, 4};
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 1;
    cout << minSize(arr, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find size of
// minimum possible array after
// removing elements according
// to given rules
class GFG
{

    static int MAX = 1000;

    // dp[i][j] denotes the minimum
    // number of elements left in
    // the subarray arr[i..j].
    static int dp[][] = new int[MAX][MAX];

    static int minSizeRec(int arr[], int low,
                            int high, int k)
    {
        // If already evaluated
        if (dp[low][high] != -1)
        {
            return dp[low][high];
        }

        // If size of array is less than 3
        if ((high - low + 1) < 3)
        {
            return high - low + 1;
        }

        // Initialize result as the
        // case when first element is
        // separated (not removed
        // using given rules)
        int res = 1 + minSizeRec(arr,
                        low + 1, high, k);

        // Now consider all cases when
        // first element forms a triplet
        // and removed. Check for all
        // possible triplets (low, i, j)
        for (int i = low + 1; i <= high - 1; i++)
        {
            for (int j = i + 1; j <= high; j++)
            {
                // Check if this triplet
                // follows the given rules of
                // removal. And elements
                // between 'low' and 'i' , and
                // between 'i' and 'j' can
                // be recursively removed.
                if (arr[i] == (arr[low] + k) &&
                    arr[j] == (arr[low] + 2 * k) &&
                    minSizeRec(arr, low + 1, i - 1, k) == 0 &&
                    minSizeRec(arr, i + 1, j - 1, k) == 0)
                {
                    res = Math.min(res, minSizeRec(arr, j + 1, high, k));
                }
            }
        }

        // Insert value in table and return result
        return (dp[low][high] = res);
    }

    // This function mainly initializes
    // dp table and calls recursive
    // function minSizeRec
    static int minSize(int arr[], int n, int k)
    {
        for (int i = 0; i < MAX; i++)
        {
            for (int j = 0; j < MAX; j++)
            {
                dp[i][j] = -1;
            }
        }
        return minSizeRec(arr, 0, n - 1, k);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {2, 3, 4, 5, 6, 4};
        int n = arr.length;
        int k = 1;
        System.out.println(minSize(arr, n, k));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find size of
# minimum possible array after
# removing elements according to given rules
MAX=1000

dp=[[-1 for i in range(MAX)] for i in range(MAX)]
# dp[i][j] denotes the minimum number of elements left in
# the subarray arr[i..j].

def minSizeRec(arr,low,high,k):

    # If already evaluated
    if dp[low][high] != -1:
        return dp[low][high]

    # If size of array is less than 3
    if (high-low + 1) < 3:
        return (high-low + 1)

    # Initialize result as the case when first element is
    # separated (not removed using given rules)
    res = 1 + minSizeRec(arr, low+1, high, k)

    # Now consider all cases when
    # first element forms a triplet
    # and removed. Check for all possible
    # triplets (low, i, j)

    for i in range(low+1,high):

        for j in range(i+1,high+1):

            # Check if this triplet follows the given rules of
            # removal. And elements between 'low' and 'i' , and
            # between 'i' and 'j' can be recursively removed.
            if (arr[i]==(arr[low]+k) and arr[j] == (arr[low] + 2*k) and
                minSizeRec(arr, low+1, i-1, k) == 0 and
                minSizeRec(arr, i+1, j-1, k) == 0):
                res=min(res,minSizeRec(arr,j+1,high,k) )

    # Insert value in table and return result
    dp[low][high] = res
    return res

# This function mainly initializes dp table and calls
# recursive function minSizeRec
def minSize(arr,n,k):
    dp=[[-1 for i in range(MAX)] for i in range(MAX)]
    return minSizeRec(arr, 0, n-1, k)

# Driver program to test above function
if __name__=='__main__':
    arr=[2, 3, 4, 5, 6, 4]
    n=len(arr)
    k=1
    print(minSize(arr,n,k))

# this code is contributed by sahilshelangia    

```

## C#

```
// C# program to find size of
// minimum possible array after
// removing elements according
// to given rules
using System;

class GFG
{

    static int MAX = 1000;

    // dp[i,j] denotes the minimum
    // number of elements left in
    // the subarray arr[i..j].
    static int [,]dp = new int[MAX, MAX];

    static int minSizeRec(int []arr, int low,
                            int high, int k)
    {
        // If already evaluated
        if (dp[low, high] != -1)
        {
            return dp[low, high];
        }

        // If size of array is less than 3
        if ((high - low + 1) < 3)
        {
            return high - low + 1;
        }

        // Initialize result as the
        // case when first element is
        // separated (not removed
        // using given rules)
        int res = 1 + minSizeRec(arr,
                        low + 1, high, k);

        // Now consider all cases when
        // first element forms a triplet
        // and removed. Check for all
        // possible triplets (low, i, j)
        for (int i = low + 1; i <= high - 1; i++)
        {
            for (int j = i + 1; j <= high; j++)
            {
                // Check if this triplet
                // follows the given rules of
                // removal. And elements
                // between 'low' and 'i' , and
                // between 'i' and 'j' can
                // be recursively removed.
                if (arr[i] == (arr[low] + k) &&
                    arr[j] == (arr[low] + 2 * k) &&
                    minSizeRec(arr, low + 1, i - 1, k) == 0 &&
                    minSizeRec(arr, i + 1, j - 1, k) == 0)
                {
                    res = Math.Min(res, minSizeRec(arr, j + 1, high, k));
                }
            }
        }

        // Insert value in table and return result
        return (dp[low, high] = res);
    }

    // This function mainly initializes
    // dp table and calls recursive
    // function minSizeRec
    static int minSize(int []arr, int n, int k)
    {
        for (int i = 0; i < MAX; i++)
        {
            for (int j = 0; j < MAX; j++)
            {
                dp[i, j] = -1;
            }
        }
        return minSizeRec(arr, 0, n - 1, k);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {2, 3, 4, 5, 6, 4};
        int n = arr.Length;
        int k = 1;
        Console.WriteLine(minSize(arr, n, k));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to find size of
    // minimum possible array after
    // removing elements according
    // to given rules

    let MAX = 1000;

    // dp[i][j] denotes the minimum
    // number of elements left in
    // the subarray arr[i..j].
    let dp = new Array(MAX);

    for(let i = 0; i < MAX; i++)
    {
        dp[i] = new Array(MAX);
        for(let j = 0; j < MAX; j++)
        {
            dp[i][j] = 0;
        }
    }

    function minSizeRec(arr, low, high, k)
    {
        // If already evaluated
        if (dp[low][high] != -1)
        {
            return dp[low][high];
        }

        // If size of array is less than 3
        if ((high - low + 1) < 3)
        {
            return high - low + 1;
        }

        // Initialize result as the
        // case when first element is
        // separated (not removed
        // using given rules)
        let res = 1 + minSizeRec(arr, low + 1, high, k);

        // Now consider all cases when
        // first element forms a triplet
        // and removed. Check for all
        // possible triplets (low, i, j)
        for (let i = low + 1; i <= high - 1; i++)
        {
            for (let j = i + 1; j <= high; j++)
            {
                // Check if this triplet
                // follows the given rules of
                // removal. And elements
                // between 'low' and 'i' , and
                // between 'i' and 'j' can
                // be recursively removed.
                if (arr[i] == (arr[low] + k) &&
                    arr[j] == (arr[low] + 2 * k) &&
                    minSizeRec(arr, low + 1, i - 1, k) == 0 &&
                    minSizeRec(arr, i + 1, j - 1, k) == 0)
                {
                    res = Math.min(res, minSizeRec(arr, j + 1, high, k));
                }
            }
        }

        // Insert value in table and return result
        return (dp[low][high] = res);
    }

    // This function mainly initializes
    // dp table and calls recursive
    // function minSizeRec
    function minSize(arr, n, k)
    {
        for (let i = 0; i < MAX; i++)
        {
            for (let j = 0; j < MAX; j++)
            {
                dp[i][j] = -1;
            }
        }
        return minSizeRec(arr, 0, n - 1, k);
    }

    let arr = [2, 3, 4, 5, 6, 4];
    let n = arr.length;
    let k = 1;
    document.write(minSize(arr, n, k));

    // This code is contributed by mukesh07.
</script>
```

**输出:**

```
0
```

本文由 [Ekta Goel](https://www.linkedin.com/pub/ekta-goel/75/12a/3a6) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息