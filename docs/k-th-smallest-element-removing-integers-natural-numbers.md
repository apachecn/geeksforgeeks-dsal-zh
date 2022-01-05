# 从自然数中去掉一些整数后的第 K 个最小元素

> 原文:[https://www . geesforgeks . org/k-th-最小元素-移除-整数-自然数/](https://www.geeksforgeeks.org/k-th-smallest-element-removing-integers-natural-numbers/)

给定一个大小为**‘n’**的数组 **arr[]** 和一个正整数 **k** 。考虑一系列自然数，从中去掉 arr[0]，arr[1]，arr[2]，…，arr[p]。现在的任务是在剩下的自然数集中找到第 k 个最小的数。如果没有这样的号码，打印“-1”。

**示例:**

```
Input : arr[] = { 1 } and k = 1.
Output: 2
Natural numbers are {1, 2, 3, 4, .... }
After removing {1}, we get {2, 3, 4, ...}.
Now, K-th smallest element = 2.

Input : arr[] = {1, 3}, k = 4.
Output : 6
First 5 Natural number {1, 2, 3, 4, 5, 6,  .. }
After removing {1, 3}, we get {2, 4, 5, 6, ... }.
```

**方法 1(简单):**
制作一个有/无自然数的辅助数组 b[]，并用 0 初始化所有数组。使数组 arr[]中的所有整数等于 1，即 b[arr[i]] = 1。现在，运行一个循环，每当遇到未标记的单元格时递减 k。当 k 的值为 0 时，我们得到答案。

下面是这种方法的实现:

## C++

```
// C++ program to find the K-th smallest element
// after removing some integers from natural number.
#include <bits/stdc++.h>
#define MAX 1000000
using namespace std;

// Return the K-th smallest element.
int ksmallest(int arr[], int n, int k)
{
    // Making an array, and mark all number as unmarked.
    int b[MAX];
    memset(b, 0, sizeof b);

    // Marking the number present in the given array.
    for (int i = 0; i < n; i++)
        b[arr[i]] = 1;

    for (int j = 1; j < MAX; j++) {
        // If j is unmarked, reduce k by 1.
        if (b[j] != 1)
            k--;

        // If k is 0 return j.
        if (!k)
            return j;
    }
}

// Driven Program
int main()
{
    int k = 1;
    int arr[] = { 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << ksmallest(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the K-th smallest element
// after removing some integers from natural number.
class GFG {

    static final int MAX = 1000000;

    // Return the K-th smallest element.
    static int ksmallest(int arr[], int n, int k)
    {
        // Making an array, and mark
        // all number as unmarked.
        int b[] = new int[MAX];

        // Marking the number present
        // in the given array.
        for (int i = 0; i < n; i++) {
            b[arr[i]] = 1;
        }

        for (int j = 1; j < MAX; j++) {
            // If j is unmarked, reduce k by 1.
            if (b[j] != 1) {
                k--;
            }

            // If k is 0 return j.
            if (k != 1) {
                return j;
            }
        }
        return Integer.MAX_VALUE;
    }

    // Driven code
    public static void main(String[] args)
    {
        int k = 1;
        int arr[] = { 1 };
        int n = arr.length;
        System.out.println(ksmallest(arr, n, k));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find the K-th smallest element
# after removing some integers from natural number.
MAX = 1000000

# Return the K-th smallest element.
def ksmallest(arr, n, k):

    # Making an array, and mark all number as unmarked.
    b = [0]*MAX;

    # Marking the number present in the given array.
    for i in range(n):
        b[arr[i]] = 1;

    for j in range(1, MAX):
        # If j is unmarked, reduce k by 1.
        if (b[j] != 1):
            k-= 1;

        # If k is 0 return j.
        if (k is not 1):
            return j;

# Driven Program
k = 1;
arr = [ 1 ];
n = len(arr);
print(ksmallest(arr, n, k));

# This code contributed by Rajput-Ji
```

## C#

```
// C# program to find the K-th smallest element
// after removing some integers from natural number.
using System;

class GFG {

    static int MAX = 1000000;

    // Return the K-th smallest element.
    static int ksmallest(int[] arr, int n, int k)
    {
        // Making an array, and mark
        // all number as unmarked.
        int[] b = new int[MAX];

        // Marking the number present
        // in the given array.
        for (int i = 0; i < n; i++) {
            b[arr[i]] = 1;
        }

        for (int j = 1; j < MAX; j++) {
            // If j is unmarked, reduce k by 1.
            if (b[j] != 1) {
                k--;
            }

            // If k is 0 return j.
            if (k != 1) {
                return j;
            }
        }
        return int.MaxValue;
    }

    // Driven code
    public static void Main()
    {
        int k = 1;
        int[] arr = { 1 };
        int n = arr.Length;
        Console.WriteLine(ksmallest(arr, n, k));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the K-th smallest element
// after removing some integers from natural number.
$MAX = 10000;

// Return the K-th smallest element.
function ksmallest($arr, $n, $k)
{
    global $MAX;

    // Making an array, and mark all number as unmarked.
    $b=array_fill(0, $MAX, 0);

    // Marking the number present in the given array.
    for ($i = 0; $i < $n; $i++)
        $b[$arr[$i]] = 1;

    for ($j = 1; $j < $MAX; $j++)
    {
        // If j is unmarked, reduce k by 1.
        if ($b[$j] != 1)
            $k--;

        // If k is 0 return j.
        if ($k == 0)
            return $j;
    }
}

// Driver code
    $k = 1;
    $arr = array( 1 );
    $n = count($arr);
    echo ksmallest($arr, $n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the K-th
// smallest element after removing some
// integers from natural number.

let MAX = 1000000;

// Return the K-th smallest element.
function ksmallest(arr, n, k)
{

    // Making an array, and mark
    // all number as unmarked.
    let b = [];

    // Marking the number present
    // in the given array.
    for(let i = 0; i < n; i++)
    {
        b[arr[i]] = 1;
    }

    for(let j = 1; j < MAX; j++)
    {

        // If j is unmarked, reduce k by 1.
        if (b[j] != 1)
        {
            k--;
        }

        // If k is 0 return j.
        if (k != 1)
        {
            return j;
        }
    }
    return Number.MAX_VALUE;
}

// Driver code   
let k = 1;
let arr = [1];
let n = arr.length;

document.write(ksmallest(arr, n, k));

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n)。

**方法二(高效):**
首先，排序数组 arr[]。注意，在 0 和 arr[0]之间会有 arr[0]–1 个数字，类似地，在 arr[0]和 arr[1]之间会有 arr[1]–arr[0]–1 个数字，以此类推。因此，如果 K 位于 arr[I]–arr[I+1]–1 之间，则返回该范围内的第 K 个最小元素。否则通过 arr[I]–arr[I+1]–1 减少 k，即 k = k –( arr[I]–arr[I+1]–1)。

解决问题的算法:

```
1\. Sort the array arr[].
2\. For i = 1 to k. Find c = arr[i+1] - arr[i] -1.
  a) if k - c <= 0, return arr[i-1] + k.
  b) else k = k - c.
```

下面是这种方法的实现:

## C++

```
// C++ program to find the Kth smallest element
// after removing some integer from first n
// natural number.
#include <bits/stdc++.h>
using namespace std;

// Return the K-th smallest element.
int ksmallest(int arr[], int n, int k)
{
    sort(arr, arr + n);

    // Checking if k lies before 1st element
    if (k < arr[0])
        return k;

    // If k is the first element of array arr[].
    if (k == arr[0])
        return arr[0] + 1;

    // If k is more than last element
    if (k > arr[n - 1])
        return k + n;

    // If first element of array is 1.
    if (arr[0] == 1)
        k--;

    // Reducing k by numbers before arr[0].
    else
        k -= (arr[0] - 1);

    // Finding k'th smallest element after removing
    // array elements.
    for (int i = 1; i < n; i++) {
        // Finding count of element between i-th
        // and (i-1)-th element.
        int c = arr[i] - arr[i - 1] - 1;
        if (k <= c)
            return arr[i - 1] + k;
        else
            k -= c;
    }

    return arr[n - 1] + k;
}

// Driven Program
int main()
{
    int k = 1;
    int arr[] = { 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << ksmallest(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// Kth smallest element after
// removing some integer from
// first n natural number.
import java.util.Arrays;
import java.io.*;

class GFG {

    // Return the K-th
    // smallest element.
    static int ksmallest(int arr[],
                         int n, int k)
    {
        // sort(arr, arr+n);
        Arrays.sort(arr);

        // Checking if k lies
        // before 1st element
        if (k < arr[0])
            return k;

        // If k is the first
        // element of array arr[].
        if (k == arr[0])
            return arr[0] + 1;

        // If k is more
        // than last element
        if (k > arr[n - 1])
            return k + n;

        // If first element
        // of array is 1.
        if (arr[0] == 1)
            k--;

        // Reducing k by numbers
        // before arr[0].
        else
            k -= (arr[0] - 1);

        // Finding k'th smallest
        // element after removing
        // array elements.
        for (int i = 1; i < n; i++) {
            // Finding count of
            // element between i-th
            // and (i-1)-th element.
            int c = arr[i] - arr[i - 1] - 1;
            if (k <= c)
                return arr[i - 1] + k;
            else
                k -= c;
        }

        return arr[n - 1] + k;
    }

    // Driven Code
    public static void main(String[] args)
    {
        int k = 1;
        int arr[] = { 1 };
        int n = arr.length;
        System.out.println(ksmallest(arr, n, k));
    }
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 program to find the Kth
# smallest element after
# removing some integer from
# first n natural number.

# Return the K-th
# smallest element.
def ksmallest(arr, n, k):

    arr.sort();

    # Checking if k lies
    # before 1st element
    if (k < arr[0]):
        return k;

    # If k is the first
    # element of array arr[].
    if (k == arr[0]):
        return arr[0] + 1;

    # If k is more
    # than last element
    if (k > arr[n - 1]):
        return k + n;

    # If first element
    # of array is 1.
    if (arr[0] == 1):
        k-= 1;

    # Reducing k by numbers
    # before arr[0].
    else:
        k -= (arr[0] - 1);

    # Finding k'th smallest element
    # after removing array elements.
    for i in range(1, n):
        # Finding count of element between
        # i-th and (i-1)-th element.
        c = arr[i] - arr[i - 1] - 1;
        if (k <= c):
            return arr[i - 1] + k;
        else:
            k -= c;

    return arr[n - 1] + k;

# Driver Code
k = 1;
arr =[ 1 ];
n = len(arr);
print(ksmallest(arr, n, k));

# This code is contributed by mits
```

## C#

```
// C# program to find the
// Kth smallest element after
// removing some integer from
// first n natural number.
using System;

class GFG {
    // Return the K-th
    // smallest element.
    static int ksmallest(int[] arr,
                         int n, int k)
    {
        // sort(arr, arr+n);
        Array.Sort(arr);

        // Checking if k lies
        // before 1st element
        if (k < arr[0])
            return k;

        // If k is the first
        // element of array arr[].
        if (k == arr[0])
            return arr[0] + 1;

        // If k is more
        // than last element
        if (k > arr[n - 1])
            return k + n;

        // If first element
        // of array is 1.
        if (arr[0] == 1)
            k--;

        // Reducing k by numbers
        // before arr[0].
        else
            k -= (arr[0] - 1);

        // Finding k'th smallest
        // element after removing
        // array elements.
        for (int i = 1; i < n; i++) {
            // Finding count of
            // element between i-th
            // and (i-1)-th element.
            int c = arr[i] - arr[i - 1] - 1;
            if (k <= c)
                return arr[i - 1] + k;
            else
                k -= c;
        }

        return arr[n - 1] + k;
    }

    // Driver Code
    static public void Main()
    {
        int k = 1;
        int[] arr = { 1 };
        int n = arr.Length;
        Console.WriteLine(ksmallest(arr, n, k));
    }
}

// This code is contributed
// by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the Kth
// smallest element after
// removing some integer from
// first n natural number.

// Return the K-th
// smallest element.
function ksmallest($arr, $n, $k)
{
    sort($arr);

    // Checking if k lies
    // before 1st element
    if ($k < $arr[0])
        return $k;

    // If k is the first
    // element of array arr[].
    if ($k == $arr[0])
        return $arr[0] + 1;

    // If k is more
    // than last element
    if ($k > $arr[$n - 1])
        return $k + $n;

    // If first element
    // of array is 1.
    if ($arr[0] == 1)
        $k--;

    // Reducing k by numbers
    // before arr[0].
    else
        $k -= ($arr[0] - 1);

    // Finding k'th smallest element
    // after removing array elements.
    for ($i = 1; $i < $n; $i++)
    {
        // Finding count of element between
        // i-th and (i-1)-th element.
        $c = $arr[$i] - $arr[$i - 1] - 1;
        if ($k <= $c)
            return $arr[$i - 1] + $k;
        else
            $k -= $c;
    }

    return $arr[$n - 1] + $k;
}

// Driver Code
$k = 1;
$arr = array ( 1 );
$n = sizeof($arr);
echo ksmallest($arr, $n, $k);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// Kth smallest element after
// removing some integer from
// first n natural number.

// Return the K-th
// smallest element.
function ksmallest(arr, n, k)
{

    // sort(arr, arr+n);
    arr.sort(function(a, b){return a - b});

    // Checking if k lies
    // before 1st element
    if (k < arr[0])
        return k;

    // If k is the first
    // element of array arr[].
    if (k == arr[0])
        return arr[0] + 1;

    // If k is more
    // than last element
    if (k > arr[n - 1])
        return k + n;

    // If first element
    // of array is 1.
    if (arr[0] == 1)
        k--;

    // Reducing k by numbers
    // before arr[0].
    else
        k -= (arr[0] - 1);

    // Finding k'th smallest
    // element after removing
    // array elements.
    for(let i = 1; i < n; i++)
    {

        // Finding count of
        // element between i-th
        // and (i-1)-th element.
        let c = arr[i] - arr[i - 1] - 1;
        if (k <= c)
            return arr[i - 1] + k;
        else
            k -= c;
    }
    return arr[n - 1] + k;
}

// Driver code
let k = 1;
let arr = [1];
let n = arr.length;

document.write(ksmallest(arr, n, k));

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
2
```

更高效的方法:[自然数去掉给定整数后的第 K 个最小元素|集合 2](https://www.geeksforgeeks.org/k-th-smallest-element-removing-given-integers-natural-numbers-set-2/)
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。