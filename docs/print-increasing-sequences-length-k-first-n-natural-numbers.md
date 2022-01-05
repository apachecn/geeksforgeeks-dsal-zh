# 打印前 n 个自然数中长度为 k 的所有递增序列

> 原文:[https://www . geesforgeks . org/print-递增-sequence-length-k-first-n-natural-numbers/](https://www.geeksforgeeks.org/print-increasing-sequences-length-k-first-n-natural-numbers/)

给定两个正整数 n 和 k，打印所有长度为 k 的递增序列，使得每个序列中的元素都来自前 n 个自然数。

**示例:**

```
Input: k = 2, n = 3
Output: 1 2
        1 3
        2 3 

Input: k = 5, n = 5
Output: 1 2 3 4 5

Input: k = 3, n = 5
Output: 1 2 3
        1 2 4
        1 2 5
        1 3 4
        1 3 5
        1 4 5
        2 3 4
        2 3 5
        2 4 5
        3 4 5
```

**强烈建议尽量减少浏览器，先自己试试这个。**
这是一个很好的递归问题。其思想是创建一个长度为 k 的数组。该数组存储当前序列。对于数组中的每个位置，我们检查前一个元素，并一个接一个地放置大于前一个元素的所有元素。如果没有前一个元素(第一个位置)，我们把所有的数字从 1 到 n。

以下是上述想法的实现:

## C++

```
// C++ program to  print all increasing sequences of
// length 'k' such that the elements in every sequence
// are from first 'n' natural numbers.
#include<iostream>
using namespace std;

// A utility function to print contents of arr[0..k-1]
void printArr(int arr[], int k)
{
    for (int i=0; i<k; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// A recursive function to print all increasing sequences
// of first n natural numbers.  Every sequence should be
// length k. The array arr[] is used to store current
// sequence.
void printSeqUtil(int n, int k, int &len, int arr[])
{
    // If length of current increasing sequence becomes k,
    // print it
    if (len == k)
    {
        printArr(arr, k);
        return;
    }

    // Decide the starting number to put at current position:
    // If length is 0, then there are no previous elements
    // in arr[].  So start putting new numbers with 1.
    // If length is not 0, then start from value of
    // previous element plus 1.
    int i = (len == 0)? 1 : arr[len-1] + 1;

    // Increase length
    len++;

    // Put all numbers (which are greater than the previous
    // element) at new position.
    while (i<=n)
    {
        arr[len-1] = i;
        printSeqUtil(n, k, len, arr);
        i++;
    }

    // This is important. The variable 'len' is shared among
    // all function calls in recursion tree. Its value must be
    // brought back before next iteration of while loop
    len--;
}

// This function prints all increasing sequences of
// first n natural numbers. The length of every sequence
// must be k.  This function mainly uses printSeqUtil()
void printSeq(int n, int k)
{
    int arr[k];  // An array to store individual sequences
    int len = 0; // Initial length of current sequence
    printSeqUtil(n, k, len, arr);
}

// Driver program to test above functions
int main()
{
    int k = 3, n = 7;
    printSeq(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// increasing sequences of
// length 'k' such that the
// elements in every sequence
// are from first 'n'
// natural numbers.

class GFG {

    // A utility function to print
    // contents of arr[0..k-1]
    static void printArr(int[] arr, int k)
    {
        for (int i = 0; i < k; i++)
            System.out.print(arr[i] + " ");
        System.out.print("\n");
    }

    // A recursive function to print
    // all increasing sequences
    // of first n natural numbers.
    // Every sequence should be
    // length k. The array arr[] is
    // used to store current sequence
    static void printSeqUtil(int n, int k,
                             int len, int[] arr)
    {

        // If length of current increasing
        // sequence becomes k, print it
        if (len == k)
        {
            printArr(arr, k);
            return;
        }

        // Decide the starting number
        // to put at current position:
        // If length is 0, then there
        // are no previous elements
        // in arr[]. So start putting
        // new numbers with 1.
        // If length is not 0,
        // then start from value of
        // previous element plus 1.
        int i = (len == 0) ? 1 : arr[len - 1] + 1;

        // Increase length
        len++;

        // Put all numbers (which are
        // greater than the previous
        // element) at new position.
        while (i <= n)
        {
            arr[len - 1] = i;
            printSeqUtil(n, k, len, arr);
            i++;
        }

        // This is important. The
        // variable 'len' is shared among
        // all function calls in recursion
        // tree. Its value must be
        // brought back before next
        // iteration of while loop
        len--;
    }

    // This function prints all
    // increasing sequences of
    // first n natural numbers.
    // The length of every sequence
    // must be k. This function
    // mainly uses printSeqUtil()
    static void printSeq(int n, int k)
    {

        // An array to store
        // individual sequences
        int[] arr = new int[k];

        // Initial length of
        // current sequence
        int len = 0;
        printSeqUtil(n, k, len, arr);
    }

    // Driver Code
    static public void main (String[] args)
    {
        int k = 3, n = 7;
        printSeq(n, k);
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python3 program to print all
# increasing sequences of length
# 'k' such that the elements in
# every sequence are from first
# 'n' natural numbers.

# A utility function to
# print contents of arr[0..k-1]
def printArr(arr, k):
    for i in range(k):
        print(arr[i], end = " ");
    print();

# A recursive function to print
# all increasing sequences of
# first n natural numbers. Every
# sequence should be length k.
# The array arr[] is used to
# store current sequence.
def printSeqUtil(n, k,len1, arr):

    # If length of current
    # increasing sequence
    # becomes k, print it
    if (len1 == k):
        printArr(arr, k);
        return;

    # Decide the starting number
    # to put at current position:
    # If length is 0, then there
    # are no previous elements
    # in arr[]. So start putting
    # new numbers with 1\. If length
    # is not 0, then start from value
    # of previous element plus 1.
    i = 1 if(len1 == 0) else (arr[len1 - 1] + 1);

    # Increase length
    len1 += 1;

    # Put all numbers (which are greater
    # than the previous element) at
    # new position.
    while (i <= n):
        arr[len1 - 1] = i;
        printSeqUtil(n, k, len1, arr);
        i += 1;

    # This is important. The variable
    # 'len' is shared among all function
    # calls in recursion tree. Its value
    # must be brought back before next
    # iteration of while loop
    len1 -= 1;

# This function prints all increasing
# sequences of first n natural numbers.
# The length of every sequence must be
# k. This function mainly uses printSeqUtil()
def printSeq(n, k):
        arr = [0] * k; # An array to store
                       # individual sequences
        len1 = 0; # Initial length of
                  # current sequence
        printSeqUtil(n, k, len1, arr);

# Driver Code
k = 3;
n = 7;
printSeq(n, k);

# This code is contributed by mits
```

## C#

```
// C# program to print all
// increasing sequences of
// length 'k' such that the
// elements in every sequence
// are from first 'n'
// natural numbers.
using System;

class GFG {

    // A utility function to print
    // contents of arr[0..k-1]
    static void printArr(int[] arr, int k)
    {
        for (int i = 0; i < k; i++)
            Console.Write(arr[i] + " ");
        Console.WriteLine();
    }

    // A recursive function to print
    // all increasing sequences
    // of first n natural numbers.
    // Every sequence should be
    // length k. The array arr[] is
    // used to store current sequence
    static void printSeqUtil(int n, int k,
                             int len, int[] arr)
    {

        // If length of current increasing
        // sequence becomes k, print it
        if (len == k)
        {
            printArr(arr, k);
            return;
        }

        // Decide the starting number
        // to put at current position:
        // If length is 0, then there
        // are no previous elements
        // in arr[]. So start putting
        // new numbers with 1.
        // If length is not 0,
        // then start from value of
        // previous element plus 1.
        int i = (len == 0) ? 1 : arr[len - 1] + 1;

        // Increase length
        len++;

        // Put all numbers (which are
        // greater than the previous
        // element) at new position.
        while (i <= n)
        {
            arr[len - 1] = i;
            printSeqUtil(n, k, len, arr);
            i++;
        }

        // This is important. The
        // variable 'len' is shared among
        // all function calls in recursion
        // tree. Its value must be
        // brought back before next
        // iteration of while loop
        len--;
    }

    // This function prints all
    // increasing sequences of
    // first n natural numbers.
    // The length of every sequence
    // must be k. This function
    // mainly uses printSeqUtil()
    static void printSeq(int n, int k)
    {

        // An array to store
        // individual sequences
        int[] arr = new int[k];

        // Initial length of
        // current sequence
        int len = 0;
        printSeqUtil(n, k, len, arr);
    }

    // Driver Code
    static public void Main ()
    {
        int k = 3, n = 7;
        printSeq(n, k);
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all
// increasing sequences of
// length 'k' such that the
// elements in every sequence
// are from first 'n' natural
// numbers.

// A utility function to
// print contents of arr[0..k-1]
function printArr($arr, $k)
{
    for ($i = 0; $i < $k; $i++)
        echo $arr[$i], " ";
        echo "\n";
}

// A recursive function to
// print all increasing
// sequences of first n
// natural numbers. Every
// sequence should be length
// k. The array arr[] is used
// to store current sequence.
function printSeqUtil($n, $k,
                      $len, $arr)
{
    // If length of current
    // increasing sequence
    // becomes k, print it
    if ($len == $k)
    {
        printArr($arr, $k);
        return;
    }

    // Decide the starting number
    // to put at current position:
    // If length is 0, then there
    // are no previous elements
    // in arr[]. So start putting
    // new numbers with 1\. If length
    // is not 0, then start from value
    // of previous element plus 1.
    $i = ($len == 0)? 1 :
          $arr[$len - 1] + 1;

    // Increase length
    $len++;

    // Put all numbers (which are
    // greater than the previous
    // element) at new position.
    while ($i <= $n)
    {
        $arr[$len-1] = $i;
        printSeqUtil($n, $k,
                     $len, $arr);
        $i++;
    }

    // This is important. The
    // variable 'len' is shared
    // among all function calls
    // in recursion tree. Its
    // value must be brought back
    // before next iteration of
    // while loop

    $len--;
}

// This function prints all
// increasing sequences of
// first n natural numbers.
// The length of every sequence
// must be k. This function
// mainly uses printSeqUtil()
function printSeq($n, $k)
{
        $arr = array(); // An array to store
                        // individual sequences
        $len = 0; // Initial length of
                  // current sequence
        printSeqUtil($n, $k,
                     $len, $arr);
}

// Driver Code
$k = 3;
$n = 7;
printSeq($n, $k);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to print all
// increasing sequences of
// length 'k' such that the
// elements in every sequence
// are from first 'n'
// natural numbers.

// A utility function to print
// contents of arr[0..k-1]
function printArr(arr, k)
{
    for(let i = 0; i < k; i++)
        document.write(arr[i] + " ");

    document.write("</br>");
}

// A recursive function to print
// all increasing sequences
// of first n natural numbers.
// Every sequence should be
// length k. The array arr[] is
// used to store current sequence
function printSeqUtil(n, k, len, arr)
{

    // If length of current increasing
    // sequence becomes k, print it
    if (len == k)
    {
        printArr(arr, k);
        return;
    }

    // Decide the starting number
    // to put at current position:
    // If length is 0, then there
    // are no previous elements
    // in arr[]. So start putting
    // new numbers with 1.
    // If length is not 0,
    // then start from value of
    // previous element plus 1.
    let i = (len == 0) ? 1 : arr[len - 1] + 1;

    // Increase length
    len++;

    // Put all numbers (which are
    // greater than the previous
    // element) at new position.
    while (i <= n)
    {
        arr[len - 1] = i;
        printSeqUtil(n, k, len, arr);
        i++;
    }

    // This is important. The
    // variable 'len' is shared among
    // all function calls in recursion
    // tree. Its value must be
    // brought back before next
    // iteration of while loop
    len--;
}

// This function prints all
// increasing sequences of
// first n natural numbers.
// The length of every sequence
// must be k. This function
// mainly uses printSeqUtil()
function printSeq(n, k)
{

    // An array to store
    // individual sequences
    let arr = new Array(k);

    // Initial length of
    // current sequence
    let len = 0;
    printSeqUtil(n, k, len, arr);
}

// Driver code
let k = 3, n = 7;
printSeq(n, k);

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
1 2 3
1 2 4
1 2 5
1 2 6
1 2 7
1 3 4
1 3 5
1 3 6
1 3 7
1 4 5
1 4 6
1 4 7
1 5 6
1 5 7
1 6 7
2 3 4
2 3 5
2 3 6
2 3 7
2 4 5
2 4 6
2 4 7
2 5 6
2 5 7
2 6 7
3 4 5
3 4 6
3 4 7
3 5 6
3 5 7
3 6 7
4 5 6
4 5 7
4 6 7
5 6 7
```

本文由**阿琼**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息