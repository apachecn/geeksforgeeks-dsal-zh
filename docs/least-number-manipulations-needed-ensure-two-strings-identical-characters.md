# 确保两个字符串具有相同字符所需的最少操作次数

> 原文:[https://www . geesforgeks . org/最少数字操作-需要-确保-两个字符串-相同-字符/](https://www.geeksforgeeks.org/least-number-manipulations-needed-ensure-two-strings-identical-characters/)

给定两个字符串，返回确保两个字符串具有相同字符所需的最少操作次数的值，即两个字符串成为彼此的[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。

**示例:**

```
Input : s1 = "aab"
        s2 = "aba" 
Output :  2
Explanation : string 1 contains 2 a's and 1 b, 
also string 2 contains same characters

Input : s1 = "abc"
        s2 = "cdd"
Output : 2
Explanation : string 1 contains 1 a, 1 b, 1 c
while string 2 contains 1 c and 2 d's
so there are 2 different characters
```

**问题来源:**[Yatra.com 采访心得|第七集](https://www.geeksforgeeks.org/yatra-com-interview-experience-set-7/)

这个想法是为两个字符串分别创建一个额外的计数数组，然后计算字符的差异。

## C++

```
// C++ program to count least number
// of manipulations to have two strings
// set of same characters
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// return the count of manipulations
// required
int leastCount(string s1, string s2, int n)
{
    int count1[MAX_CHAR] = { 0 };
    int count2[MAX_CHAR] = { 0 };

    // count the number of different
    // characters in both strings
    for (int i = 0; i < n; i++) {
        count1[s1[i] - 'a'] += 1;
        count2[s2[i] - 'a'] += 1;
    }

    // check the difference in characters
    // by comparing count arrays
    int res = 0;
    for (int i = 0; i < MAX_CHAR; i++) {
        if (count1[i] != 0) {
            res += abs(count1[i] - count2[i]);
        }
    }
    return res;
}

// driver program
int main()
{
    string s1 = "abc";
    string s2 = "cdd";
    int len = s1.length();
    int res = leastCount(s1, s2, len);
    cout << res << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count least number
// of manipulations to have two
// strings set of same characters
import java.io.*;

public class GFG {

    static int MAX_CHAR = 26;

    // return the count of manipulations
    // required
    static int leastCount(String s1,
                        String s2, int n)
    {

        int[] count1 = new int[MAX_CHAR];
        int[] count2 = new int[MAX_CHAR];

        // count the number of different
        // characters in both strings
        for (int i = 0; i < n; i++)
        {
            count1[s1.charAt(i) - 'a'] += 1;
            count2[s2.charAt(i) - 'a'] += 1;
        }

        // check the difference in characters
        // by comparing count arrays
        int res = 0;

        for (int i = 0; i < MAX_CHAR; i++)
        {
            if (count1[i] != 0) {
                res += Math.abs(count1[i]
                                 - count2[i]);
            }
        }

        return res;
    }

    // driver program
    static public void main(String[] args)
    {
        String s1 = "abc";
        String s2 = "cdd";
        int len = s1.length();
        int res = leastCount(s1, s2, len);

        System.out.println(res);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to count least number
# of manipulations to have two strings
# set of same characters
MAX_CHAR = 26

# return the count of manipulations
# required
def leastCount(s1, s2, n):

    count1 = [0] * MAX_CHAR
    count2 = [0] * MAX_CHAR

    # count the number of different
    # characters in both strings
    for i in range ( n):
        count1[ord(s1[i]) - ord('a')] += 1
        count2[ord(s2[i]) - ord('a')] += 1

    # check the difference in characters
    # by comparing count arrays
    res = 0
    for i in range (MAX_CHAR):
        if (count1[i] != 0):
            res += abs(count1[i] - count2[i])

    return res

# Driver Code
if __name__ == "__main__":

    s1 = "abc"
    s2 = "cdd"
    l = len(s1)
    res = leastCount(s1, s2, l)
    print (res)

# This code is contributed by ita_c
```

## C#

```
// C# program to count least number
// of manipulations to have two strings
// set of same characters
using System;

public class GFG {

    static int MAX_CHAR = 26;

    // return the count of manipulations
    // required
    static int leastCount(string s1,
                        string s2, int n)
    {

        int[] count1 = new int[MAX_CHAR];
        int[] count2 = new int[MAX_CHAR];

        // count the number of different
        // characters in both strings
        for (int i = 0; i < n; i++)
        {
            count1[s1[i] - 'a'] += 1;
            count2[s2[i] - 'a'] += 1;
        }

        // check the difference in characters
        // by comparing count arrays
        int res = 0;
        for (int i = 0; i < MAX_CHAR; i++)
        {
            if (count1[i] != 0) {
                res += Math.Abs(count1[i]
                                - count2[i]);
            }
        }

        return res;
    }

    // driver program
    static public void Main()
    {
        string s1 = "abc";
        string s2 = "cdd";
        int len = s1.Length;
        int res = leastCount(s1, s2, len);
        Console.WriteLine(res);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// Javascript program to count least number
// of manipulations to have two
// strings set of same characters
let  MAX_CHAR = 26;

// Return the count of manipulations
// required
function leastCount(s1, s2, n)
{
    let count1 = new Array(MAX_CHAR);
    let count2 = new Array(MAX_CHAR);

    for(let i = 0; i < MAX_CHAR; i++)
    {
        count1[i] = 0;
        count2[i] = 0;
    }

    // Count the number of different
    // characters in both strings
    for(let i = 0; i < n; i++)
    {
        count1[s1[i].charCodeAt(0) -
                 'a'.charCodeAt(0)] += 1;
        count2[s2[i].charCodeAt(0) -
                 'a'.charCodeAt(0)] += 1;
    }

    // Check the difference in characters
    // by comparing count arrays
    let res = 0;

    for(let i = 0; i < MAX_CHAR; i++)
    {
        if (count1[i] != 0)
        {
            res += Math.abs(count1[i] - count2[i]);
        }
    }
    return res;
}

// Driver Code
let s1 = "abc";
let s2 = "cdd";
let len = s1.length;
let res = leastCount(s1, s2, len);

document.write(res);

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
2
```

本文由 [**曼德普·辛格**](https://github.com/msdeep14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。