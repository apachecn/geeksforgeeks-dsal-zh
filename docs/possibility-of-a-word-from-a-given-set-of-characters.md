# 从给定的一组字符中选择一个单词的可能性

> 原文:[https://www . geesforgeks . org/给定字符集的单词可能性/](https://www.geeksforgeeks.org/possibility-of-a-word-from-a-given-set-of-characters/)

给定两个字符串“s”和“q”，检查 q 的所有字符是否都出现在“s”中。
示例:

```
Example:
Input: s = "abctd"
       q = "cat"
Output: Yes
Explanation:
All characters of "cat" are
present in "abctd"

Input: s = dog
       hod
Output: No
Explanation:
Given query 'hod' hod has the letter
'h' which is not available in set 'dog', 
hence the output is no.
```

一个**简单的解决方法**就是逐个尝试所有的角色。在“q”中找出它的出现次数，然后在“s”中找出它的出现次数。“q”中的出现次数必须小于或等于“s”中的相同次数。如果所有字符都满足此条件，则返回 true。否则返回 false。
一个**有效的解决方案**是创建一个长度为 256(可能字符数)的频率数组，并将其初始化为 0。然后我们计算每个元素在 s 中出现的频率。在对' s '中的字符进行计数后，我们遍历' q '并检查每个字符的频率是否小于它在' s '中的频率，方法是降低它在为' s '构造的频率数组中的频率。
下面给出的是上述方法的实施

## C++

```
// CPP program to check if a query string
// is present is given set.
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 256;

bool isPresent(string s, string q)
{
    // Count occurrences of all characters
    // in s.
    int freq[MAX_CHAR] = { 0 };
    for (int i = 0; i < s.length(); i++)
        freq[s[i]]++;

    // Check if number of occurrences of
    // every character in q is less than
    // or equal to that in s.
    for (int i = 0; i < q.length(); i++) {
        freq[q[i]]--;
        if (freq[q[i]] < 0)
           return false;
    }

    return true;
}

// driver program
int main()
{
    string s = "abctd";
    string q = "cat";

    if (isPresent(s, q))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to check if a query
// string is present is given set.
import java.io.*;

public class GFG {

    static int MAX_CHAR = 256;

    static boolean isPresent(String s, String q)
    {

        // Count occurrences of all
        // characters in s.
        int []freq = new int[MAX_CHAR];
        for (int i = 0; i < s.length(); i++)
            freq[s.charAt(i)]++;

        // Check if number of occurrences of
        // every character in q is less than
        // or equal to that in s.
        for (int i = 0; i < q.length(); i++)
        {
            freq[q.charAt(i)]--;

            if (freq[q.charAt(i)] < 0)
                return false;
        }

        return true;
    }

    // driver program
    static public void main (String[] args)
    {
        String s = "abctd";
        String q = "cat";

        if (isPresent(s, q))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to check if a query
# string is present is given set.
MAX_CHAR = 256

def isPresent(s, q):

    # Count occurrences of all characters
    # in s.
    freq = [0] *  MAX_CHAR
    for i in range(0 , len(s)):
        freq[ord(s[i])] += 1

    # Check if number of occurrences of
    # every character in q is less than
    # or equal to that in s.
    for i in range(0, len(q)):
        freq[ord(q[i])] -= 1
        if (freq[ord(q[i])] < 0):
            return False

    return True

# driver program
s = "abctd"
q = "cat"

if (isPresent(s, q)):
    print("Yes")
else:
    print("No")

# This code is contributed by Smitha
```

## C#

```
// C# program to check if a query
// string is present is given set.
using System;

public class GFG {

    static int MAX_CHAR = 256;

    static bool isPresent(string s, string q)
    {

        // Count occurrences of all
        // characters in s.
        int []freq = new int[MAX_CHAR];

        for (int i = 0; i < s.Length; i++)
            freq[s[i]]++;

        // Check if number of occurrences of
        // every character in q is less than
        // or equal to that in s.
        for (int i = 0; i < q.Length; i++)
        {
            freq[q[i]]--;

            if (freq[q[i]] < 0)
                return false;
        }

        return true;
    }

    // driver program
    static public void Main ()
    {
        string s = "abctd";
        string q = "cat";

        if (isPresent(s, q))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a query string
// is present is given set.

function isPresent($s, $q)
{

    // Count occurrences of
    // all characters in s.
    $freq = array(256);
    for ($i = 0; $i < 256; $i++)
        $freq[$i] = 0;

    for ($i = 0; $i < strlen($s); $i++)
        $freq[ ord($s[$i]) - ord('a') ]++ ;

    // Check if number of occurrences of
    // every character in q is less than
    // or equal to that in s.
    for ($i = 0; $i < strlen($q); $i++)
    {
        $freq[ord($q[$i]) - ord('a')]--;
        if ($freq[ord($q[$i]) - ord('a')] < 0)
        return false;
    }

    return true;
}

    // Driver Code
    $s = "abctd";
    $q = "cat";

    if (isPresent($s, $q))
        echo "Yes";
    else
        echo "No";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if a query
    // string is present is given set.

    let MAX_CHAR = 256;

    function isPresent(s, q)
    {

        // Count occurrences of all
        // characters in s.
        let freq = new Array(MAX_CHAR);
        freq.fill(0);

        for (let i = 0; i < s.length; i++)
            freq[s[i]]++;

        // Check if number of occurrences of
        // every character in q is less than
        // or equal to that in s.
        for (let i = 0; i < q.length; i++)
        {
            freq[q[i]]--;

            if (freq[q[i]] < 0)
                return false;
        }

        return true;
    }

    let s = "abctd";
    let q = "cat";

    if (isPresent(s, q))
      document.write("Yes");
    else
      document.write("No");

</script>
```

输出:

```
Yes
```

**时间复杂度:** O(n)
本文由[**twickl Bajaj**](https://auth.geeksforgeeks.org/profile.php?user=Twinkl Bajaj)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。