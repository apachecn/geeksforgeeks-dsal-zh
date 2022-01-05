# 查找两个缺失的数字|集合 2(基于异或的解决方案)

> 原文:[https://www . geesforgeks . org/find-two-missing-numbers-set-2-xor-based-solution/](https://www.geeksforgeeks.org/find-two-missing-numbers-set-2-xor-based-solution/)

给定 n 个唯一整数的数组，其中数组中的每个元素都在范围[1，n]内。数组包含所有不同的元素，数组的大小为(n-2)。因此，该数组中缺少该范围内的两个数字。找出两个丢失的数字。
**例:**

```
Input  : arr[] = {1, 3, 5, 6}, n = 6
Output : 2 4

Input : arr[] = {1, 2, 4}, n = 5
Output : 3 5

Input : arr[] = {1, 2}, n = 4
Output : 3 4
```

[找出两个缺失的数字|集合 1(一个有趣的线性时间解)](https://www.geeksforgeeks.org/find-two-missing-numbers-set-1-an-interesting-linear-time-solution/)
我们在上面的文章中讨论了解决这个问题的两种方法。方法 1 需要 O(n)个额外空间，而方法 2 会导致溢出。在这篇文章中，讨论了一个新的解决方案。这里讨论的解决方案是 O(n)时间，O(1)额外空间，并且不会导致溢出。
以下是步骤。

1.  求所有数组元素和从 1 到 n 的自然数的异或，让数组为 arr[] = {1，3，5，6}

    ```
       XOR = (1 ^ 3  ^ 5 ^ 6) ^ (1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 6)
    ```

2.  根据异或的性质，相同的元素将抵消，我们将剩下 2 异或 4 = 6 (110)。但是我们不知道确切的数字，让它们是 X 和 y。
3.  只有当 X 和 Y 中的对应位不同时，才会在 xor 中设置一个位。这是理解的关键一步。
4.  我们在异或运算中取一个设定位。让我们考虑 XOR 中最右边的设置位，set_bit_no = 010
5.  现在，如果我们将 arr[]和 1 到 n 中最右边的所有元素进行异或运算，我们将得到一个重复的数字，比如 x.

    ```
    Ex: Elements in arr[] with bit set: {3, 6}
    Elements from 1 to n with bit set {2, 3, 6}
    Result of XOR'ing all these is x = 2.
    ```

6.  类似地，如果我们对 arr[]和 1 到 n 的所有没有设置最右边位的元素进行异或运算，我们将得到另一个元素，比如 y.

    ```
    Ex: Elements in arr[] with bit not set: {1, 5}
    Elements from 1 to n with bit not set {1, 4, 5}
    Result of XOR'ing all these is y = 4 
    ```

下面是以上步骤的实现。

## C++

```
// C++ Program to find 2 Missing Numbers using O(1)
// extra space and no overflow.
#include<bits/stdc++.h>

// Function to find two missing numbers in range
// [1, n]. This function assumes that size of array
// is n-2 and all array elements are distinct
void findTwoMissingNumbers(int arr[], int n)
{
    /* Get the XOR of all elements in arr[] and
       {1, 2 .. n} */
    int XOR = arr[0];
    for (int i = 1; i < n-2; i++)
        XOR ^= arr[i];
    for (int i = 1; i <= n; i++)
        XOR ^= i;

    // Now XOR has XOR of two missing elements. Any set
    // bit in it must be set in one missing and unset in
    // other missing number

    // Get a set bit of XOR (We get the rightmost set bit)
    int set_bit_no = XOR & ~(XOR-1);

    // Now divide elements in two sets by comparing rightmost
    // set bit of XOR with bit at same position in each element.
    int x = 0, y = 0; // Initialize missing numbers
    for (int i = 0; i < n-2; i++)
    {
        if (arr[i] & set_bit_no)
            x = x ^ arr[i]; /*XOR of first set in arr[] */
        else
            y = y ^ arr[i]; /*XOR of second set in arr[] */
    }
    for (int i = 1; i <= n; i++)
    {
        if (i & set_bit_no)
            x = x ^ i; /* XOR of first set in arr[] and
                         {1, 2, ...n }*/
        else
            y = y ^ i; /* XOR of second set in arr[] and
                         {1, 2, ...n } */
    }

    printf("Two Missing Numbers are\n %d %d", x, y);
}

// Driver program to test above function
int main()
{
    int arr[] = {1, 3, 5, 6};

    // Range of numbers is 2 plus size of array
    int n = 2 + sizeof(arr)/sizeof(arr[0]);

    findTwoMissingNumbers(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find 2 Missing Numbers 
import java.util.*;

class GFG {

    // Function to find two missing numbers in range
    // [1, n]. This function assumes that size of array
    // is n-2 and all array elements are distinct
    static void findTwoMissingNumbers(int arr[], int n)
    {
        /* Get the XOR of all elements in arr[] and
           {1, 2 .. n} */
        int XOR = arr[0];
        for (int i = 1; i < n-2; i++)
            XOR ^= arr[i];
        for (int i = 1; i <= n; i++)
            XOR ^= i;

        // Now XOR has XOR of two missing elements.
        // Any set bit in it must be set in one missing
        // and unset in other missing number

        // Get a set bit of XOR (We get the rightmost
        // set bit)
        int set_bit_no = XOR & ~(XOR-1);

        // Now divide elements in two sets by comparing
        // rightmost set bit of XOR with bit at same 
        // position in each element.
        int x = 0, y = 0; // Initialize missing numbers
        for (int i = 0; i < n-2; i++)
        {
            if ((arr[i] & set_bit_no) > 0)

                /*XOR of first set in arr[] */
                x = x ^ arr[i]; 
            else
                /*XOR of second set in arr[] */
                y = y ^ arr[i]; 
        }

        for (int i = 1; i <= n; i++)
        {
            if ((i & set_bit_no)>0)

                /* XOR of first set in arr[] and
                   {1, 2, ...n }*/
                x = x ^ i; 
            else
                /* XOR of second set in arr[] and
                    {1, 2, ...n } */
                y = y ^ i; 
        }

        System.out.println("Two Missing Numbers are ");
        System.out.println( x + " " + y);
    }

    /* Driver program to test above function */
    public static void main(String[] args) 
    {
         int arr[] = {1, 3, 5, 6};

         // Range of numbers is 2 plus size of array
         int n = 2 +arr.length;

         findTwoMissingNumbers(arr, n);

        }
    }

// This code is contributed by Arnav Kr. Mandal.    
```

## 蟒蛇 3

```
# Python Program to find 2 Missing
# Numbers using O(1)
# extra space and no overflow.

# Function to find two missing
# numbers in range
# [1, n]. This function assumes
# that size of array
# is n-2 and all array elements
# are distinct
def findTwoMissingNumbers(arr, n):

        # Get the XOR of all
        # elements in arr[] and
    # {1, 2 .. n} 
    XOR = arr[0]
    for i in range(1,n-2):
        XOR ^= arr[i]
    for i in range(1,n+1):
        XOR ^= i

    # Now XOR has XOR of two
        # missing elements. Any set
    # bit in it must be set in
        # one missing and unset in
    # other missing number

    # Get a set bit of XOR 
        # (We get the rightmost set bit)
    set_bit_no = XOR & ~(XOR-1)

    # Now divide elements in two sets
        # by comparing rightmost
    # set bit of XOR with bit at same
        # position in each element.
    x = 0

        # Initialize missing numbers
    y = 0 
    for i in range(0,n-2):
        if arr[i] & set_bit_no:

                # XOR of first set in arr[] 
            x = x ^ arr[i]  
        else:

                # XOR of second set in arr[] 
            y = y ^ arr[i]  
    for i in range(1,n+1):
        if i & set_bit_no:

                # XOR of first set in arr[] and
                # {1, 2, ...n }
            x = x ^ i 

        else:

                # XOR of second set in arr[] and
                # {1, 2, ...n } 
            y = y ^ i

    print ("Two Missing Numbers are\n%d %d"%(x,y))

# Driver program to test
# above function
arr = [1, 3, 5, 6]

# Range of numbers is 2
# plus size of array
n = 2 + len(arr)
findTwoMissingNumbers(arr, n)

# This code is contributed
# by Shreyanshi Arun.
```

## C#

```
// Program to find 2 Missing Numbers
using System;

class GFG {

    // Function to find two missing
    // numbers in range [1, n].This
    // function assumes that size of
    // array is n-2 and all array
    // elements are distinct
    static void findTwoMissingNumbers(int[] arr, int n)
    {
        // Get the XOR of all elements
        // in arr[] and {1, 2 .. n}
        int XOR = arr[0];

        for (int i = 1; i < n - 2; i++)
            XOR ^= arr[i];

        for (int i = 1; i <= n; i++)
            XOR ^= i;

        // Now XOR has XOR of two missing
        // element. Any set bit in it must
        // be set in one missing and unset
        // in other missing number
        // Get a set bit of XOR (We get the
        // rightmost set bit)
        int set_bit_no = XOR & ~(XOR - 1);

        // Now divide elements in two sets
        // by comparing rightmost set bit
        // of XOR with bit at same position
        // in each element.
        int x = 0, y = 0;

        // Initialize missing numbers
        for (int i = 0; i < n - 2; i++) {

            if ((arr[i] & set_bit_no) > 0)

                // XOR of first set in arr[]
                x = x ^ arr[i];

            else
                // XOR of second set in arr[]
                y = y ^ arr[i];
        }

        for (int i = 1; i <= n; i++) {
            if ((i & set_bit_no) > 0)
                // XOR of first set in arr[]
                // and {1, 2, ...n }
                x = x ^ i;

            else
                // XOR of second set in arr[]
                // and {1, 2, ...n }
                y = y ^ i;
        }

        Console.WriteLine("Two Missing Numbers are ");
        Console.WriteLine(x + " " + y);
    }

    // Driver program
    public static void Main()
    {
        int[] arr = { 1, 3, 5, 6 };

        // Range of numbers is 2 plus
        // size of array
        int n = 2 + arr.Length;

        findTwoMissingNumbers(arr, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find 2 Missing 
// Numbers using O(1) extra
// space and no overflow.

// Function to find two
// missing numbers in range
// [1, n]. This function 
// assumes that size of array
// is n-2 and all array 
// elements are distinct
function findTwoMissingNumbers($arr, $n)
{

    // Get the XOR of all 
    // elements in arr[] and
    // {1, 2 .. n} 
    $XOR = $arr[0];
    for ($i = 1; $i < $n - 2; $i++)
        $XOR ^= $arr[$i];
    for ($i = 1; $i <= $n; $i++)
        $XOR ^= $i;

    // Now XOR has XOR of two
    // missing elements. Any set
    // bit in it must be set in 
    // one missing and unset in
    // other missing number

    // Get a set bit of XOR 
    // (We get the rightmost
    // set bit)
    $set_bit_no = $XOR & ~($XOR - 1);

    // Now divide elements in two
    // sets by comparing rightmost
    // set bit of XOR with bit at 
    // same position in each element.

    $x = 0;

    // Initialize missing numbers
    $y = 0; 
    for ($i = 0; $i < $n - 2; $i++)
    {
        if ($arr[$i] & $set_bit_no)

            // XOR of first set in arr[] 
            $x = $x ^ $arr[$i]; 

        else

            // XOR of second set in arr[] 
            $y = $y ^ $arr[$i]; 
    }
    for ($i = 1; $i <= $n; $i++)
    {
        if ($i & $set_bit_no)

            // XOR of first set in arr[]
            // and {1, 2, ...n }
            $x = $x ^ $i; 

        else

            // XOR of second set in arr[]
            // and {1, 2, ...n }
            $y = $y ^ $i; 
    }

    echo "Two Missing Numbers are\n", $x;
    echo "\n", $y;
}

    // Driver Code
    $arr = array(1, 3, 5, 6);

    // Range of numbers is 2
    // plus size of array
    $n = 2 + count($arr);

    findTwoMissingNumbers($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find 2 
// Missing Numbers using O(1)
// extra space and no overflow.

// Function to find two missing numbers in range
// [1, n]. This function assumes that size of array
// is n-2 and all array elements are distinct
function findTwoMissingNumbers(arr, n)
{
    /* Get the XOR of all elements in arr[] and
       {1, 2 .. n} */
    let XOR = arr[0];
    for (let i = 1; i < n-2; i++)
        XOR ^= arr[i];
    for (let i = 1; i <= n; i++)
        XOR ^= i;

    // Now XOR has XOR of two missing
    // elements. Any set
    // bit in it must be set in 
    // one missing and unset in
    // other missing number

    // Get a set bit of XOR 
    // (We get the rightmost set bit)
    let set_bit_no = XOR & ~(XOR-1);

    // Now divide elements in two 
    // sets by comparing rightmost
    // set bit of XOR with bit at same
    // position in each element.
    let x = 0, y = 0; // Initialize missing numbers
    for (let i = 0; i < n-2; i++)
    {
        if (arr[i] & set_bit_no)
            x = x ^ arr[i]; /*XOR of first set in arr[] */
        else
            y = y ^ arr[i]; /*XOR of second set in arr[] */
    }
    for (let i = 1; i <= n; i++)
    {
        if (i & set_bit_no)
            x = x ^ i; /* XOR of first set in arr[] and
                         {1, 2, ...n }*/
        else
            y = y ^ i; /* XOR of second set in arr[] and
                         {1, 2, ...n } */
    }

    document.write(`Two Missing Numbers are<br> ${x} ${y}`);
}

// Driver program to test above function
    let arr = [1, 3, 5, 6];

    // Range of numbers is 2 plus size of array
    n = 2 + arr.length;

    findTwoMissingNumbers(arr, n);

</script>
```

**输出:**

```
Two Missing Numbers are
2 4
```

时间复杂度:O(n)
辅助空间:O(1)
无整数溢出
本文由 **Shivam Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。