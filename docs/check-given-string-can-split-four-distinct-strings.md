# 检查给定的字符串是否可以分成四个不同的字符串

> 原文:[https://www . geesforgeks . org/check-given-string-can-split-四个不同的字符串/](https://www.geeksforgeeks.org/check-given-string-can-split-four-distinct-strings/)

给定一个字符串，任务是检查我们是否可以将它分成 4 个字符串，这样每个字符串都不是空的，并且彼此不同。

**示例:**

```
Input : str[] = "geeksforgeeks"
Output : Yes
"geeks", "for", "gee", "ks" are four 
distinct strings that can form from
given string.

Input : str[] = "aaabb"
Output : No
```

观察如果字符串的长度大于等于 10，那么每次都可以拆分成四部分。假设，长度是 10，那么长度为 1，2，3，4 的字符串可以被制作。
对于长度小于 10 的字符串，我们可以使用蛮力，即迭代所有可能的字符串分割方法，并检查每一种方法。

```
If length is more than 10
   return true
Else (If length is less than 10)
   Use Brute Force method to check
   if we can break it in four distinct
   strings.
```

以下是上述想法的实现。

## C++

```
// C++ program to check if we can break a string
// into four distinct strings.
#include<bits/stdc++.h>
using namespace std;

// Return if the given string can be split or not.
bool check(string s)
{
    // We can always break a string of size 10 or
    // more into four distinct strings.
    if (s.size() >= 10)
        return true;

    // Brute Force
    for (int i =1; i < s.size(); i++)
    {
        for (int j = i + 1; j < s.size(); j++)
        {
            for (int k = j + 1; k < s.size(); k++)
            {
                // Making 4 string from the given string
                string s1 = s.substr(0, i);
                string s2 = s.substr(i, j - i);
                string s3 = s.substr(j, k - j);
                string s4 = s.substr(k, s.size() - k);

                // Checking if they are distinct or not.
                if (s1 != s2 && s1 != s3 && s1 != s4 &&
                        s2 != s3 && s2 != s4 && s3 != s4)
                    return true;
            }
        }
    }

    return false;
}

// Driven Program
int main()
{
    string str = "aaabb";

    (check(str))? (cout << "Yes" << endl):
                  (cout << "No" << endl);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if we can break a string
// into four distinct strings.
class GFG
{

    // Return true if both strings are equal
    public static boolean strcheck(String s1, String s2)
    {
        if (s1.compareTo(s2) != 0)
            return false;
        return true;
    }

    // Return if the given string can be split or not.
    public static boolean check(String s)
    {
        if (s.length() >= 10)
            return true;

        // Brute Force
        for (int i = 1; i < s.length(); i++)
        {
            for (int j = i + 1; j < s.length(); j++)
            {
                for (int k = j + 1; k < s.length(); k++)
                {

                    // Making 4 string from the given string
                    String s1 = "", s2 = "", s3 = "", s4 = "";
                    try
                    {
                        s1 = s.substring(0, i);
                        s2 = s.substring(i, j - i);
                        s3 = s.substring(j, k - j);
                        s4 = s.substring(k, s.length() - k);
                    }
                    catch (StringIndexOutOfBoundsException e) {
                    }

                    // Checking if they are distinct or not.
                    if (strcheck(s1, s2) && strcheck(s1, s3) &&
                        strcheck(s1, s4) && strcheck(s2, s3) &&
                        strcheck(s2, s4) && strcheck(s3, s4))
                        return true;
                }
            }
        }

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "aaabb";
        if (check(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to check if we can
# break a into four distinct strings.

# Return if the given string can be
# split or not.
def check(s):

    # We can always break a of size 10 or
    # more into four distinct strings.
    if (len(s) >= 10):
        return True

    # Brute Force
    for i in range(1, len(s)):

        for j in range(i + 1, len(s)):

            for k in range(j + 1, len(s)):

                # Making 4 from the given
                s1 = s[0:i]
                s2 = s[i:j - i]
                s3 = s[j: k - j]
                s4 = s[k: len(s) - k]

                # Checking if they are distinct or not.
                if (s1 != s2 and s1 != s3 and s1 != s4 and
                    s2 != s3 and s2 != s4 and s3 != s4):
                    return True

    return False

# Driver Code
if __name__ == '__main__':
    str = "aaabb"

    print("Yes") if(check(str)) else print("NO")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to check if we can break a string
// into four distinct strings.
using System;

class GFG
{

    // Return true if both strings are equal
    public static Boolean strcheck(String s1,
                                   String s2)
    {
        if (s1.CompareTo(s2) != 0)
            return false;
        return true;
    }

    // Return if the given string
    // can be split or not.
    public static Boolean check(String s)
    {
        if (s.Length >= 10)
            return true;

        // Brute Force
        for (int i = 1; i < s.Length; i++)
        {
            for (int j = i + 1; j < s.Length; j++)
            {
                for (int k = j + 1; k < s.Length; k++)
                {

                    // Making 4 string from the given string
                    String s1 = "", s2 = "",
                           s3 = "", s4 = "";
                    try
                    {
                        s1 = s.Substring(0, i);
                        s2 = s.Substring(i, j - i);
                        s3 = s.Substring(j, k - j);
                        s4 = s.Substring(k, s.Length - k);
                    }
                    catch (Exception e) {
                    }

                    // Checking if they are distinct or not.
                    if (strcheck(s1, s2) && strcheck(s1, s3) &&
                        strcheck(s1, s4) && strcheck(s2, s3) &&
                        strcheck(s2, s4) && strcheck(s3, s4))
                        return true;
                }
            }
        }
        return false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "aaabb";
        if (check(str))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to check if we can break a string
    // into four distinct strings.

    // Return true if both strings are equal
    function strcheck(s1, s2)
    {
        if (s1.localeCompare(s2) != 0)
            return false;
        return true;
    }

    // Return if the given string can be split or not.
    function check(s)
    {
        if (s.length >= 10)
            return true;

        // Brute Force
        for (let i = 1; i < s.length; i++)
        {
            for (let j = i + 1; j < s.length; j++)
            {
                for (let k = j + 1; k < s.length; k++)
                {

                    // Making 4 string from the given string
                    let s1 = "", s2 = "", s3 = "", s4 = "";
                    s1 = s.substring(0, i);
                    s2 = s.substring(i, i + j - i);
                    s3 = s.substring(j, j + k - j);
                    s4 = s.substring(k, k + s.length - k);

                    // Checking if they are distinct or not.
                    if (strcheck(s1, s2) && strcheck(s1, s3) &&
                        strcheck(s1, s4) && strcheck(s2, s3) &&
                        strcheck(s2, s4) && strcheck(s3, s4))
                        return true;
                }
            }
        }

        return false;
    }

    let str = "aaabb";
    if (check(str))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**输出:**

```
No
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。