# 稳定排序后元素的位置

> 原文:[https://www.geeksforgeeks.org/position-element-stable-sort/](https://www.geeksforgeeks.org/position-element-stable-sort/)

给定一个可能包含重复元素的整数数组，这个数组的一个元素就给了我们，如果应用稳定的排序算法，我们需要告诉这个元素在数组中的最终位置。
**例:**

```
Input  : arr[] = [3, 4, 3, 5, 2, 3, 4, 3, 1, 5], index = 5
Output : 4
Element initial index – 5 (third 3)
After sorting array by stable sorting algorithm, we get 
array as shown below
[1(8), 2(4), 3(0), 3(2), 3(5), 3(7), 4(1), 4(6), 5(3), 5(9)]
with their initial indices shown in parentheses next to them,
Element's index after sorting = 4
```

解决这个问题的一个简单方法是使用任何稳定的排序算法，如[插入排序](//quiz.geeksforgeeks.org/insertion-sort/”)、[合并排序](//quiz.geeksforgeeks.org/merge-sort/”)等，然后获得给定元素的新索引，但是我们可以在不排序数组的情况下解决这个问题。
因为元素在排序数组中的位置仅由小于给定元素的元素决定。我们计算所有小于给定元素的数组元素，对于那些等于给定元素的元素，在给定元素的索引之前出现的元素将包含在较小元素的计数中，这将确保结果索引的稳定性。
实现上述方法的简单代码如下:

## C++

```
// C++ program to get index of array element in
// sorted array
#include <bits/stdc++.h>
using namespace std;

// Method returns the position of arr[idx] after
// performing stable-sort on array
int getIndexInSortedArray(int arr[], int n, int idx)
{
    /* Count of elements smaller than current
        element plus the equal element occurring
        before given index*/
    int result = 0;
    for (int i = 0; i < n; i++) {
        // If element is smaller then increase
        // the smaller count
        if (arr[i] < arr[idx])
            result++;

        // If element is equal then increase count
        // only if it occurs before
        if (arr[i] == arr[idx] && i < idx)
            result++;
    }
    return result;
}

// Driver code to test above methods
int main()
{
    int arr[] = { 3, 4, 3, 5, 2, 3, 4, 3, 1, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int idxOfEle = 5;
    cout << getIndexInSortedArray(arr, n, idxOfEle);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get index of array
// element in sorted array

class ArrayIndex {

    // Method returns the position of
    // arr[idx] after performing stable-sort
    // on array
    static int getIndexInSortedArray(int arr[],
                                     int n, int idx)
    {
        /*  Count of elements smaller than
        current element plus the equal element
        occurring before given index*/
        int result = 0;
        for (int i = 0; i < n; i++) {

            // If element is smaller then
            // increase the smaller count
            if (arr[i] < arr[idx])
                result++;

            // If element is equal then increase
            // count only if it occurs before
            if (arr[i] == arr[idx] && i < idx)
                result++;
        }
        return result;
    }

    // Driver code to test above methods
    public static void main(String[] args)
    {
        int arr[] = { 3, 4, 3, 5, 2, 3, 4, 3, 1, 5 };
        int n = arr.length;

        int idxOfEle = 5;
        System.out.println(getIndexInSortedArray(arr,
                                                 n, idxOfEle));
    }
}

// This code is contributed by Raghav sharma
```

## 计算机编程语言

```
# Python program to get index of array element in
# sorted array
# Method returns the position of arr[idx] after
# performing stable-sort on array

def getIndexInSortedArray(arr, n, idx):
       # Count of elements smaller than current
       # element plus the equal element occurring
       # before given index
    result = 0
    for i in range(n):
        # If element is smaller then increase
        # the smaller count
        if (arr[i] < arr[idx]):
            result += 1

        # If element is equal then increase count
        # only if it occurs before
        if (arr[i] == arr[idx] and i < idx):
            result += 1
    return result;

# Driver code to test above methods
arr = [3, 4, 3, 5, 2, 3, 4, 3, 1, 5]
n = len(arr)

idxOfEle = 5
print getIndexInSortedArray(arr, n, idxOfEle)

# Contributed by: Afzal Ansari
```

## C#

```
// C# program to get index of array
// element in sorted array
using System;

class ArrayIndex {

    // Method returns the position of
    // arr[idx] after performing stable-sort
    // on array
    static int getIndexInSortedArray(int[] arr,
                                     int n, int idx)
    {
        /* Count of elements smaller than
        current element plus the equal element
        occurring before given index*/
        int result = 0;
        for (int i = 0; i < n; i++) {

            // If element is smaller then
            // increase the smaller count
            if (arr[i] < arr[idx])
                result++;

            // If element is equal then increase
            // count only if it occurs before
            if (arr[i] == arr[idx] && i < idx)
                result++;
        }
        return result;
    }

    // Driver code to test above methods
    public static void Main()
    {
        int[] arr = { 3, 4, 3, 5, 2, 3, 4, 3, 1, 5 };
        int n = arr.Length;

        int idxOfEle = 5;
        Console.WriteLine(getIndexInSortedArray(arr, n,
                                            idxOfEle));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get index of
// array element in sorted array

// Method returns the position of
// arr[idx] after performing
// stable-sort on array
function getIndexInSortedArray( $arr, $n, $idx)
{

    /* Count of elements smaller
       than current    element plus
       the equal element occurring
       before given index */
    $result = 0;
    for($i = 0; $i < $n; $i++)
    {

        // If element is smaller then
        // increase the smaller count
        if ($arr[$i] < $arr[$idx])
            $result++;

        // If element is equal then
        // increase count only if
        // it occurs before
        if ($arr[$i] == $arr[$idx] and
                           $i < $idx)
            $result++;
    }
    return $result;
}

    // Driver Code
    $arr = array(3, 4, 3, 5, 2, 3, 4, 3, 1, 5);
    $n =count($arr);

    $idxOfEle = 5;
    echo getIndexInSortedArray($arr, $n,
                             $idxOfEle);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to get index of array
// element in sorted array

    // Method returns the position of
    // arr[idx] after performing stable-sort
    // on array
    function getIndexInSortedArray(arr,
                                     n, idx)
    {
        /*  Count of elements smaller than
        current element plus the equal element
        occurring before given index*/
        let result = 0;
        for (let i = 0; i < n; i++) {

            // If element is smaller then
            // increase the smaller count
            if (arr[i] < arr[idx])
                result++;

            // If element is equal then increase
            // count only if it occurs before
            if (arr[i] == arr[idx] && i < idx)
                result++;
        }
        return result;
    }

// Driver Code
        let arr = [ 3, 4, 3, 5, 2, 3, 4, 3, 1, 5 ];
        let n = arr.length;

        let idxOfEle = 5;
        document.write(getIndexInSortedArray(arr,
                                                 n, idxOfEle));

// This code is contributed by code_hunt.                                                
</script>
```

输出:

```
4
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。