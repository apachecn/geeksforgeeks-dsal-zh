# 计算数组中的交叉线

> 原文:[https://www.geeksforgeeks.org/counting-cross-lines-array/](https://www.geeksforgeeks.org/counting-cross-lines-array/)

给定不同元素的未排序数组。任务是在对数组元素进行排序后，计算数组元素中形成的交叉线的数量。
**注意:**在排序前和排序后的相同数组元素之间画一条线。
**示例:**

```
Input :  arr[] = { 3, 2, 1, 4, 5 }
Output : 3
      before sort: 3  2  1  4  5
                    \ | /   |  | 
                     \|/    |  |
                    / | \   |  |
      After sort : 1  2  3  4  5 
      line (1 to 1) cross line (2 to 2)
      line (1 to 1) cross line (3 to 3)
      line (2 to 2) cross line (3 to 3)
Note: the line between two 4s and the line 
between two 5s don't cross any other lines; 

Input : arr[] = { 5, 4, 3, 1 }
Output : 6
```

**这个问题的简单解决方法**是基于[插入排序](https://www.geeksforgeeks.org/insertion-sort/)。我们简单地一个接一个地挑选每个数组元素，并试图找到它在排序数组中的适当位置。在找到它在元素中的适当位置的过程中，我们必须穿过所有值大于当前元素的 element_line。
以下是以上想法的实现:

## C++

```
// c++ program to count cross line in array
#include <bits/stdc++.h>
using namespace std;

// function return count of cross line in an array
int countCrossLine(int arr[], int n)
{
    int count_crossline = 0;
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        /* Move elements of arr[0..i-1], that are
          greater than key, to one position ahead
          of their current position */
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;

            // increment cross line by one
            count_crossline++;
        }
        arr[j + 1] = key;
    }
    return count_crossline;
}

// driver program to test above function
int main()
{
    int arr[] = { 4, 3, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countCrossLine(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// cross line in array

class GFG
{
    static int countCrossLine(int arr[],
                              int n)
    {
        int count_crossline = 0;
        int i, key, j;
        for (i = 1; i < n; i++)
        {
            key = arr[i];
            j = i - 1;

            // Move elements of arr[0..i-1],
            // that are greater than key,
            // to one position ahead of
            // their current position
            while (j >= 0 && arr[j] > key)
            {
                arr[j + 1] = arr[j];
                j = j - 1;

                // increment cross
                // line by one
                count_crossline++;
            }
            arr[j + 1] = key;
        }

        return count_crossline;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = new int[]{ 4, 3, 1, 2 };
        int n = arr.length;
        System.out.print(countCrossLine(arr, n));
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to count
# cross line in array
def countCrossLine(arr, n):
    count_crossline = 0;
    i, key, j = 0, 0, 0;
    for i in range(1, n):
        key = arr[i];
        j = i - 1;

        # Move elements of arr[0..i-1],
        # that are greater than key,
        # to one position ahead of
        # their current position
        while (j >= 0 and arr[j] > key):
            arr[j + 1] = arr[j];
            j = j - 1;

            # increment cross
            # line by one
            count_crossline += 1;
        arr[j + 1] = key;
    return count_crossline;

# Driver Code
if __name__ == '__main__':
    arr = [4, 3, 1, 2];
    n = len(arr);
    print(countCrossLine(arr, n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to count cross line in array
using System;

class GFG {

    // function return count of cross line
    // in an array
    static int countCrossLine(int []arr, int n)
    {
        int count_crossline = 0;
        int i, key, j;
        for (i = 1; i < n; i++) {
            key = arr[i];
            j = i - 1;

            /* Move elements of arr[0..i-1],
            that are greater than key, to one
            position ahead of their current
            position */
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;

                // increment cross line by one
                count_crossline++;
            }
            arr[j + 1] = key;
        }

        return count_crossline;
    }

    // Driver code
    public static void Main()
    {
        int []arr = new int[]{ 4, 3, 1, 2 };
        int n = arr.Length;
        Console.Write(countCrossLine(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// cross line in array

// Function return count
// of cross line in an array
function countCrossLine($arr, $n)
{

    $count_crossline = 0;
    $i; $key; $j;
    for ($i = 1; $i < $n; $i++)
    {
        $key = $arr[$i];
        $j = $i - 1;

        /* Move elements of arr[0..i-1], that are
           greater than key, to one position ahead
           of their current position */
        while ($j >= 0 and $arr[$j] > $key)
        {
            $arr[$j + 1] = $arr[$j];
            $j = $j - 1;

            // increment cross line by one
            $count_crossline++;
        }
        $arr[$j + 1] = $key;
    }
    return $count_crossline;
}

    // Driver Code
    $arr = array( 4, 3, 1, 2 );
    $n = count($arr);
    echo countCrossLine($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to count cross line in array

// function return count of cross line in an array
function countCrossLine( arr,  n)
{
    let count_crossline = 0;
    let i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        /* Move elements of arr[0..i-1], that are
          greater than key, to one position ahead
          of their current position */
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;

            // increment cross line by one
            count_crossline++;
        }
        arr[j + 1] = key;
    }
    return count_crossline;
}

// driver code

    let arr = [ 4, 3, 1, 2 ];
    let n = arr.length;
    document.write(countCrossLine(arr, n) + "</br");

</script>
```

**输出:**

```
5
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(1)
**高效解**基于[合并排序](https://www.geeksforgeeks.org/merge-sort/)和[倒排计数](https://www.geeksforgeeks.org/counting-inversions/)。

```
   lets we have arr[] { 2, 4, 1, 3 }
                         \   \ /   /
                          \  / \ /
                          / \  / \
   After sort   arr[] { 1, 2, 3, 4 }
   and here all inversion are (2, 1), (4, 1), (4, 3)
   that mean line 1 : cross line 4, 2 
             line 2 : cross line 1 
             line 4 : cross line 3, 1
             line 3 : cross line 3
 so total unique cross_line are: 3  
```

合并期间
以下是上述想法的实现。

## C++

```
// c++ program to count cross line in array
#include <bits/stdc++.h>
using namespace std;

// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
void merge(int arr[], int l, int m, int r, int* count_crossline)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;

    /* create temp arrays */
    int L[n1], R[n2];

    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    /* Merge the temp arrays back into arr[l..r]*/
    i = 0; // Initial index of first subarray
    j = 0; // Initial index of second subarray
    k = l; // Initial index of merged subarray
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        }
        else {
            arr[k] = R[j];

            //====================================//
            //======= MAIN PORTION OF CODE ======//
            //===================================//
            // add all line which is cross by current element
            *count_crossline += (n1 - i);
            j++;
        }
        k++;
    }

    /* Copy the remaining elements of L[], if there
    are any */
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    /* Copy the remaining elements of R[], if there
    are any */
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

/* l is for left index and r is right index of the
sub-array of arr to be sorted */
void mergeSort(int arr[], int l, int r, int* count_crossline)
{
    if (l < r) {

        // Same as (l+r)/2, but avoids overflow for
        // large l and h
        int m = l + (r - l) / 2;

        // Sort first and second halves
        mergeSort(arr, l, m, count_crossline);
        mergeSort(arr, m + 1, r, count_crossline);

        merge(arr, l, m, r, count_crossline);
    }
}

// function return count of cross line in an array
int countCrossLine(int arr[], int n)
{
    int count_crossline = 0;
    mergeSort(arr, 0, n - 1, &count_crossline);

    return count_crossline;
}

// driver program to test above function
int main()
{
    int arr[] = { 12, 11, 13, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countCrossLine(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count cross line in array
import java.util.*;

class GFG
{
    static int count_crossline;

    // Merges two subarrays of arr[].
    // First subarray is arr[l..m]
    // Second subarray is arr[m+1..r]
    static void merge(int arr[], int l, int m, int r)
    {
        int i, j, k;
        int n1 = m - l + 1;
        int n2 = r - m;

        /* create temp arrays */
        int[] L = new int[n1];
        int[] R = new int[n2];

        /* Copy data to temp arrays L[] and R[] */
        for (i = 0; i < n1; i++)
        {
            L[i] = arr[l + i];
        }
        for (j = 0; j < n2; j++)
        {
            R[j] = arr[m + 1 + j];
        }

        /* Merge the temp arrays back into arr[l..r]*/
        i = 0; // Initial index of first subarray
        j = 0; // Initial index of second subarray
        k = l; // Initial index of merged subarray
        while (i < n1 && j < n2)
        {
            if (L[i] <= R[j])
            {
                arr[k] = L[i];
                i++;
            }
            else
            {
                arr[k] = R[j];

                //====================================//
                //======= MAIN PORTION OF CODE ======//
                //===================================//
                // add all line which is cross by current element
                count_crossline += (n1 - i);
                j++;
            }
            k++;
        }

        /* Copy the remaining elements of L[],
        if there are any */
        while (i < n1)
        {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy the remaining elements of R[],
        if there are any */
        while (j < n2)
        {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    /* l is for left index and r is right index of the
    sub-array of arr to be sorted */
    static void mergeSort(int arr[], int l, int r)
    {
        if (l < r)
        {

            // Same as (l+r)/2, but avoids overflow for
            // large l and h
            int m = l + (r - l) / 2;

            // Sort first and second halves
            mergeSort(arr, l, m);
            mergeSort(arr, m + 1, r);

            merge(arr, l, m, r);
        }
    }

    // function return count of cross line in an array
    static int countCrossLine(int arr[], int n)
    {
        mergeSort(arr, 0, n - 1);

        return count_crossline;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {12, 11, 13, 5, 6, 7};
        int n = arr.length;
        System.out.println(countCrossLine(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to count cross line in array
using System;

class GFG
{
    static int count_crossline;

    // Merges two subarrays of []arr.
    // First subarray is arr[l..m]
    // Second subarray is arr[m+1..r]
    static void merge(int []arr, int l,
                        int m, int r)
    {
        int i, j, k;
        int n1 = m - l + 1;
        int n2 = r - m;

        /* create temp arrays */
        int[] L = new int[n1];
        int[] R = new int[n2];

        /* Copy data to temp arrays L[] and R[] */
        for (i = 0; i < n1; i++)
        {
            L[i] = arr[l + i];
        }
        for (j = 0; j < n2; j++)
        {
            R[j] = arr[m + 1 + j];
        }

        /* Merge the temp arrays back into arr[l..r]*/
        i = 0; // Initial index of first subarray
        j = 0; // Initial index of second subarray
        k = l; // Initial index of merged subarray
        while (i < n1 && j < n2)
        {
            if (L[i] <= R[j])
            {
                arr[k] = L[i];
                i++;
            }
            else
            {
                arr[k] = R[j];

                //====================================//
                //======= MAIN PORTION OF CODE ======//
                //===================================//
                // add all line which is cross by current element
                count_crossline += (n1 - i);
                j++;
            }
            k++;
        }

        /* Copy the remaining elements of L[],
        if there are any */
        while (i < n1)
        {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy the remaining elements of R[],
        if there are any */
        while (j < n2)
        {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    /* l is for left index and r is right index of the
    sub-array of arr to be sorted */
    static void mergeSort(int []arr, int l, int r)
    {
        if (l < r)
        {

            // Same as (l+r)/2, but avoids overflow for
            // large l and h
            int m = l + (r - l) / 2;

            // Sort first and second halves
            mergeSort(arr, l, m);
            mergeSort(arr, m + 1, r);

            merge(arr, l, m, r);
        }
    }

    // function return count of cross line in an array
    static int countCrossLine(int []arr, int n)
    {
        mergeSort(arr, 0, n - 1);

        return count_crossline;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = {12, 11, 13, 5, 6, 7};
        int n = arr.Length;
        Console.WriteLine(countCrossLine(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to count cross line in array

    let count_crossline = 0;

    // Merges two subarrays of arr[].
    // First subarray is arr[l..m]
    // Second subarray is arr[m+1..r]
    function merge(arr, l, m, r)
    {
        let i, j, k;
        let n1 = m - l + 1;
        let n2 = r - m;

        /* create temp arrays */
        let L = [];
        let R = [];

        /* Copy data to temp arrays L[] and R[] */
        for (i = 0; i < n1; i++)
        {
            L[i] = arr[l + i];
        }
        for (j = 0; j < n2; j++)
        {
            R[j] = arr[m + 1 + j];
        }

        /* Merge the temp arrays back into arr[l..r]*/
        i = 0; // Initial index of first subarray
        j = 0; // Initial index of second subarray
        k = l; // Initial index of merged subarray
        while (i < n1 && j < n2)
        {
            if (L[i] <= R[j])
            {
                arr[k] = L[i];
                i++;
            }
            else
            {
                arr[k] = R[j];

                //====================================//
                //======= MAIN PORTION OF CODE ======//
                //===================================//
                // add all line which is cross by current element
                count_crossline += (n1 - i);
                j++;
            }
            k++;
        }

        /* Copy the remaining elements of L[],
        if there are any */
        while (i < n1)
        {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy the remaining elements of R[],
        if there are any */
        while (j < n2)
        {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    /* l is for left index and r is right index of the
    sub-array of arr to be sorted */
    function mergeSort(arr, l, r)
    {
        if (l < r)
        {

            // Same as (l+r)/2, but avoids overflow for
            // large l and h
            let m = l + Math.floor((r - l) / 2);

            // Sort first and second halves
            mergeSort(arr, l, m);
            mergeSort(arr, m + 1, r);

            merge(arr, l, m, r);
        }
    }

    // function return count of cross line in an array
    function countCrossLine(arr, n)
    {
        mergeSort(arr, 0, n - 1);

        document.write(count_crossline);
    }

// Driver code
        let arr = [12, 11, 13, 5, 6, 7];
        let n = arr.length;
        countCrossLine(arr, n);

    // This code is contributed by code_hunt.
</script>
```

**输出:**

```
>10
```

**时间复杂度:** O(nlogn)
参考:[https://www.careercup.com/question?id=5669565693427712](https://www.careercup.com/question?id=5669565693427712)
本文由 [**尼尚辛格**](https://www.facebook.com/nishant.chaudhary.7334) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。