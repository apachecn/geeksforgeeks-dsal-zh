# 将 m 插入 n，使得 m 从位 j 开始，到位 I 结束

> 原文:[https://www . geesforgeks . org/insert-m-n-m-starts-bit-j-ends-bit/](https://www.geeksforgeeks.org/insertion-m-n-m-starts-bit-j-ends-bit/)

我们有两个数字 n 和 m，以及两个位的位置 I 和 j。从 j 到 I 开始将 m 的位插入 n。我们可以假设位 j 到 I 有足够的空间来容纳所有 m。也就是说，如果 m = 10011，您可以假设 j 和 I 之间至少有 5 位。例如，您不会有 j = 3 和 i = 2，因为 m 不能完全容纳在位 3 和位 2 之间。
**例:**

```
Input : n = 1024
        m = 19
        i = 2
        j = 6;
Output : n = 1100
Binary representations of input numbers
m in binary is (10011)2
n in binary is (10000000000)2
Binary representations of output number
(10000000000)2

Input : n = 5
        m = 3
        i = 1
        j = 2
Output : 7
```

**算法:**

```
1\. Clear the bits j through i in n 

2\. Shift m so that it lines up with bits j through i 

3\. Return Bitwise AND of m and n. 
```

最棘手的部分是第一步。我们如何清除 n 中的位？我们可以用面具来做。除了位 j 到 I 中的 0，此掩码将全部为 1。我们通过首先创建掩码的左半部分，然后创建右半部分来创建此掩码。
以下是上述方法的实施。

## C++

```
// C++ program for implementation of updateBits()
#include <bits/stdc++.h>
using namespace std;

// Function to updateBits M insert to N.
int updateBits(int n, int m, int i, int j)
{
    /* Create a mask to clear bits i through j
      in n. EXAMPLE: i = 2, j = 4\. Result
      should be 11100011\. For simplicity, we'll
      use just 8 bits for the example. */

    int allOnes = ~0; // will equal sequence of all ls

    // ls before position j, then 0s. left = 11100000
    int left= allOnes << (j + 1);

    // l's after position i. right = 00000011
    int right = ((1 << i) - 1);

    // All ls, except for 0s between i and j. mask 11100011
    int mask = left | right;

    /* Clear bits j through i then put min there */
    int n_cleared = n & mask; // Clear bits j through i.
    int m_shifted = m << i;   // Move m into correct position.

    return (n_cleared | m_shifted); // OR them, and we're done!
}

// Driver Code
int main()
{
    int n = 1024; // in Binary N= 10000000000
    int m = 19;   // in Binary M= 10011
    int i = 2, j = 6;

    cout << updateBits(n,m,i,j);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of updateBits()

class UpdateBits
{
    // Function to updateBits M insert to N.
    static int updateBits(int n, int m, int i, int j)
    {
        /* Create a mask to clear bits i through j
          in n. EXAMPLE: i = 2, j = 4\. Result
          should be 11100011\. For simplicity, we'll
          use just 8 bits for the example. */

        int allOnes = ~0; // will equal sequence of all ls

        // ls before position j, then 0s. left = 11100000
        int left= allOnes << (j + 1);

        // l's after position i. right = 00000011
        int right = ((1 << i) - 1);

        // All ls, except for 0s between i and j. mask 11100011
        int mask = left | right;

        /* Clear bits j through i then put min there */
        // Clear bits j through i.
        int n_cleared = n & mask;
        // Move m into correct position.
        int m_shifted = m << i; 

        // OR them, and we're done!
        return (n_cleared | m_shifted);
    }

    public static void main (String[] args)
    {
        // in Binary N= 10000000000
        int n = 1024;

        // in Binary M= 10011
        int m = 19;  

        int i = 2, j = 6;

        System.out.println(updateBits(n,m,i,j));
    }
}
```

## 蟒蛇 3

```
# Python3 program for implementation
# of updateBits()

# Function to updateBits M insert to N.
def updateBits(n, m, i, j):

    # Create a mask to clear bits i through
    # j in n. EXAMPLE: i = 2, j = 4\. Result
    # should be 11100011\. For simplicity,
    # we'll use just 8 bits for the example.

    # will equal sequence of all ls
    allOnes = ~0

    # ls before position j,
    # then 0s. left = 11100000
    left = allOnes << (j + 1)

    # l's after position i. right = 00000011
    right = ((1 << i) - 1)

    # All ls, except for 0s between
    # i and j. mask 11100011
    mask = left | right

    # Clear bits j through i then put min there
    n_cleared = n & mask

    # Move m into correct position.
    m_shifted = m << i

    return (n_cleared | m_shifted)

# Driver Code
n = 1024 # in Binary N = 10000000000
m = 19   # in Binary M = 10011
i = 2; j = 6
print(updateBits(n, m, i, j))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program for implementation of
// updateBits()
using System;

class GFG {

    // Function to updateBits M
    // insert to N.
    static int updateBits(int n, int m,
                           int i, int j)
    {

        /* Create a mask to clear bits i
          through j in n. EXAMPLE: i = 2,
          j = 4\. Result should be 11100011.
          For simplicity, we'll use just 8
          bits for the example. */

        // will equal sequence of all ls
        int allOnes = ~0;

        // ls before position j, then 0s.
        // left = 11100000
        int left= allOnes << (j + 1);

        // l's after position i.
        // right = 00000011
        int right = ((1 << i) - 1);

        // All ls, except for 0s between i
        // and j. mask 11100011
        int mask = left | right;

        /* Clear bits j through i then put
        min there */
        // Clear bits j through i.
        int n_cleared = n & mask;

        // Move m into correct position.
        int m_shifted = m << i; 

        // OR them, and we're done!
        return (n_cleared | m_shifted);
    }

    public static void Main()
    {

        // in Binary N= 10000000000
        int n = 1024;

        // in Binary M= 10011
        int m = 19;  
        int i = 2, j = 6;

        Console.WriteLine(updateBits(n, m, i, j));
    }
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for implementation
// of updateBits()

// Function to updateBits
// M insert to N.

function updateBits($n, $m, $i, $j)
{
    // Create a mask to clear
    // bits i through j in n.
    // EXAMPLE: i = 2, j = 4.
    // Result should be 11100011.
    // For simplicity, we'll use
    // just 8 bits for the example.

    // will equal sequence of all ls
    $allOnes = ~0;

    // ls before position j, then
    // 0s. left = 11100000
    $left= $allOnes << ($j + 1);

    // l's after position i.
    // right = 00000011
    $right = ((1 << $i) - 1);

    // All ls, except for 0s between
    // i and j. mask 11100011
    $mask = $left | $right;

    // Clear bits j through i
    // then put min there

    // Clear bits j through i.
    $n_cleared = $n & $mask;

    // Move m into correct position.
    $m_shifted = $m << $i;

    // OR them, and we're done!
    return ($n_cleared | $m_shifted);
}

// Driver Code

// in Binary N= 10000000000
$n = 1024;

// in Binary M= 10011
$m = 19;
$i = 2;
$j = 6;

echo updateBits($n, $m, $i, $j);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for implementation of updateBits()

    // Function to updateBits M insert to N.
    function updateBits(n,m,i,j)
    {
        /* Create a mask to clear bits i through j
        in n. EXAMPLE: i = 2, j = 4\. Result
        should be 11100011\. For simplicity, we'll
        use just 8 bits for the example. */

        let allOnes = ~0; // will equal sequence of all ls

        // ls before position j, then 0s. left = 11100000
        let left= allOnes << (j + 1);

        // l's after position i. right = 00000011
        let right = ((1 << i) - 1);

        // All ls, except for 0s between i and j. mask 11100011
        let mask = left | right;

        /* Clear bits j through i then put min there */
        // Clear bits j through i.
        let n_cleared = n & mask;
        // Move m into correct position.
        let m_shifted = m << i;

        // OR them, and we're done!
        return (n_cleared | m_shifted);
    }

        // in Binary N= 10000000000
        let n = 1024;

        // in Binary M= 10011
        let m = 19;

        let i = 2, j = 6;

        document.write(updateBits(n,m,i,j));

// This code is contributed by sravan

</script>
```

**输出:**

```
 1100  // in Binary (10001001100)2
```

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。