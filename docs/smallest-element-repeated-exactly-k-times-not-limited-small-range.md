# 最小元素精确重复‘k’次(不限于小范围)

> 原文:[https://www . geesforgeks . org/最小元素-重复-精确-k 次-不限-小范围/](https://www.geeksforgeeks.org/smallest-element-repeated-exactly-k-times-not-limited-small-range/)

给定一个大小为 n 的数组，目标是找出最小的重复次数正好为 k 的数，其中 k > 0？
和
示例:

```
Input : a[] = {2, 1, 3, 1, 2, 2}
        k = 3
Output : 2

Input : a[] = {3, 4, 3, 2, 1, 5, 5} 
        k = 2
Output : 3
Explanation: As 3 is smaller than 5\. 
So 3 should be printed.
```

我们在下面的帖子中讨论了这个问题的不同解决方案。
[一个数组中最小的元素被精确地重复‘k’次](https://www.geeksforgeeks.org/smallest-element-array-repeated-exactly-k-times/)
上面讨论的解决方案要么被限制在小范围内，要么在超过线性的时间内工作。在这篇文章中，我们讨论了一种基于哈希的解决方案，它可以在 O(n)时间内工作，并且适用于任何范围。下面是一些抽象的步骤。
1)创建一个存储元素及其频率的散列图。
2)遍历给定数组。对于每个被遍历的元素，增加它的频率。
3)遍历哈希图，打印频率为 k 的最小元素

## C++

```
// C++ program to find the smallest element
// with frequency exactly k.
#include <bits/stdc++.h>
using namespace std;

int smallestKFreq(int a[], int n, int k)
{
    unordered_map<int, int> m;

    // Map is used to store the count of
    // elements present in the array
    for (int i = 0; i < n; i++)
        m[a[i]]++;

    // Traverse the map and find minimum
    // element with frequency k.
    int res = INT_MAX;
    for (auto it = m.begin(); it != m.end(); ++it)
        if (it->second == k)
           res = min(res, it->first);

    return (res != INT_MAX)? res : -1;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 1, 3, 1 };
    int k = 2;
    int n = sizeof(arr) / (sizeof(arr[0]));
    cout << smallestKFreq(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest element
// with frequency exactly k.
import java.util.*;

class GFG {

    public static int smallestKFreq(int a[], int n, int k)
    {
        HashMap<Integer, Integer> m = new HashMap<Integer, Integer>();

        // Map is used to store the count of
        // elements present in the array
        for (int i = 0; i < n; i ++)

            if (m.containsKey(a[i]))
                m.put(a[i], m.get(a[i]) + 1);

           else m.put(a[i], 1);

        // Traverse the map and find minimum
        // element with frequency k.
        int res = Integer.MAX_VALUE;
        Set<Integer> s = m.keySet();

        for (int temp : s)
            if (m.get(temp) == k)
               res = Math.min(res, temp);

        return (res != Integer.MAX_VALUE)? res : -1;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 2, 2, 1, 3, 1 };
        int k = 2;

        System.out.println(smallestKFreq(arr, arr.length, k));

    }
  }
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
from collections import defaultdict
import sys

# Python program to find the smallest element
# with frequency exactly k.
def smallestKFreq(arr, n, k):
    mp = defaultdict(lambda : 0)

    # Map is used to store the count of
    # elements present in the array
    for i in range(n):
        mp[arr[i]] += 1

    # Traverse the map and find minimum
    # element with frequency k.
    res = sys.maxsize
    res1 = sys.maxsize

    for key,values in mp.items():

        if values == k:
            res = min(res, key)
    return res if res != res1 else -1

# Driver code
arr = [2, 2, 1, 3, 1]
k = 2
n = len(arr)
print(smallestKFreq(arr, n, k))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to find the smallest element
// with frequency exactly k.
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

    public static int smallestKFreq(int []a, int n, int k)
    {
        Dictionary<int,int> m = new Dictionary<int,int>();

        // Map is used to store the count of
        // elements present in the array
        for (int i = 0; i < n; i ++)

            if (m.ContainsKey(a[i]))
            {
                var v = m[a[i]];
                m.Remove(a[i]);
                m.Add(a[i],v + 1);
            }
        else m.Add(a[i], 1);

        // Traverse the map and find minimum
        // element with frequency k.
        int res = int.MaxValue;
        HashSet<int> s = new HashSet<int>(m.Keys.ToArray());

        foreach (int temp in s)
            if (m[temp] == k)
            res = Math.Min(res, temp);

        return (res != int.MaxValue)? res : -1;
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        int []arr = { 2, 2, 1, 3, 1 };
        int k = 2;

        Console.WriteLine(smallestKFreq(arr, arr.Length, k));

    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find the smallest element
// with frequency exactly k.

function smallestKFreq(a, n, k) {
    let m = new Map();

    // Map is used to store the count of
    // elements present in the array
    for (let i = 0; i < n; i++)

        if (m.has(a[i]))
            m.set(a[i], m.get(a[i]) + 1);

        else m.set(a[i], 1);

    // Traverse the map and find minimum
    // element with frequency k.
    let res = Number.MAX_SAFE_INTEGER;
    let s = m.keys();

    for (let temp of s)
        if (m.get(temp) == k)
            res = Math.min(res, temp);

    return (res != Number.MAX_SAFE_INTEGER) ? res : -1;
}

/* Driver program to test above function */

let arr = [2, 2, 1, 3, 1];
let k = 2;

document.write(smallestKFreq(arr, arr.length, k));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
1
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
**相关文章:**
[最小重复 k 次的次数](https://www.geeksforgeeks.org/smallest-element-array-repeated-exactly-k-times/)
本文由**吉檀迦利·夏尔马**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。