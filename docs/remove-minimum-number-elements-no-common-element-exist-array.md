# 删除最少数量的元素，使得两个数组中都不存在公共元素

> 原文:[https://www . geesforgeks . org/remove-最小数量-元素-无-公共-元素-存在-数组/](https://www.geeksforgeeks.org/remove-minimum-number-elements-no-common-element-exist-array/)

给定分别由 n 和 m 个元素组成的两个数组 A[]和 B[]。找到要从每个数组中移除的元素的最小数量，以便两个数组中都不存在公共元素。
**例:**

```
Input : A[] = { 1, 2, 3, 4}
        B[] = { 2, 3, 4, 5, 8 }
Output : 3
We need to remove 2, 3 and 4 from any array.

Input : A[] = { 4, 2, 4, 4}
        B[] = { 4, 3 }
Output : 1
We need to remove 4 from B[]

Input : A[] = { 1, 2, 3, 4 }
        B[] = { 5, 6, 7 }
Output : 0
There is no common element in both.
```

计算两个数组中每个数字的出现次数。如果两个数组中都有一个数字，则从出现次数较少的数组中删除该数字，并将其添加到结果中。

## C++

```
// CPP program to find minimum element
// to remove so no common element
// exist in both array
#include <bits/stdc++.h>
using namespace std;

// To find no elements to remove
// so no common element exist
int minRemove(int a[], int b[], int n, int m)
{
    // To store count of array element
    unordered_map<int, int> countA, countB;

    // Count elements of a
    for (int i = 0; i < n; i++)
        countA[a[i]]++;

    // Count elements of b
    for (int i = 0; i < m; i++)
        countB[b[i]]++;

    // Traverse through all common element, and
    // pick minimum occurrence from two arrays
    int res = 0;
    for (auto x : countA)
        if (countB.find(x.first) != countB.end())
            res += min(x.second, countB[x.first]);

    // To return count of minimum elements
    return res;
}

// Driver program to test minRemove()
int main()
{
    int a[] = { 1, 2, 3, 4 };
    int b[] = { 2, 3, 4, 5, 8 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = sizeof(b) / sizeof(b[0]);

    cout << minRemove(a, b, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to Remove minimum number of elements
// such that no common element exist in both array
import java.util.*;

class GFG {

    // To find no elements to remove
    // so no common element exist
    public static int minRemove(int a[], int b[], int n,
                                                 int m)
    {
        // To store count of array element
        HashMap<Integer, Integer> countA = new HashMap<
                                          Integer, Integer>();
        HashMap<Integer, Integer> countB = new HashMap<
                                          Integer, Integer>();

        // Count elements of a
        for (int i = 0; i < n; i++){
           if (countA.containsKey(a[i]))
                countA.put(a[i], countA.get(a[i]) + 1);

           else countA.put(a[i], 1);

        }

        // Count elements of b
        for (int i = 0; i < m; i++){
             if (countB.containsKey(b[i]))
                    countB.put(b[i], countB.get(b[i]) + 1);

               else countB.put(b[i], 1);
        }

        // Traverse through all common element, and
        // pick minimum occurrence from two arrays
        int res = 0;

        Set<Integer> s = countA.keySet();

        for (int x : s)
            if(countB.containsKey(x))
                res += Math.min(countB.get(x),
                               countA.get(x));

        // To return count of minimum elements
        return res;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {

            int a[] = { 1, 2, 3, 4 };
            int b[] = { 2, 3, 4, 5, 8 };
            int n = a.length;
            int m = b.length;

            System.out.println(minRemove(a, b, n, m));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find minimum
# element to remove so no common
# element exist in both array

# To find no elements to remove
# so no common element exist
def minRemove(a, b, n, m):

    # To store count of array element
    countA = dict()
    countB = dict()

    # Count elements of a
    for i in range(n):
        countA[a[i]] = countA.get(a[i], 0) + 1

    # Count elements of b
    for i in range(n):
        countB[b[i]] = countB.get(b[i], 0) + 1

    # Traverse through all common
    # element, and pick minimum
    # occurrence from two arrays
    res = 0
    for x in countA:
        if x in countB.keys():
            res += min(countA[x],countB[x])

    # To return count of
    # minimum elements
    return res

# Driver Code
a = [ 1, 2, 3, 4 ]
b = [2, 3, 4, 5, 8 ]
n = len(a)
m = len(b)
print(minRemove(a, b, n, m))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# Code to Remove minimum number of elements
// such that no common element exist in both array
using System;
using System.Collections.Generic;

class GFG
{

    // To find no elements to remove
    // so no common element exist
    public static int minRemove(int []a, int []b, int n,
                                                int m)
    {
        // To store count of array element
        Dictionary<int,int> countA = new Dictionary<int,int>();
        Dictionary<int,int>countB = new Dictionary<int,int>();

        // Count elements of a
        for (int i = 0; i < n; i++)
        {
            if (countA.ContainsKey(a[i]))
            {
                var v = countA[a[i]];
                countA.Remove(countA[a[i]]);
                countA.Add(a[i], v + 1);
            }
            else countA.Add(a[i], 1);

        }  

        // Count elements of b
        for (int i = 0; i < m; i++)
        {
            if (countB.ContainsKey(b[i]))
            {
                var v = countB[b[i]];
                countB.Remove(countB[b[i]]);
                countB.Add(b[i], v + 1);
            }
            else countB.Add(b[i], 1);
        }

        // Traverse through all common element, and
        // pick minimum occurrence from two arrays
        int res = 0;

        foreach (int x in countA.Keys)
            if(countB.ContainsKey(x))
                res += Math.Min(countB[x],
                            countA[x]);

        // To return count of minimum elements
        return res;
    }

    /* Driver code */
    public static void Main(String[] args)
    {

            int []a = { 1, 2, 3, 4 };
            int []b = { 2, 3, 4, 5, 8 };
            int n = a.Length;
            int m = b.Length;

            Console.WriteLine(minRemove(a, b, n, m));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Code to Remove
// minimum number of elements
// such that no common element
// exist in both array

    // To find no elements to remove
    // so no common element exist
    function minRemove(a,b,n,m)
    {
        // To store count of array element
        let countA = new Map();
        let countB = new Map();

        // Count elements of a
        for (let i = 0; i < n; i++){
           if (countA.has(a[i]))
                countA.set(a[i],
                countA.get(a[i]) + 1);

           else
               countA.set(a[i], 1);

        }

        // Count elements of b
        for (let i = 0; i < m; i++){
             if (countB.has(b[i]))
                    countB.set(b[i],
                    countB.get(b[i]) + 1);

             else
                   countB.set(b[i], 1);
        }

        // Traverse through all
        // common element, and
        // pick minimum occurrence
        // from two arrays
        let res = 0;

        for (let x of countA.keys())
            if(countB.has(x))
                res += Math.min(countB.get(x),
                               countA.get(x));

        // To return count of minimum elements
        return res;
    }

    /* Driver program to test above function */
    let a=[1, 2, 3, 4 ];
    let b=[2, 3, 4, 5, 8];
    let n = a.length;
    let m = b.length;
    document.write(minRemove(a, b, n, m));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
3
```

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。