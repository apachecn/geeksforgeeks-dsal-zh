# 在有数字对的数组中找到唯一的对

> 原文:[https://www . geesforgeks . org/find-unique-pair-array-pairs-numbers/](https://www.geeksforgeeks.org/find-unique-pair-array-pairs-numbers/)

给定一个数组，其中除了一对(两个元素)之外，每个元素都出现两次。找到这一独特配对的元素。
示例:

```
Input  : 6, 1, 3, 5, 1, 3, 7, 6
Output : 5 7
All elements appear twice except 5 and 7

Input  : 1 3 4 1
Output : 3 4
```

这个想法是基于下面的帖子。
[找到两个缺失的数字|集合 2(基于异或的解)](https://www.geeksforgeeks.org/find-two-missing-numbers-set-2-xor-based-solution/)
1。对数组中的每个元素进行异或运算，剩下的就是两个不同元素的异或运算，这就是我们的结果。让这个异或为“**异或**”
2。现在在**异或**中找到一个设定位。
3。现在将数组元素分成两组。一个组将步骤 2 中找到的位设置为 1，另一个组将该位设置为 0。
4。第一组元素的异或将是我们的第一个元素。第二组元素的异或就是我们的第二个元素。

## C++

```
// C program to find a unique pair in an array
// of pairs.
#include <stdio.h>

void findUniquePair(int arr[], int n)
{
    // XOR each element and get XOR of two unique
    // elements(ans)
    int XOR = arr[0];
    for (int i = 1; i < n; i++)
        XOR = XOR ^ arr[i];

    // Now XOR has XOR of two missing elements. Any set
    // bit in it must be set in one missing and unset in
    // other missing number

    // Get a set bit of XOR (We get the rightmost set bit)
    int set_bit_no = XOR & ~(XOR-1);

    // Now divide elements in two sets by comparing rightmost
    // set bit of XOR with bit at same position in each element.
    int x = 0, y = 0; // Initialize missing numbers
    for (int i = 0; i < n; i++)
    {
        if (arr[i] & set_bit_no)
            x = x ^ arr[i]; /*XOR of first set in arr[] */
        else
            y = y ^ arr[i]; /*XOR of second set in arr[] */
    }

    printf("The unique pair is (%d, %d)", x, y);

}

// Driver code
int main()
{
    int a[] = { 6, 1, 3, 5, 1, 3, 7, 6 };
    int n = sizeof(a)/sizeof(a[0]);
    findUniquePair(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a unique pair
// in an array of pairs.
class GFG
{
    static void findUniquePair(int[] arr, int n)
    {
        // XOR each element and get XOR of two
        // unique elements(ans)
        int XOR = arr[0];

        for (int i = 1; i < n; i++)
            XOR = XOR ^ arr[i];

        // Now XOR has XOR of two missing elements.
        // Any set bit in it must be set in one
        // missing and unset in other missing number

        // Get a set bit of XOR (We get the
        // rightmost set bit)
        int set_bit_no = XOR & ~(XOR-1);

        // Now divide elements in two sets by
        // comparing rightmost set bit of XOR with
        // bit at same position in each element.
        // Initialize missing numbers
        int x = 0, y = 0;

        for (int i = 0; i < n; i++)
        {
            if ((arr[i] & set_bit_no)>0)

                /*XOR of first set in arr[] */
                x = x ^ arr[i];
            else
                /*XOR of second set in arr[] */
                y = y ^ arr[i];
        }

        System.out.println("The unique pair is (" +
                               x + "," + y + ")");

    }

    // Driver code
    public static void main (String[] args) {
    int[] a = { 6, 1, 3, 5, 1, 3, 7, 6 };
    int n = a.length;
    findUniquePair(a, n);
    }

}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python 3 program to find a unique
# pair in an array of pairs.
def findUniquePair(arr, n):

    # XOR each element and get XOR
    # of two unique elements(ans)
    XOR = arr[0]
    for i in range(1, n):
        XOR = XOR ^ arr[i]

    # Now XOR has XOR of two missing
    # elements. Any set bit in it
    # must be set in one missing and
    # unset in other missing number

    # Get a set bit of XOR (We get
    # the rightmost set bit)
    set_bit_no = XOR & ~(XOR - 1)

    # Now divide elements in two sets
    # by comparing rightmost set bit
    # of XOR with bit at same position
    # in each element.
    x = 0
    y = 0 # Initialize missing numbers
    for i in range(0, n):

        if (arr[i] & set_bit_no):

            # XOR of first set in
            # arr[]
            x = x ^ arr[i]
        else:

            # XOR of second set
            # in arr[]
            y = y ^ arr[i]

    print("The unique pair is (", x,
             ", ", y, ")", sep = "")

# Driver code
a = [6, 1, 3, 5, 1, 3, 7, 6 ]
n = len(a)
findUniquePair(a, n)

# This code is contributed by Smitha.
```

## C#

```
// C# program to find a unique pair
// in an array of pairs.
using System;

class GFG {

    static void findUniquePair(int[] arr, int n)
    {

        // XOR each element and get XOR of two
        // unique elements(ans)
        int XOR = arr[0];

        for (int i = 1; i < n; i++)
            XOR = XOR ^ arr[i];

        // Now XOR has XOR of two missing
        // elements. Any set bit in it must
        // be set in one missing and unset
        // in other missing number

        // Get a set bit of XOR (We get the
        // rightmost set bit)
        int set_bit_no = XOR & ~(XOR - 1);

        // Now divide elements in two sets by
        // comparing rightmost set bit of XOR
        // with bit at same position in each
        // element. Initialize missing numbers
        int x = 0, y = 0;

        for (int i = 0; i < n; i++)
        {
            if ((arr[i] & set_bit_no) > 0)

                /*XOR of first set in arr[] */
                x = x ^ arr[i];
            else

                /*XOR of second set in arr[] */
                y = y ^ arr[i];
        }

        Console.WriteLine("The unique pair is ("
                           + x + ", " + y + ")");
    }

    // Driver code
    public static void Main ()
    {
        int[] a = { 6, 1, 3, 5, 1, 3, 7, 6 };
        int n = a.Length;

        findUniquePair(a, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a
// unique pair in an array
// of pairs.

function findUniquePair($arr, $n)
{

    // XOR each element and
    // get XOR of two unique
    // elements(ans)
    $XOR = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $XOR = $XOR ^ $arr[$i];

    // Now XOR has XOR of two
    // missing elements. Any set
    // bit in it must be set in
    // one missing and unset in
    // other missing number

    // Get a set bit of XOR
    // (We get the rightmost set bit)
    $set_bit_no = $XOR & ~($XOR-1);

    // Now divide elements in two
    // sets by comparing rightmost
    // set bit of XOR with bit at
    // same position in each element.
    // Initialize missing numbers
    $x = 0;
    $y = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] & $set_bit_no)

            // XOR of first set in arr[]
            $x = $x ^ $arr[$i];
        else

            // XOR of second set in arr[]
            $y = $y ^ $arr[$i];
    }

    echo"The unique pair is ", "(",$x," ", $y,")";

}

    // Driver code
    $a = array(6, 1, 3, 5, 1, 3, 7, 6);
    $n = count($a);
    findUniquePair($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to find a unique pair
// in an array of pairs.

   function findUniquePair(arr, n)
    {
        // XOR each element and get XOR of two
        // unique elements(ans)
        let XOR = arr[0];

        for (let i = 1; i < n; i++)
            XOR = XOR ^ arr[i];

        // Now XOR has XOR of two missing elements.
        // Any set bit in it must be set in one
        // missing and unset in other missing number

        // Get a set bit of XOR (We get the
        // rightmost set bit)
        let set_bit_no = XOR & ~(XOR-1);

        // Now divide elements in two sets by
        // comparing rightmost set bit of XOR with
        // bit at same position in each element.
        // Initialize missing numbers
        let x = 0, y = 0;

        for (let i = 0; i < n; i++)
        {
            if ((arr[i] & set_bit_no)>0)

                /*XOR of first set in arr[] */
                x = x ^ arr[i];
            else
                /*XOR of second set in arr[] */
                y = y ^ arr[i];
        }

        document.write("The unique pair is (" +
                               x + "," + y + ")" + "<br/>");

    }

// driver function

    let a = [ 6, 1, 3, 5, 1, 3, 7, 6 ];
    let n = a.length;
    findUniquePair(a, n);

</script>   
```

输出:

```
The unique pair is (7, 5)
```

本文由 **Dhiman Mayank** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。