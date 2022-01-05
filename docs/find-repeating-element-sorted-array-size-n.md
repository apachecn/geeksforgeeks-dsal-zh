# 在大小为 n 的排序数组中找到唯一的重复元素

> 原文:[https://www . geesforgeks . org/find-repeating-element-sorted-array-size-n/](https://www.geeksforgeeks.org/find-repeating-element-sorted-array-size-n/)

给定包含 1 到 n-1 范围内元素的 n 个元素的排序数组，即一个元素出现两次，任务是找到数组中的重复元素。
**例:**

```
Input :  arr[] = { 1, 2 , 3 , 4 , 4}
Output :  4

Input :  arr[] = { 1 , 1 , 2 , 3 , 4}
Output :  1
```

一种**天真的方法**是扫描整个数组，检查一个元素是否出现两次，然后返回。这种方法需要 O(n)个时间。
一个**高效**的方法就是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。

观察:如果元素“X”是重复的，那么它必须在数组的索引“X”处。所以这个问题简化为寻找任何一个值与其索引相同的元素。

## C++

```
// C++ program to find the only repeating element in an
// array of size n and elements from range 1 to n-1.
#include <bits/stdc++.h>
using namespace std;

// Returns index of second appearance of a repeating element
// The function assumes that array elements are in range from
// 1 to n-1.
int FindRepeatingElement(int arr[], int size){
    int lo = 0;
    int hi = size - 1;
    int mid;

    while(lo <= hi){
        mid = (lo+hi)/2;

        if(arr[mid] <= mid){
            hi = mid-1;
        }
        else{
            lo = mid + 1;
        }
    }

    return lo;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    int index = findRepeatingElement(arr, n);
    if (index != -1)
        cout << arr[index];
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the only repeating element in an
// array of size n and elements from range 1 to n-1.

class Test
{
    // Returns index of second appearance of a repeating element
    // The function assumes that array elements are in range from
    // 1 to n-1.
    static int findRepeatingElement(int arr[], int low, int high)
    {
        // low = 0 , high = n-1;
        if (low > high)
            return -1;

        int mid = (low + high) / 2;

        // Check if the mid element is the repeating one
        if (arr[mid] != mid + 1)
        {
            if (mid > 0 && arr[mid]==arr[mid-1])
                return mid;

            // If mid element is not at its position that means
            // the repeated element is in left
            return  findRepeatingElement(arr, low, mid-1);
        }

        // If mid is at proper position then repeated one is in
        // right.
        return findRepeatingElement(arr, mid+1, high);
    }

    // Driver method
    public static void main(String[] args)
    {
        int  arr[] = {1, 2, 3, 3, 4, 5};
        int index = findRepeatingElement(arr, 0, arr.length-1);
        if (index != -1)
            System.out.println(arr[index]);
    }
}
```

## 计算机编程语言

```
# Python program to find the only repeating element in an
# array of size n and elements from range 1 to n-1

# Returns index of second appearance of a repeating element
# The function assumes that array elements are in range from
# 1 to n-1.
def findRepeatingElement(arr, low, high):

    # low = 0 , high = n-1
    if low > high:
        return -1

    mid = (low + high) / 2

    # Check if the mid element is the repeating one
    if (arr[mid] != mid + 1):

        if (mid > 0 and arr[mid]==arr[mid-1]):
            return mid

        # If mid element is not at its position that means
        # the repeated element is in left
        return  findRepeatingElement(arr, low, mid-1)

    # If mid is at proper position then repeated one is in
    # right.
    return findRepeatingElement(arr, mid+1, high)

# Driver code
arr = [1, 2, 3, 3, 4, 5]
n = len(arr)
index = findRepeatingElement(arr, 0, n-1)
if (index is not -1):
    print arr[index]

#This code is contributed by Afzal Ansari
```

## C#

```
// C# program to find the only repeating
// element in an array of size n and
// elements from range 1 to n-1.
using System;

class Test
{
    // Returns index of second appearance of a
    // repeating element. The function assumes that
    // array elements are in range from 1 to n-1.
    static int findRepeatingElement(int []arr, int low,
                                              int high)
    {
        // low = 0 , high = n-1;
        if (low > high)
            return -1;

        int mid = (low + high) / 2;

        // Check if the mid element
        // is the repeating one
        if (arr[mid] != mid + 1)
        {
            if (mid > 0 && arr[mid]==arr[mid-1])
                return mid;

            // If mid element is not at its position
            // that means the repeated element is in left
            return findRepeatingElement(arr, low, mid-1);
        }

        // If mid is at proper position
        // then repeated one is in right.
        return findRepeatingElement(arr, mid+1, high);
    }

    // Driver method
    public static void Main()
    {
        int []arr = {1, 2, 3, 3, 4, 5};
        int index = findRepeatingElement(arr, 0, arr.Length-1);
        if (index != -1)
        Console.Write(arr[index]);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the only
// repeating element in an array
// of size n and elements from
// range 1 to n-1.

// Returns index of second
// appearance of a repeating
// element. The function assumes
// that array elements are in
// range from 1 to n-1.
function findRepeatingElement($arr,
                              $low,
                              $high)
{
    // low = 0 , high = n-1;
    if ($low > $high)
        return -1;

    $mid = floor(($low + $high) / 2);

    // Check if the mid element
    // is the repeating one
    if ($arr[$mid] != $mid + 1)
    {
        if ($mid > 0 && $arr[$mid] ==
                        $arr[$mid - 1])
            return $mid;

        // If mid element is not at
        // its position that means
        // the repeated element is in left
        return findRepeatingElement($arr, $low,
                                    $mid - 1);
    }

    // If mid is at proper position
    // then repeated one is in right.
    return findRepeatingElement($arr, $mid + 1,
                                        $high);
}

// Driver code
$arr = array(1, 2, 3, 3, 4, 5);
$n = sizeof($arr);
$index = findRepeatingElement($arr, 0,
                              $n - 1);
if ($index != -1)
echo $arr[$index];

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>
      // JavaScript program to find the only repeating element in an
      // array of size n and elements from range 1 to n-1.

      // Returns index of second appearance of a repeating element
      // The function assumes that array elements are in range from
      // 1 to n-1.
      function findRepeatingElement(arr, low, high)
      {

        // low = 0 , high = n-1;
        if (low > high) return -1;

        var mid = parseInt((low + high) / 2);

        // Check if the mid element is the repeating one
        if (arr[mid] != mid + 1)
        {
          if (mid > 0 && arr[mid] == arr[mid - 1]) return mid;

          // If mid element is not at its position that means
          // the repeated element is in left
          return findRepeatingElement(arr, low, mid - 1);
        }

        // If mid is at proper position then repeated one is in
        // right.
        return findRepeatingElement(arr, mid + 1, high);
      }

      // Driver code
      var arr = [1, 2, 3, 3, 4, 5];
      var n = arr.length;
      var index = findRepeatingElement(arr, 0, n - 1);
      if (index != -1) document.write(arr[index]);

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
3
```

**时间复杂度:** O(log n)
本文由[**Sahil Chhabra(KILLER)**](https://www.facebook.com/sahil.chhabra.965)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。