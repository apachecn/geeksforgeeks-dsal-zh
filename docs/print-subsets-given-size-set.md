# 打印一组给定大小的所有子集

> 原文:[https://www.geeksforgeeks.org/print-subsets-given-size-set/](https://www.geeksforgeeks.org/print-subsets-given-size-set/)

用不同的元素生成给定数组的所有可能的大小子集。

**示例:**

```
Input  : arr[] = {1, 2, 3, 4}
         r = 2
Output :  1 2
          1 3
          1 4
          2 3
          2 4
          3 4

Input  : arr[] = {10, 20, 30, 40, 50}
         r = 3
Output : 10 20 30 
         10 20 40 
         10 20 50 
         10 30 40 
         10 30 50 
         10 40 50 
         20 30 40 
         20 30 50 
         20 40 50 
         30 40 50 
```

这个问题是一样的[打印给定大小 n 的数组中 r 元素的所有可能组合](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)。
这里的思路类似于[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)。我们逐一考虑输入数组的每一个元素，并针对两种情况重复出现:
1)元素包含在当前组合中(我们将元素放入 data【】中，并增加 data【】中的下一个可用索引)
2)元素排除在当前组合中(我们不放入元素，也不改变索引)
当 data【】中的元素数量变为等于 r(组合的大小)时，我们打印它。
该方法主要基于帕斯卡恒等式，即**n<sub>Cr</sub>= n-1<sub>Cr</sub>+n-1<sub>Cr-1</sub>T16】**

## C++

```
// C++ Program to print all combination of size r in
// an array of size n
#include <iostream>
using namespace std;

void combinationUtil(int arr[], int n, int r,
                     int index, int data[], int i);

// The main function that prints all combinations of
// size r in arr[] of size n. This function mainly
// uses combinationUtil()
void printCombination(int arr[], int n, int r)
{

    // A temporary array to store all combination
    // one by one
    int data[r];

    // Print all combination using temporary array 'data[]'
    combinationUtil(arr, n, r, 0, data, 0);
}

/* arr[]  ---> Input Array
   n      ---> Size of input array
   r      ---> Size of a combination to be printed
   index  ---> Current index in data[]
   data[] ---> Temporary array to store current combination
   i      ---> index of current element in arr[]     */
void combinationUtil(int arr[], int n, int r, int index,
                     int data[], int i)
{
    // Current combination is ready, print it
    if (index == r) {
        for (int j = 0; j < r; j++)
            cout <<" "<< data[j];
        cout <<"\n";
        return;
    }

    // When no more elements are there to put in data[]
    if (i >= n)
        return;

    // current is included, put next at next location
    data[index] = arr[i];
    combinationUtil(arr, n, r, index + 1, data, i + 1);

    // current is excluded, replace it with next
    // (Note that i+1 is passed, but index is not
    // changed)
    combinationUtil(arr, n, r, index, data, i + 1);
}

// Driver program to test above functions
int main()
{
    int arr[] = { 10, 20, 30, 40, 50 };
    int r = 3;
    int n = sizeof(arr) / sizeof(arr[0]);
    printCombination(arr, n, r);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C++ Program to print all combination of size r in
// an array of size n
#include <stdio.h>
void combinationUtil(int arr[], int n, int r,
                     int index, int data[], int i);

// The main function that prints all combinations of
// size r in arr[] of size n. This function mainly
// uses combinationUtil()
void printCombination(int arr[], int n, int r)
{
    // A temporary array to store all combination
    // one by one
    int data[r];

    // Print all combination using temporary array 'data[]'
    combinationUtil(arr, n, r, 0, data, 0);
}

/* arr[]  ---> Input Array
   n      ---> Size of input array
   r      ---> Size of a combination to be printed
   index  ---> Current index in data[]
   data[] ---> Temporary array to store current combination
   i      ---> index of current element in arr[]     */
void combinationUtil(int arr[], int n, int r, int index,
                     int data[], int i)
{
    // Current combination is ready, print it
    if (index == r) {
        for (int j = 0; j < r; j++)
            printf("%d ", data[j]);
        printf("\n");
        return;
    }

    // When no more elements are there to put in data[]
    if (i >= n)
        return;

    // current is included, put next at next location
    data[index] = arr[i];
    combinationUtil(arr, n, r, index + 1, data, i + 1);

    // current is excluded, replace it with next
    // (Note that i+1 is passed, but index is not
    // changed)
    combinationUtil(arr, n, r, index, data, i + 1);
}

// Driver program to test above functions
int main()
{
    int arr[] = { 10, 20, 30, 40, 50 };
    int r = 3;
    int n = sizeof(arr) / sizeof(arr[0]);
    printCombination(arr, n, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all combination of size
// r in an array of size n
import java.io.*;

class Permutation {

    /* arr[]  ---> Input Array
    data[] ---> Temporary array to store current combination
    start & end ---> Starting and Ending indexes in arr[]
    index  ---> Current index in data[]
    r ---> Size of a combination to be printed */
    static void combinationUtil(int arr[], int n, int r,
                          int index, int data[], int i)
    {
        // Current combination is ready to be printed,
        // print it
        if (index == r) {
            for (int j = 0; j < r; j++)
                System.out.print(data[j] + " ");
            System.out.println("");
            return;
        }

        // When no more elements are there to put in data[]
        if (i >= n)
            return;

        // current is included, put next at next
        // location
        data[index] = arr[i];
        combinationUtil(arr, n, r, index + 1,
                               data, i + 1);

        // current is excluded, replace it with
        // next (Note that i+1 is passed, but
        // index is not changed)
        combinationUtil(arr, n, r, index, data, i + 1);
    }

    // The main function that prints all combinations
    // of size r in arr[] of size n. This function
    // mainly uses combinationUtil()
    static void printCombination(int arr[], int n, int r)
    {
        // A temporary array to store all combination
        // one by one
        int data[] = new int[r];

        // Print all combination using temporary
        // array 'data[]'
        combinationUtil(arr, n, r, 0, data, 0);
    }

    /* Driver function to check for above function */
    public static void main(String[] args)
    {
        int arr[] = { 10, 20, 30, 40, 50 };
        int r = 3;
        int n = arr.length;
        printCombination(arr, n, r);
    }
}
/* This code is contributed by Devesh Agrawal */
```

## 蟒蛇 3

```
# Python3 program to print all
# subset combination of n
# element in given set of r element .

# arr[] ---> Input Array
# data[] ---> Temporary array to
#             store current combination
# start & end ---> Starting and Ending
#                  indexes in arr[]
# index ---> Current index in data[]
# r ---> Size of a combination
#        to be printed
def combinationUtil(arr, n, r,
                    index, data, i):
    # Current combination is
    # ready to be printed,
    # print it
    if(index == r):
        for j in range(r):
            print(data[j], end = " ")
        print(" ")
        return

    # When no more elements
    # are there to put in data[]
    if(i >= n):
        return

    # current is included,
    # put next at next
    # location
    data[index] = arr[i]
    combinationUtil(arr, n, r,
                    index + 1, data, i + 1)

    # current is excluded,
    # replace it with
    # next (Note that i+1
    # is passed, but index
    # is not changed)
    combinationUtil(arr, n, r, index,
                    data, i + 1)

# The main function that
# prints all combinations
# of size r in arr[] of
# size n. This function
# mainly uses combinationUtil()
def printcombination(arr, n, r):

    # A temporary array to
    # store all combination
    # one by one
    data = list(range(r))

    # Print all combination
    # using temporary
    # array 'data[]'
    combinationUtil(arr, n, r,
                    0, data, 0)

# Driver Code
arr = [10, 20, 30, 40, 50]

r = 3
n = len(arr)
printcombination(arr, n, r)

# This code is contributed
# by Ambuj sahu
```

## C#

```
// C# program to print all combination
// of size r in an array of size n
using System;

class GFG {

    /* arr[] ---> Input Array
    data[] ---> Temporary array to store
    current combination start & end --->
    Starting and Ending indexes in arr[]
    index ---> Current index in data[]
    r ---> Size of a combination to be
    printed */
    static void combinationUtil(int []arr,
                  int n, int r, int index,
                          int []data, int i)
    {

        // Current combination is ready to
        // be printed, print it
        if (index == r)
        {
            for (int j = 0; j < r; j++)
                Console.Write(data[j] + " ");

            Console.WriteLine("");

            return;
        }

        // When no more elements are there
        // to put in data[]
        if (i >= n)
            return;

        // current is included, put next
        // at next location
        data[index] = arr[i];
        combinationUtil(arr, n, r, index + 1,
                                data, i + 1);

        // current is excluded, replace
        // it with next (Note that i+1
        // is passed, but index is not
        // changed)
        combinationUtil(arr, n, r, index,
                                data, i + 1);
    }

    // The main function that prints all
    // combinations of size r in arr[] of
    // size n. This function mainly uses
    // combinationUtil()
    static void printCombination(int []arr,
                                int n, int r)
    {

        // A temporary array to store all
        // combination one by one
        int []data = new int[r];

        // Print all combination using
        // temporary array 'data[]'
        combinationUtil(arr, n, r, 0, data, 0);
    }

    /* Driver function to check for
    above function */
    public static void Main()
    {
        int []arr = { 10, 20, 30, 40, 50 };
        int r = 3;
        int n = arr.Length;

        printCombination(arr, n, r);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to print all combination of
// size r in an array of size n

// The main function that prints all
// combinations of size r in arr[] of
// size n. This function mainly uses
// combinationUtil()
function printCombination( $arr, $n, $r)
{
    // A temporary array to store all
    // combination one by one
    $data = array();

    // Print all combination using
    // temporary array 'data[]'
    combinationUtil($arr, $n, $r, 0, $data, 0);
}

/* arr[] ---> Input Array
n ---> Size of input array
r ---> Size of a combination to be printed
index ---> Current index in data[]
data[] ---> Temporary array to store
current combination
i ---> index of current element in arr[] */
function combinationUtil( $arr, $n, $r, $index,
                    $data, $i)
{
    // Current combination is ready, print it
    if ($index == $r) {
        for ( $j = 0; $j < $r; $j++)
            echo $data[$j]," ";
        echo "\n";
        return;
    }

    // When no more elements are there to
    // put in data[]
    if ($i >= $n)
        return;

    // current is included, put next at
    // next location
    $data[$index] = $arr[$i];
    combinationUtil($arr, $n, $r, $index + 1,
                              $data, $i + 1);

    // current is excluded, replace it with
    // next (Note that i+1 is passed, but
    // index is not changed)
    combinationUtil($arr, $n, $r, $index,
                            $data, $i + 1);
}

// Driver program to test above functions
    $arr = array( 10, 20, 30, 40, 50 );
    $r = 3;
    $n = count($arr);
    printCombination($arr, $n, $r);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to print all combination
    // of size r in an array of size n

    /* arr[] ---> Input Array
    data[] ---> Temporary array to store
    current combination start & end --->
    Starting and Ending indexes in arr[]
    index ---> Current index in data[]
    r ---> Size of a combination to be
    printed */
    function combinationUtil(arr, n, r, index, data, i)
    {

        // Current combination is ready to
        // be printed, print it
        if (index == r)
        {
            for (let j = 0; j < r; j++)
                document.write(data[j] + " ");

            document.write("</br>");

            return;
        }

        // When no more elements are there
        // to put in data[]
        if (i >= n)
            return;

        // current is included, put next
        // at next location
        data[index] = arr[i];
        combinationUtil(arr, n, r, index + 1,
                                data, i + 1);

        // current is excluded, replace
        // it with next (Note that i+1
        // is passed, but index is not
        // changed)
        combinationUtil(arr, n, r, index,
                                data, i + 1);
    }

    // The main function that prints all
    // combinations of size r in arr[] of
    // size n. This function mainly uses
    // combinationUtil()
    function printCombination(arr, n, r)
    {

        // A temporary array to store all
        // combination one by one
        let data = new Array(r);
        data.fill(0);

        // Print all combination using
        // temporary array 'data[]'
        combinationUtil(arr, n, r, 0, data, 0);
    }

    let arr = [ 10, 20, 30, 40, 50 ];
    let r = 3;
    let n = arr.length;

    printCombination(arr, n, r);

</script>
```

**输出:**

```
10 20 30 
10 20 40 
10 20 50 
10 30 40 
10 30 50 
10 40 50 
20 30 40 
20 30 50 
20 40 50 
30 40 50 
```

关于处理输入数组中重复项的更多解决方案和想法，请参考下面的帖子。
[打印给定大小 n 的数组中 r 元素的所有可能组合](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)。

本文由 **Dhiman Mayank** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。