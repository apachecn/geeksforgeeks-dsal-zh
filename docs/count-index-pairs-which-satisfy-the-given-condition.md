# 计数满足给定条件的索引对

> 原文:[https://www . geeksforgeeks . org/count-index-pairs-满足给定条件/](https://www.geeksforgeeks.org/count-index-pairs-which-satisfy-the-given-condition/)

给定第一个 **N** 自然数的排列 **P** ，任务是对索引对 **(i，j)** 进行计数，使得 **P[i] + P[j] = max(P[x])** ，其中 **i ≤ x ≤ j** 。
**举例:**

> **输入:** P[] = {3，4，1，5，2}
> **输出:** 2
> 只有有效的索引对是(0，4)和(0，2)
> **输入:** P[] = {1，3，2}
> **输出:** 1

**天真的方法:**我们可以通过迭代所有可能的对 **(i，j)** 来解决这个问题，并且每次都获得它们之间的最大值。这种方法的时间复杂度将是 **O(n <sup>3</sup> )** 。
**有效方法:**将最大元素固定在一个线段上，并迭代其左侧或右侧的元素。如果当前最大值是 x，而我们找到的元素是 y，那么检查元素 x-y 是否可以与 y 形成一个子段(即 x 是 y 和 x-y 之间的段上的最大值)。这在 O(n*n)
中有效，但是如果我们可以预先计算 x 是最大元素的线段的边界，并且总是选择迭代线段的较小部分，那么时间复杂度将降低到 O(nlogn)。
因为每个元素的处理次数不会超过 logn 次，所以如果我们在 m 大小的段中处理它，那么它的较小部分包含的元素不超过 m/2 个(我们后面会处理，这个段的较小部分包含的元素不超过 m/4 个)，以此类推..).
以下是上述方法的实施:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count of
// required index pairs
int Count_Segment(int p[], int n)
{
    // To store the required count
    int count = 0;

    // Array to store the left elements
    // upto which current element is maximum
    int upto[n + 1];
    for(int i = 0; i < n + 1; i++)
    upto[i] = 0;

    // Iterating through the whole permutation
    // except first and last element
    int j = 0,curr = 0;
    for (int i = 1; i < n + 1; i++)
    {

        // If current element can be maximum
        // in a subsegment
        if (p[i] > p[i - 1] and p[i] > p[i + 1])
        {

            // Current maximum
            curr = p[i];

            // Iterating for smaller values then
            // current maximum on left of it
            j = i - 1;
            while (j >= 0 and p[j] < curr)
            {
            // Storing left borders
                // of the current maximum
                upto[p[j]]= curr;
                j -= 1;
            }

            // Iterating for smaller values then
            // current maximum on right of it
            j = i + 1;
            while (j < n and p[j] < curr)
            {

                // Condition satisfies
                if (upto[curr-p[j]] == curr)
                    count += 1;
                j+= 1;
            }

        }
    }

    // Return count of subsegments
    return count;
}

// Driver Code
int main()
{

    int p[] = {3, 4, 1, 5, 2};
    int n = sizeof(p)/sizeof(p[0]);
    cout << (Count_Segment(p, n));
    return 0;
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of
// required index pairs
static int Count_Segment(int p[], int n)
{
    // To store the required count
    int count = 0;

    // Array to store the left elements
    // upto which current element is maximum
    int []upto = new int[n + 1];
    for(int i = 0; i < n + 1; i++)
    upto[i] = 0;

    // Iterating through the whole permutation
    // except first and last element
    int j = 0,curr = 0;
    for (int i = 1; i < n ; i++)
    {

        // If current element can be maximum
        // in a subsegment
        if (p[i] > p[i - 1] && p[i] > p[i + 1])
        {

            // Current maximum
            curr = p[i];

            // Iterating for smaller values then
            // current maximum on left of it
            j = i - 1;
            while (j >= 0 && p[j] < curr)
            {
                // Storing left borders
                // of the current maximum
                upto[p[j]]= curr;
                j -= 1;
            }

            // Iterating for smaller values then
            // current maximum on right of it
            j = i + 1;
            while (j < n && p[j] < curr)
            {

                // Condition satisfies
                if (upto[curr-p[j]] == curr)
                    count += 1;
                j+= 1;
            }

        }
    }

    // Return count of subsegments
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int p[] = {3, 4, 1, 5, 2};
    int n = p.length;
    System.out.println(Count_Segment(p, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the count of
# required index pairs
def Count_Segment(p, n):

    # To store the required count
    count = 0

    # Array to store the left elements
    # upto which current element is maximum
    upto = [False]*(n + 1)

    # Iterating through the whole permutation
    # except first and last element
    for i in range(1, n-1):

        # If current element can be maximum
        # in a subsegment
        if p[i]>p[i-1] and p[i]>p[i + 1]:

            # Current maximum
            curr = p[i]

            # Iterating for smaller values then
            # current maximum on left of it
            j = i-1
            while j>= 0 and p[j]<curr:

                # Storing left borders
                # of the current maximum
                upto[p[j]]= curr
                j-= 1

            # Iterating for smaller values then
            # current maximum on right of it
            j = i + 1
            while j<n and p[j]<curr:

                # Condition satisfies
                if upto[curr-p[j]]== curr:
                    count+= 1
                j+= 1

    # Return count of subsegments
    return count

# Driver Code
if __name__=="__main__":
    p =[3, 4, 1, 5, 2]
    n = len(p)
    print(Count_Segment(p, n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// required index pairs
static int Count_Segment(int []p, int n)
{
    // To store the required count
    int count = 0;

    // Array to store the left elements
    // upto which current element is maximum
    int []upto = new int[n + 1];
    for(int i = 0; i < n + 1; i++)
    upto[i] = 0;

    // Iterating through the whole permutation
    // except first and last element
    int j = 0,curr = 0;
    for (int i = 1; i < n ; i++)
    {

        // If current element can be maximum
        // in a subsegment
        if (p[i] > p[i - 1] && p[i] > p[i + 1])
        {

            // Current maximum
            curr = p[i];

            // Iterating for smaller values then
            // current maximum on left of it
            j = i - 1;
            while (j >= 0 && p[j] < curr)
            {
                // Storing left borders
                // of the current maximum
                upto[p[j]]= curr;
                j= j - 1;
            }

            // Iterating for smaller values then
            // current maximum on right of it
            j = i + 1;
            while (j < n && p[j] < curr)
            {

                // Condition satisfies
                if (upto[curr-p[j]] == curr)
                    count += 1;
                j= j+ 1;
            }

        }
    }

    // Return count of subsegments
    return count;
}

// Driver Code
static public void Main ()
{
    int []p = {3, 4, 1, 5, 2};
    int n = p.Length;
    Console.WriteLine(Count_Segment(p, n));
}
}

/* This code contributed by ajit*/
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the count of
    // required index pairs
    function Count_Segment(p , n) {
        // To store the required count
        var count = 0;

        // Array to store the left elements
        // upto which current element is maximum
        var upto = Array(n + 1).fill(0);
        for (i = 0; i < n + 1; i++)
            upto[i] = 0;

        // Iterating through the whole permutation
        // except first and last element
        var j = 0, curr = 0;
        for (i = 1; i < n; i++) {

            // If current element can be maximum
            // in a subsegment
            if (p[i] > p[i - 1] && p[i] > p[i + 1]) {

                // Current maximum
                curr = p[i];

                // Iterating for smaller values then
                // current maximum on left of it
                j = i - 1;
                while (j >= 0 && p[j] < curr) {
                    // Storing left borders
                    // of the current maximum
                    upto[p[j]] = curr;
                    j -= 1;
                }

                // Iterating for smaller values then
                // current maximum on right of it
                j = i + 1;
                while (j < n && p[j] < curr) {

                    // Condition satisfies
                    if (upto[curr - p[j]] == curr)
                        count += 1;
                    j += 1;
                }

            }
        }

        // Return count of subsegments
        return count;
    }

    // Driver Code

        var p = [ 3, 4, 1, 5, 2 ];
        var n = p.length;
        document.write(Count_Segment(p, n));
// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
2
```