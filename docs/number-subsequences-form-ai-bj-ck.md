# a^i b^j c^k 形式的子序列数

> 原文:[https://www . geesforgeks . org/number-subseques-form-ai-bj-CK/](https://www.geeksforgeeks.org/number-subsequences-form-ai-bj-ck/)

给定一个字符串，计算 a <sup>i</sup> b <sup>j</sup> c <sup>k</sup> 形式的子序列数，即它由 i 'a '字符组成，后跟 j 'b '字符，后跟 k 'c '字符，其中 i > = 1，j > =1，k > = 1。
**注意:**如果为两个子序列选择的数组索引集不同，则认为这两个子序列不同。
预期时间复杂度:O(n)
**示例:**

```
Input  : abbc
Output : 3
Subsequences are abc, abc and abbc

Input  : abcabc
Output : 7
Subsequences are abc, abc, abbc, aabc
abcc, abc and abc
```

**方法:**
我们遍历给定的字符串。对于每个遇到的字符，我们执行以下操作:
**1)** 初始化由不同的“a”组合引起的不同子序列的计数。让这个计数成为一个计数。
**2)** 初始化由‘b’的不同组合引起的不同子序列的计数。让这个计数成为 bCount。
**3)** 初始化由不同的“c”组合引起的不同子序列的计数。让这个计数被计数。
**4)** 遍历给定字符串的所有字符。对当前字符 **s[i]**
**做以下操作如果当前字符是‘a’**，那么有以下可能:
a)当前字符开始一个新的子序列。
b)当前字符是计数子序列的一部分。
c)当前字符不是计数子序列的一部分。
因此我们做一个 count =(1+2 * a count)；
**如果当前字符是‘b’**，那么有以下可能:
a)当前字符以一个计数子序列开始一个新的 b 的子序列。
b)当前字符是 bCount 子序列的一部分。
c)当前字符不是计数子序列的一部分。
因此我们做 b count =(a count+2 * b count)；
**如果当前字符是‘c’**，那么有以下几种可能:
a)当前字符以 bCount 子序列开始一个新的 c 的子序列。
b)当前字符是帐户子序列的一部分。
c)当前字符不是帐户子序列的一部分。
所以我们做 account =(b count+2 * cCount)；
**5)** 最后我们返回 cCount
**举例说明方法:**

*   aCount 是字母“a”的子序列数。

*   考虑这个例子:aa。
*   我们可以看到这个的 aCount 是 3，因为我们可以选择这些可能性:(xa，ax，aa) (x 表示我们没有使用那个字符)。还要注意，这与中间的字符无关，即 aa 和 ccbabbbcac 的 aCount 是相同的，因为两者都正好有 2 a。

*   现在，加上 1 a，我们现在有了以下新的子序列:每个旧的子序列，每个旧的子序列+新的 a，以及新的字母 a。所以总共有**个计数+ 1 个计数+1 个**子序列。

*   现在，让我们来考虑 bCount，一些 a，然后一些 b 的子序列的数量。在‘aab’中，我们看到 bCount 应该是 3 (axb，xab，aab)，因为这只是我们可以选择前两个 a 的子序列，然后是 b 的方法的数量，所以每次我们添加 ab，方法的数量就会增加一个 aCount。

*   让我们找到“aabb”的 bCount。我们已经确定 aab 有 3 个子序列，所以我们肯定还有这些。此外，我们可以将新的 b 添加到这些子序列中的任何一个上，以获得另外 3 个。最后，我们必须计算不使用任何其他 b 的子序列，根据最后一段的逻辑，这只是一个计数。所以，这之后的 bCount 只是旧的 b count * 2+a count；

*   账户类似。

以下是上述思路的实现:

## C++

```
// C++ program to count subsequences of the
// form a^i b^j c^k
#include <bits/stdc++.h>
using namespace std;

// Returns count of subsequences of the form
// a^i b^j c^k
int countSubsequences(string s)
{
    // Initialize counts of different subsequences
    // caused by different combination of 'a'
    int aCount = 0;

    // Initialize counts of different subsequences
    // caused by different combination of 'a' and
    // different combination of 'b'
    int bCount = 0;

    // Initialize counts of different subsequences
    // caused by different combination of 'a', 'b'
    // and 'c'.
    int cCount = 0;

    // Traverse all characters of given string
    for (unsigned int i = 0; i < s.size(); i++) {
        /* If current character is 'a', then
           there are the following possibilities :
             a) Current character begins a new
                subsequence.
             b) Current character is part of aCount
                subsequences.
             c) Current character is not part of
                aCount subsequences. */
        if (s[i] == 'a')
            aCount = (1 + 2 * aCount);

        /* If current character is 'b', then
           there are following possibilities :
             a) Current character begins a new
                subsequence of b's with aCount
                subsequences.
             b) Current character is part of bCount
                subsequences.
             c) Current character is not part of
                bCount subsequences. */
        else if (s[i] == 'b')
            bCount = (aCount + 2 * bCount);

        /* If current character is 'c', then
           there are following possibilities :
             a) Current character begins a new
                subsequence of c's with bCount
                subsequences.
             b) Current character is part of cCount
                subsequences.
             c) Current character is not part of
                cCount subsequences. */
        else if (s[i] == 'c')
            cCount = (bCount + 2 * cCount);
    }

    return cCount;
}

// Driver code
int main()
{
    string s = "abbc";
    cout << countSubsequences(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count subsequences of the
// form a^i b^j c^k
public class No_of_subsequence {

    // Returns count of subsequences of the form
    // a^i b^j c^k
    static int countSubsequences(String s)
    {
        // Initialize counts of different subsequences
        // caused by different combination of 'a'
        int aCount = 0;

        // Initialize counts of different subsequences
        // caused by different combination of 'a' and
        // different combination of 'b'
        int bCount = 0;

        // Initialize counts of different subsequences
        // caused by different combination of 'a', 'b'
        // and 'c'.
        int cCount = 0;

        // Traverse all characters of given string
        for (int i = 0; i < s.length(); i++) {
            /* If current character is 'a', then
               there are following possibilities :
                 a) Current character begins a new
                    subsequence.
                 b) Current character is part of aCount
                    subsequences.
                 c) Current character is not part of
                    aCount subsequences. */
            if (s.charAt(i) == 'a')
                aCount = (1 + 2 * aCount);

            /* If current character is 'b', then
               there are following possibilities :
                 a) Current character begins a new
                    subsequence of b's with aCount
                    subsequences.
                 b) Current character is part of bCount
                    subsequences.
                 c) Current character is not part of
                    bCount subsequences. */
            else if (s.charAt(i) == 'b')
                bCount = (aCount + 2 * bCount);

            /* If current character is 'c', then
               there are following possibilities :
                 a) Current character begins a new
                    subsequence of c's with bCount
                    subsequences.
                 b) Current character is part of cCount
                    subsequences.
                 c) Current character is not part of
                    cCount subsequences. */
            else if (s.charAt(i) == 'c')
                cCount = (bCount + 2 * cCount);
        }

        return cCount;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "abbc";
        System.out.println(countSubsequences(s));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to count
# subsequences of the form
# a ^ i b ^ j c ^ k

# Returns count of subsequences
# of the form a ^ i b ^ j c ^ k
def countSubsequences(s):

    # Initialize counts of different
    # subsequences caused by different
    # combination of 'a'
    aCount = 0

    # Initialize counts of different
    # subsequences caused by different
    # combination of 'a' and different
    # combination of 'b'
    bCount = 0

    # Initialize counts of different
    # subsequences caused by different
    # combination of 'a', 'b' and 'c'.
    cCount = 0

    # Traverse all characters
    # of given string
    for i in range(len(s)):

        # If current character is 'a',
        # then there are following
        # possibilities :
        # a) Current character begins
        # a new subsequence.
        # b) Current character is part
        # of aCount subsequences.
        # c) Current character is not
        # part of aCount subsequences.
        if (s[i] == 'a'):
            aCount = (1 + 2 * aCount)

        # If current character is 'b', then
        # there are following possibilities :
        # a) Current character begins a
        # new subsequence of b's with
        # aCount subsequences.
        # b) Current character is part
        # of bCount subsequences.
        # c) Current character is not
        # part of bCount subsequences.
        elif (s[i] == 'b'):
            bCount = (aCount + 2 * bCount)

        # If current character is 'c', then
        # there are following possibilities :
        # a) Current character begins a
        # new subsequence of c's with
        # bCount subsequences.
        # b) Current character is part
        # of cCount subsequences.
        # c) Current character is not
        # part of cCount subsequences.
        elif (s[i] == 'c'):
            cCount = (bCount + 2 * cCount)

    return cCount

# Driver code
if __name__ == "__main__":
    s = "abbc"
    print(countSubsequences(s))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count subsequences
// of the form a^i b^j c^k
using System;

public class GFG {

    // Returns count of subsequences
    // of the form a^i b^j c^k
    static int countSubsequences(String s)
    {
        // Initialize counts of different
        // subsequences caused by different
        // combination of 'a'
        int aCount = 0;

        // Initialize counts of different
        // subsequences caused by different
        // combination of 'a' and
        // different combination of 'b'
        int bCount = 0;

        // Initialize counts of different
        // subsequences caused by different
        // combination of 'a', 'b' and 'c'
        int cCount = 0;

        // Traverse all characters of given string
        for (int i = 0; i < s.Length; i++) {

            // If current character is 'a', then
            // there are following possibilities :
            // a) Current character begins a
            // new subsequence.
            // b) Current character is part
            // of aCount subsequences
            // c) Current character is not part
            // of aCount subsequences.

            if (s[i] == 'a')
                aCount = (1 + 2 * aCount);

            // If current character is 'b', then
            // there are following possibilities :
            // a) Current character begins a new
            // subsequence of b's with aCount
            // subsequences.
            // b) Current character is part of bCount
            // subsequences.
            // c) Current character is not part of
            // bCount subsequences.
            else if (s[i] == 'b')
                bCount = (aCount + 2 * bCount);

            // If current character is 'c', then
            // there are following possibilities :
            // a) Current character begins a new
            // subsequence of c's with bCount
            // subsequences.
            // b) Current character is part of cCount
            // subsequences.
            // c) Current character is not part of
            // cCount subsequences.
            else if (s[i] == 'c')
                cCount = (bCount + 2 * cCount);
        }

        return cCount;
    }

    // Driver code
    public static void Main()
    {
        String s = "abbc";
        Console.Write(countSubsequences(s));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count subsequences
// of the form a^i b^j c^k

// Returns count of subsequences
// of the form a^i b^j c^k
function countSubsequences($s)
{

    // Initialize counts of
    // different subsequences
    // caused by different
    // combination of 'a'
    $aCount = 0;

    // Initialize counts of
    // different subsequences
    // caused by different
    // combination of 'a' and
    // different combination of 'b'
    $bCount = 0;

    // Initialize counts of
    // different subsequences
    // caused by different
    // combination of 'a', 'b'
    // and 'c'.
    $cCount = 0;

    // Traverse all characters
    // of given string
    for($i = 0; $i < strlen($s); $i++)
    {

        /* If current character is 'a', then
        there are following possibilities :
            a) Current character begins a new
                subsequence.
            b) Current character is part of aCount
                subsequences.
            c) Current character is not part of
                aCount subsequences. */
        if ($s[$i] == 'a')
            $aCount = (1 + 2 * $aCount);

        /* If current character is 'b', then
        there are following possibilities :
            a) Current character begins a new
                subsequence of b's with aCount
                subsequences.
            b) Current character is part of bCount
                subsequences.
            c) Current character is not part of
                bCount subsequences. */
        else if ($s[$i] == 'b')
            $bCount = ($aCount + 2 * $bCount);

        /* If current character is 'c', then
        there are following possibilities :
            a) Current character begins a new
                subsequence of c's with bCount
                subsequences.
            b) Current character is part of cCount
                subsequences.
            c) Current character is not part of
                cCount subsequences. */
        else if ($s[$i] == 'c')
            $cCount = ($bCount + 2 * $cCount);
    }

    return $cCount;
}

    // Driver Code
    $s = "abbc";
    echo countSubsequences($s) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Returns count of subsequences
    // of the form a^i b^j c^k
    function countSubsequences(s)
    {
        // Initialize counts of different
        // subsequences caused by different
        // combination of 'a'
        let aCount = 0;

        // Initialize counts of different
        // subsequences caused by different
        // combination of 'a' and
        // different combination of 'b'
        let bCount = 0;

        // Initialize counts of different
        // subsequences caused by different
        // combination of 'a', 'b' and 'c'
        let cCount = 0;

        // Traverse all characters of given string
        for (let i = 0; i < s.length; i++) {

            // If current character is 'a', then
            // there are following possibilities :
            // a) Current character begins a
            // new subsequence.
            // b) Current character is part
            // of aCount subsequences
            // c) Current character is not part
            // of aCount subsequences.

            if (s[i] == 'a')
                aCount = (1 + 2 * aCount);

            // If current character is 'b', then
            // there are following possibilities :
            // a) Current character begins a new
            // subsequence of b's with aCount
            // subsequences.
            // b) Current character is part of bCount
            // subsequences.
            // c) Current character is not part of
            // bCount subsequences.
            else if (s[i] == 'b')
                bCount = (aCount + 2 * bCount);

            // If current character is 'c', then
            // there are following possibilities :
            // a) Current character begins a new
            // subsequence of c's with bCount
            // subsequences.
            // b) Current character is part of cCount
            // subsequences.
            // c) Current character is not part of
            // cCount subsequences.
            else if (s[i] == 'c')
                cCount = (bCount + 2 * cCount);
        }

        return cCount;
    }
// Driver Code

     let s = "abbc";
     document.write(countSubsequences(s));

</script>
```

**输出:**

```
3
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    需要遍历字符串一次。
*   **辅助空间:** O(1)。
    不需要额外的空间。

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。