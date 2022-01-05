# 使用恒定空间在线性时间内对大小为 3 的子序列进行排序

> 原文:[https://www . geesforgeks . org/sorted-subserial-size-3-linear-time-use-constant-space/](https://www.geeksforgeeks.org/sorted-subsequence-size-3-linear-time-using-constant-space/)

给定一个数组，任务是找到该数组的三个元素，使它们处于排序形式，即对于任意三个元素 a[i]、a[j]和 a[k]，它们遵循以下关系: **a[i] < a[j] < a[k]** ，其中 **i < j < k** 。这个问题必须使用**恒定空间**或者没有额外空间来解决。
这个问题已经用线性空间在线性时间里解决了: [**在线性时间里找到大小为 3 的排序子序列**](https://www.geeksforgeeks.org/find-a-sorted-subsequence-of-size-3-in-linear-time)
**示例:**

```
Input: arr[] = {12, 11, 10, 5, 2, 6, 30} 
Output: 5 6 30 
        or 2 6 30
Explanation: Answer is 5, 6, 30 because 5 < 6 < 30 
and they occur in this sequence in the array.

Input: arr[] = {5, 7, 4, 8}
Output: 5 7 8
Explanation: Answer is 5 ,7 ,8 because 5 < 7 < 8 
and they occur in the same sequence in the array 
```

**解:**目标是找到三个元素 **a、b** 、**和 c** ，使得 **a < b < c** ，元素在数组中必须以相同的顺序出现。
**方法:**该问题涉及找到三个元素 a、b、c，其中 a < b < c，并且它们必须以与数组中相同的顺序出现。所以任何一步的直觉都必须照此进行。其中一个变量*(小)*应该存储数组的最小元素，第二个变量*(大)*在*(小)*变量中已经有一个较小的值时会被赋值。这将导致形成一对两个变量，这将形成所需序列的前两个元素。类似地，如果在前两个变量已经赋值时，可以在赋值的数组中找到另一个值，并且该值小于当前元素，则第三个值的搜索将完成。这完成了三元组 a、b 和 c，使得 a < b < c 以与数组相似的顺序排列。
**<u>算法</u>**

1.  创建三个变量，*小的*–存储最小的元素，*大的*–存储序列的第二个元素，*I*–循环计数器
2.  从开始到结束沿着输入数组移动。
3.  如果当前元素小于或等于变量*小*，更新变量。
4.  否则，如果当前元素小于或等于变量*大于*，则更新该变量。所以在这一瞬间我们得到了一对*(小，大)*，其中*小<大*它们以所需的顺序出现。
5.  否则，如果前面两种情况不匹配，打破循环，因为我们得到了一对，其中当前元素大于两个变量*小*和*大*。将索引存储在变量 *i* 中。
6.  如果没有遇到 break 语句，那么可以保证不存在这样的三元组。
7.  否则有一个三元组满足标准，但变量*小*可能已被更新为新的较小值。
8.  所以遍历数组从开始到索引 I。
9.  将变量*小*重新分配给任何小于*大*的元素，保证存在一个。
10.  打印数值*小*、*大*和带数组元素

**<u>实施</u>**

## C++

```
// C/C++ program to find a sorted sub-sequence of
// size 3 using constant space
#include <bits/stdc++.h>
using namespace std;

// A function to fund a sorted sub-sequence of size 3
void find3Numbers(int arr[], int n)
{
    // Initializing small and large(second smaller)
    // by INT_MAX
    int small = INT_MAX, large = INT_MAX;
    int i;
    for (i = 0; i < n; i++)
    {
        // Update small for smallest value of array
        if (arr[i] <= small)
            small = arr[i];

        // Update large for second smallest value of
        // array after occurrence of small
        else if (arr[i] <= large)
            large = arr[i];

        // If we reach here, we found 3 numbers in
        // increasing order : small, large and arr[i]
        else
            break;
    }

    if (i == n)
    {
        printf("No such triplet found");
        return;
    }

    // last and second last will be same, but first
    // element can be updated retrieving first element
    // by looping upto i
    for (int j = 0; j <= i; j++)
    {
        if (arr[j] < large)
        {
            small = arr[j];
            break;
        }
    }

    printf("%d %d %d", small, large, arr[i]);
    return;
}

// Driver program to test above function
int main()
{
    int arr[] = {5, 7, 4, 8};
    int n = sizeof(arr)/sizeof(arr[0]);
    find3Numbers(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a sorted subsequence of
// size 3 using constant space

class GFG
{
    // A function to fund a sorted subsequence of size 3
    static void find3Numbers(int arr[], int n)
    {
        // Initializing small and large(second smaller)
        // by INT_MAX
        int small = +2147483647, large = +2147483647;
        int i;
        for (i = 0; i < n; i++)
        {
            // Update small for smallest value of array
            if (arr[i] <= small)
                small = arr[i];

            // Update large for second smallest value of
            // array after occurrence of small
            else if (arr[i] <= large)
                large = arr[i];

            // If we reach here, we found 3 numbers in
            // increasing order : small, large and arr[i]
            else
                break;
        }

        if (i == n)
        {
            System.out.print("No such triplet found");
            return;
        }

        // last and second last will be same, but first
        // element can be updated retrieving first element
        // by looping upto i
        for (int j = 0; j <= i; j++)
        {
            if (arr[j] < large)
            {
                small = arr[j];
                break;
            }
        }

        System.out.print(small+" "+large+" "+arr[i]);
        return;
    }

    // Driver program
    public static void main(String arg[])
    {
        int arr[] = {5, 7, 4, 8};
        int n = arr.length;
        find3Numbers(arr, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find a sorted subsequence
# of size 3 using constant space

# Function to fund a sorted subsequence of size 3
def find3Numbers(arr, n):

    # Initializing small and large(second smaller)
    # by INT_MAX
    small = +2147483647
    large = +2147483647

    for i in range(n):

        # Update small for smallest value of array
        if (arr[i] <= small):
            small = arr[i]

        # Update large for second smallest value of
        # array after occurrence of small
        elif (arr[i] <= large):
            large = arr[i]

        # If we reach here, we found 3 numbers in
        # increasing order : small, large and arr[i]
        else:
            break

    if (i == n):

        print("No such triplet found")
        return

    # last and second last will be same, but
    # first element can be updated retrieving
    # first element by looping upto i
    for j in range(i + 1):

        if (arr[j] < large):

            small = arr[j]
            break

    print(small," ",large," ",arr[i])
    return

# Driver program
arr= [5, 7, 4, 8]
n = len(arr)
find3Numbers(arr, n)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find a sorted sub-sequence of
// size 3 using constant space
using System;

class GFG {

    // A function to fund a sorted sub-sequence
    // of size 3
    static void find3Numbers(int []arr, int n)
    {

        // Initializing small and large(second smaller)
        // by INT_MAX
        int small = +2147483647, large = +2147483647;
        int i;
        for (i = 0; i < n; i++)
        {

            // Update small for smallest value of array
            if (arr[i] <= small)
                small = arr[i];

            // Update large for second smallest value of
            // array after occurrence of small
            else if (arr[i] <= large)
                large = arr[i];

            // If we reach here, we found 3 numbers in
            // increasing order : small, large and arr[i]
            else
                break;
        }

        if (i == n)
        {
            Console.Write("No such triplet found");
            return;
        }

        // last and second last will be same, but first
        // element can be updated retrieving first element
        // by looping upto i
        for (int j = 0; j <= i; j++)
        {
            if (arr[j] < large)
            {
                small = arr[j];
                break;
            }
        }

        Console.Write(small + " " + large + " " + arr[i]);
        return;
    }

    // Driver program
    public static void Main()
    {
        int []arr = {5, 7, 4, 8};
        int n = arr.Length;
        find3Numbers(arr, n);
    }
}
<br>

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a sorted
// subsequence of size 3 using
// constant space

// A function to fund a sorted
// subsequence of size 3
function find3Numbers($arr, $n)
{

    // Initializing small and
    // large(second smaller)
    // by INT_MAX
    $small = PHP_INT_MAX;
    $large = PHP_INT_MAX;
    $i;
    for($i = 0; $i < $n; $i++)
    {
        // Update small for smallest
        // value of array
        if ($arr[$i] <= $small)
            $small = $arr[$i];

        // Update large for second
        // smallest value of after
        // occurrence of small
        else if ($arr[$i] <= $large)
            $large = $arr[$i];

        // If we reach here, we
        // found 3 numbers in
        // increasing order :
        // small, large and arr[i]
        else
            break;
    }

    if ($i == $n)
    {
        echo "No such triplet found";
        return;
    }

    // last and second last will
    // be same, but first
    // element can be updated
    // retrieving first element
    // by looping upto i
    for($j = 0; $j <= $i; $j++)
    {
        if ($arr[$j] < $large)
        {
            $small = $arr[$j];
            break;
        }
    }

    echo $small," ", $large," ", $arr[$i];
    return;
}

    // Driver Code
    $arr = array(5, 7, 4, 8);
    $n = count($arr);
    find3Numbers($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find a
    // sorted sub-sequence of
    // size 3 using constant space

    // A function to fund a sorted sub-sequence
    // of size 3
    function find3Numbers(arr, n)
    {

        // Initializing small and large(second smaller)
        // by INT_MAX
        let small = +2147483647, large = +2147483647;
        let i;
        for (i = 0; i < n; i++)
        {

            // Update small for smallest value of array
            if (arr[i] <= small)
                small = arr[i];

            // Update large for second smallest value of
            // array after occurrence of small
            else if (arr[i] <= large)
                large = arr[i];

            // If we reach here, we found 3 numbers in
            // increasing order : small, large and arr[i]
            else
                break;
        }

        if (i == n)
        {
            document.write("No such triplet found");
            return;
        }

        // last and second last will be same, but first
        // element can be updated retrieving first element
        // by looping upto i
        for (let j = 0; j <= i; j++)
        {
            if (arr[j] < large)
            {
                small = arr[j];
                break;
            }
        }

        document.write(small + " " + large + " " + arr[i]);
        return;
    }

    let arr = [5, 7, 4, 8];
    let n = arr.length;
    find3Numbers(arr, n);

</script>
```

**输出:**

```
5 7 8
```

**<u>复杂度分析</u> :**

*   **时间复杂度:** O(n)。
    由于数组只遍历两次，时间复杂度为 **O(2*n)** ，等于 **O(n)** 。

*   **空间复杂度:** O(1)。
    由于只存储三个元素，空间复杂度不变或 **O(1)** 。

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。