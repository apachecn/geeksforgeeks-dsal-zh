# 数组中的第 k 个不同(或非重复)元素。

> 原文:[https://www . geesforgeks . org/k-th-distinct-or-non-repeating-element in a-array/](https://www.geeksforgeeks.org/k-th-distinct-or-non-repeating-element-in-an-array/)

给定一个整数数组，打印数组中的第 k 个不同元素。给定的数组可能包含重复项，输出应该打印所有唯一元素中的第 k 个元素。如果 k 大于不同元素的数量，打印-1。
**例:**

```
Input : arr[] = {1, 2, 1, 3, 4, 2}, 
        k = 2
Output : 4

First non-repeating element is 3
Second non-repeating element is 4

Input : arr[] = {1, 2, 50, 10, 20, 2}, 
        k = 3
Output : 10

Input : {2, 2, 2, 2}, 
        k = 2
Output : -1
```

一个**简单的解决方案**是使用两个嵌套循环，其中外部循环从左到右拾取元素，内部循环检查拾取的元素是否存在于其他地方。如果不存在，则递增不同元素的计数。如果计数变成 k，返回当前元素。

## C++

```
// C++ program to print k-th distinct
// element in a given array
#include <bits/stdc++.h>
using namespace std;

// Returns k-th distinct
// element in arr.
int printKDistinct(int arr[], int n,
                              int k)
{
    int dist_count = 0;
    for (int i = 0; i < n; i++)
    {
        // Check if current element is
        // present somewhere else.
        int j;
        for (j = 0; j < n; j++)
            if (i != j && arr[j] == arr[i])
                break;

        // If element is unique
        if (j == n)
            dist_count++;

        if (dist_count == k)
            return arr[i];
    }

    return -1;
}

// Driver Code
int main ()
{
    int ar[] = {1, 2, 1, 3, 4, 2};
    int n = sizeof(ar) / sizeof(ar[0]);
    int k = 2;
    cout << printKDistinct(ar, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print k-th distinct
// element in a given array
class GFG
{
    // Returns k-th distinct element in arr.
    static int printKDistinct(int arr[],
                                  int n,
                                  int k)
    {
        int dist_count = 0;
        for (int i = 0; i < n; i++)
        {

            // Check if current element is
            // present somewhere else.
            int j;

            for (j = 0; j < n; j++)
                if (i != j && arr[j] == arr[i])
                    break;

            // If element is unique
            if (j == n)
                dist_count++;

            if (dist_count == k)
                return arr[i];
        }

        return -1;
    }

    //Driver code
    public static void main (String[] args)
    {

        int ar[] = {1, 2, 1, 3, 4, 2};
        int n = ar.length;
        int k = 2;

        System.out.print(printKDistinct(ar, n, k));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to prk-th distinct
# element in a given array

# Returns k-th distinct
# element in arr.
def printKDistinct(arr, n, k):
    dist_count = 0
    for i in range(n):

        # Check if current element is
        # present somewhere else.
        j = 0
        while j < n:
            if (i != j and arr[j] == arr[i]):
                break
            j += 1

        # If element is unique
        if (j == n):
            dist_count += 1

        if (dist_count == k):
            return arr[i]

    return -1

# Driver Code
ar = [1, 2, 1, 3, 4, 2]
n = len(ar)
k = 2
print(printKDistinct(ar, n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to print k-th distinct
// element in a given array
using System;

class GFG
{
    // Returns k-th distinct element in arr
    static int printKDistinct(int []arr,
                                  int n,
                                  int k)
    {

        int dist_count = 0;
        for (int i = 0; i < n; i++)
        {

            // Check if current element is
            // present somewhere else.
            int j;

            for (j = 0; j < n; j++)
                if (i != j && arr[j] == arr[i])
                    break;

            // If element is unique
            if (j == n)
                dist_count++;

            if (dist_count == k)
                return arr[i];
        }

        return -1;
    }

    //Driver code
    public static void Main ()
    {

        int []ar = {1, 2, 1, 3, 4, 2};
        int n = ar.Length;
        int k = 2;

        Console.Write(printKDistinct(ar, n, k));
    }
}

// This code is contributed by nitn mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print k-th
// distinct element in a
// given array

// Returns k-th distinct
// element in arr.
function printKDistinct($arr,
                        $n, $k)
{
    $dist_count = 0;
    for ($i = 0; $i < $n; $i++)
    {
        // Check if current element
        // is present somewhere else.
        $j;
        for ($j = 0; $j < $n; $j++)
            if ($i != $j && $arr[$j] ==
                            $arr[$i])
                break;

        // If element is unique
        if ($j == $n)
            $dist_count++;

        if ($dist_count == $k)
            return $arr[$i];
    }

    return -1;
}

// Driver Code
$ar = array(1, 2, 1, 3, 4, 2);
$n = sizeof($ar) / sizeof($ar[0]);
$k = 2;
echo printKDistinct($ar, $n, $k);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
//Javascript program to print k-th distinct
// element in a given array

// Returns k-th distinct
// element in arr.
function printKDistinct(arr, n,  k)
{
    var dist_count = 0;
    for (var i = 0; i < n; i++)
    {
        // Check if current element is
        // present somewhere else.
        var j;
        for (j = 0; j < n; j++)
            if (i != j && arr[j] == arr[i])
                break;

        // If element is unique
        if (j == n)
            dist_count++;

        if (dist_count == k)
            return arr[i];
    }

    return -1;
}

var ar = [1, 2, 1, 3, 4, 2];
    var n = ar.length;
    var k = 2;
    document.write( printKDistinct(ar, n, k));

//This code is contributed by SoumikMondal
</script>
```

**输出:**

```
4
```

一个有效的解决方案是使用哈希平均在 O(n)时间内解决这个问题。
**1)** 创建一个空哈希表。
**2)** 从左到右遍历输入数组，并将元素及其计数存储在哈希表中。
**3)** 从左到右再次遍历输入数组。继续计算计数为 1 的元素。
**4)** 如果计数变为 k，返回当前元素。

## C++

```
// C++ program to print k-th
// distinct element in a
// given array
#include <bits/stdc++.h>
using namespace std;

// Returns k-th distinct
// element in arr
int printKDistinct(int arr[],
                   int n, int k)
{
    // Traverse input array and
    // store counts if individual
    // elements.
    unordered_map<int, int> h;
    for (int i = 0; i < n; i++)
        h[arr[i]]++;

    // If size of hash is
    // less than k.
    if (h.size() < k)
        return -1;

    // Traverse array again and
    // find k-th element with
    // count as 1.
    int dist_count = 0;
    for (int i = 0; i < n; i++)
    {
        if (h[arr[i]] == 1)
            dist_count++;
        if (dist_count == k)
            return arr[i];
    }

    return -1;
}

// Driver Code
int main ()
{
    int ar[] = {1, 2, 1, 3, 4, 2};
    int n = sizeof(ar) / sizeof(ar[0]);
    cout << printKDistinct(ar, n, 2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print k-th distinct
// element in a given array
import java.util.*;

class GfG
{

// Returns k-th distinct
// element in arr.
static int printKDistinct(int arr[],
                        int n, int k)
{
    //int dist_count = 0;
    Map <Integer, Integer> h =
       new HashMap<Integer, Integer> ();

    for (int i = 0; i < n; i++)
    {
        if(h.containsKey(arr[i]))
            h.put(arr[i], h.get(arr[i]) + 1);
        else
            h.put(arr[i], 1);
    }

    // If size of hash is
    // less than k.
    if (h.size() < k)
        return -1;

    // Traverse array again and
    // find k-th element with
    // count as 1.
    int dist_count = 0;
    for (int i = 0; i < n; i++)
    {
        if (h.get(arr[i]) == 1)
            dist_count++;
        if (dist_count == k)
            return arr[i];
    }
    return -1;
}

// Driver Code
public static void main (String[] args)
{
    int ar[] = {1, 2, 1, 3, 4, 2};
    int n = ar.length;
    System.out.println(printKDistinct(ar, n, 2));
}
}

// This code is contributed by
// Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to print k-th
# distinct element in a given array
def printKDistinct(arr, size, KthIndex):
    dict = {}
    vect = []
    for i in range(size):
        if(arr[i] in dict):
            dict[arr[i]] = dict[arr[i]] + 1
        else:
            dict[arr[i]] = 1
    for i in range(size):
        if(dict[arr[i]] > 1):
            continue
        else:
            KthIndex = KthIndex - 1
        if(KthIndex == 0):
            return arr[i]
    return -1

# Driver Code
arr = [1, 2, 1, 3, 4, 2]
size = len(arr)
print(printKDistinct(arr, size, 2))

# This code is contributed
# by Akhand Pratap Singh
```

## C#

```
// C# program to print k-th distinct
// element in a given array
using System;
using System.Collections.Generic;

class GfG
{

// Returns k-th distinct
// element in arr.
static int printKDistinct(int []arr,
                        int n, int k)
{
    Dictionary<int, int> h = new Dictionary<int, int>();
    for (int i = 0; i < n; i++)
    {
        if(h.ContainsKey(arr[i]))
        {
            var val = h[arr[i]];
            h.Remove(arr[i]);
            h.Add(arr[i], val + 1);

        }    
        else
            h.Add(arr[i], 1);
    }

    // If size of hash is
    // less than k.
    if (h.Count < k)
        return -1;

    // Traverse array again and
    // find k-th element with
    // count as 1.
    int dist_count = 0;
    for (int i = 0; i < n; i++)
    {
        if (h[arr[i]] == 1)
            dist_count++;
        if (dist_count == k)
            return arr[i];
    }
    return -1;
}

// Driver Code
public static void Main (String[] args)
{
    int []ar = {1, 2, 1, 3, 4, 2};
    int n = ar.Length;
    Console.WriteLine(printKDistinct(ar, n, 2));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to print k-th distinct
// element in a given array

    // Returns k-th distinct
    // element in arr.
    function printKDistinct(arr,n,k)
    {
        // int dist_count = 0;
    let h = new Map();

    for (let i = 0; i < n; i++)
    {
        if(h.has(arr[i]))
            h.set(arr[i], h.get(arr[i]) + 1);
        else
            h.set(arr[i], 1);
    }

    // If size of hash is
    // less than k.
    if (h.length < k)
        return -1;

    // Traverse array again and
    // find k-th element with
    // count as 1.
    let dist_count = 0;
    for (let i = 0; i < n; i++)
    {
        if (h.get(arr[i]) == 1)
            dist_count++;
        if (dist_count == k)
            return arr[i];
    }
    return -1;
    }

    // Driver Code
    let ar=[1, 2, 1, 3, 4, 2];
    let n = ar.length;
    document.write(printKDistinct(ar, n, 2));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
4
```

本文由**阿夫扎尔·安萨里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。