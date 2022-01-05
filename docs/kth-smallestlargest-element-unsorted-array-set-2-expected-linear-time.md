# 未排序数组中第 K 个最小/最大元素|集合 2(预期线性时间)

> 原文:[https://www . geesforgeks . org/kth-small estimal-element-unsorted-array-set-2-expect-linear-time/](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)

我们建议阅读以下文章作为这篇文章的先决条件。

[未排序数组中第 K 个最小/最大元素|集合 1](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)

给定一个数组和一个数字 k，其中 k 小于数组的大小，我们需要找到给定数组中的第 k 个最小元素。假设所有的数组元素都是不同的。

**示例:**

```
Input: arr[] = {7, 10, 4, 3, 20, 15}
       k = 3
Output: 7

Input: arr[] = {7, 10, 4, 3, 20, 15}
       k = 4
Output: 10
```

我们在这里讨论了三种不同的解决方案。

在这篇文章中，讨论了方法 5，这主要是在[之前的](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)文章中讨论的方法 4(快速选择)的扩展。这个想法是随机选择一个枢轴元素。为了实现随机划分，我们使用随机函数 [rand()](http://www.cplusplus.com/reference/cstdlib/rand/) 在 l 和 r 之间生成索引，用最后一个元素交换随机生成索引处的元素，最后调用以最后一个元素为轴心的标准划分过程。

以下是上述随机快速选择的实现。

## C++

```
// C++ implementation of randomized quickSelect
#include<iostream>
#include<climits>
#include<cstdlib>
using namespace std;

int randomPartition(int arr[], int l, int r);

// This function returns k'th smallest element in arr[l..r] using
// QuickSort based method. ASSUMPTION: ELEMENTS IN ARR[] ARE DISTINCT
int kthSmallest(int arr[], int l, int r, int k)
{
    // If k is smaller than number of elements in array
    if (k > 0 && k <= r - l + 1)
    {
        // Partition the array around a random element and
        // get position of pivot element in sorted array
        int pos = randomPartition(arr, l, r);

        // If position is same as k
        if (pos-l == k-1)
            return arr[pos];
        if (pos-l > k-1) // If position is more, recur for left subarray
            return kthSmallest(arr, l, pos-1, k);

        // Else recur for right subarray
        return kthSmallest(arr, pos+1, r, k-pos+l-1);
    }

    // If k is more than the number of elements in the array
    return INT_MAX;
}

void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Standard partition process of QuickSort(). It considers the last
// element as pivot and moves all smaller element to left of it and
// greater elements to right. This function is used by randomPartition()
int partition(int arr[], int l, int r)
{
    int x = arr[r], i = l;
    for (int j = l; j <= r - 1; j++)
    {
        if (arr[j] <= x)
        {
            swap(&arr[i], &arr[j]);
            i++;
        }
    }
    swap(&arr[i], &arr[r]);
    return i;
}

// Picks a random pivot element between l and r and partitions
// arr[l..r] around the randomly picked element using partition()
int randomPartition(int arr[], int l, int r)
{
    int n = r-l+1;
    int pivot = rand() % n;
    swap(&arr[l + pivot], &arr[r]);
    return partition(arr, l, r);
}

// Driver program to test above methods
int main()
{
    int arr[] = {12, 3, 5, 7, 4, 19, 26};
    int n = sizeof(arr)/sizeof(arr[0]), k = 3;
    cout << "K'th smallest element is " << kthSmallest(arr, 0, n-1, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k'th smallest element in expected
// linear time
class KthSmallst
{
    // This function returns k'th smallest element in arr[l..r]
    // using QuickSort based method. ASSUMPTION: ALL ELEMENTS
    // IN ARR[] ARE DISTINCT
    int kthSmallest(int arr[], int l, int r, int k)
    {
        // If k is smaller than number of elements in array
        if (k > 0 && k <= r - l + 1)
        {
            // Partition the array around a random element and
            // get position of pivot element in sorted array
            int pos = randomPartition(arr, l, r);

            // If position is same as k
            if (pos-l == k-1)
                return arr[pos];

            // If position is more, recur for left subarray
            if (pos-l > k-1)
                return kthSmallest(arr, l, pos-1, k);

            // Else recur for right subarray
            return kthSmallest(arr, pos+1, r, k-pos+l-1);
        }

        // If k is more than number of elements in array
        return Integer.MAX_VALUE;
    }

    // Utility method to swap arr[i] and arr[j]
    void swap(int arr[], int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Standard partition process of QuickSort(). It considers
    // the last element as pivot and moves all smaller element
    // to left of it and greater elements to right. This function
    // is used by randomPartition()
    int partition(int arr[], int l, int r)
    {
        int x = arr[r], i = l;
        for (int j = l; j <= r - 1; j++)
        {
            if (arr[j] <= x)
            {
                swap(arr, i, j);
                i++;
            }
        }
        swap(arr, i, r);
        return i;
    }

    // Picks a random pivot element between l and r and
    // partitions arr[l..r] arount the randomly picked
    // element using partition()
    int randomPartition(int arr[], int l, int r)
    {
        int n = r-l+1;
        int pivot = (int)(Math.random()) * (n-1);
        swap(arr, l + pivot, r);
        return partition(arr, l, r);
    }

    // Driver method to test above
    public static void main(String args[])
    {
        KthSmallst ob = new KthSmallst();
        int arr[] = {12, 3, 5, 7, 4, 19, 26};
        int n = arr.length,k = 3;
        System.out.println("K'th smallest element is "+
                        ob.kthSmallest(arr, 0, n-1, k));
    }
}
/*This code is contributed by Rajat Mishra*/
```

## 蟒蛇 3

```
# Python3 implementation of randomized
# quickSelect
import random

# This function returns k'th smallest
# element in arr[l..r] using QuickSort
# based method. ASSUMPTION: ELEMENTS
# IN ARR[] ARE DISTINCT
def kthSmallest(arr, l, r, k):

    # If k is smaller than number of
    # elements in array
    if (k > 0 and k <= r - l + 1):

        # Partition the array around a random
        # element and get position of pivot
        # element in sorted array
        pos = randomPartition(arr, l, r)

        # If position is same as k
        if (pos - l == k - 1):
            return arr[pos]
        if (pos - l > k - 1): # If position is more,
                            # recur for left subarray
            return kthSmallest(arr, l, pos - 1, k)

        # Else recur for right subarray
        return kthSmallest(arr, pos + 1, r,
                        k - pos + l - 1)

    # If k is more than the number of
    # elements in the array
    return 999999999999

def swap(arr, a, b):
    temp = arr[a]
    arr[a] = arr[b]
    arr[b] = temp

# Standard partition process of QuickSort().
# It considers the last element as pivot and
# moves all smaller element to left of it and
# greater elements to right. This function
# is used by randomPartition()
def partition(arr, l, r):
    x = arr[r]
    i = l
    for j in range(l, r):
        if (arr[j] <= x):
            swap(arr, i, j)
            i += 1
    swap(arr, i, r)
    return i

# Picks a random pivot element between l and r
# and partitions arr[l..r] around the randomly
# picked element using partition()
def randomPartition(arr, l, r):
    n = r - l + 1
    pivot = int(random.random() * n)
    swap(arr, l + pivot, r)
    return partition(arr, l, r)

# Driver Code
if __name__ == '__main__':

    arr = [12, 3, 5, 7, 4, 19, 26]
    n = len(arr)
    k = 3
    print("K'th smallest element is",
        kthSmallest(arr, 0, n - 1, k))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find k'th smallest
// element in expected linear time
using System;

class GFG
{
// This function returns k'th smallest
// element in arr[l..r] using QuickSort
// based method. ASSUMPTION: ALL ELEMENTS
// IN ARR[] ARE DISTINCT
int kthSmallest(int []arr, int l, int r, int k)
{
    // If k is smaller than number
    // of elements in array
    if (k > 0 && k <= r - l + 1)
    {
        // Partition the array around a
        // random element and get position
        // of pivot element in sorted array
        int pos = randomPartition(arr, l, r);

        // If position is same as k
        if (pos-l == k - 1)
            return arr[pos];

        // If position is more, recur
        // for left subarray
        if (pos - l > k - 1)
            return kthSmallest(arr, l, pos - 1, k);

        // Else recur for right subarray
        return kthSmallest(arr, pos + 1, r,
                        k - pos + l - 1);
    }

    // If k is more than number of
    // elements in array
    return int.MaxValue;
}

// Utility method to swap arr[i] and arr[j]
void swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// Standard partition process of QuickSort().
// It considers the last element as pivot and
// moves all smaller element to left of it
// and greater elements to right. This function
// is used by randomPartition()
int partition(int []arr, int l, int r)
{
    int x = arr[r], i = l;
    for (int j = l; j <= r - 1; j++)
    {
        if (arr[j] <= x)
        {
            swap(arr, i, j);
            i++;
        }
    }
    swap(arr, i, r);
    return i;
}

// Picks a random pivot element between
// l and r and partitions arr[l..r]
// around the randomly picked element
// using partition()
int randomPartition(int []arr, int l, int r)
{
    int n = r - l + 1;
    Random rnd = new Random();
    int rand = rnd.Next(0, 1);
    int pivot = (int)(rand * (n - 1));
    swap(arr, l + pivot, r);
    return partition(arr, l, r);
}

// Driver Code
public static void Main()
{
    GFG ob = new GFG();
    int []arr = {12, 3, 5, 7, 4, 19, 26};
    int n = arr.Length,k = 3;
    Console.Write("K'th smallest element is "+
            ob.kthSmallest(arr, 0, n - 1, k));
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to find k'th smallest
// element in expected linear time

// This function returns k'th smallest
// element in arr[l..r] using QuickSort based method.
// ASSUMPTION: ELEMENTS IN ARR[] ARE DISTINCT
function kthSmallest($arr, $l, $r, $k)
{
    // If k is smaller than number of elements in array
    if ($k > 0 && $k <= $r - $l + 1)
    {
        // Partition the array around a random element and
        // get position of pivot element in sorted array
        $pos = randomPartition($arr, $l, $r);

        // If position is same as k
        if ($pos-$l == $k-1)
            return $arr[$pos];

        // If position is more, recur for left subarray
        if ($pos-$l > $k-1)
            return kthSmallest($arr, $l, $pos-1, $k);

        // Else recur for right subarray
        return kthSmallest($arr, $pos+1, $r,
                            $k-$pos+$l-1);
    }

    // If k is more than the number of elements in the array
    return PHP_INT_MAX;
}

function swap($a, $b)
{
    $temp = $a;
    $a = $b;
    $b = $temp;
}

// Standard partition process of QuickSort().
// It considers the last element as pivot
// and moves all smaller element to left
// of it and greater elements to right.
// This function is used by randomPartition()
function partition($arr, $l, $r)
{
    $x = $arr[$r];
    $i = $l;
    for ($j = $l; $j <= $r - 1; $j++)
    {
        if ($arr[$j] <= $x)
        {
            list($arr[$i], $arr[$j])=array($arr[$j],$arr[$i]);
            //swap(&arr[i], &arr[j]);
            $i++;
        }
    }
    list($arr[$i], $arr[$r])=array($arr[$r],$arr[$i]);
    //swap(&arr[i], &arr[r]);
    return $i;
}

// Picks a random pivot element between
// l and r and partitions arr[l..r] around
// the randomly picked element using partition()
function randomPartition($arr, $l, $r)
{
    $n = $r-$l+1;
    $pivot = rand() % $n;

    list($arr[$l + $pivot], $arr[$r]) =
            array($arr[$r],$arr[$l + $pivot] );

    //swap(&arr[l + pivot], &arr[r]);
    return partition($arr, $l, $r);
}

// Driver program to test the above methods
    $arr = array(12, 3, 5, 7, 4, 19, 260);
    $n = sizeof($arr)/sizeof($arr[0]);
    $k = 3;
    echo "K'th smallest element is " ,
            kthSmallest($arr, 0, $n-1, $k);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find k'th smallest element in expected
// linear time

// This function returns k'th smallest element in arr[l..r]
// using QuickSort based method. ASSUMPTION: ALL ELEMENTS
// IN ARR[] ARE DISTINCT
function kthSmallest(arr,l,r,k)
{
    // If k is smaller than number of elements in array
        if (k > 0 && k <= r - l + 1)
        {
            // Partition the array around a random element and
            // get position of pivot element in sorted array
            let pos = randomPartition(arr, l, r);

            // If position is same as k
            if (pos-l == k-1)
                return arr[pos];

            // If position is more, recur for left subarray
            if (pos-l > k-1)
                return kthSmallest(arr, l, pos-1, k);

            // Else recur for right subarray
            return kthSmallest(arr, pos+1, r, k-pos+l-1);
        }

        // If k is more than number of elements in array
        return Integer.MAX_VALUE;
}

// Utility method to swap arr[i] and arr[j]
function swap(arr,i,j)
{
    let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
}

// Standard partition process of QuickSort(). It considers
// the last element as pivot and moves all smaller element
// to left of it and greater elements to right. This function
// is used by randomPartition()
function partition(arr,l,r)
{
    let x = arr[r], i = l;
        for (let j = l; j <= r - 1; j++)
        {
            if (arr[j] <= x)
            {
                swap(arr, i, j);
                i++;
            }
        }
        swap(arr, i, r);
        return i;
}

// Picks a random pivot element between l and r and
// partitions arr[l..r] arount the randomly picked
// element using partition()
function randomPartition(arr,l,r)
{
        let n = r-l+1;
        let pivot = Math.floor((Math.random()) * (n-1));
        swap(arr, l + pivot, r);
        return partition(arr, l, r);
}

let arr=[12, 3, 5, 7, 4, 19, 26];
let n = arr.length,k = 3;
document.write("K'th smallest element is "+
kthSmallest(arr, 0, n-1, k));

// This code is contributed by rag2127

</script>
```

**输出:**

```
K'th smallest element is 5
```

**时间复杂度:**
以上解的最坏情况时间复杂度仍然是 O(n <sup>2</sup> )。在最坏的情况下，随机化函数可能总是选择一个角元素。上述随机化快速选择的预期时间复杂度为 O(n)，证明见 [CLRS 书](http://www.flipkart.com/introduction-algorithms-english-3rd/p/itmdwxyrafdburzg?pid=9788120340077&affid=sandeepgfg)或 [MIT 视频讲座](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-046j-introduction-to-algorithms-sma-5503-fall-2005/video-lectures/lecture-6-order-statistics-median/)。分析中的假设是，随机数生成器同样可能生成输入范围内的任何数字。

**来源:**
[麻省理工学院订单统计视频讲座，中位数](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-046j-introduction-to-algorithms-sma-5503-fall-2005/video-lectures/lecture-6-order-statistics-median/)
[Clifford Stein，Thomas H. Cormen，Charles E. Leiserson，Ronald L.](http://www.flipkart.com/introduction-algorithms-8120340078/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg) 算法导论

本文由**希瓦姆**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息