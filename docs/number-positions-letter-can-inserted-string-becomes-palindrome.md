# 可以插入一个字母使一个字符串变成回文的位置数

> 原文:[https://www . geesforgeks . org/number-positions-letter-can-insert-string-变成-回文/](https://www.geeksforgeeks.org/number-positions-letter-can-inserted-string-becomes-palindrome/)

给定一个字符串 **str** ，我们需要找到一个字母(小写)可以插入的位置数，这样字符串就变成了回文。
**例:**

```
Input : str = "abca"
Output : possible palindromic strings: 
         1) acbca (at position 2)
         2) abcba (at position 4)
         Hence, the output is 2.

Input : str = "aaa"
Output : possible palindromic strings:
         1) aaaa
         2) aaaa
         3) aaaa
         4) aaaa
         Hence, the output is 4\. 
```

**幼稚法:**这种方法是在每个可能的位置，即 N+1 个位置插入全部 26 个字母，并在每个位置检查这种插入是否使其成为回文并增加计数。
**有效方法:**
首先你必须观察到，我们必须只在该点的字符违反回文条件时进行插入，即![S[i] != S[N-i-1]  ](img/17b5c63a00cd3d993015d4dabdce3cb4.png "Rendered by QuickLaTeX.com")。现在基于以上事实会有两种情况:
**情况一:**如果给定的字符串已经是回文
那我们只能在插入不违反回文的位置插入。
1)如果长度是偶数，那么我们总是可以在中间插入任何一个字母。
2)如果长度是奇数，那么我们可以在中间、左边或右边插入字母。
3)在这两种情况下，我们都可以在等于:
**(中间字母左侧连续 ch 的数量)*2** 的位置插入中间的字母(让它成为**‘CH’**)。
**例二:**如果不是回文
如上所述，我们应该从![S[i] != S[N-1-i]  ](img/50d24419582311fe26bf6d67c74b4a93.png "Rendered by QuickLaTeX.com")的位置开始插入，所以我们增加计数，检查其他位置的插入是否成为回文。
1)如果![S[i]...S[N-i-2]  ](img/b5ef7c8d22a2b564fb35272d12f80373.png "Rendered by QuickLaTeX.com")是回文，那么我们可以在![S[i]  ](img/140989c170562f374a74dc046000690b.png "Rendered by QuickLaTeX.com")之前的任意位置插入*直到![S[K] != S[N-i-1]  ](img/91df297ecf5fda658eec163d53e51740.png "Rendered by QuickLaTeX.com")， **K** 在![[i-1, 0]  ](img/31e76097444b84add259e79acf301c27.png "Rendered by QuickLaTeX.com")范围内。(*字母= S[N-i-1])
2。)如果![S[i+1]...S[N-i-1]  ](img/3cfe7d478c7c8a2ee042e8e190536a4f.png "Rendered by QuickLaTeX.com")是回文，那么我们可以在![S[n-i-1]  ](img/b85eda9ce33434ff0088e9ce7c2b53c7.png "Rendered by QuickLaTeX.com")之后的任意位置插入*直到![S[K] != S[i]  ](img/44fb9b1ba71aee903cd71ffc72f27a07.png "Rendered by QuickLaTeX.com")， **K** 在范围![[N-i, N-1]  ](img/10db2cdd3028e7d7b142aa1b24661ecc.png "Rendered by QuickLaTeX.com")内。(*字母= S[i])
在所有情况下，我们都会不断增加计数。

## C++

```
// CPP code to find the no.of positions where a
// letter can be inserted to make it a palindrome
#include <bits/stdc++.h>
using namespace std;

// Function to check if the string is palindrome
bool isPalindrome(string &s, int i, int j)
{
    int p = j;
    for (int k = i; k <= p; k++) {
        if (s[k] != s[p])
            return false;
        p--;
    }
    return true;
}

int countWays(string &s)
{
    // to know the length of string
    int n = s.length();
    int count = 0;

    // if the given string is a palindrome(Case-I)
    if (isPalindrome(s, 0, n - 1))
    {
        // Sub-case-III)
        for (int i = n / 2; i < n; i++)
        {
            if (s[i] == s[i + 1])
                count++;
            else
                break;
        }
        if (n % 2 == 0) // if the length is even
        {
            count++;
            count = 2 * count + 1; // sub-case-I
        } else
            count = 2 * count + 2; // sub-case-II
    } else {
        for (int i = 0; i < n / 2; i++) {

            // insertion point
            if (s[i] != s[n - 1 - i])
            {
                int j = n - 1 - i;

                // Case-I
                if (isPalindrome(s, i, n - 2 - i))
                {
                    for (int k = i - 1; k >= 0; k--) {
                        if (s[k] != s[j])
                            break;
                        count++;
                    }
                    count++;
                }

                // Case-II
                if (isPalindrome(s, i + 1, n - 1 - i))
                {
                    for (int k = n - i; k < n; k++) {
                        if (s[k] != s[i])
                            break;
                        count++;
                    }
                    count++;
                }
                break;
            }
        }
    }

    return count;
}

// Driver code
int main()
{
    string s = "abca";
    cout << countWays(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the no.of positions where a
// letter can be inserted to make it a palindrome

import java.io.*;

class GFG {

    // Function to check if the string is palindrome
    static boolean isPalindrome(String s, int i, int j)
    {
        int p = j;
        for (int k = i; k <= p; k++) {
            if (s.charAt(k) != s.charAt(p))
                return false;
            p--;
        }

        return true;
    }

    static int countWays(String s)
    {

        // to know the length of string
        int n = s.length();
        int count = 0;

        // if the given string is a palindrome(Case-I)
        if (isPalindrome(s, 0, n - 1)) {

            // Sub-case-III)
            for (int i = n / 2; i < n; i++) {
                if (s.charAt(i) == s.charAt(i + 1))
                    count++;
                else
                    break;
            }

            if (n % 2 == 0) // if the length is even
            {
                count++;
                count = 2 * count + 1; // sub-case-I
            }
            else
                count = 2 * count + 2; // sub-case-II
        }
        else {
            for (int i = 0; i < n / 2; i++) {

                // insertion point
                if (s.charAt(i) != s.charAt(n - 1 - i)) {
                    int j = n - 1 - i;

                    // Case-I
                    if (isPalindrome(s, i, n - 2 - i)) {
                        for (int k = i - 1; k >= 0; k--) {
                            if (s.charAt(k) != s.charAt(j))
                                break;
                            count++;
                        }
                        count++;
                    }

                    // Case-II
                    if (isPalindrome(s, i + 1, n - 1 - i)) {
                        for (int k = n - i; k < n; k++) {
                            if (s.charAt(k) != s.charAt(i))
                                break;
                            count++;
                        }
                        count++;
                    }
                    break;
                }
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abca";
        System.out.println(countWays(s));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 code to find the no.of positions
# where a letter can be inserted to make it
# a palindrome

# Function to check if the string
# is palindrome
def isPalindrome(s, i, j):

    p = j
    for k in range(i, p + 1):
        if (s[k] != s[p]):
            return False
        p -= 1

    return True

def countWays(s):

    # to know the length of string
    n = len(s)
    count = 0

    # if the given string is a palindrome(Case-I)
    if (isPalindrome(s, 0, n - 1)) :

        # Sub-case-III)
        for i in range(n // 2, n):

            if (s[i] == s[i + 1]):
                count += 1
            else:
                break

        if (n % 2 == 0): # if the length is even
            count += 1
            count = 2 * count + 1 # sub-case-I
        else:
            count = 2 * count + 2 # sub-case-II
    else :
        for i in range(n // 2) :

            # insertion point
            if (s[i] != s[n - 1 - i]) :
                j = n - 1 - i

                # Case-I
                if (isPalindrome(s, i, n - 2 - i)) :
                    for k in range(i - 1, -1, -1):
                        if (s[k] != s[j]):
                            break
                        count += 1

                    count += 1

                # Case-II
                if (isPalindrome(s, i + 1, n - 1 - i)) :
                    for k in range(n - i, n) :
                        if (s[k] != s[i]):
                            break
                        count += 1

                    count += 1

                break

    return count

# Driver code
if __name__ == "__main__":

    s = "abca"
    print(countWays(s))

# This code is contributed by ita_c
```

## C#

```
// C# code to find the no. of positions
// where a letter can be inserted
// to make it a palindrome.
using System;

class GFG {

    // Function to check if the
    // string is palindrome
    static bool isPalindrome(String s, int i,
                                       int j)
    {
        int p = j;
        for (int k = i; k <= p; k++)
        {
            if (s[k] != s[p])
                return false;
            p--;
        }

        return true;
    }

    static int countWays(String s)
    {

        // to know the length of string
        int n = s.Length;
        int count = 0;

        // if the given string is
        // a palindrome(Case-I)
        if (isPalindrome(s, 0, n - 1)) {

            // Sub-case-III)
            for (int i = n / 2; i < n; i++) {
                if (s[i] == s[i + 1])
                    count++;
                else
                    break;
            }

            // if the length is even
            if (n % 2 == 0)
            {
                count++;

                // sub-case-I
                count = 2 * count + 1;
            }
            else

                // sub-case-II
                count = 2 * count + 2;
        }
        else {
            for (int i = 0; i < n / 2; i++) {

                // insertion point
                if (s[i] != s[n - 1 - i]) {
                    int j = n - 1 - i;

                    // Case-I
                    if (isPalindrome(s, i, n - 2 - i)) {
                        for (int k = i - 1; k >= 0; k--) {
                            if (s[k] != s[j])
                                break;
                            count++;
                        }
                        count++;
                    }

                    // Case-II
                    if (isPalindrome(s, i + 1, n - 1 - i)) {
                        for (int k = n - i; k < n; k++) {
                            if (s[k] != s[i])
                                break;
                            count++;
                        }
                        count++;
                    }
                    break;
                }
            }
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        String s = "abca";
        Console.Write(countWays(s));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the no. of
// positions where a letter can
// be inserted to make it a palindrome

// Function to check if the
// string is palindrome
function isPalindrome($s, $i, $j)
{
    $p = $j;
    for ($k = $i; $k <= $p; $k++)
    {
        if ($s[$k] != $s[$p])
            return false;
        $p--;
    }
    return true;
}

function countWays($s)
{

    // to know the length of string
    $n = strlen($s);
    $count = 0;

    // if the given string is
    // a palindrome(Case-I)
    if (isPalindrome($s, 0, $n - 1))
    {

        // Sub-case-III)
        for ($i = $n / 2; $i < $n; $i++)
        {
            if ($s[$i] == $s[$i + 1])
                $count++;
            else
                break;
        }

        // if the length is even
        if ($n % 2 == 0)
        {
            $count++;

            // sub-case-I
            $count = 2 * $count + 1;
        }
        else

            // sub-case-II
            $count = 2 * $count + 2;
    }
    else
    {
        for ($i = 0; $i < $n / 2; $i++)
        {

            // insertion point
            if ($s[$i] != $s[$n - 1 - $i])
            {
                $j = $n - 1 - $i;

                // Case-I
                if (isPalindrome($s, $i, $n - 2 - $i))
                {
                    for ($k = $i - 1; $k >= 0; $k--)
                    {
                        if ($s[$k] != $s[$j])
                            break;
                        $count++;
                    }
                    $count++;
                }

                // Case-II
                if (isPalindrome($s, $i + 1,$n - 1 - $i))
                {
                    for ($k = $n - $i; $k < $n; $k++)
                    {
                        if ($s[$k] != $s[$i])
                            break;
                        $count++;
                    }
                    $count++;
                }
                break;
            }
        }
    }

    return $count;
}

// Driver code
$s = "abca";
echo countWays($s) ;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// Javascript code to find the no.of positions where a
// letter can be inserted to make it a palindrome   
    function isPalindrome(s,i,j)
    {
        let p = j;
    for (let k = i; k <= p; k++)
    {
        if (s[k] != s[p])
            return false;
        p--;
    }
    return true;
    }

// Function to check if the string is palindrome
function countWays(s)
{

    // to know the length of string
    let n = s.length;
    let count = 0;

    // if the given string is a palindrome(Case-I)
    if (isPalindrome(s, 0, n - 1))
    {

        // Sub-case-III)
        for (let i = n / 2; i < n; i++)
        {
            if (s[i] == s[i + 1])
                count++;
            else
                break;
        }
        if (n % 2 == 0) // if the length is even
        {
            count++;
            count = 2 * count + 1; // sub-case-I
        } else
            count = 2 * count + 2; // sub-case-II
    } else {
        for (let i = 0; i < n / 2; i++) {

            // insertion point
            if (s[i] != s[n - 1 - i])
            {
                let j = n - 1 - i;

                // Case-I
                if (isPalindrome(s, i, n - 2 - i))
                {
                    for (let k = i - 1; k >= 0; k--) {
                        if (s[k] != s[j])
                            break;
                        count++;
                    }
                    count++;
                }

                // Case-II
                if (isPalindrome(s, i + 1, n - 1 - i))
                {
                    for (let k = n - i; k < n; k++) {
                        if (s[k] != s[i])
                            break;
                        count++;
                    }
                    count++;
                }
                break;
            }
        }
    }

    return count;
}

// Driver code
let s = "abca";
document.write( countWays(s));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
2
```

本文由**哈沙·莫加利**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。