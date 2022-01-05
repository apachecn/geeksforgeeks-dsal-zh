# 在经过排序和旋转的重复数组中搜索元素

> 原文:[https://www . geeksforgeeks . org/search-一个包含重复项的排序和旋转数组中的元素/](https://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-rotated-array-with-duplicates/)

给定一个经过排序和旋转的数组 **arr[]** ，任务是在 O(log n)时间内找到旋转数组中的一个元素(有重复)。
**注意:**打印关键所在的索引。如果有多个答案，请打印其中任何一个

**示例:**

> **输入:** arr[] = {3，3，3，1，2，3}，键= 3
> T3】输出: 0
> arr[0] = 3
> 
> **输入:** arr[] = {3，3，3，1，2，3}，键= 11
> **输出:** -1
> 11 不在给定数组中。

**做法:**思路和[上一个一样，没有重复。](https://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/)唯一的区别是，由于重复项的存在， **arr[low] == arr[mid]** 是可能的，前半部分可能是无序的(即不是按升序，例如{3，1，2，3，3，3，3})，我们必须单独处理这个案例。
在这种情况下，保证 **arr【高】**也等于 **arr【中】**，所以可以在原逻辑之前检查条件 **arr【中】== arr【低】== arr【高】**，如果是，则通过 **1** 向中间左右移动并重复。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the index of the
// key in arr[l..h] if the key is present
// otherwise return -1
int search(int arr[], int l, int h, int key)
{
    if (l > h)
        return -1;

    int mid = l + (h - l) / 2;
    if (arr[mid] == key)
        return mid;

    // The tricky case, just update left and right
    if ((arr[l] == arr[mid])
        && (arr[h] == arr[mid]))
    {
        ++l;
        --h;
        return search(arr, l, h, key);
    }

    // If arr[l...mid] is sorted
    if (arr[l] <= arr[mid]) {

        // As this subarray is sorted, we can quickly
        // check if key lies in any of the halves
        if (key >= arr[l] && key <= arr[mid])
            return search(arr, l, mid - 1, key);

        // If key does not lie in the first half
        // subarray then divide the other half
        // into two subarrays such that we can
        // quickly check if key lies in the other half
        return search(arr, mid + 1, h, key);
    }

    // If arr[l..mid] first subarray is not sorted
    // then arr[mid... h] must be sorted subarray
    if (key >= arr[mid] && key <= arr[h])
        return search(arr, mid + 1, h, key);

    return search(arr, l, mid - 1, key);
}

// Driver code
int main()
{
    int arr[] = { 3, 3, 1, 2, 3, 3 };
    int n = sizeof(arr) / sizeof(int);
    int key = 3;

    cout << search(arr, 0, n - 1, key);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the index of the
    // key in arr[l..h] if the key is present
    // otherwise return -1
    static int search(int arr[], int l, int h, int key)
    {
        if (l > h)
            return -1;

        int mid = l + (h - l) / 2;
        if (arr[mid] == key)
            return mid;

        // The tricky case, just update left and right
        if ((arr[l] == arr[mid])
            && (arr[h] == arr[mid]))
        {
            l++;
            h--;
              return search(arr,l,h,key);
        }

        // If arr[l...mid] is sorted
        else if (arr[l] <= arr[mid])
        {

            // As this subarray is sorted, we can quickly
            // check if key lies in any of the halves
            if (key >= arr[l] && key <= arr[mid])
                return search(arr, l, mid - 1, key);

            // If key does not lie in the first half
            // subarray then divide the other half
            // into two subarrays such that we can
            // quickly check if key lies in the other half
            else
              return search(arr, mid + 1, h, key);
        }

        // If arr[l..mid] first subarray is not sorted
        // then arr[mid... h] must be sorted subarray
           else  if (key >= arr[mid] && key <= arr[h])
            return search(arr, mid + 1, h, key);

        return search(arr, l, mid - 1, key);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] ={3, 3, 1, 2, 3, 3};
        int n = arr.length;
        int key = 3;

        System.out.println(search(arr, 0, n - 1, key));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the index of the
# key in arr[l..h] if the key is present
# otherwise return -1
def search(arr, l, h, key) :

    if (l > h) :
        return -1;

    mid = (l + h) // 2;
    if (arr[mid] == key) :
        return mid;

    # The tricky case, just update left and right
    if ((arr[l] == arr[mid]) and (arr[h] == arr[mid])) :
        l += 1;
        h -= 1;
        return search(arr, l, h, key)
    # If arr[l...mid] is sorted
    if (arr[l] <= arr[mid]) :

        # As this subarray is sorted, we can quickly
        # check if key lies in any of the halves
        if (key >= arr[l] and key <= arr[mid]) :
            return search(arr, l, mid - 1, key);

        # If key does not lie in the first half
        # subarray then divide the other half
        # into two subarrays such that we can
        # quickly check if key lies in the other half
        return search(arr, mid + 1, h, key);

    # If arr[l..mid] first subarray is not sorted
    # then arr[mid... h] must be sorted subarray
    if (key >= arr[mid] and key <= arr[h]) :
        return search(arr, mid + 1, h, key);

    return search(arr, l, mid - 1, key);

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 3, 1, 2, 3, 3 ];
    n = len(arr);
    key = 3;

    print(search(arr, 0, n - 1, key));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the index of the
    // key in arr[l..h] if the key is present
    // otherwise return -1
    static int search(int []arr, int l, int h, int key)
    {
        if (l > h)
            return -1;

        int mid = l + (h - l) / 2;
        if (arr[mid] == key)
            return mid;

        // The tricky case, just update left and right
        if ((arr[l] == arr[mid])
            && (arr[h] == arr[mid]))
        {
            ++l;
            --h;
            return search(arr, l, h, key)
        }

        // If arr[l...mid] is sorted
        if (arr[l] <= arr[mid])
        {

            // As this subarray is sorted, we can quickly
            // check if key lies in any of the halves
            if (key >= arr[l] && key <= arr[mid])
                return search(arr, l, mid - 1, key);

            // If key does not lie in the first half
            // subarray then divide the other half
            // into two subarrays such that we can
            // quickly check if key lies in the other half
            return search(arr, mid + 1, h, key);
        }

        // If arr[l..mid] first subarray is not sorted
        // then arr[mid... h] must be sorted subarray
        if (key >= arr[mid] && key <= arr[h])
            return search(arr, mid + 1, h, key);

        return search(arr, l, mid - 1, key);
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 3, 3, 1, 2, 3, 3 };
        int n = arr.Length;
        int key = 3;

        Console.WriteLine(search(arr, 0, n - 1, key));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the index of the
    // key in arr[l..h] if the key is present
    // otherwise return -1
    function search(arr, l, h, key)
    {
        if (l > h)
            return -1;

        let mid = parseInt((l + h) / 2, 10);
        if (arr[mid] == key)
            return mid;

        // The tricky case, just update left and right
        if ((arr[l] == arr[mid])
            && (arr[h] == arr[mid]))
        {
            ++l;
            --h;
            return search(arr, l, h, key)
        }

        // If arr[l...mid] is sorted
        if (arr[l] <= arr[mid])
        {

            // As this subarray is sorted, we can quickly
            // check if key lies in any of the halves
            if (key >= arr[l] && key <= arr[mid])
                return search(arr, l, mid - 1, key);

            // If key does not lie in the first half
            // subarray then divide the other half
            // into two subarrays such that we can
            // quickly check if key lies in the other half
            return search(arr, mid + 1, h, key);
        }

        // If arr[l..mid] first subarray is not sorted
        // then arr[mid... h] must be sorted subarray
        if (key >= arr[mid] && key <= arr[h])
            return search(arr, mid + 1, h, key);

        return search(arr, l, mid - 1, key);
    }

    let arr = [ 3, 3, 1, 2, 3, 3 ];
    let n = arr.length;
    let key = 3;

    document.write(search(arr, 0, n - 1, key));

</script>
```

**Output**

```
4
```