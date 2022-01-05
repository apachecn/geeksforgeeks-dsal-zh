# 插值搜索

> 原文:[https://www.geeksforgeeks.org/interpolation-search/](https://www.geeksforgeeks.org/interpolation-search/)

给定 n 个均匀分布的值 arr[]，编写一个函数来搜索数组中的特定元素 x。
线性搜索在 O(n)时间内找到元素，[跳转搜索](https://www.geeksforgeeks.org/jump-search/)用 O(√ n)时间，[二分搜索法](https://www.geeksforgeeks.org/binary-search/)用 O(Log n)时间。
对于排序数组中的值均匀分布的情况，插值搜索是对[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的改进。二分搜索法总是去中间元素检查。另一方面，根据被搜索的关键字的值，插值搜索可以去往不同的位置。例如，如果关键字的值更接近最后一个元素，插值搜索可能会开始向末端搜索。
要找到要搜索的位置，它使用以下公式。

```
// The idea of formula is to return higher value of pos
// when element to be searched is closer to arr[hi]. And
// smaller value when closer to arr[lo]
pos = lo + [ (x-arr[lo])*(hi-lo) / (arr[hi]-arr[Lo]) ]

arr[] ==> Array where elements need to be searched
x     ==> Element to be searched
lo    ==> Starting index in arr[]
hi    ==> Ending index in arr[]
```

**pos 的公式可以推导如下。**

```
Let's assume that the elements of the array are linearly distributed. 

General equation of line : y = m*x + c.
y is the value in the array and x is its index.

Now putting value of lo,hi and x in the equation
arr[hi] = m*hi+c ----(1)
arr[lo] = m*lo+c ----(2)
x = m*pos + c     ----(3)

m = (arr[hi] - arr[lo] )/ (hi - lo)

subtracting eqxn (2) from (3)
x - arr[lo] = m * (pos - lo)
lo + (x - arr[lo])/m = pos
pos = lo + (x - arr[lo]) *(hi - lo)/(arr[hi] - arr[lo])
```

**算法**
除了上面的分区逻辑，其余的插值算法都是一样的。
**步骤 1:** 在一个循环中，使用探针位置公式计算“pos”的值。
**第二步:**如果匹配，返回该项目的索引，退出。
**步骤 3:** 如果项目小于 arr[pos]，计算左子阵列的探头位置。否则，在右子数组中计算相同的值。
**步骤 4:** 重复，直到找到匹配项或子阵列减少到零。
下面是算法的实现。

## C++

```
// C++ program to implement interpolation search
#include<bits/stdc++.h>
using namespace std;

// If x is present in arr[0..n-1], then returns
// index of it, else returns -1.
int interpolationSearch(int arr[], int n, int x)
{
    // Find indexes of two corners
    int lo = 0, hi = (n - 1);

    // Since array is sorted, an element present
    // in array must be in range defined by corner
    while (lo <= hi && x >= arr[lo] && x <= arr[hi])
    {
        if (lo == hi)
        {
            if (arr[lo] == x) return lo;
            return -1;
        }
        // Probing the position with keeping
        // uniform distribution in mind.
        int pos = lo + (((double)(hi - lo) /
            (arr[hi] - arr[lo])) * (x - arr[lo]));

        // Condition of target found
        if (arr[pos] == x)
            return pos;

        // If x is larger, x is in upper part
        if (arr[pos] < x)
            lo = pos + 1;

        // If x is smaller, x is in the lower part
        else
            hi = pos - 1;
    }
    return -1;
}

// Driver Code
int main()
{
    // Array of items on which search will
    // be conducted.
    int arr[] = {10, 12, 13, 16, 18, 19, 20, 21,
                 22, 23, 24, 33, 35, 42, 47};
    int n = sizeof(arr)/sizeof(arr[0]);

    int x = 18; // Element to be searched
    int index = interpolationSearch(arr, n, x);

    // If element was found
    if (index != -1)
        cout << "Element found at index " << index;
    else
        cout << "Element not found.";
    return 0;
}

// This code is contributed by Mukul Singh.
```

## C++

```
// C++ program to implement interpolation
// search with recursion
#include <bits/stdc++.h>
using namespace std;

// If x is present in arr[0..n-1], then returns
// index of it, else returns -1.
int interpolationSearch(int arr[], int lo, int hi, int x)
{
    int pos;

    // Since array is sorted, an element present
    // in array must be in range defined by corner
    if (lo <= hi && x >= arr[lo] && x <= arr[hi]) {

        // Probing the position with keeping
        // uniform distribution in mind.
        pos = lo
              + (((double)(hi - lo) / (arr[hi] - arr[lo]))
                 * (x - arr[lo]));

        // Condition of target found
        if (arr[pos] == x)
            return pos;

        // If x is larger, x is in right sub array
        if (arr[pos] < x)
            return interpolationSearch(arr, pos + 1, hi, x);

        // If x is smaller, x is in left sub array
        if (arr[pos] > x)
            return interpolationSearch(arr, lo, pos - 1, x);
    }
    return -1;
}

// Driver Code
int main()
{

    // Array of items on which search will
    // be conducted.
    int arr[] = { 10, 12, 13, 16, 18, 19, 20, 21,
                  22, 23, 24, 33, 35, 42, 47 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Element to be searched
    int x = 18;
    int index = interpolationSearch(arr, 0, n - 1, x);

    // If element was found
    if (index != -1)
        cout << "Element found at index " << index;
    else
        cout << "Element not found.";

    return 0;
}

// This code is contributed by equbalzeeshan
```

## C

```
// C program to implement interpolation search
// with recursion
#include <stdio.h>

// If x is present in arr[0..n-1], then returns
// index of it, else returns -1.
int interpolationSearch(int arr[], int lo, int hi, int x)
{
    int pos;
    // Since array is sorted, an element present
    // in array must be in range defined by corner
    if (lo <= hi && x >= arr[lo] && x <= arr[hi]) {
        // Probing the position with keeping
        // uniform distribution in mind.
        pos = lo
              + (((double)(hi - lo) / (arr[hi] - arr[lo]))
                 * (x - arr[lo]));

        // Condition of target found
        if (arr[pos] == x)
            return pos;

        // If x is larger, x is in right sub array
        if (arr[pos] < x)
            return interpolationSearch(arr, pos + 1, hi, x);

        // If x is smaller, x is in left sub array
        if (arr[pos] > x)
            return interpolationSearch(arr, lo, pos - 1, x);
    }
    return -1;
}

// Driver Code
int main()
{
    // Array of items on which search will
    // be conducted.
    int arr[] = { 10, 12, 13, 16, 18, 19, 20, 21,
                  22, 23, 24, 33, 35, 42, 47 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int x = 18; // Element to be searched
    int index = interpolationSearch(arr, 0, n - 1, x);

    // If element was found
    if (index != -1)
        printf("Element found at index %d", index);
    else
        printf("Element not found.");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement interpolation
// search with recursion
import java.util.*;

class GFG {

    // If x is present in arr[0..n-1], then returns
    // index of it, else returns -1.
    public static int interpolationSearch(int arr[], int lo,
                                          int hi, int x)
    {
        int pos;

        // Since array is sorted, an element
        // present in array must be in range
        // defined by corner
        if (lo <= hi && x >= arr[lo] && x <= arr[hi]) {

            // Probing the position with keeping
            // uniform distribution in mind.
            pos = lo
                  + (((hi - lo) / (arr[hi] - arr[lo]))
                     * (x - arr[lo]));

            // Condition of target found
            if (arr[pos] == x)
                return pos;

            // If x is larger, x is in right sub array
            if (arr[pos] < x)
                return interpolationSearch(arr, pos + 1, hi,
                                           x);

            // If x is smaller, x is in left sub array
            if (arr[pos] > x)
                return interpolationSearch(arr, lo, pos - 1,
                                           x);
        }
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Array of items on which search will
        // be conducted.
        int arr[] = { 10, 12, 13, 16, 18, 19, 20, 21,
                      22, 23, 24, 33, 35, 42, 47 };

        int n = arr.length;

        // Element to be searched
        int x = 18;
        int index = interpolationSearch(arr, 0, n - 1, x);

        // If element was found
        if (index != -1)
            System.out.println("Element found at index "
                               + index);
        else
            System.out.println("Element not found.");
    }
}

// This code is contributed by equbalzeeshan
```

## 计算机编程语言

```
# Python3 program to implement
# interpolation search
# with recursion

# If x is present in arr[0..n-1], then
# returns index of it, else returns -1.

def interpolationSearch(arr, lo, hi, x):

    # Since array is sorted, an element present
    # in array must be in range defined by corner
    if (lo <= hi and x >= arr[lo] and x <= arr[hi]):

        # Probing the position with keeping
        # uniform distribution in mind.
        pos = lo + ((hi - lo) // (arr[hi] - arr[lo]) *
                    (x - arr[lo]))

        # Condition of target found
        if arr[pos] == x:
            return pos

        # If x is larger, x is in right subarray
        if arr[pos] < x:
            return interpolationSearch(arr, pos + 1,
                                       hi, x)

        # If x is smaller, x is in left subarray
        if arr[pos] > x:
            return interpolationSearch(arr, lo,
                                       pos - 1, x)
    return -1

# Driver code

# Array of items in which
# search will be conducted
arr = [10, 12, 13, 16, 18, 19, 20,
       21, 22, 23, 24, 33, 35, 42, 47]
n = len(arr)

# Element to be searched
x = 18
index = interpolationSearch(arr, 0, n - 1, x)

if index != -1:
    print("Element found at index", index)
else:
    print("Element not found")

# This code is contributed by Hardik Jain
```

## C#

```
// C# program to implement
// interpolation search
using System;

class GFG{

// If x is present in
// arr[0..n-1], then
// returns index of it,
// else returns -1.
static int interpolationSearch(int []arr, int lo,
                               int hi, int x)
{
    int pos;

    // Since array is sorted, an element
    // present in array must be in range
    // defined by corner
    if (lo <= hi && x >= arr[lo] &&
                    x <= arr[hi])
    {

        // Probing the position
        // with keeping uniform
        // distribution in mind.
        pos = lo + (((hi - lo) /
                (arr[hi] - arr[lo])) *
                      (x - arr[lo]));

        // Condition of
        // target found
        if(arr[pos] == x)
        return pos;

        // If x is larger, x is in right sub array
        if(arr[pos] < x)
            return interpolationSearch(arr, pos + 1,
                                       hi, x);

        // If x is smaller, x is in left sub array
        if(arr[pos] > x)
            return interpolationSearch(arr, lo,
                                       pos - 1, x);
    }
    return -1;
}

// Driver Code
public static void Main()
{

    // Array of items on which search will
    // be conducted.
    int []arr = new int[]{ 10, 12, 13, 16, 18,
                           19, 20, 21, 22, 23,
                           24, 33, 35, 42, 47 };

    // Element to be searched                      
    int x = 18;
    int n = arr.Length;
    int index = interpolationSearch(arr, 0, n - 1, x);

    // If element was found
    if (index != -1)
        Console.WriteLine("Element found at index " +
                           index);
    else
        Console.WriteLine("Element not found.");
}
}

// This code is contributed by equbalzeeshan
```

## java 描述语言

```
<script>
// Javascript program to implement Interpolation Search

// If x is present in arr[0..n-1], then returns
// index of it, else returns -1.

function interpolationSearch(arr, lo, hi, x){
  let pos;

  // Since array is sorted, an element present
  // in array must be in range defined by corner

  if (lo <= hi && x >= arr[lo] && x <= arr[hi]) {

    // Probing the position with keeping
    // uniform distribution in mind.
    pos = lo + Math.floor(((hi - lo) / (arr[hi] - arr[lo])) * (x - arr[lo]));;

    // Condition of target found
        if (arr[pos] == x){
          return pos;
        }

        // If x is larger, x is in right sub array
        if (arr[pos] < x){
          return interpolationSearch(arr, pos + 1, hi, x);
        }

        // If x is smaller, x is in left sub array
        if (arr[pos] > x){
          return interpolationSearch(arr, lo, pos - 1, x);
        }
    }
    return -1;
}

// Driver Code
let arr = [10, 12, 13, 16, 18, 19, 20, 21,
           22, 23, 24, 33, 35, 42, 47];

let n = arr.length;

// Element to be searched
let x = 18
let index = interpolationSearch(arr, 0, n - 1, x);

// If element was found
if (index != -1){
   document.write(`Element found at index ${index}`)
}else{
   document.write("Element not found");
}

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output**

```
Element found at index 4
```

本文由 **Aayu sachdev** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。