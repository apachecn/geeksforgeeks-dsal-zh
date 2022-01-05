# 打印所有等于给定数 x 的和的非递增序列

> 原文:[https://www . geeksforgeeks . org/print-all-non-递增-给定数字的和序列/](https://www.geeksforgeeks.org/print-all-non-increasing-sequences-of-sum-equal-to-a-given-number/)

给定一个数字 x，打印总和等于 x 的所有可能的非递增序列。

示例:

```
Input: x = 3
Output: 1 1 1
        2 1
        3

Input: x = 4
Output: 1 1 1 1
        2 1 1
        2 2
        3 1
        4
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
这个想法是使用递归函数，一个数组 arr[]来逐个存储所有序列，一个索引变量 curr_idx 来存储 arr[]中的当前下一个索引。下面是算法。
1)如果当前总和等于 x，则打印当前序列。
2)将从 1 到 x-curr_sum 的所有可能的数字放在数组中的 curr_idx 处。这里 curr_sum 是 arr[]中当前元素的总和。放置数字后，对 curr_sum + number 和 curr_idx+1 进行循环。

下面是以上步骤的实现。

## C++

```
// C++ program to generate all non-increasing
// sequences of sum equals to x
#include<bits/stdc++.h>
using namespace std;

// Utility function to print array
// arr[0..n-1]
void printArr(int arr[], int n)
{
    for(int i = 0; i < n; i++)
      cout << arr[i] << " ";
    cout << endl;
}

// Recursive Function to generate all
// non-increasing sequences
// with sum x
// arr[]    --> Elements of current sequence
// curr_sum --> Current Sum
// curr_idx --> Current index in arr[]
void generateUtil(int x, int arr[], int curr_sum,
                                    int curr_idx)
{

   // If current sum is equal to x,
   // then we found a sequence
   if (curr_sum == x)
   {
      printArr(arr, curr_idx);
      return;
   }

   // Try placing all numbers from
   // 1 to x-curr_sum at current index
   int num = 1;

   // The placed number must also be
   // smaller than previously placed
   // numbers and it may be equal to
   // the previous stored value, i.e.,
   // arr[curr_idx-1] if there exists
   // a previous number
   while (num <= x - curr_sum &&
         (curr_idx == 0 ||
          num <= arr[curr_idx - 1]))
   {

       // Place number at curr_idx
       arr[curr_idx] = num;

       // Recur
       generateUtil(x, arr, curr_sum + num,
                            curr_idx + 1);

       // Try next number
       num++;
   }
}

// A wrapper over generateUtil()
void generate(int x)
{

    // Array to store sequences on by one
    int arr[x];
    generateUtil(x, arr, 0, 0);
}

// Driver code
int main()
{
    int x = 5;
    generate(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate all non-increasing
// sequences of sum equals to x
class GFG {

    // Utility function to print array
    // arr[0..n-1]
    static void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.printf("%d ", arr[i]);

        System.out.println("");
    }

    // Recursive Function to generate all
    // non-increasing sequences with sum x
    // arr[] --> Elements of current sequence
    // curr_sum --> Current Sum
    // curr_idx --> Current index in arr[]
    static void generateUtil(int x, int arr[],
                     int curr_sum, int curr_idx)
    {

        // If current sum is equal to x, then
        // we found a sequence
        if (curr_sum == x)
        {
            printArr(arr, curr_idx);
            return;
        }

        // Try placing all numbers from 1 to
        // x-curr_sum at current index
        int num = 1;

        // The placed number must also be
           // smaller than previously placed
           // numbers and it may be equal to
           // the previous stored value, i.e.,
           // arr[curr_idx-1] if there exists
           // a previous number
        while (num <= x - curr_sum &&
                             (curr_idx == 0 ||
                     num <= arr[curr_idx - 1]))
        {

            // Place number at curr_idx
            arr[curr_idx] = num;

            // Recur
            generateUtil(x, arr, curr_sum+num,
                                     curr_idx + 1);

            // Try next number
            num++;
        }
    }

    // A wrapper over generateUtil()
    static void generate(int x)
    {

        // Array to store sequences on by one
        int arr[] = new int [x];
        generateUtil(x, arr, 0, 0);
    }

    // Driver program
    public static void main(String[] args)
    {
        int x = 5;
        generate(x);
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python3 program to generate all
# non-increasing sequences of sum
# equals to x

# Utility function to print array
# arr[0..n-1]
def printArr(arr, n):

    for i in range(0, n):
        print(arr[i], end = " ")

    print("")

# Recursive Function to generate
# all non-increasing sequences
# with sum x arr[] --> Elements
# of current sequence
# curr_sum --> Current Sum
# curr_idx --> Current index in
# arr[]
def generateUtil(x, arr, curr_sum,
                         curr_idx):

# If current sum is equal to x,
# then we found a sequence
    if (curr_sum == x):

        printArr(arr, curr_idx)
        return

    # Try placing all numbers from
    # 1 to x-curr_sum at current
    # index
    num = 1

    # The placed number must also be
    # smaller than previously placed
    # numbers and it may be equal to
    # the previous stored value, i.e.,
    # arr[curr_idx-1] if there exists
    # a previous number
    while (num <= x - curr_sum and
                (curr_idx == 0 or
           num <= arr[curr_idx - 1])):

        # Place number at curr_idx
        arr[curr_idx] = num

        # Recur
        generateUtil(x, arr,
            curr_sum + num, curr_idx + 1)

        # Try next number
        num += 1

# A wrapper over generateUtil()
def generate(x):

    # Array to store sequences
    # on by one
    arr = [0] * x
    generateUtil(x, arr, 0, 0)

# Driver program
x = 5
generate(x)

# This code is contributed
# by Smitha.
```

## C#

```
// C# program to generate all non-increasing
// sequences of sum equals to x
using System;

class GFG {

    // Utility function to print array
    // arr[0..n-1]
    static void printArr(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write( arr[i]);

        Console.WriteLine();
    }

    // Recursive Function to generate all
    // non-increasing sequences with sum x
    // arr[] --> Elements of current sequence
    // curr_sum --> Current Sum
    // curr_idx --> Current index in arr[]
    static void generateUtil(int x, int []arr,
                     int curr_sum, int curr_idx)
    {

        // If current sum is equal to x, then
        // we found a sequence
        if (curr_sum == x)
        {
            printArr(arr, curr_idx);
            return;
        }

        // Try placing all numbers from 1 to
        // x-curr_sum at current index
        int num = 1;

        // The placed number must also be
        // smaller than previously placed
           // numbers and it may be equal to
           // the previous stored value, i.e.,
           // arr[curr_idx-1] if there exists
           // a previous number
        while (num <= x - curr_sum &&
                             (curr_idx == 0 ||
                     num <= arr[curr_idx - 1]))
        {

            // Place number at curr_idx
            arr[curr_idx] = num;

            // Recur
            generateUtil(x, arr, curr_sum+num,
                                     curr_idx + 1);

            // Try next number
            num++;
        }
    }

    // A wrapper over generateUtil()
    static void generate(int x)
    {

        // Array to store sequences on by one
        int []arr = new int [x];
        generateUtil(x, arr, 0, 0);
    }

    // Driver program
    public static void Main()
    {
        int x = 5;
        generate(x);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate all
// non-increasing sequences
// of sum equals to x

// function to print array
// arr[0..n-1]
function printArr($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    echo $arr[$i] , " ";
    echo " \n";
}

// Recursive Function to generate
// all non-increasing sequences
// with sum x
// arr[] --> Elements of current sequence
// curr_sum --> Current Sum
// curr_idx --> Current index in arr[]
function generateUtil($x, $arr, $curr_sum,
                                $curr_idx)
{

    // If current sum is equal to x,
    // then we found a sequence
    if ($curr_sum == $x)
    {
        printArr($arr, $curr_idx);
        return;
    }

    // Try placing all numbers from
    // 1 to x-curr_sum at current index
    $num = 1;

    // The placed number must also be
    // smaller than previously placed
    // numbers and it may be equal to
    // the previous stored value, i.e.,
    // arr[curr_idx-1] if there exists
    // a previous number
    while ($num <= $x - $curr_sum and
          ($curr_idx == 0 or $num <=
                $arr[$curr_idx - 1]))
    { 
        // Place number at curr_idx
        $arr[$curr_idx] = $num;

        // Recur
        generateUtil($x, $arr, $curr_sum +
                     $num, $curr_idx + 1);

        // Try next number
        $num++;
    }
}

// A wrapper over generateUtil()
function generate($x)
{
    // Array to store
    // sequences on by one
    $arr = array();
    generateUtil($x, $arr, 0, 0);
}

    // Driver Code
    $x = 5;
    generate($x);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to generate all
// non-increasing sequences of sum equals to x

// Utility function to print array
// arr[0..n-1]
function printArr(arr, n)
{
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ");

    document.write("</br>");
}

// Recursive Function to generate all
// non-increasing sequences with sum x
// arr[] --> Elements of current sequence
// curr_sum --> Current Sum
// curr_idx --> Current index in arr[]
function generateUtil(x, arr, curr_sum, curr_idx)
{

    // If current sum is equal to x, then
    // we found a sequence
    if (curr_sum == x)
    {
        printArr(arr, curr_idx);
        return;
    }

    // Try placing all numbers from 1 to
    // x-curr_sum at current index
    let num = 1;

    // The placed number must also be
    // smaller than previously placed
    // numbers and it may be equal to
    // the previous stored value, i.e.,
    // arr[curr_idx-1] if there exists
    // a previous number
    while (num <= x - curr_sum &&
          (curr_idx == 0 ||
          num <= arr[curr_idx - 1]))
    {

        // Place number at curr_idx
        arr[curr_idx] = num;

        // Recur
        generateUtil(x, arr, curr_sum + num,
                             curr_idx + 1);

        // Try next number
        num++;
    }
}

// A wrapper over generateUtil()
function generate(x)
{

    // Array to store sequences on by one
    let arr = new Array(x);
    generateUtil(x, arr, 0, 0);
}

// Driver code  
let x = 5;

generate(x);

// This code is contributed by divyeshrabadiya07    

</script>
```

**输出:**

```
1 1 1 1 1
2 1 1 1
2 2 1
3 1 1
3 2
4 1
5
```

本文由**阿希什·古普塔**投稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息