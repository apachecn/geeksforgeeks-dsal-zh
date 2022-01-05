# 使用大小为 3 的子阵列旋转进行排序

> 原文:[https://www . geesforgeks . org/sorting-可能使用-size-3-subarray-rotation/](https://www.geeksforgeeks.org/sorting-possible-using-size-3-subarray-rotation/)

给定一个整数值数组，该数组只需通过一个操作排序——子数组旋转，其中子数组大小应为 3。例如，如果我们的数组是(1 2 3 4)，那么我们可以一步达到(1 4 2 3)，(3 1 2 4)。我们需要知道是否有可能用这个操作对整个数组进行排序。
**例:**

```
Input  : arr[] = [1, 3, 4, 2]
Output : Yes
Possible by below rotations, 
[1, 3, 4, 2] -> [1, 4, 2, 3] -> 
[1, 2, 3, 4]

Input  : arr[] = [1, 2, 4, 3]
Output : No
Not possible to sort above array by any 3 
size subarray rotation.
```

假设我们有一个子阵列作为[A[i] A[i+1] A[i+2]]。经过一次旋转，我们得到[A[i+2]，A[i]，A[i+1]]
如果我们观察旋转前后的[逆](https://www.geeksforgeeks.org/counting-inversions/)，我们可以看到逆的宇称不变，即如果[A[i] A[i+1] A[i+2]]有偶数个逆[A[i+2] A[i] A[i+1]]将有偶数个逆。奇数反转也是如此。由于 A[i+2]的移动，反转要么增加 2，要么减少 2，要么保持不变，即它们的奇偶性不会改变。
观察上述事实后，我们可以说，如果初始数组配置有偶数个反转，则有可能使它们变为零，使数组完全排序，否则没有。我们使用[基于合并排序的方法来计数倒排](https://www.geeksforgeeks.org/counting-inversions/)。得到逆矩阵的个数后，我们可以很容易地检查逆矩阵的奇偶性，从而得出是否有可能对数组进行排序。

## C++

```
// C++ program to check whether we can sort
// given array using 3 size subarray rotation
// or not
#include <bits/stdc++.h>
using namespace std;

/* This function merges two sorted arrays and
   returns inversion count in the arrays.*/
int merge(int arr[], int temp[], int left,
                        int mid, int right)
{
    int i, j, k;
    int inv_count = 0;

    i = left; /* i is index for left subarray*/
    j = mid;  /* j is index for right subarray*/
    k = left; /* k is index for resultant merged
                 subarray*/
    while ((i <= mid - 1) && (j <= right))
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
        {
            temp[k++] = arr[j++];

            /* this is tricky -- see above
               explanation/diagram for merge()*/
            inv_count = inv_count + (mid - i);
        }
    }

    /* Copy the remaining elements of left subarray
      (if there are any) to temp */
    while (i <= mid - 1)
        temp[k++] = arr[i++];

    /* Copy the remaining elements of right subarray
       (if there are any) to temp*/
    while (j <= right)
       temp[k++] = arr[j++];

    /* Copy back the merged elements to original
       array */
    for (i = left; i <= right; i++)
        arr[i] = temp[i];

    return inv_count;
}

/* An auxiliary recursive function that sorts
   the input array and returns the number of
   inversions in the array. */
int _mergeSort(int arr[], int temp[], int left,
                                      int right)
{
    int mid, inv_count = 0;
    if (right > left)
    {
        /* Divide the array into two parts and
           call _mergeSortAndCountInv() for each
           of the parts */
        mid = (right + left)/2;

        /* Inversion count will be sum of inversions
           in left-part, right-part and number of
           inversions in merging */
        inv_count  = _mergeSort(arr, temp, left,
                                           mid);
        inv_count += _mergeSort(arr, temp, mid+1,
                                          right);

        /* Merge the two parts */
        inv_count += merge(arr, temp, left, mid+1,
                                            right);
    }
    return inv_count;
}

/* This function sorts the input array and returns the
   number of inversions in the array */
int mergeSort(int arr[], int array_size)
{
    int *temp = (int *)malloc(sizeof(int)*array_size);
    return _mergeSort(arr, temp, 0, array_size - 1);
}

// method returns true is array can be sorted by 3
// size subarray rotation
bool possibleSortingBy3SizeSubarray(int arr[], int N)
{
    int numberOfInversion = mergeSort(arr, N);

    // if number of inversions are even then only
    // we can sort the array
    return (numberOfInversion % 2 == 0);
}

//  Driver code to test above methods
int main()
{
    int arr[] = {1, 3, 4, 2};
    int N = sizeof(arr) / sizeof(int);

    possibleSortingBy3SizeSubarray(arr, N)?
        cout << "Yes\n" : cout << "No\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether we can sort
// given array using 3 size subarray rotation
// or not
import java.io.*;

class GFG
{
    /* This function merges two sorted arrays and
    returns inversion count in the arrays.*/
    public static int merge(int[] arr, int left, int mid, int right)
    {
        int[] temp = new int[arr.length];
        int inv_count = 0;
        int i = left; /* i is index for left subarray*/
        int j = mid; /* j is index for right subarray*/
        int k = left; /* k is index for resultant merged
                         subarray*/

        while((i <= mid-1) && (j <= right))
        {
            if(arr[i] <= arr[j])
            {
                temp[k++] = arr[i];
                i++;
            }
            else
            {
                temp[k++] = arr[j];
                j++;

                /* this is tricky -- see above
                explanation/diagram for merge()*/
                inv_count = inv_count + (mid-i);
            }
        }

        /* Copy the remaining elements of left subarray
        (if there are any) to temp */
        while(i <= (mid-1))
            temp[k++] = arr[i++];

        /* Copy the remaining elements of right subarray
        (if there are any) to temp*/
        while(j <= right)
            temp[k++] = arr[j++];

        /* Copy back the merged elements to original
        array */   
        for (int l = left; l <= right; l++)
            arr[l] = temp[l];

        return inv_count;
    }

    /* An auxiliary recursive function that sorts
    the input array and returns the number of
    inversions in the array. */
    public static int _mergeSort(int[] arr, int left, int right)
    {

       int mid, inv_count = 0;
       if(left < right)
       {

            /* Divide the array into two parts and
            call _mergeSortAndCountInv() for each
            of the parts */
            mid = (left + right)/2;

            /* Inversion count will be sum of inversions
            in left-part, right-part and number of
            inversions in merging */
            inv_count = _mergeSort(arr, left, mid);
            inv_count += _mergeSort(arr, mid+1, right);

            inv_count += merge(arr, left, mid+1, right);

        }
       return inv_count;

   }

    /* This function sorts the input array and returns the
    number of inversions in the array */
    public static int mergeSort(int[] arr, int N)
    {

        return _mergeSort(arr, 0, N-1);
    }

    public static boolean possibleSortingBy3SizeSubarray(int arr[], int N)
    {
        int numberOfInversion = mergeSort(arr, N);

        // if number of inversions are even then only
        // we can sort the array
        return (numberOfInversion % 2 == 0);
    }

    //  Driver code to test above methods
    public static void main (String[] args)
    {

        int arr[] = {1, 3, 4, 2};
        int N = arr.length;

        if(possibleSortingBy3SizeSubarray(arr, N))
            System.out.println( "Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check whether we can sort
# given array using 3 size subarray rotation or not

# This function merges two sorted arrays and
# returns inversion count in the arrays.
def merge(arr, temp, left, mid, right):

    # i is index for left subarray
    # j is index for right subarray
    # k is index for resultant merged subarray
    i, j, k, inv_count = left, mid, left, 0

    while (i <= mid - 1) and (j <= right):

        if arr[i] <= arr[j]:
            temp[k] = arr[i]
            k, i = k + 1, i + 1

        else:
            temp[k] = arr[j]
            k, j = k + 1, j + 1

            # This is tricky -- see above
            # explanation/diagram for merge()
            inv_count = inv_count + (mid - i)

    # Copy the remaining elements of left
    # subarray (if there are any) to temp
    while i <= mid - 1:
        temp[k] = arr[i]
        k, i = k + 1, i + 1

    # Copy the remaining elements of right
    # subarray (if there are any) to temp
    while j <= right:
        temp[k] = arr[j]
        k, j = k + 1, j + 1

    # Copy back the merged elements
    # to original array
    for i in range(left, right + 1):
        arr[i] = temp[i]

    return inv_count

# An auxiliary recursive function that
# sorts the input array and returns the
# number of inversions in the array.
def _mergeSort(arr, temp, left, right):

    inv_count = 0
    if right > left:

        # Divide the array into two parts
        # and call _mergeSortAndCountInv()
        # for each of the parts
        mid = (right + left) // 2

        # Inversion count will be sum of
        # inversions in left-part, right-part
        # and number of inversions in merging
        inv_count = _mergeSort(arr, temp, left, mid)
        inv_count += _mergeSort(arr, temp, mid + 1, right)

        # Merge the two parts
        inv_count += merge(arr, temp, left, mid + 1, right)

    return inv_count

# This function sorts the input array and
# returns the number of inversions in the array
def mergeSort(arr, array_size):

    temp = [None] * array_size
    return _mergeSort(arr, temp, 0, array_size - 1)

# method returns true is array can be
# sorted by 3 size subarray rotation
def possibleSortingBy3SizeSubarray(arr, N):

    numberOfInversion = mergeSort(arr, N)

    # if number of inversions are even
    # then only we can sort the array
    return (numberOfInversion % 2 == 0)

# Driver Code
if __name__ == "__main__":

    arr = [1, 3, 4, 2]
    N = len(arr)

    if possibleSortingBy3SizeSubarray(arr, N):
        print("Yes")
    else:
        print("No")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to check whether we
// can sort given array using 3 size
// subarray rotation or not.
using System;

class GFG
{
    /* This function merges two sorted arrays and
       returns inversion count in the arrays.*/
    public static int merge(int []arr, int left,
                             int mid, int right)
    {
        int []temp = new int[arr.Length];
        int inv_count = 0;

        /* i is index for left subarray*/
        int i = left;

        /* j is index for right subarray*/
        int j = mid; 

        /* k is index for resultant merged subarray*/
        int k = left;

        while((i <= mid-1) && (j <= right))
        {
            if(arr[i] <= arr[j])
            {
                temp[k++] = arr[i];
                i++;
            }
            else
            {
                temp[k++] = arr[j];
                j++;

                /* this is tricky -- see above
                explanation/diagram for merge()*/
                inv_count = inv_count + (mid-i);
            }
        }

        /* Copy the remaining elements of
           left subarray (if there are any)
           to temp */
        while(i <= (mid-1))
            temp[k++] = arr[i++];

        /* Copy the remaining elements of
           right subarray (if there are any)
           to temp*/
        while(j <= right)
            temp[k++] = arr[j++];

        /* Copy back the merged elements
           to original array */
        for (int l = left; l <= right; l++)
            arr[l] = temp[l];

        return inv_count;
    }

    /* An auxiliary recursive function that sorts
       the input array and returns the number of
       inversions in the array. */
    public static int _mergeSort(int []arr, int left,
                                           int right)
    {
      int mid, inv_count = 0;
      if(left < right)
      {
            /* Divide the array into two parts and
               call _mergeSortAndCountInv() for each
               of the parts */
            mid = (left + right)/2;

            /* Inversion count will be sum of inversions
               in left-part, right-part and number of
               inversions in merging */
            inv_count = _mergeSort(arr, left, mid);
            inv_count += _mergeSort(arr, mid+1, right);
            inv_count += merge(arr, left, mid+1, right);

     }
    return inv_count;

}

    /* This function sorts the input array
       and returns the number of inversions
       in the array */
    public static int mergeSort(int[] arr, int N)
    {
        return _mergeSort(arr, 0, N-1);
    }

    public static bool possibleSortingBy3SizeSubarray(int []arr,
                                                          int N)
    {
        int numberOfInversion = mergeSort(arr, N);

        // if number of inversions are even
        // then only we can sort the array
        return (numberOfInversion % 2 == 0);
    }

    // Driver code to test above methods
    public static void Main ()
    {
        int []arr = {1, 3, 4, 2};
        int N = arr.Length;

        if(possibleSortingBy3SizeSubarray(arr, N))
            Console.Write( "Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// JavaScript program to check whether we can sort
// given array using 3 size subarray rotation
// or not

/* This function merges two sorted arrays and
returns inversion count in the arrays.*/
function merge(arr, left, mid, right) {
    let temp = new Array(arr.length);
    let inv_count = 0;
    let i = left; /* i is index for left subarray*/
    let j = mid; /* j is index for right subarray*/
    let k = left; /* k is index for resultant merged
                        subarray*/

    while ((i <= mid - 1) && (j <= right)) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i];
            i++;
        }
        else {
            temp[k++] = arr[j];
            j++;

            /* this is tricky -- see above
            explanation/diagram for merge()*/
            inv_count = inv_count + (mid - i);
        }
    }

    /* Copy the remaining elements of left subarray
    (if there are any) to temp */
    while (i <= (mid - 1))
        temp[k++] = arr[i++];

    /* Copy the remaining elements of right subarray
    (if there are any) to temp*/
    while (j <= right)
        temp[k++] = arr[j++];

    /* Copy back the merged elements to original
    array */
    for (let l = left; l <= right; l++)
        arr[l] = temp[l];

    return inv_count;
}

/* An auxiliary recursive function that sorts
the input array and returns the number of
inversions in the array. */
function _mergeSort(arr, left, right) {

    let mid, inv_count = 0;
    if (left < right) {

        /* Divide the array into two parts and
        call _mergeSortAndCountInv() for each
        of the parts */
        mid = Math.floor((left + right) / 2);

        /* Inversion count will be sum of inversions
        in left-part, right-part and number of
        inversions in merging */
        inv_count = _mergeSort(arr, left, mid);
        inv_count += _mergeSort(arr, mid + 1, right);

        inv_count += merge(arr, left, mid + 1, right);

    }
    return inv_count;

}

/* This function sorts the input array and returns the
number of inversions in the array */
function mergeSort(arr, N) {

    return _mergeSort(arr, 0, N - 1);
}

function possibleSortingBy3SizeSubarray(arr, N) {
    let numberOfInversion = mergeSort(arr, N);

    // if number of inversions are even then only
    // we can sort the array
    return (numberOfInversion % 2 == 0);
}

// Driver code to test above methods

let arr = [1, 3, 4, 2];
let N = arr.length;

if (possibleSortingBy3SizeSubarray(arr, N))
    document.write("Yes");
else
    document.write("No");

</script>
```

**输出:**

```
Yes
```

时间复杂度:O(n Log n)
本文由[T2【Utkarsh Trivedi】T4 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。