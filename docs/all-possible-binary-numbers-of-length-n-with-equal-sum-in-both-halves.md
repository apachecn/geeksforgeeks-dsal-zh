# 长度为 n 的所有可能的二进制数，在两半中具有相等的和

> 原文:[https://www . geeksforgeeks . org/所有可能的二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进制二进](https://www.geeksforgeeks.org/all-possible-binary-numbers-of-length-n-with-equal-sum-in-both-halves/)

给定一个数字 n，我们需要打印所有 n 位二进制数，并且在左半部分和右半部分相等。如果 n 是奇数，那么中间元素可以是 0 或 1。
**例:**

```
Input  : n = 4
Output : 0000 0101 0110 1001 1010 1111 
Input : n = 5
Output : 00000 00100 01001 01101 01010 01110 10001 10101 10010 10110 11011 11111 
```

这个想法是递归地构建左半部分和右半部分，并跟踪它们中 1 的计数之间的差异。当差异变为 0 并且没有更多字符需要添加时，我们会打印一个字符串。

## C++

```
// C++ program to generate all binary strings with
// equal sums in left and right halves.
#include <bits/stdc++.h>
using namespace std;

/* Default values are used only in initial call.
   n is number of bits remaining to be filled
   di is current difference between sums of
      left and right halves.
   left and right are current half substrings. */
void equal(int n, string left="", string right="",
                                        int di=0)
{
    // TWO BASE CASES
    // If there are no more characters to add (n is 0)
    if (n == 0)
    {
        // If difference between counts of 1s and
        // 0s is 0 (di is 0)
        if (di == 0)
            cout << left + right << " ";
        return;
    }

    /* If 1 remains than string length was odd */
    if (n == 1)
    {
        // If difference is 0, we can put remaining
        // bit in middle.
        if (di == 0)
        {
            cout << left + "0" + right << " ";
            cout << left + "1" + right << " ";
        }
        return;
    }

    /* If difference is more than what can be
       be covered with remaining n digits
       (Note that lengths of left and right
        must be same) */
    if ((2 * abs(di) <= n))
    { 

         /* add 0 to end in both left and right
         half. Sum in both half will not
               change*/
         equal(n-2, left+"0", right+"0", di);

         /* add 0 to end in both left and right
         half* subtract 1 from di as right
         sum is increased by 1*/
         equal(n-2, left+"0", right+"1", di-1);

        /* add 1  in end in left half and 0 to the
        right half. Add 1 to di as left sum is
        increased by 1*/
        equal(n-2, left+"1", right+"0", di+1);

        /* add 1 in end to both left and right
          half the sum will not change*/
        equal(n-2, left+"1", right+"1", di);
    }
}

/* driver function */
int main()
{
    int n = 5; // n-bits
    equal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate all binary strings
// with equal sums in left and right halves.
import java.util.*;

class GFG
{

// Default values are used only in initial call.
// n is number of bits remaining to be filled
// di is current difference between sums of
// left and right halves.
// left and right are current half substrings.
static void equal(int n, String left,
                         String right, int di)
{
    // TWO BASE CASES
    // If there are no more characters to add (n is 0)
    if (n == 0)
    {
        // If difference between counts of 1s and
        // 0s is 0 (di is 0)
        if (di == 0)
            System.out.print(left + right + " ");
        return;
    }

    /* If 1 remains than string length was odd */
    if (n == 1)
    {
        // If difference is 0, we can put
        // remaining bit in middle.
        if (di == 0)
        {
            System.out.print(left + "0" + right + " ");
            System.out.print(left + "1" + right + " ");
        }
        return;
    }

    /* If difference is more than what can be
    be covered with remaining n digits
    (Note that lengths of left and right
     must be same) */
    if ((2 * Math.abs(di) <= n))
    {

            // add 0 to end in both left and right
            // half. Sum in both half will not
            // change
            equal(n - 2, left + "0", right + "0", di);

            // add 0 to end in both left and right
            // half* subtract 1 from di as right
            // sum is increased by 1
            equal(n - 2, left + "0", right + "1", di - 1);

        // add 1 in end in left half and 0 to the
        // right half. Add 1 to di as left sum is
        // increased by 1*
        equal(n - 2, left + "1", right + "0", di + 1);

        // add 1 in end to both left and right
        // half the sum will not change
        equal(n - 2, left + "1", right + "1", di);
    }
}

// Driver Code
public static void main(String args[])
{
    int n = 5;

    // n-bits
    equal(n, "", "", 0);
}
}

// This code is contributed
// by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python program to generate all binary strings with
# equal sums in left and right halves.

# Default values are used only in initial call.
# n is number of bits remaining to be filled
# di is current difference between sums of
# left and right halves.
# left and right are current half substrings.
def equal(n: int, left = "", right = "", di = 0):

    # TWO BASE CASES
    # If there are no more characters to add (n is 0)
    if n == 0:

        # If difference between counts of 1s and
        # 0s is 0 (di is 0)
        if di == 0:
            print(left + right, end = " ")
        return

    # If 1 remains than string length was odd
    if n == 1:

        # If difference is 0, we can put remaining
        # bit in middle.
        if di == 0:
            print(left + "0" + right, end = " ")
            print(left + "1" + right, end = " ")
        return

    # If difference is more than what can be
    # be covered with remaining n digits
    # (Note that lengths of left and right
    # must be same)
    if 2 * abs(di) <= n:

        # add 0 to end in both left and right
        # half. Sum in both half will not
        # change
        equal(n - 2, left + "0", right + "0", di)

        # add 0 to end in both left and right
        # half* subtract 1 from di as right
        # sum is increased by 1
        equal(n - 2, left + "0", right + "1", di - 1)

        # add 1 in end in left half and 0 to the
        # right half. Add 1 to di as left sum is
        # increased by 1
        equal(n - 2, left + "1", right + "0", di + 1)

        # add 1 in end to both left and right
        # half the sum will not change
        equal(n - 2, left + "1", right + "1", di)

# Driver Code
if __name__ == "__main__":
    n = 5 # n-bits
    equal(5)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to generate all binary strings
// with equal sums in left and right halves.
using System;

class GFG
{

// Default values are used only in initial call.
// n is number of bits remaining to be filled
// di is current difference between sums of
// left and right halves.
// left and right are current half substrings.
static void equal(int n, String left,
                         String right, int di)
{
    // TWO BASE CASES
    // If there are no more characters
    // to add (n is 0)
    if (n == 0)
    {
        // If difference between counts of 1s
        // and 0s is 0 (di is 0)
        if (di == 0)
            Console.Write(left + right + " ");
        return;
    }

    /* If 1 remains than string length was odd */
    if (n == 1)
    {
        // If difference is 0, we can put
        // remaining bit in middle.
        if (di == 0)
        {
            Console.Write(left + "0" +
                          right + " ");
            Console.Write(left + "1" +
                          right + " ");
        }
        return;
    }

    /* If difference is more than what can be
    be covered with remaining n digits
    (Note that lengths of left and right
    must be same) */
    if ((2 * Math.Abs(di) <= n))
    {

            // add 0 to end in both left and right
            // half. Sum in both half will not
            // change
            equal(n - 2, left + "0", right + "0", di);

            // add 0 to end in both left and right
            // half* subtract 1 from di as right
            // sum is increased by 1
            equal(n - 2, left + "0",
                  right + "1", di - 1);

        // add 1 in end in left half and 0 to the
        // right half. Add 1 to di as left sum is
        // increased by 1*
        equal(n - 2, left + "1",
              right + "0", di + 1);

        // add 1 in end to both left and right
        // half the sum will not change
        equal(n - 2, left + "1", right + "1", di);
    }
}

// Driver Code
public static void Main(String []args)
{
    int n = 5;

    // n-bits
    equal(n, "", "", 0);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to generate all binary strings
// with equal sums in left and right halves.

// Default values are used only in initial call.
// n is number of bits remaining to be filled
// di is current difference between sums of
// left and right halves.
// left and right are current half substrings.
function equal(n,left,right,di)
{
    // TWO BASE CASES
    // If there are no more characters to add (n is 0)
    if (n == 0)
    {
        // If difference between counts of 1s and
        // 0s is 0 (di is 0)
        if (di == 0)
            document.write(left + right + " ");
        return;
    }

    /* If 1 remains than string length was odd */
    if (n == 1)
    {
        // If difference is 0, we can put
        // remaining bit in middle.
        if (di == 0)
        {
            document.write(left + "0" + right + " ");
            document.write(left + "1" + right + " ");
        }
        return;
    }

    /* If difference is more than what can be
    be covered with remaining n digits
    (Note that lengths of left and right
     must be same) */
    if ((2 * Math.abs(di) <= n))
    {

            // add 0 to end in both left and right
            // half. Sum in both half will not
            // change
            equal(n - 2, left + "0", right + "0", di);

            // add 0 to end in both left and right
            // half* subtract 1 from di as right
            // sum is increased by 1
            equal(n - 2, left + "0", right + "1", di - 1);

        // add 1 in end in left half and 0 to the
        // right half. Add 1 to di as left sum is
        // increased by 1*
        equal(n - 2, left + "1", right + "0", di + 1);

        // add 1 in end to both left and right
        // half the sum will not change
        equal(n - 2, left + "1", right + "1", di);
    }
}

// Driver Code
let n = 5;

// n-bits
equal(n, "", "", 0);

// This code is contributed by rag2127

</script>
```

**输出:**

```
10001 10101 10010 10110 11011 11111 
```

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。