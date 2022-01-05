# 检查排序后的数组是否可以被分成两个和为 k 的对

> 原文:[https://www . geesforgeks . org/check-if-a-sorted-array-can-divide-in-pain-then-sum-k/](https://www.geeksforgeeks.org/check-if-a-sorted-array-can-be-divided-in-pairs-whose-sum-is-k/)

给定一个排序的整数数组和一个数字 k，写一个函数，如果给定的数组可以分成对，那么每个对的和就是 k。
预期的时间复杂度 O(n)和额外的空间 O(1)。这个问题是下面问题的变体，但是有一个不同的有趣的解决方案，只需要 O(1)个空间。
[检查一个数组是否可以分成其和可以被 k 整除的对](https://www.geeksforgeeks.org/check-if-an-array-can-be-divided-into-pairs-whose-sum-is-divisible-by-k/)

示例:

```
Input: arr[] = {1, 3, 3, 5}, k = 6
Output: True
We can divide array into (1, 5) and (3, 3).
Sum of both of these pairs is 6.

Input: arr[] = {2, 5, 5, 5, 5, 8}, k = 10
Output: True
We can divide array into (2, 8), (5, 5) and 
(5, 5). Sum of all these pairs is 10.
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**

一个简单的解决方案是迭代每个元素 arr[i]。查找是否有另一个尚未访问的值为(k–arr[I])的元素。如果没有这样的元素，则返回 false。如果找到一对，则将两个元素都标记为已访问。该解决方案的时间复杂度为 0(n)<sup>2</sup>，需要 0(n)个额外空间。
更好的解决方案是使用哈希。这篇文章给出的解决方案可以很容易地修改为工作。这个解决方案的时间复杂度是 O9n)，但是它需要额外的哈希表空间。
一个**高效的解决方案**是使用**在中间相遇算法**中讨论的方法 1 [在这里](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)。

```
1) Initialize two index variables
  (a) Initialize first to the leftmost index: l = 0
  (b) Initialize second  the rightmost index:  r = n-1
2) Loop while l < r.
  (a) If (A[l] + A[r] != k)  then return false
  (b) Else r--, l++
```

下面是上述算法的实现。

## C++

```
// A C++ program to check if arr[0..n-1] can be divided
// in pairs such that every pair has sum k.
#include <bits/stdc++.h>
using namespace std;

// Returns true if arr[0..n-1] can be divided into pairs
// with sum equal to k.
bool canPairsSorted(int arr[], int n, int k)
{
   // An odd length array cannot be divided into pairs
   if (n & 1)
       return false;  

   // Traverse from both sides of array
   int l = 0, r = n-1;
   while (l < r)
   {
       // If array can be divided, then sum of current
       // elements must be sum
       if (arr[l] + arr[r] != k)
          return false;

       // Move index variables
       l++; r--;
   }

   return true;
}

/* Driver program to test above function */
int main()
{
    int arr[] = {1, 2, 3, 3, 3, 3, 4, 5};
    int n = 6;
    int n = sizeof(arr)/sizeof(arr[0]);
    canPairs(arr, n, k)? cout << "True": cout << "False";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if arr[0..n-1] can be divided
// in pairs such that every pair has sum k.

class GFG {

// Returns true if arr[0..n-1] can be divided into pairs
// with sum equal to k.
    static boolean canPairs(int arr[], int n, int k) {
// An odd length array cannot be divided into pairs
        if (n == 1) {
            return false;
        }

// Traverse from both sides of array
        int l = 0, r = n - 1;
        while (l < r) {
            // If array can be divided, then sum of current
            // elements must be sum
            if (arr[l] + arr[r] != k) {
                return false;
            }

            // Move index variables
            l++;
            r--;
        }

        return true;
    }

// Drivers code
    public static void main(String[] args) {
        int arr[] = {1, 2, 3, 3, 3, 3, 4, 5};
        int k = 6;
        int n = arr.length;
        if (canPairs(arr, n, k)) {
            System.out.println("True");
        } else {
            System.out.println("False");
        }
    }
}
//This code contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A Python3 program to check if arr[0..n-1] can be
# divided in pairs such that every pair has sum k.

# Returns true if arr[0..n-1] can be divided
# into pairs with sum equal to k.
def canPairsSorted(arr, n, k):

    # An odd length array cannot
    # be divided into pairs
    if (n & 1):
        return False;

    # Traverse from both sides of array
    l = 0; r = n - 1;
    while (l < r):

        # If array can be divided, then
        # sum of current elements must be sum
        if (arr[l] + arr[r] != k):
            return False;

        # Move index variables
        l = l + 1; r = r - 1;

    return True

# Driver Code
arr = [1, 2, 3, 3, 3, 3, 4, 5]
k = 6
n = len(arr)
if(canPairsSorted(arr, n, k)):
    print("True")
else:
    print("False");

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to check if arr[0..n-1]
// can be divided in pairs such that
// every pair has sum k.
using System;

class GFG
{

// Returns true if arr[0..n-1]
// can be divided into pairs
// with sum equal to k.
static bool canPairs(int []arr, int n, int k)
{
    // An odd length array cannot
    // be divided into pairs
    if (n == 1)
    {
        return false;
    }

    // Traverse from both sides of array
    int l = 0, r = n - 1;
    while (l < r)
    {
        // If array can be divided,
        // then sum of current
        // elements must be sum
        if (arr[l] + arr[r] != k)
        {
            return false;
        }

        // Move index variables
        l++;
        r--;
    }

    return true;
}

// Driver code
public static void Main()
{
    int []arr = {1, 2, 3, 3, 3, 3, 4, 5};
    int k = 6;
    int n = arr.Length;
    if (canPairs(arr, n, k))
    {
        Console.Write("True");
    }
    else
    {
        Console.Write("False");
    }
}
}

// This code is contributed by PrinciRaj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to check if arr[0..n-1]
// can be divided in pairs such that
// every pair has sum k.

// Returns true if arr[0..n-1] can be
// divided into pairs with sum equal to k.
function canPairs(&$arr, $n, $k)
{
    // An odd length array cannot be
    // divided into pairs
    if ($n & 1)
        return false;

    // Traverse from both sides of array
    $l = 0;
    $r = $n - 1;
    while ($l < $r)
    {
        // If array can be divided, then sum
        // of current elements must be sum
        if ($arr[$l] + $arr[$r] != $k)
            return false;

        // Move index variables
        $l++;
        $r--;
    }

    return true;
}

// Driver Code
$arr = array(1, 2, 3, 3, 3, 3, 4, 5);
$n = 6;
$k = 6;
$n = sizeof($arr);
if (canPairs($arr, $n, $k))
    echo ("True");
else
    echo ("False");

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Java Script program to check if arr[0..n-1] can be divided
// in pairs such that every pair has sum k.

// Returns true if arr[0..n-1] can be divided into pairs
// with sum equal to k.
    function canPairs(arr,n,k) {
// An odd length array cannot be divided into pairs
        if (n == 1) {
            return false;
        }

// Traverse from both sides of array
        let l = 0, r = n - 1;
        while (l < r)
        {

            // If array can be divided, then sum of current
            // elements must be sum
            if (arr[l] + arr[r] != k) {
                return false;
            }

            // Move index variables
            l++;
            r--;
        }

        return true;
    }

// Drivers code
        let arr = [1, 2, 3, 3, 3, 3, 4, 5];
        let k = 6;
        let n = arr.length;
        if (canPairs(arr, n, k)) {
            document.write("True");
        } else {
            document.write("False");
        }

// This code is contributed by Gottumukkala Sravan Kumar (171fa07058)
</script>
```

**输出:**

```
 True 
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由**普里扬卡**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。