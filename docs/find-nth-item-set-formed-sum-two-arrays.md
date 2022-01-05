# 在两个数组之和形成的集合中找到第 N 个项目

> 原文:[https://www . geesforgeks . org/find-n th-item-set-formed-sum-two-arrays/](https://www.geeksforgeeks.org/find-nth-item-set-formed-sum-two-arrays/)

给定两个排序的数组，我们可以得到一组和(从第一个中添加一个元素，从第二个中添加一个元素)。在按排序顺序考虑的构成集合的元素中找到第 N 个元素。
**注:**集合和应具有唯一元素。

**示例:**

```
Input: arr1[] = {1, 2}
        arr2[] = {3, 4}
        N = 3
Output: 6
We get following elements set of sums.
4(1+3), 5(2+3 or 1+4), 6(2+4)
Third element in above set is 6.

Input: arr1[] = { 1,3, 4, 8, 10} 
        arr2[] = {20, 22, 30, 40} 
        N = 4
Output: 25
We get following elements set of sums.
21(1+20), 23(1+22 or 20+3), 24(20+4), 25(22+3)...
Fourth element is 25.
```

问于:微软采访

**进场:**

*   运行两个循环，一个用于第一个阵列，第二个用于第二个阵列。
*   只需考虑每一对，并将它们的总和存储在一个自平衡 BST(在 C++中通过 set 和 map 实现)中。
*   我们在 C++中使用 set，因为我们只需要查看元素是否存在，不需要键、值对。
*   遍历集合并返回集合中的第 N 个元素。

下面是上述方法的实现:

## C++

```
// C++ program to find N'th element in a set formed
// by sum of two arrays
#include<bits/stdc++.h>
using namespace std;

//Function to calculate the set of sums
int calculateSetOfSum(int arr1[], int size1, int arr2[],
                      int size2, int N)
{
    // Insert each pair sum into set. Note that a set
    // stores elements in sorted order and unique elements
    set<int> s;
    for (int i=0 ; i < size1; i++)
        for (int j=0; j < size2; j++)
            s.insert(arr1[i]+arr2[j]);

    // If set has less than N elements
    if (s.size() < N)
       return -1;

    // Find N'tb item in set and return it
    set<int>::iterator it = s.begin();
    for (int count=1; count<N; count++)
        it++;
    return *it;
}

// Driver code
int main()
{
    int arr1[] = {1, 2};
    int size1 = sizeof(arr1) / sizeof(arr1[0]);
    int arr2[] = {3, 4};
    int size2 = sizeof(arr2) / sizeof(arr2[0]);

    int N = 3;
    int res = calculateSetOfSum(arr1, size1, arr2, size2, N);
    if (res == -1)
        cout << "N'th term doesn't exists in set";
    else
        cout << "N'th element in the set of sums is "
             << res;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N'th element in a set formed
// by sum of two arrays
import java.util.*;

class GFG
{

// Function to calculate the set of sums
static int calculateSetOfSum(int arr1[], int size1, int arr2[],
                                            int size2, int N)
{
    // Insert each pair sum into set. Note that a set
    // stores elements in sorted order and unique elements
    SortedSet<Integer> s = new TreeSet<Integer>();
    for (int i = 0; i < size1; i++)
        for (int j = 0; j < size2; j++)
            s.add(arr1[i]+arr2[j]);

    // If set has less than N elements
    if (s.size() < N)
    return -1;

    // Find N'tb item in set and return it

    return (int)s.toArray()[ N-1 ];
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = {1, 2};
    int size1 = arr1.length;
    int arr2[] = {3, 4};
    int size2 = arr2.length;

    int N = 3;
    int res = calculateSetOfSum(arr1, size1, arr2, size2, N);
    if (res == -1)
        System.out.println("N'th term doesn't exists in set");
    else
        System.out.println("N'th element in the set of sums is "
            +res);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find N'th element in
// a set formed by sum of two arrays
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

// Function to calculate the set of sums
static int calculateSetOfSum(int []arr1, int size1,
                             int []arr2, int size2,
                             int N)
{
    // Insert each pair sum into set.
    // Note that a set stores elements in
    // sorted order and unique elements
    HashSet<int> s = new HashSet<int>();
    for (int i = 0; i < size1; i++)
        for (int j = 0; j < size2; j++)
            s.Add(arr1[i] + arr2[j]);

    // If set has less than N elements
    if (s.Count < N)
    return -1;

    // Find N'tb item in set and return it
    int []last = s.ToArray();
    return last[s.Count - 1];
}

// Driver code
public static void Main(String[] args)
{
    int []arr1 = {1, 2};
    int size1 = arr1.Length;
    int []arr2 = {3, 4};
    int size2 = arr2.Length;

    int N = 3;
    int res = calculateSetOfSum(arr1, size1,
                                arr2, size2, N);
    if (res == -1)
        Console.WriteLine("N'th term doesn't exists in set");
    else
        Console.WriteLine("N'th element in the set" +
                               " of sums is " + res);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find N'th
// element in a set formed
// by sum of two arrays

// Function to calculate the set of sums
function calculateSetOfSum(arr1, size1,
                           arr2, size2, N)
{

    // Insert each pair sum into set.
    // Note that a set stores elements
    // in sorted order and unique elements
    let s = new Set();
    for(let i = 0; i < size1; i++)
        for(let j = 0; j < size2; j++)
            s.add(arr1[i]+arr2[j]);

    // If set has less than N elements
    if (s.size < N)
        return -1;

    // Find N'tb item in set and return it
    return Array.from(s)[N - 1];
}

// Driver code
let arr1 = [ 1, 2 ];
let size1 = arr1.length;
let arr2 = [ 3, 4 ];
let size2 = arr2.length;
let N = 3;

let res = calculateSetOfSum(arr1, size1,
                            arr2, size2, N);
if (res == -1)
    document.write("N'th term doesn't " +
                   "exists in set");
else
    document.write("N'th element in the set " +
                   "of sums is " + res);

// This code is contributed by rag2127

</script>
```

**Output**

```
N'th element in the set of sums is 6
```

**时间复杂度:** O(mn log (mn))其中 m 是第一个数组的大小，n 是第二个数组的大小。

本文由 [**萨希尔·查布拉(akku)**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。