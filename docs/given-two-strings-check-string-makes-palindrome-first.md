# 给定两个字符串，先检查哪个字符串构成回文

> 原文:[https://www . geesforgeks . org/given-two-string-check-string-makes-回文-first/](https://www.geeksforgeeks.org/given-two-strings-check-string-makes-palindrome-first/)

给定两个长度相等的字符串“A”和“B”。两个玩家玩一个游戏，他们都从各自的字符串中选择一个字符(第一个从 A 中选择，第二个从 B 中选择)，并放入第三个字符串(最初是空的)。能做出第三串回文的玩家，就是赢家。如果第一个玩家先做回文，然后打印“A”，否则打印“B”。如果字符串变空，没有人能组成回文，那么打印“B”。
**例:**

```
Input : A = ab
        B = ab
Output : B
First player puts 'a' (from string A)
Second player puts 'a' (from string B) 
which make palindrome. 
The result would be same even if A picks
'b' as first character.

Input : A = aba
        B = cde
Output : A

Input : A = ab
        B = cd
Output : B
None of the string will be able to
make a palindrome (of length > 1)
in any situation. So B will win.
```

举几个例子后，我们可以观察到‘A’(或第一个玩家)只有当它有一个角色出现不止一次，并且没有出现在‘B’中时，才能获胜。

## C++

```
// Given two strings, check which string
// makes palindrome first.
#include<bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// returns winner of two strings
char stringPalindrome(string A, string B)
{
    // Count frequencies of characters in
    // both given strings
    int countA[MAX_CHAR] = {0};
    int countB[MAX_CHAR] = {0};
    int l1 = A.length(), l2 = B.length();
    for(int i=0; i<l1;i++)
        countA[A[i]-'a']++;
    for(int i=0; i<l2;i++)
        countB[B[i]-'a']++;

    // Check if there is a character that
    // appears more than once in A and does
    // not appear in B
    for (int i=0 ;i <26;i++)
        if ((countA[i] >1 && countB[i] == 0))
           return 'A';

    return 'B';
}

// Driver Code
int main()
{
    string a = "abcdea";
    string b = "bcdesg";
    cout << stringPalindrome(a,b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check which string
// makes palindrome first.
public class First_Palin {

    static final int MAX_CHAR = 26;

    // returns winner of two strings
    static char stringPalindrome(String A, String B)
    {
        // Count frequencies of characters in
        // both given strings
        int[] countA = new int[MAX_CHAR];
        int[] countB = new int[MAX_CHAR];

        int l1 = A.length();
        int l2 = B.length();

        for (int i = 0; i < l1; i++)
            countA[A.charAt(i) - 'a']++;

        for (int i = 0; i < l2; i++)
            countB[B.charAt(i) - 'a']++;

        // Check if there is a character that
        // appears more than once in A and does
        // not appear in B
        for (int i = 0; i < 26; i++)
            if ((countA[i] > 1 && countB[i] == 0))
                return 'A';

        return 'B';
    }

    // Driver Code
public static void main(String args[])
    {
        String a = "abcdea";
        String b = "bcdesg";
        System.out.println(stringPalindrome(a, b));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Given two strings, check which string
# makes palindrome first.

MAX_CHAR = 26

# returns winner of two strings
def stringPalindrome(A, B):

    # Count frequencies of characters
    # in both given strings
    countA = [0] * MAX_CHAR
    countB = [0] * MAX_CHAR
    l1 = len(A)
    l2 = len(B)
    for i in range(l1):
        countA[ord(A[i]) - ord('a')] += 1
    for i in range(l2):
        countB[ord(B[i]) - ord('a')] += 1

    # Check if there is a character that
    # appears more than once in A and
    # does not appear in B
    for i in range(26):
        if ((countA[i] > 1 and countB[i] == 0)):
            return 'A'
    return 'B'

# Driver Code
if __name__ == '__main__':
    a = "abcdea"
    b = "bcdesg"
    print(stringPalindrome(a, b))

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to check which string
// makes palindrome first.
using System;

class First_Palin {

    static int MAX_CHAR = 26;

    // returns winner of two strings
    static char stringPalindrome(string A, string B)
    {
        // Count frequencies of characters in
        // both given strings
        int[] countA = new int[MAX_CHAR];
        int[] countB = new int[MAX_CHAR];

        int l1 = A.Length;
        int l2 = B.Length;

        for (int i = 0; i < l1; i++)
            countA[A[i] - 'a']++;

        for (int i = 0; i < l2; i++)
            countB[B[i] - 'a']++;

        // Check if there is a character that
        // appears more than once in A and does
        // not appear in B
        for (int i = 0; i < 26; i++)
            if ((countA[i] > 1 && countB[i] == 0))
                return 'A';

        return 'B';
    }

    // Driver Code
    public static void Main()
    {
        string a = "abcdea";
        string b = "bcdesg";
    Console.WriteLine(stringPalindrome(a, b));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Given two strings, check which string
// makes palindrome first.

$MAX_CHAR = 26;

// returns winner of two strings
function stringPalindrome($A, $B)
{
    global $MAX_CHAR;

    // Count frequencies of characters in
    // both given strings
    $countA = array_fill(0, $MAX_CHAR, 0);
    $countB = array_fill(0, $MAX_CHAR, 0);
    $l1 = strlen($A);
    $l2 = strlen($B);
    for($i = 0; $i < $l1; $i++)
        $countA[ord($A[$i])-ord('a')]++;
    for($i = 0; $i < $l2; $i++)
        $countB[ord($B[$i])-ord('a')]++;

    // Check if there is a character that
    // appears more than once in A and does
    // not appear in B
    for ($i = 0 ; $i < 26; $i++)
        if (($countA[$i] > 1 && $countB[$i] == 0))
        return 'A';

    return 'B';
}

    // Driver Code
    $a = "abcdea";
    $b = "bcdesg";
    echo stringPalindrome($a,$b);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to check which string
// makes palindrome first.

    var MAX_CHAR = 26;

    // returns winner of two strings
    function stringPalindrome(A, B)
    {
        // Count frequencies of characters in
        // both given strings
        var countA = Array.from({length: MAX_CHAR}, (_, i) => 0);
        var countB = Array.from({length: MAX_CHAR}, (_, i) => 0);

        var l1 = A.length;
        var l2 = B.length;

        for (var i = 0; i < l1; i++)
            countA[A.charAt(i).charCodeAt(0) - 'a'.charCodeAt(0)]++;

        for (var i = 0; i < l2; i++)
            countB[B.charAt(i).charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // Check if there is a character that
        // appears more than once in A and does
        // not appear in B
        for (var i = 0; i < 26; i++)
            if ((countA[i] > 1 && countB[i] == 0))
                return 'A';

        return 'B';
    }

    // Driver Code
    var a = "abcdea";
    var b = "bcdesg";
    document.write(stringPalindrome(a, b));

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
A
```

本文由**阿克谢·拉杰普特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。