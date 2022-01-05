# 绝对差小于 k 的数组中的三元组

> 原文:[https://www . geesforgeks . org/triplets-array-absolute-difference-less-k/](https://www.geeksforgeeks.org/triplets-array-absolute-difference-less-k/)

给定一个由 **n** 个元素和一个整数 **k** 组成的数组**[]**。任务是找到三元组(x，y，k)的个数，其中 0 < = x，y，k < n 和 x，y，k 是数组 A[]中的索引，这样:
| A[x]–A[y]|<= k
| A[y]–A[z]|<= k
| A[z]–A[x]|<= k

**示例:**

```
Input : A[] = { 1, 1, 2, 2, 3 }, k = 1
Output : 5
(0, 1, 2), (0, 1, 3), (0, 2, 3), (1, 2, 3),
(2, 3, 4) are the triplet whose element will 
satisfy the above three condition.

Input : A[] = { 1, 2, 3 }, k = 1
Output : 0
```

一个**简单的解决方案**是运行三个嵌套循环，并用给定的约束对三元组进行计数。

一个**高效的解决方案**是基于这样一个事实:重新排列数组中的元素不会影响答案，因为基本上，我们希望索引 x，y，z 按递增顺序排列，而不是 A[x]，A[y]，A[z]排序。假设，A[x]在索引 y，A[y]在 z，A[z]在 x，我们仍然可以选择三元组(x，y，z)，因为任何两个元素之差小于 k 的条件仍然成立。

现在，为了计算满足上述条件的三元组索引(x，y，z)的数量，我们将对给定的数组进行排序。现在，对于每个元素 A[i]，i >= 2，我们将找到 A[I]–k 的下界指数，比如 lb。现在，观察索引 lb 和 I 之间的所有元素都小于 A[i]，任何两个元素之间的差都将小于或等于 k。因此，索引 I 处的元素可以被视为索引 z，我们可以从 lb 到 I–1 中选择任何两个元素。因此，这将使三连音的计数增加<sup>I–lb</sup>C<sup>2</sup>。

下面是该方法的实现:

## C++

```
// CPP program to count triplets with difference less
// than k.
#include <bits/stdc++.h>
using namespace std;

// Return the lower bound i.e smallest index of
// element having value greater or equal to value
int binary_lower(int value, int arr[], int n)
{
    int start = 0;
    int end = n - 1;
    int ans = -1;
    int mid;

    while (start <= end) {
        mid = (start + end) / 2;
        if (arr[mid] >= value) {
            end = mid - 1;
            ans = mid;
        }
        else {
            start = mid + 1;
        }
    }
    return ans;
}

// Return the number of triplet indices satisfies
// the three constraints
int countTriplet(int arr[], int n, int k)
{
    int count = 0;

    // sort the array
    sort(arr, arr + n);

    // for each element from index 2 to n - 1.
    for (int i = 2; i < n; i++) {

        // finding the lower bound of arr[i] - k.
        int cur = binary_lower(arr[i] - k, arr, n);

        // If there are at least two elements between
        // lower bound and current element.
        if (cur <= i - 2) {

            // increment the count by lb - i C 2.
            count += ((i - cur) * (i - cur - 1)) / 2;
        }
    }

    return count;
}
int main()
{
    int arr[] = { 1, 1, 2, 2, 3 };
    int k = 1;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countTriplet(arr, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count triplets
// with difference less than k.
import java.io.*;
import java .util.*;

class GFG
{

// Return the lower bound i.e
// smallest index of element
// having value greater or
// equal to value
static int binary_lower(int value,
                        int arr[],
                        int n)
{
    int start = 0;
    int end = n - 1;
    int ans = -1;
    int mid;

    while (start <= end)
    {
        mid = (start + end) / 2;
        if (arr[mid] >= value)
        {
            end = mid - 1;
            ans = mid;
        }
        else
        {
            start = mid + 1;
        }
    }
    return ans;
}

// Return the number of
// triplet indices satisfies
// the three constraints
static int countTriplet(int arr[],
                        int n, int k)
{
    int count = 0;

    // sort the array
    Arrays.sort(arr);

    // for each element from
    // index 2 to n - 1.
    for (int i = 2; i < n; i++)
    {

        // finding the lower
        // bound of arr[i] - k.
        int cur = binary_lower(arr[i] - k,
                               arr, n);

        // If there are at least two
        // elements between lower
        // bound and current element.
        if (cur <= i - 2)
        {

            // increment the count
            // by lb - i C 2.
            count += ((i - cur) *
                      (i - cur - 1)) / 2;
        }
    }
    return count;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {1, 1, 2, 2, 3};
    int k = 1;
    int n = arr.length;

    System.out.println(countTriplet(arr, n, k));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to count
# triplets with difference less
# than k.

# Return the lower bound
# i.e smallest index of
# element having value greater
# or equal to value
def binary_lower(value, arr, n):

    start = 0
    end = n - 1
    ans = -1

    while (start <= end) :
        mid = (start + end) // 2
        if (arr[mid] >= value) :
            end = mid - 1
            ans = mid

        else :
            start = mid + 1

    return ans

# Return the number of triplet
# indices satisfies
# the three constraints
def countTriplet(arr, n, k):

    count = 0

    # sort the array
    arr.sort()

    # for each element from
    # index 2 to n - 1.
    for i in range(2, n) :

        # finding the lower bound
        # of arr[i] - k.
        cur = (binary_lower(arr[i] - k
                            , arr, n))

        # If there are at least
        # two elements between
        # lower bound and current element.
        if (cur <= i - 2) :

            # increment the count by
            # lb - i C 2.
            count += ((i - cur) *
                     (i - cur - 1)) // 2

    return count

# Driver code       
if __name__ == "__main__":
    arr = [ 1, 1, 2, 2, 3 ]
    k = 1
    n = len(arr)

    print(countTriplet(arr, n, k))

# This code is contributed by
# ChitraNayal
```

## C#

```
// C# program to count triplets
// with difference less than k.
using System;

class GFG
{

// Return the lower bound i.e
// smallest index of element
// having value greater or
// equal to value
static int binary_lower(int value,
                        int []arr,
                        int n)
{
    int start = 0;
    int end = n - 1;
    int ans = -1;
    int mid;

    while (start <= end)
    {
        mid = (start + end) / 2;
        if (arr[mid] >= value)
        {
            end = mid - 1;
            ans = mid;
        }
        else
        {
            start = mid + 1;
        }
    }
    return ans;
}

// Return the number of
// triplet indices satisfies
// the three constraints
static int countTriplet(int []arr,
                        int n, int k)
{
    int count = 0;

    // sort the array
    Array.Sort(arr);

    // for each element from
    // index 2 to n - 1.
    for (int i = 2; i < n; i++)
    {

        // finding the lower
        // bound of arr[i] - k.
        int cur = binary_lower(arr[i] - k,
                               arr, n);

        // If there are at least two
        // elements between lower
        // bound and current element.
        if (cur <= i - 2)
        {

            // increment the count
            // by lb - i C 2.
            count += ((i - cur) *
                      (i - cur - 1)) / 2;
        }
    }
    return count;
}

// Driver Code
public static void Main ()
{
    int []arr = {1, 1, 2, 2, 3};
    int k = 1;
    int n = arr.Length;

    Console.WriteLine(countTriplet(arr, n, k));
}
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>

// Javascript program to count triplets with difference less
// than k.

// Return the lower bound i.e smallest index of
// element having value greater or equal to value
function binary_lower(value, arr, n)
{
    var start = 0;
    var end = n - 1;
    var ans = -1;
    var mid;

    while (start <= end) {
        mid = parseInt((start + end) / 2);
        if (arr[mid] >= value) {
            end = mid - 1;
            ans = mid;
        }
        else {
            start = mid + 1;
        }
    }
    return ans;
}

// Return the number of triplet indices satisfies
// the three constraints
function countTriplet(arr, n, k)
{
    var count = 0;

    // sort the array
    arr.sort((a,b)=>a-b)

    // for each element from index 2 to n - 1.
    for (var i = 2; i < n; i++) {

        // finding the lower bound of arr[i] - k.
        var cur = binary_lower(arr[i] - k, arr, n);

        // If there are at least two elements between
        // lower bound and current element.
        if (cur <= i - 2) {

            // increment the count by lb - i C 2.
            count += parseInt(((i - cur) * (i - cur - 1)) / 2);
        }
    }

    return count;
}

// Driver code
var arr = [ 1, 1, 2, 2, 3 ];
var k = 1;
var n = arr.length;
document.write( countTriplet(arr, n, k));

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
5
```

**复杂度:** O(nlogn)