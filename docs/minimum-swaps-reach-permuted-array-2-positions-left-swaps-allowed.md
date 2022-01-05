# 到达置换数组的最小互换，最多允许 2 个位置的剩余互换

> 原文:[https://www . geesforgeks . org/minimum-swaps-reach-置换-array-2-positions-left-swaps-allowed/](https://www.geeksforgeeks.org/minimum-swaps-reach-permuted-array-2-positions-left-swaps-allowed/)

给定长度为 N 的前 N 个自然数的置换数组，我们需要知道在排序后的前 N 个自然数数组中达到给定置换数组所需的最小交换次数，其中一个数最多可以交换 2 个位置。如果上述交换条件无法到达置换数组，则无法打印。

**示例:**

```
Input : arr = [1, 2, 5, 3, 4]
Output : 2
We can reach to above-permuted array 
in total 2 swaps as shown below,
[1, 2, 3, 4, 5] -> [1, 2, 3, 5, 4] -> 
[1, 2, 5, 3, 4]

Input : arr[] = [5, 1, 2, 3, 4]
Output : Not Possible
It is not possible to reach above array 
just by swapping numbers 2 positions left
to it.
```

我们可以用[反演](https://www.geeksforgeeks.org/counting-inversions/)来解决这个问题。我们可以看到，如果一个数的位置距离它的实际位置超过 2 个位置，那么仅仅通过与左边 2 个位置的元素交换是不可能到达那里的，如果所有元素都满足这个性质(右边有< =2 个比它小的元素)，那么答案将仅仅是数组中逆序的总数，因为将数组转换成置换数组需要许多交换。
我们可以使用合并排序技术找到 N log N 时间内的反演次数[这里解释](https://www.geeksforgeeks.org/counting-inversions/)所以解的总时间复杂度将仅为 O(N log N)。

## C++

```
// C++ program to find minimum number of swaps
// to reach a permutation with at most 2 left
// swaps allowed for every element
#include <bits/stdc++.h>
using namespace std;

/* This funt merges two sorted arrays and returns inversion
   count in the arrays.*/
int merge(int arr[], int temp[], int left, int mid, int right)
{
    int inv_count = 0;

    int i = left; /* i is index for left subarray*/
    int j = mid;  /* j is index for right subarray*/
    int k = left; /* k is index for resultant merged subarray*/
    while ((i <= mid - 1) && (j <= right))
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
        {
            temp[k++] = arr[j++];
            inv_count = inv_count + (mid - i);
        }
    }

    /* Copy the remaining elements of left subarray
    (if there are any) to temp*/
    while (i <= mid - 1)
        temp[k++] = arr[i++];

    /* Copy the remaining elements of right subarray
    (if there are any) to temp*/
    while (j <= right)
       temp[k++] = arr[j++];

    /*Copy back the merged elements to original array*/
    for (i = left; i <= right; i++)
        arr[i] = temp[i];

    return inv_count;
}

/* An auxiliary recursive function that sorts the
   input array and returns the number of inversions
   in the array. */
int _mergeSort(int arr[], int temp[], int left, int right)
{
    int mid, inv_count = 0;
    if (right > left)
    {
        /* Divide the array into two parts and
           call _mergeSortAndCountInv() for each
           of the parts */
        mid = (right + left)/2;

        /* Inversion count will be sum of inversions
          in left-part, right-part and number of inversions
          in merging */
        inv_count  = _mergeSort(arr, temp, left, mid);
        inv_count += _mergeSort(arr, temp, mid+1, right);

        /*Merge the two parts*/
        inv_count += merge(arr, temp, left, mid+1, right);
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

// method returns minimum number of swaps to reach
// permuted array 'arr'
int minSwapToReachArr(int arr[], int N)
{
    //  loop over all elements to check Invalid
    // permutation condition
    for (int i = 0; i < N; i++)
    {
        /*  if an element is at distance more than 2
            from its actual position then it is not
            possible to reach permuted array just
            by swapping with 2 positions left elements
            so returning -1   */
        if ((arr[i] - 1) - i > 2)
            return -1;
    }

    /*  If permuted array is not Invalid, then number
        of Inversion in array will be our final answer */
    int numOfInversion = mergeSort(arr, N);
    return numOfInversion;
}

//  Driver code to test above methods
int main()
{
    //  change below example
    int arr[] = {1, 2, 5, 3, 4};
    int N = sizeof(arr) / sizeof(int);
    int res = minSwapToReachArr(arr, N);
    if (res == -1)
        cout << "Not Possible\n";
    else
        cout << res << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number of swaps to reach a
// permutation with at most 2 left
// swaps allowed for every element
class GFG
{

    /* This funt merges two sorted
    arrays and returns inversion
    count in the arrays.*/
    static int merge(int arr[], int temp[], int left,
                                int mid, int right)
    {
        int inv_count = 0;

        int i = left;

        /* i is index for left subarray*/
        int j = mid;

        /* j is index for right subarray*/
        int k = left;

        /* k is index for resultant merged subarray*/
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
            {
                temp[k++] = arr[i++];
            }
            else
            {
                temp[k++] = arr[j++];
                inv_count = inv_count + (mid - i);
            }
        }

        /* Copy the remaining elements
        of left subarray (if there
         are any) to temp*/
        while (i <= mid - 1)
        {
            temp[k++] = arr[i++];
        }

        /* Copy the remaining elements
        of right subarray (if there
        are any) to temp*/
        while (j <= right)
        {
            temp[k++] = arr[j++];
        }

        /* Copy back the merged elements
        to original array*/
        for (i = left; i <= right; i++)
        {
            arr[i] = temp[i];
        }

        return inv_count;
    }

    /* An auxiliary recursive function
     that sorts the input array and
     returns the number of inversions
    in the array. */
    static int _mergeSort(int arr[], int temp[],
                            int left, int right)
    {
        int mid, inv_count = 0;
        if (right > left)
        {
            /* Divide the array into two parts and
            call _mergeSortAndCountInv() for each
            of the parts */
            mid = (right + left) / 2;

            /* Inversion count will be sum of inversions
            in left-part, right-part and number of inversions
            in merging */
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid + 1, right);

            /* Merge the two parts*/
            inv_count += merge(arr, temp, left, mid + 1, right);
        }
        return inv_count;
    }

    /* This function sorts the input array and returns the
    number of inversions in the array */
    static int mergeSort(int arr[], int array_size)
    {
        int[] temp = new int[array_size];
        return _mergeSort(arr, temp, 0, array_size - 1);
    }

    // method returns minimum number of 
    // swaps to reach permuted array 'arr'
    static int minSwapToReachArr(int arr[], int N)
    {
        // loop over all elements to check Invalid
        // permutation condition
        for (int i = 0; i < N; i++)
        {
            /* if an element is at distance more than 2
            from its actual position then it is not
            possible to reach permuted array just
            by swapping with 2 positions left elements
            so returning -1 */
            if ((arr[i] - 1) - i > 2)
            {
                return -1;
            }
        }

        /* If permuted array is not Invalid, then number
        of Inversion in array will be our final answer */
        int numOfInversion = mergeSort(arr, N);
        return numOfInversion;
    }

    // Driver code
    public static void main(String[] args)
    {

        // change below example
        int arr[] = {1, 2, 5, 3, 4};
        int N = arr.length;
        int res = minSwapToReachArr(arr, N);
        System.out.println(res == -1 ? "Not Possible\n" : res);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find minimum number of
# swaps to reach a permutation with at most
# 2 left swaps allowed for every element

# This funt merges two sorted arrays and
# returns inversion count in the arrays.
def merge(arr, temp, left, mid, right):

    inv_count = 0

    i = left # i is index for left subarray
    j = mid # j is index for right subarray
    k = left # k is index for resultant merged subarray
    while (i <= mid - 1) and (j <= right):

        if arr[i] <= arr[j]:
            temp[k] = arr[i]
            k, i = k + 1, i + 1

        else:
            temp[k] = arr[j]
            k, j = k + 1, j + 1
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

    # Copy back the merged elements to original array
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

# method returns minimum number of
# swaps to reach permuted array 'arr'
def minSwapToReachArr(arr, N):

    # loop over all elements to check
    # Invalid permutation condition
    for i in range(0, N):

        # if an element is at distance more than 2
        # from its actual position then it is not
        # possible to reach permuted array just
        # by swapping with 2 positions left elements
        # so returning -1
        if (arr[i] - 1) - i > 2:
            return -1

    # If permuted array is not Invalid, then number
    # of Inversion in array will be our final answer
    numOfInversion = mergeSort(arr, N)
    return numOfInversion

# Driver code to test above methods
if __name__ == "__main__":

    # change below example
    arr = [1, 2, 5, 3, 4]
    N = len(arr)
    res = minSwapToReachArr(arr, N)
    if res == -1:
        print("Not Possible")
    else:
        print(res)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find minimum
// number of swaps to reach a
// permutation with at most 2 left
// swaps allowed for every element
using System;
class GFG
{

    /* This funt merges two sorted
    arrays and returns inversion
    count in the arrays.*/
    static int merge(int []arr, int []temp,
                     int left, int mid, int right)
    {
        int inv_count = 0;

        int i = left;

        /* i is index for left subarray*/
        int j = mid;

        /* j is index for right subarray*/
        int k = left;

        /* k is index for resultant merged subarray*/
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
            {
                temp[k++] = arr[i++];
            }
            else
            {
                temp[k++] = arr[j++];
                inv_count = inv_count + (mid - i);
            }
        }

        /* Copy the remaining elements
        of left subarray (if there
        are any) to temp*/
        while (i <= mid - 1)
        {
            temp[k++] = arr[i++];
        }

        /* Copy the remaining elements
        of right subarray (if there
        are any) to temp*/
        while (j <= right)
        {
            temp[k++] = arr[j++];
        }

        /* Copy back the merged elements
        to original array*/
        for (i = left; i <= right; i++)
        {
            arr[i] = temp[i];
        }

        return inv_count;
    }

    /* An auxiliary recursive function
    that sorts the input array and
    returns the number of inversions
    in the array. */
    static int _mergeSort(int []arr, int []temp,
                          int left, int right)
    {
        int mid, inv_count = 0;
        if (right > left)
        {
            /* Divide the array into two parts and
            call _mergeSortAndCountInv() for each
            of the parts */
            mid = (right + left) / 2;

            /* Inversion count will be sum of inversions
            in left-part, right-part and number of inversions
            in merging */
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid + 1, right);

            /* Merge the two parts*/
            inv_count += merge(arr, temp, left, mid + 1, right);
        }
        return inv_count;
    }

    /* This function sorts the input array and returns
    the number of inversions in the array */
    static int mergeSort(int []arr, int array_size)
    {
        int[] temp = new int[array_size];
        return _mergeSort(arr, temp, 0, array_size - 1);
    }

    // method returns minimum number of
    // swaps to reach permuted array 'arr'
    static int minSwapToReachArr(int []arr, int N)
    {
        // loop over all elements to check Invalid
        // permutation condition
        for (int i = 0; i < N; i++)
        {
            /* if an element is at distance more than 2
            from its actual position then it is not
            possible to reach permuted array just
            by swapping with 2 positions left elements
            so returning -1 */
            if ((arr[i] - 1) - i > 2)
            {
                return -1;
            }
        }

        /* If permuted array is not Invalid, then number
        of Inversion in array will be our final answer */
        int numOfInversion = mergeSort(arr, N);
        return numOfInversion;
    }

    // Driver code
    static void Main()
    {

        // change below example
        int []arr = {1, 2, 5, 3, 4};
        int N = arr.Length;
        int res = minSwapToReachArr(arr, N);
        if(res == -1)
        Console.WriteLine("Not Possible");
        else
        Console.WriteLine(res);
    }
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// JavaScript program to find minimum
// number of swaps to reach a
// permutation with at most 2 left
// swaps allowed for every element

    /* This funt merges two sorted
    arrays and returns inversion
    count in the arrays.*/
    function merge(arr, temp, left,
                                mid, right)
    {
        let inv_count = 0;

        let i = left;

        /* i is index for left subarray*/
        let j = mid;

        /* j is index for right subarray*/
        let k = left;

        /* k is index for resultant merged subarray*/
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
            {
                temp[k++] = arr[i++];
            }
            else
            {
                temp[k++] = arr[j++];
                inv_count = inv_count + (mid - i);
            }
        }

        /* Copy the remaining elements
        of left subarray (if there
         are any) to temp*/
        while (i <= mid - 1)
        {
            temp[k++] = arr[i++];
        }

        /* Copy the remaining elements
        of right subarray (if there
        are any) to temp*/
        while (j <= right)
        {
            temp[k++] = arr[j++];
        }

        /* Copy back the merged elements
        to original array*/
        for (i = left; i <= right; i++)
        {
            arr[i] = temp[i];
        }

        return inv_count;
    }

    /* An auxiliary recursive function
     that sorts the input array and
     returns the number of inversions
    in the array. */
    function _mergeSort(arr, temp, left, right)
    {
        let mid, inv_count = 0;
        if (right > left)
        {
            /* Divide the array into two parts and
            call _mergeSortAndCountInv() for each
            of the parts */
            mid = (right + left) / 2;

            /* Inversion count will be sum of inversions
            in left-part, right-part and number of inversions
            in merging */
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid + 1, right);

            /* Merge the two parts*/
            inv_count += merge(arr, temp, left, mid + 1, right);
        }
        return inv_count;
    }

    /* This function sorts the input array and returns the
    number of inversions in the array */
    function mergeSort(arr, array_size)
    {
        let temp = Array.from({length: array_size}, (_, i) => 0);
        return _mergeSort(arr, temp, 0, array_size - 1);
    }

    // method returns minimum number of 
    // swaps to reach permuted array 'arr'
    function minSwapToReachArr(arr, N)
    {
        // loop over all elements to check Invalid
        // permutation condition
        for (let i = 0; i < N; i++)
        {
            /* if an element is at distance more than 2
            from its actual position then it is not
            possible to reach permuted array just
            by swapping with 2 positions left elements
            so returning -1 */
            if ((arr[i] - 1) - i > 2)
            {
                return -1;
            }
        }

        /* If permuted array is not Invalid, then number
        of Inversion in array will be our final answer */
        let numOfInversion = mergeSort(arr, N);
        return numOfInversion;
    }

// Driver Code

     // change below example
        let arr = [1, 2, 5, 3, 4];
        let N = arr.length;
        let res = minSwapToReachArr(arr, N);
        document.write(res == -1 ? "Not Possible\n" : res);

</script>
```

**输出:**

```
2
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。