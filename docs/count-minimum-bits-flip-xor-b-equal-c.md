# 计算翻转的最小位数，使得 A 和 B 的异或等于 C

> 原文:[https://www . geesforgeks . org/count-minimum-bits-flip-xor-b-equal-c/](https://www.geeksforgeeks.org/count-minimum-bits-flip-xor-b-equal-c/)

给定一个由三个二进制序列 A、B 和 C 组成的 N 位序列。计算翻转 A 和 B 所需的最小位数，使 A 和 B 的异或等于 c。例如:

```
Input: N = 3
       A = 110
       B = 101
       C = 001
Output: 1
We only need to flip the bit of 2nd position
of either A or B, such that A ^ B = C i.e., 
100 ^ 101 = 001
```

**一种**天真的方法**是生成 A 和 B 中所有可能的比特组合，然后对它们进行异或运算，以检查它是否等于 C。**这种方法的时间复杂度**呈指数增长，因此对于大数值的 n 来说不是更好。
一种**高效的**方法是使用异或的概念。** 

```
XOR Truth Table
  **Input**    **Output**
 X     Y     Z
 0     0  -  0
 0     1  -  1
 1     0  -  1
 1     1  -  0
```

**如果我们一般化，我们会发现在 A 和 B 的任何位置，我们只需要翻转 A 或 B 的第 i <sup>个</sup> (0 到 N-1)个位置，否则我们将无法实现最小位数。
所以在 i (0 到 N-1)的任何位置，你都会遇到两种情况，即 A[i] == B[i]或 A[i]！= B[i]。我们一个一个来讨论。** 

*   **如果 A[i] == B[i]，那么这些位的异或将为 0，在 C[]中出现两种情况:C[i]==0 或 C[i]==1。
    如果 C[i] == 0，则不需要翻转该位，但是如果 C[i] == 1，则我们必须在 A[i]或 B[i]中翻转该位，以便 1^0 == 1 或 0^1 == 1。** 
*   **如果 A[i]！= B[i]然后这些位的异或得到 1，在 C 中再次出现两种情况，即 C[i] == 0 或 C[i] == 1。
    因此，如果 C[i] == 1，那么我们不需要翻转该位，但是如果 C[i] == 0，那么我们需要翻转 A[i]或 B[i]中的位，以便 0^0==0 或 1^1==0** 

## **C++**

```
// C++ code to count the Minimum bits in A and B
#include<bits/stdc++.h>
using namespace std;

int totalFlips(char *A, char *B, char *C, int N)
{
    int count = 0;
    for (int i=0; i < N; ++i)
    {
        // If both A[i] and B[i] are equal
        if (A[i] == B[i] && C[i] == '1')
            ++count;

        // If Both A and B are unequal
        else if (A[i] != B[i] && C[i] == '0')
            ++count;
    }
    return count;
}

//Driver Code
int main()
{
    //N represent total count of Bits
    int N = 5;
    char a[] = "10100";
    char b[] = "00010";
    char c[] = "10011";

    cout << totalFlips(a, b, c, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to count the Minimum bits in A and B
class GFG {

    static int totalFlips(String A, String B,
                                String C, int N)
    {
        int count = 0;

        for (int i = 0; i < N; ++i)
        {
            // If both A[i] and B[i] are equal
            if (A.charAt(i) == B.charAt(i) &&
                            C.charAt(i) == '1')
                ++count;

            // If Both A and B are unequal
            else if (A.charAt(i) != B.charAt(i)
                          && C.charAt(i) == '0')
                ++count;
        }

        return count;
    }

    //driver code
    public static void main (String[] args)
    {
        //N represent total count of Bits
        int N = 5;
        String a = "10100";
        String b = "00010";
        String c = "10011";

        System.out.print(totalFlips(a, b, c, N));
    }
}

// This code is contributed by Anant Agarwal.
```

## **计算机编程语言**

```
# Python code to find minimum bits to be flip
def totalFlips(A, B, C, N):

    count = 0
    for i in range(N):

        # If both A[i] and B[i] are equal
        if A[i] == B[i] and C[i] == '1':
            count=count+1

        # if A[i] and B[i] are unequal
        elif A[i] != B[i] and C[i] == '0':
            count=count+1
    return count

# Driver Code
# N represent total count of Bits
N = 5
a = "10100"
b = "00010"
c = "10011"
print(totalFlips(a, b, c, N))
```

## **C#**

```
// C# code to count the Minimum
// bits flip in A and B
using System;

class GFG {

    static int totalFlips(string A, string B,
                          string C, int N)
    {
        int count = 0;
        for (int i = 0; i < N; ++i) {

            // If both A[i] and B[i] are equal
            if (A[i] == B[i] && C[i] == '1')
                ++count;

            // If Both A and B are unequal
            else if (A[i] != B[i] && C[i] == '0')
                ++count;
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        // N represent total count of Bits
        int N = 5;
        string a = "10100";
        string b = "00010";
        string c = "10011";

        Console.Write(totalFlips(a, b, c, N));
    }
}

// This code is contributed by Anant Agarwal.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP code to count the
// Minimum bits in A and B

function totalFlips($A, $B, $C, $N)
{
    $count = 0;
    for ($i = 0; $i < $N; ++$i)
    {
        // If both A[i] and
        // B[i] are equal
        if ($A[$i] == $B[$i] &&
            $C[$i] == '1')
            ++$count;

        // If Both A and
        // B are unequal
        else if ($A[$i] != $B[$i] &&
                 $C[$i] == '0')
            ++$count;
    }
    return $count;
}

// Driver Code

// N represent total count of Bits
$N = 5;
$a = "10100";
$b = "00010";
$c = "10011";

echo totalFlips($a, $b, $c, $N);

// This code is contributed by nitin mittal.
?>
```

## **java 描述语言**

```
<script>

// Javascript code to count the Minimum bits in A and B

function totalFlips(A, B, C, N)
    {
        let count = 0;
        for (let i = 0; i < N; ++i) {

            // If both A[i] and B[i] are equal
            if (A[i] == B[i] && C[i] == '1')
                ++count;

            // If Both A and B are unequal
            else if (A[i] != B[i] && C[i] == '0')
                ++count;
        }
        return count;
    }

// Driver Code

    // N represent total count of Bits
    let N = 5;
    let a = "10100";
    let b = "00010";
    let c = "10011";

    document.write(totalFlips(a, b, c, N)); 

</script>
```

****输出:****

```
2
```

****时间复杂度:**O(N)
T3】辅助空间: O(1)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。”**