# 为什么二分搜索法优于三元搜索？

> 原文:[https://www . geesforgeks . org/binary-search-preferred-三元-search/](https://www.geeksforgeeks.org/binary-search-preferred-ternary-search/)

下面是一个简单的 C++递归**二分搜索法**函数，取自这里的。

## C

```
// A recursive binary search function. It returns location of x in
// given array arr[l..r] is present, otherwise -1
int binarySearch(int arr[], int l, int r, int x)
{
   if (r >= l)
   {
        int mid = l + (r - l)/2;

        // If the element is present at the middle itself
        if (arr[mid] == x)  return mid;

        // If element is smaller than mid, then it can only be present
        // in left subarray
        if (arr[mid] > x) return binarySearch(arr, l, mid-1, x);

        // Else the element can only be present in right subarray
        return binarySearch(arr, mid+1, r, x);
   }

   // We reach here when element is not present in array
   return -1;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A recursive binary search function. It returns location of x in
// given array arr[l..r] is present, otherwise -1
static int binarySearch(int arr[], int l, int r, int x)
{
   if (r >= l)
   {
        int mid = l + (r - l)/2;

        // If the element is present at the middle itself
        if (arr[mid] == x)  return mid;

        // If element is smaller than mid, then it can only be present
        // in left subarray
        if (arr[mid] > x) return binarySearch(arr, l, mid-1, x);

        // Else the element can only be present in right subarray
        return binarySearch(arr, mid+1, r, x);
   }

   // We reach here when element is not present in array
   return -1;
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# A recursive binary search function. It returns location of x in
# given array arr[l..r] is present, otherwise -1
def binarySearch(arr, l, r, x):
   if (r >= l):
        mid = l + (r - l)/2;

   # If the element is present at the middle itself
   if (arr[mid] == x):
        return mid;

   # If element is smaller than mid, then it can only be present
   # in left subarray
    if (arr[mid] > x):
    return binarySearch(arr, l, mid-1, x);

    # Else the element can only be present in right subarray
    return binarySearch(arr, mid+1, r, x);

 # We reach here when element is not present in array
   return -1;

# This code is contributed by umadevi9616
```

## C#

```
// A recursive binary search function. It returns location of x in
// given array arr[l..r] is present, otherwise -1
static int binarySearch(int []arr, int l, int r, int x)
{
   if (r >= l)
   {
        int mid = l + (r - l)/2;

        // If the element is present at the middle itself
        if (arr[mid] == x)  return mid;

        // If element is smaller than mid, then it can only be present
        // in left subarray
        if (arr[mid] > x) return binarySearch(arr, l, mid-1, x);

        // Else the element can only be present in right subarray
        return binarySearch(arr, mid+1, r, x);
   }

   // We reach here when element is not present in array
   return -1;
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// A recursive binary search function. It returns location of x in
// given array arr[l..r] is present, otherwise -1
function binarySearch(arr , l , r , x)
{
   if (r >= l)
   {
        var mid = l + (r - l)/2;

        // If the element is present at the middle itself
        if (arr[mid] == x)  return mid;

        // If element is smaller than mid, then it can only be present
        // in left subarray
        if (arr[mid] > x) return binarySearch(arr, l, mid-1, x);

        // Else the element can only be present in right subarray
        return binarySearch(arr, mid+1, r, x);
   }

   // We reach here when element is not present in array
   return -1;
}

// This code is contributed by gauravrajput1
</script>
```

下面是一个简单的递归**三元搜索**函数:

## C

```
// A recursive ternary search function. It returns location of x in
// given array arr[l..r] is present, otherwise -1
int ternarySearch(int arr[], int l, int r, int x)
{
   if (r >= l)
   {
        int mid1 = l + (r - l)/3;
        int mid2 = mid1 + (r - l)/3;

        // If x is present at the mid1
        if (arr[mid1] == x)  return mid1;

        // If x is present at the mid2
        if (arr[mid2] == x)  return mid2;

        // If x is present in left one-third
        if (arr[mid1] > x) return ternarySearch(arr, l, mid1-1, x);

        // If x is present in right one-third
        if (arr[mid2] < x) return ternarySearch(arr, mid2+1, r, x);

        // If x is present in middle one-third
        return ternarySearch(arr, mid1+1, mid2-1, x);
   }
   // We reach here when element is not present in array
   return -1;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG
{
public static void main (String[] args)
{

// A recursive ternary search function.
// It returns location of x in given array
// arr[l..r] is present, otherwise -1
static int ternarySearch(int arr[], int l,
                         int r, int x)
{
   if (r >= l)
   {
        int mid1 = l + (r - l) / 3;
        int mid2 = mid1 + (r - l) / 3;

        // If x is present at the mid1
        if (arr[mid1] == x)  return mid1;

        // If x is present at the mid2
        if (arr[mid2] == x)  return mid2;

        // If x is present in left one-third
        if (arr[mid1] > x)
            return ternarySearch(arr, l, mid1 - 1, x);

        // If x is present in right one-third
        if (arr[mid2] < x)
            return ternarySearch(arr, mid2 + 1, r, x);

        // If x is present in middle one-third
        return ternarySearch(arr, mid1 + 1,
                                  mid2 - 1, x);
   }

   // We reach here when element is
   // not present in array
   return -1;
}
}
```

## 蟒蛇 3

```
# A recursive ternary search function. It returns location of x in
# given array arr[l..r] is present, otherwise -1
def ternarySearch(arr, l, r, x):
    if (r >= l):
        mid1 = l + (r - l)//3
        mid2 = mid1 + (r - l)//3

        # If x is present at the mid1
        if arr[mid1] == x:
            return mid1

        # If x is present at the mid2
        if arr[mid2] == x:
            return mid2

        # If x is present in left one-third
        if arr[mid1] > x:
            return ternarySearch(arr, l, mid1-1, x)

        # If x is present in right one-third
        if arr[mid2] < x:
            return ternarySearch(arr, mid2+1, r, x)

        # If x is present in middle one-third
        return ternarySearch(arr, mid1+1, mid2-1, x)

    # We reach here when element is not present in array
    return -1

# This code is contributed by ankush_953

```

## C#

```

// A recursive ternary search function.
// It returns location of x in given array
// arr[l..r] is present, otherwise -1
static int ternarySearch(int []arr, int l,
                         int r, int x)
{
   if (r >= l)
   {
        int mid1 = l + (r - l) / 3;
        int mid2 = mid1 + (r - l) / 3;

        // If x is present at the mid1
        if (arr[mid1] == x)  return mid1;

        // If x is present at the mid2
        if (arr[mid2] == x)  return mid2;

        // If x is present in left one-third
        if (arr[mid1] > x)
            return ternarySearch(arr, l, mid1 - 1, x);

        // If x is present in right one-third
        if (arr[mid2] < x)
            return ternarySearch(arr, mid2 + 1, r, x);

        // If x is present in middle one-third
        return ternarySearch(arr, mid1 + 1,
                                  mid2 - 1, x);
   }

   // We reach here when element is
   // not present in array
   return -1;
}

// This code is contributed by gauravrajput1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A recursive ternary search function.
// It returns location of x in
// given array arr[l..r] is
// present, otherwise -1
function ternarySearch($arr, $l,
                       $r, $x)
{
    if ($r >= $l)
    {
        $mid1 = $l + ($r - $l) / 3;
        $mid2 = $mid1 + ($r - l) / 3;

        // If x is present at the mid1
        if ($arr[mid1] == $x)
            return $mid1;

        // If x is present
        // at the mid2
        if ($arr[$mid2] == $x)
            return $mid2;

        // If x is present in
        // left one-third
        if ($arr[$mid1] > $x)
            return ternarySearch($arr, $l,
                                 $mid1 - 1, $x);

        // If x is present in right one-third
        if ($arr[$mid2] < $x)
            return ternarySearch($arr, $mid2 + 1,
                                         $r, $x);

        // If x is present in
        // middle one-third
        return ternarySearch($arr, $mid1 + 1,
                             $mid2 - 1, $x);
}

// We reach here when element
// is not present in array
return -1;
}

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>

    // A recursive ternary search function.
    // It returns location of x in given array
    // arr[l..r] is present, otherwise -1
    function ternarySearch(arr , l , r , x) {
        if (r >= l) {
            var mid1 = l + parseInt((r - l) / 3);
            var mid2 = mid1 + parseInt((r - l) / 3);

            // If x is present at the mid1
            if (arr[mid1] == x)
                return mid1;

            // If x is present at the mid2
            if (arr[mid2] == x)
                return mid2;

            // If x is present in left one-third
            if (arr[mid1] > x)
                return ternarySearch(arr, l, mid1 - 1, x);

            // If x is present in right one-third
            if (arr[mid2] < x)
                return ternarySearch(arr, mid2 + 1, r, x);

            // If x is present in middle one-third
            return ternarySearch(arr, mid1 + 1, mid2 - 1, x);
        }

        // We reach here when element is
        // not present in array
        return -1;

// This code is contributed by gauravrajput1
</script>
```

**在最坏的情况下，以上两者哪个做的比较少？**
从第一眼看上去，三元搜索进行比较的次数似乎较少，因为它进行 Log <sub>3</sub> n 次递归调用，但二分搜索法进行 Log <sub>2</sub> n 次递归调用。让我们仔细看看。
以下是二分搜索法最坏情况下计数比较的递归公式。

```
   T(n) = T(n/2) + 2,  T(1) = 1
```

以下是三值搜索最坏情况下计数比较的递归公式。

```
   T(n) = T(n/3) + 4, T(1) = 1
```

在二分搜索法，最坏的情况下有 2 个对数 <sub>2 个</sub> n + 1 的比较。在三元搜索中，最坏情况下有 4Log <sub>3</sub> n + 1 个比较。

```
Time Complexity for Binary search = 2clog2n + O(1)
Time Complexity for Ternary search = 4clog3n + O(1)
```

因此，三进制和二进制搜索的比较归结为表达式 2Log <sub>3</sub> n 和 Log <sub>2</sub> n 的比较。2Log <sub>3</sub> n 的值可以写成(2 / Log <sub>2</sub> 3) * Log <sub>2</sub> n。由于(2 / Log <sub>2</sub> 3)的值不止一个，所以在最坏的情况下，三进制搜索比二分搜索法做更多的比较。
**练习:**
为什么合并排序将输入数组分成两半，为什么不分成三个或更多部分？
本文由**安摩尔**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息