# 求两个数组的重叠和

> 原文:[https://www . geeksforgeeks . org/find-重叠的两个数组之和/](https://www.geeksforgeeks.org/find-the-overlapping-sum-of-two-arrays/)

给定两个数组 A[]和 B[]，每个数组有 n 个唯一的元素。任务是找到两个数组的重叠和。这是两个数组中常见元素的总和。

**注意**:数组中的元素是唯一的。也就是说，数组不包含重复项。

示例:

```
Input : A[] = {1, 5, 3, 8}
        B[] = {5, 4, 6, 7}
Output : 10
Explanation : The element which is common in both arrays is 5.
Therefore, the overlapping sum will be (5+5) = 10

Input : A[] = {1, 5, 3, 8}
        B[] = {5, 1, 8, 3}
Output : 99
```

**蛮力法:**简单的方法是，对于 A[]中的每个元素，检查它是否存在于 B[]中，如果存在于 B[]中，则将该数字加两次(一次用于 A[]，一次用于 B[])到总和中。对数组 A[]中的所有元素重复此过程。

时间复杂性:O(n^2).

**高效方法:**一种高效的方法是使用 Hashing。遍历两个数组，并将元素插入哈希表，以跟踪元素的数量。将计数等于 2 的元素相加。

下面是上述方法的实现:

## C++

```
// CPP program to find overlapping sum
#include <bits/stdc++.h>
using namespace std;

// Function for calculating
// overlapping sum of two array
int findSum(int A[], int B[], int n)
{  
    // unordered map to store count of
    // elements
    unordered_map<int,int> hash;

    // insert elements of A[] into
    // unordered_map
    for(int i=0;i<n;i++)
    {
        if(hash.find(A[i])==hash.end())
        {
            hash.insert(make_pair(A[i],1));
        }
        else
        {
            hash[A[i]]++;
        }
    }

    // insert elements of B[] into
    // unordered_map
    for(int i=0;i<n;i++)
    {
        if(hash.find(B[i])==hash.end())
        {
            hash.insert(make_pair(B[i],1));
        }
        else
        {
            hash[B[i]]++;
        }
    }

    // calculate overlapped sum
    int sum = 0;
    for(auto itr = hash.begin(); itr!=hash.end(); itr++)
    {
        if((itr->second)==2)
        {
            sum += (itr->first)*2;
        }
    }

    return sum;
}

// driver code
int main()
{
    int A[] = { 5, 4, 9, 2, 3 };
    int B[] = { 2, 8, 7, 6, 3 };

    // size of array
    int n = sizeof(A) / sizeof(A[0]);

    // function call
    cout << findSum(A, B, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find overlapping sum
import java.io.*;
import java.util.*;
class GFG
{

    // Function for calculating
    // overlapping sum of two array
    static int findSum(int A[], int B[], int n)
    {

        // unordered map to store count of 
        // elements
        HashMap<Integer, Integer> hash = new HashMap<>();

        // insert elements of A[] into
        // unordered_map
        for(int i = 0; i < n; i++)
        {
            if(!hash.containsKey(A[i]))
            {
                hash.put(A[i], 1);
            }
            else
            {
                hash.put(A[i], hash.get(A[i]) + 1);
            }
        }

        // insert elements of B[] into
        // unordered_map
        for(int i = 0; i < n; i++)
        {
            if(!hash.containsKey(B[i]))
            {
                hash.put(B[i], 1);
            }
            else
            {
                hash.put(B[i], hash.get(B[i]) + 1);
            }
        }

        // calculate overlapped sum
        int sum = 0;
        for(int itr: hash.keySet())
        {
            if(hash.get(itr) == 2)
            {
                sum += itr * 2;
            }
        }
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int A[] = { 5, 4, 9, 2, 3 };
        int B[] = { 2, 8, 7, 6, 3 };

        // size of array
        int n = A.length;
        System.out.println(findSum(A, B, n));
    }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program to find overlapping sum

# Function for calculating
# overlapping sum of two array
def findSum(A, B, n):

    # unordered map to store count of
    # elements
    hash=dict()

    # insert elements of A into
    # unordered_map
    for i in range(n):
        hash[A[i]] = hash.get(A[i], 0) + 1

    # insert elements of B into
    # unordered_map
    for i in range(n):
        hash[B[i]] = hash.get(B[i], 0) + 1

    # calculate overlapped sum
    sum = 0

    for i in hash:
        if hash[i] == 2:
            sum += i * 2

    return sum

# Driver code

A = [ 5, 4, 9, 2, 3 ]
B = [ 2, 8, 7, 6, 3 ]

# size of array
n = len(A)

# function call
print(findSum(A, B, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find overlapping sum
using System;
using System.Collections.Generic;
public class GFG
{

    // Function for calculating
    // overlapping sum of two array
    static int findSum(int[] A, int[] B, int n)
    {

        // unordered map to store count of 
        // elements
        Dictionary<int, int> hash = new Dictionary<int, int>();

        // insert elements of A[] into
        // unordered_map
        for(int i = 0; i < n; i++)
        {
            if(!hash.ContainsKey(A[i]))
            {
                hash.Add(A[i], 1);
            }
            else
            {
                hash[A[i]]++;
            }
        }

        // insert elements of B[] into
        // unordered_map
        for(int i = 0; i < n; i++)
        {
            if(!hash.ContainsKey(B[i]))
            {
                hash.Add(B[i], 1);
            }
            else
            {
                hash[B[i]]++;
            }
        }

        // calculate overlapped sum
        int sum = 0;
        foreach(KeyValuePair<int, int> itr in hash)
        {
            if(itr.Value == 2)
            {
                sum += itr.Key * 2;
            }
        }
        return sum;
    }

    // Driver code
    static public void Main ()
    {
         int[] A = { 5, 4, 9, 2, 3 };
        int[] B = { 2, 8, 7, 6, 3 };

        // size of array
        int n = A.Length;
        Console.Write(findSum(A, B, n));
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program to find overlapping sum

// Function for calculating
// overlapping sum of two array
function findSum(A, B, n)
{

    // unordered map to store count of
    // elements
    let hash = new Map();

    // Insert elements of A[] into
    // unordered_map
    for(let i = 0; i < n; i++)
    {
        if (!hash.has(A[i]))
        {
            hash.set(A[i], 1);
        }
        else
        {
            hash.set(A[i], hash.get(A[i]) + 1);
        }
    }

    // Insert elements of B[] into
    // unordered_map
    for(let i = 0; i < n; i++)
    {
        if (!hash.has(B[i]))
        {
            hash.set(B[i], 1);
        }
        else
        {
            hash.set(B[i], hash.get(B[i]) + 1);
        }
    }

    // Calculate overlapped sum
    let sum = 0;
    for(let [key, value] of hash.entries())
    {
        if(value == 2)
        {
            sum += key * 2;
        }
    }
    return sum;
}

// Driver code
let A = [ 5, 4, 9, 2, 3 ];
let B = [ 2, 8, 7, 6, 3 ];

// Size of array
let n = A.length;

document.write(findSum(A, B, n));

// This code is contributed by patel2127

</script>
```

**输出:**

```
10
```

**时间复杂度**:O(n)
T3】辅助空间 : O(n)

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。