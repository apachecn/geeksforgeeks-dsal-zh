# 小范围未排序数组中最小/最大的 kth

> 原文:[https://www . geesforgeks . org/kth-小范围内最小-最大-未排序-数组/](https://www.geeksforgeeks.org/kth-smallest-largest-in-a-small-range-unsorted-array/)

在未排序的数组中查找第 k 个最小或最大的元素，其中 k <=size of array. It is given that elements of array are in small range.
**示例:**

```
Input : arr[] = {3, 2, 9, 5, 7, 11, 13}
        k = 5
Output: 9

Input : arr[] = {16, 8, 9, 21, 43}
        k = 3
Output: 16

Input : arr[] = {50, 50, 40}
        k = 2
Output: 50
```

由于给定的数组元素在小范围内，我们可以指导索引表做一些类似[计数排序](https://www.geeksforgeeks.org/counting-sort/)的事情。我们存储元素的计数，然后遍历计数数组并打印第 k 个元素。
以下是上述算法
的实现

## C++

```
// C++ program of kth smallest/largest in
// a small range unsorted array
#include <bits/stdc++.h>
using namespace std;
#define maxs 1000001

int kthSmallestLargest(int* arr, int n, int k)
{
    int max_val = *max_element(arr, arr+n);
    int hash[max_val+1] = { 0 };

    // Storing counts of elements
    for (int i = 0; i < n; i++)
        hash[arr[i]]++;   

    // Traverse hash array build above until
    // we reach k-th smallest element.
    int count = 0;
    for (int i=0; i <= max_val; i++)
    {
        while (hash[i] > 0)
        {
           count++;
           if (count == k)
              return i;
           hash[i]--;
        }
    }

    return -1;
}

int main()
{
    int arr[] = { 11, 6, 2, 9, 4, 3, 16 };
    int n = sizeof(arr) / sizeof(arr[0]), k = 3;
    cout << "kth smallest number is: "
         << kthSmallestLargest(arr, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of kth smallest/largest in
// a small range unsorted array
import java.util.Arrays;

class GFG
{

    static int maxs = 1000001;

    static int kthSmallestLargest(int[] arr, int n, int k)
    {
        int max_val = Arrays.stream(arr).max().getAsInt();
        int hash[] = new int[max_val + 1];

        // Storing counts of elements
        for (int i = 0; i < n; i++)
        {
            hash[arr[i]]++;
        }

        // Traverse hash array build above until
        // we reach k-th smallest element.
        int count = 0;
        for (int i = 0; i <= max_val; i++)
        {
            while (hash[i] > 0)
            {
                count++;
                if (count == k)
                {
                    return i;
                }
                hash[i]--;
            }
        }

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {11, 6, 2, 9, 4, 3, 16};
        int n = arr.length, k = 3;
        System.out.println("kth smallest number is: "
                + kthSmallestLargest(arr, n, k));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program of kth smallest/largest
# in a small range unsorted array

def kthSmallestLargest(arr, n, k):
    max_val = arr[0]
    for i in range(len(arr)):
        if (arr[i] > max_val):
            max_val = arr[i]
    hash = [0 for i in range(max_val + 1)]

    # Storing counts of elements
    for i in range(n):
        hash[arr[i]] += 1

    # Traverse hash array build above until
    # we reach k-th smallest element.
    count = 0
    for i in range(max_val + 1):
        while (hash[i] > 0):
            count += 1
            if (count == k):
                return i
            hash[i] -= 1

    return -1

# Driver Code
if __name__ == '__main__':
    arr = [11, 6, 2, 9, 4, 3, 16]
    n = len(arr)
    k = 3
    print("kth smallest number is:",
           kthSmallestLargest(arr, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program of kth smallest/largest in
// a small range unsorted array
using System;
using System.Linq;

class GFG
{

    static int maxs = 1000001;

    static int kthSmallestLargest(int[] arr, int n, int k)
    {
        int max_val = arr.Max();
        int []hash = new int[max_val + 1];

        // Storing counts of elements
        for (int i = 0; i < n; i++)
        {
            hash[arr[i]]++;
        }

        // Traverse hash array build above until
        // we reach k-th smallest element.
        int count = 0;
        for (int i = 0; i <= max_val; i++)
        {
            while (hash[i] > 0)
            {
                count++;
                if (count == k)
                {
                    return i;
                }
                hash[i]--;
            }
        }
        return -1;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {11, 6, 2, 9, 4, 3, 16};
        int n = arr.Length, k = 3;
        Console.WriteLine("kth smallest number is: "
                + kthSmallestLargest(arr, n, k));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of kth smallest/largest in
// a small range unsorted array
$maxs = 1000001;

function kthSmallestLargest(&$arr, $n, $k)
{
    global $maxs;
    $max_val = max($arr);
    $hash = array_fill(0,$max_val+1, NULL);

    // Storing counts of elements
    for ($i = 0; $i < $n; $i++)
        $hash[$arr[$i]]++;   

    // Traverse hash array build above until
    // we reach k-th smallest element.
    $count = 0;
    for ($i=0; $i <= $max_val; $i++)
    {
        while ($hash[$i] > 0)
        {
           $count++;
           if ($count == $k)
              return $i;
           $hash[$i]--;
        }
    }

    return -1;
}

    $arr = array ( 11, 6, 2, 9, 4, 3, 16 );
    $n = sizeof($arr) / sizeof($arr[0]);
    $k = 3;
    echo "kth smallest number is: "
         . kthSmallestLargest($arr, $n, $k)."\n";
    return 0;
?>
```

## java 描述语言

```
<script>
// Javascript program of kth smallest/largest in
// a small range unsorted array

    let maxs = 1000001;
    function kthSmallestLargest(arr,n,k)
    {
        let max_val = Math.max(...arr);
        let hash = new Array(max_val + 1);
        for(let i=0;i<hash.length;i++)
        {
            hash[i]=0;
        }

        // Storing counts of elements
        for (let i = 0; i < n; i++)
        {
            hash[arr[i]]++;
        }

        // Traverse hash array build above until
        // we reach k-th smallest element.
        let count = 0;
        for (let i = 0; i <= max_val; i++)
        {
            while (hash[i] > 0)
            {
                count++;
                if (count == k)
                {
                    return i;
                }
                hash[i]--;
            }
        }

        return -1;
    }

    // Driver code
    let arr=[11, 6, 2, 9, 4, 3, 16];
    let n = arr.length, k = 3;
    document.write("kth smallest number is: "
                + kthSmallestLargest(arr, n, k));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
kth smallest number is: 4
```

**时间复杂度:** O(n + max_val)