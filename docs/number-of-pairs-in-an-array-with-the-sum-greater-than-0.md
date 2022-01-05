# 和大于 0 的数组中的对数

> 原文:[https://www . geeksforgeeks . org/总和大于 0 的阵列对数量/](https://www.geeksforgeeks.org/number-of-pairs-in-an-array-with-the-sum-greater-than-0/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找出数组中不同对的数量，这些对的**和为> 0** 。

**示例:**

> **输入:** arr[] = { 3，-2，1 }
> **输出:** 2
> **解释:**
> 数组中有两对元素的和为正。它们是:
> {3，-2} = 1
> {3，1} = 4
> 
> **输入:** arr[] = { -1，-1，-1，0 }
> **输出:** 0
> **说明:**
> 数组中没有和为正的元素对。

**天真方法:**这个问题的天真方法是考虑数组中所有唯一的元素对。对于每对，检查总和是否为正。
T3】时间复杂度: O(N <sup>2</sup>

**有效方法:**

*   思路是用[的概念排序](https://www.geeksforgeeks.org/sorting-algorithms/)和[两个指针手法](https://www.geeksforgeeks.org/two-pointers-technique/)。
*   对于这个问题，使用排序是因为对于总和 **arr[i] + arr[j] > 0** ，其中 I、j 是数组中的一些随机索引，或者是 **arr[i] > 0** 或者是 **arr[j] > 0** 或者是两者都是 **arr[i]和 arr[j] > 0** 。
*   因此，一旦数组被排序，因为我们需要找到唯一的对。对于每一个这样的“我”即**arr【I】>0**，我们需要找到这样的 j 的数量，即**arr【j】+arr【j】>0**。
*   这里，使用双指针技术很容易找到对的计数，因为数组是排序的。我们只需要找到条件成立的‘j’的最左边的位置。这是使用-arr[i] + 1 的**下限找到的。**
*   例如，让数组 arr[] = {-4，4，-5，5，3，-2，-3，-1，2，1}。此数组已排序。因此，数组变成{-5，-4，-3，-2，-1，1，2，3，4，5}。对于一些随机 I，我们假设 arr[i] = 4。因此，在数组 2 中找到了-3 的索引。现在，我们可以确定，对于索引 2 和 8 之间的所有值，arr[i] + arr[j] > 0 的值。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the
// number of pairs in the
// array with the sum > 0

#include <bits/stdc++.h>
using namespace std;

// Function to find the number
// of pairs in the array with
// sum > 0
int findNumOfPair(int* a, int n)
{

    // Sorting the given array
    sort(a, a + n);

    // Variable to store the count of pairs
    int ans = 0;

    // Loop to iterate through the array
    for (int i = 0; i < n; ++i) {

        // Ignore if the value is negative
        if (a[i] <= 0)
            continue;

        // Finding the index using lower_bound
        int j = lower_bound(a, a + n, -a[i] + 1) - a;

        // Finding the number of pairs between
        // two indices i and j
        ans += i - j;
    }
    return ans;
}

// Driver code
int main()
{
    int a[] = { 3, -2, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    int ans = findNumOfPair(a, n);
    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// number of pairs in the
// array with the sum > 0
import java.util.*;

class GFG {

    // Function to find the number
    // of pairs in the array with
    // sum > 0
    static int findNumOfPair(int arr[], int n)
    {

        // Sorting the given array
        Arrays.sort(arr);

        // Variable to store the count of pairs
        int ans = 0;

        // Loop to iterate through the array
        for (int i = 0; i < n; ++i) {

            // Ignore if the value is negative
            if (arr[i] <= 0)
                continue;

            /*
            minReqVal val is the min value ,which will
            give >=1 after adding with the arr[i]
            */
            int minReqVal = -arr[i] + 1;
            int j = lower_bound(arr, minReqVal);

            if (j >= 0)
                ans += i - j;
        }
        return ans;
    }

    /*
         it return the index of a minimum Number in the
         array which is just >= val
      */
    static int lower_bound(int arr[], int val)
    {
        int start = 0, end = arr.length;

        /*
          using the Binary search technique , since our
          array is sorted
        */
        while (start < end) {
            int mid = (start + end) >> 1;

            if (val > arr[mid])
                start = mid + 1;
            else
                end = mid;
        }

        // when we dont find the answer return -1
        if (start == arr.length)
            return -1;

        return start;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = {-2,-1,-1,-1,-1,0 ,1,2,3};
        int n = a.length;

        int ans = findNumOfPair(a, n);
        System.out.println(ans);
    }
}

// This code is contributed by Pradeep Mondal P
```

## 蟒蛇 3

```
# Python3 program to find the
# number of pairs in the
# array with the sum > 0
from bisect import bisect_left as lower_bound

# Function to find the number
# of pairs in the array with
# sum > 0

def findNumOfPair(a, n):

    # Sorting the given array
    a = sorted(a)

    # Variable to store the count of pairs
    ans = 0

    # Loop to iterate through the array
    for i in range(n):

        # Ignore if the value is negative
        if (a[i] <= 0):
            continue

        # Finding the index using lower_bound
        j = lower_bound(a, -a[i] + 1)

        # Finding the number of pairs between
        # two indices i and j
        ans += i - j
    return ans

# Driver code
if __name__ == '__main__':
    a = [3, -2, 1]
    n = len(a)

    ans = findNumOfPair(a, n)
    print(ans)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the
// number of pairs in the
// array with the sum > 0
using System;

class GFG {

    // Function to find the number
    // of pairs in the array with
    // sum > 0
    static int findNumOfPair(int[] arr, int n)
    {

        // Sorting the given array
        Array.Sort(arr);

        // Variable to store the count of pairs
        int ans = 0;

        // Loop to iterate through the array
        for (int i = 0; i < n; ++i) {

            // Ignore if the value is negative
            if (arr[i] <= 0)
                continue;

            /*
            minReqVal val is the min value ,which will
            give >=1 after adding with the arr[i]
            */
            int minReqVal = -arr[i] + 1;
            int j = lower_bound(arr, minReqVal);

            if (j >= 0)
                ans += i - j;
        }
        return ans;
    }

    /*
           it return the index of a minimum Number in the
           array which is just >= val
        */
    static int lower_bound(int[] arr, int val)
    {
        int start = 0, end = arr.Length;

        /*
          using the Binary search technique , since our
          array is sorted
        */
        while (start < end) {
            int mid = (start + end) >> 1;

            if (val > arr[mid])
                start = mid + 1;
            else
                end = mid;
        }

        // when we dont find the answer return -1
        if (start == arr.Length)
            return -1;

        return start;
    }

    // Driver code
    public static void Main()
    {
        int[] a = { -2, 1, 3 };
        int n = a.Length;

        int ans = findNumOfPair(a, n);
        Console.Write(ans);
    }
}

// This code is contributed by Pradeep Mondal P
```

## java 描述语言

```
<script>
// Javascript program to find the
// number of pairs in the
// array with the sum > 0

// Function to find the number
    // of pairs in the array with
    // sum > 0
function findNumOfPair(arr, n)
{

    // Sorting the given array
        arr.sort(function(a,b){return a-b;});

        // Variable to store the count of pairs
        let ans = 0;

        // Loop to iterate through the array
        for (let i = 0; i < n; ++i) {

            // Ignore if the value is negative
            if (arr[i] <= 0)
                continue;

            /*
            minReqVal val is the min value ,which will
            give >=1 after adding with the arr[i]
            */
               let minReqVal = -arr[i] + 1;
            let j = lower_bound(arr, minReqVal);

            if (j >= 0)
                ans += i - j;
        }
        return ans;
}

/*
         it return the index of a minimum Number in the
         array which is just >= val
      */
function lower_bound(arr,val)
{
    let start = 0, end = arr.length;

        /*
          using the Binary search technique , since our
          array is sorted
        */
        while (start < end) {
            let mid = (start + end) >> 1;

            if (val > arr[mid])
                start = mid + 1;
            else
                end = mid;
        }

        // when we dont find the answer return -1
        if (start == arr.length)
            return -1;

        return start;
}

// Driver code
let a=[3, -2, 1];
let n = a.length;
let ans = findNumOfPair(a, n);
document.write(ans);

// This code is contributed by unknown2108
</script>
```

**Output**

```
2
```

**时间复杂度:** O(N * log(N))