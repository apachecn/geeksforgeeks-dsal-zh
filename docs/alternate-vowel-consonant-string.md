# 交替元音和辅音串

> 原文:[https://www . geesforgeks . org/alternate-元音-辅音-string/](https://www.geeksforgeeks.org/alternate-vowel-consonant-string/)

给定一个字符串，重新排列给定字符串的字符，使元音和辅音交替出现。如果字符串不能以所需的方式重新排列，请打印“没有这样的字符串”。元音相对于彼此的顺序和辅音相对于彼此的顺序应该保持。
如果可以形成一个以上的所需字符串，则按字典顺序打印较小的字符串。
**例:**

```
Input : geeks
Output : gekes

Input : onse
Output : nose
There are two possible outcomes
"nose" and "ones".  Since "nose"
is lexicographically smaller, we 
print it.
```

1.  统计给定字符串中元音和辅音的数量。
2.  如果计数之间的差异大于 1，则返回“不可能”。
3.  如果元音比辅音多，先打印第一个元音，然后重复剩余的字符串。
4.  如果辅音多于元音，则先打印第一个辅音，并对剩余的字符串重复。
5.  如果计数相同，比较第一个元音和第一个辅音，先打印较小的一个。

## C++

```
// C++ implementation of alternate vowel and
// consonant string
#include <bits/stdc++.h>
using namespace std;

// 'ch' is vowel or not
bool isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i' ||
            ch == 'o' || ch =='u')
        return true;
    return false;
}

// create alternate vowel and consonant string
// str1[0...l1-1] and str2[start...l2-1]
string createAltStr(string str1, string str2,
                    int start, int l)
{
    string finalStr = "";

    // first adding character of vowel/consonant
    // then adding character of consonant/vowel
    for (int i=0, j=start; j<l; i++, j++)
        finalStr = (finalStr + str1.at(i)) + str2.at(j);
    return finalStr;
}

// function to find the required
// alternate vowel and consonant string
string findAltStr(string str)
{
    int nv = 0, nc = 0;
    string vstr = "", cstr = "";
    int l = str.size();
    for (int i=0; i<l; i++)
    {
        char ch = str.at(i);

        // count vowels and update vowel string
        if (isVowel(ch))
        {
            nv++;
            vstr = vstr + ch;
        }

        // count consonants and update consonant
        // string
        else
        {
            nc++;
            cstr = cstr + ch;
        }
    }

    // no such string can be formed
    if (abs(nv-nc) >= 2)
        return "no such string";

    // remove first character of vowel string
    // then create alternate string with
    // cstr[0...nc-1] and vstr[1...nv-1]
    if (nv > nc)
        return (vstr.at(0) + createAltStr(cstr, vstr, 1, nv));

    // remove first character of consonant string
    // then create alternate string with
    // vstr[0...nv-1] and cstr[1...nc-1]
    if (nc > nv)
        return (cstr.at(0) + createAltStr(vstr, cstr, 1, nc));

    // if both vowel and consonant
    // strings are of equal length
    // start creating string with consonant
    if (cstr.at(0) < vstr.at(0))
        return createAltStr(cstr, vstr, 0, nv);

    // start creating string with vowel
    return createAltStr(vstr, cstr, 0, nc);
}

// Driver program to test above
int main()
{
    string str = "geeks";
    cout << findAltStr(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of alternate vowel and
// consonant string
import java.util.*;

class GFG
{

// 'ch' is vowel or not
static boolean isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i' ||
            ch == 'o' || ch =='u')
        return true;
    return false;
}

// create alternate vowel and consonant string
// str1[0...l1-1] and str2[start...l2-1]
static String createAltStr(String str1, String str2,
                    int start, int l)
{
    String finalStr = "";

    // first adding character of vowel/consonant
    // then adding character of consonant/vowel
    for (int i = 0, j = start; j < l; i++, j++)
        finalStr = (finalStr + str1.charAt(i)) +
                                    str2.charAt(j);
    return finalStr;
}

// function to find the required
// alternate vowel and consonant string
static String findAltStr(String str)
{
    int nv = 0, nc = 0;
    String vstr = "", cstr = "";
    int l = str.length();
    for (int i = 0; i < l; i++)
    {
        char ch = str.charAt(i);

        // count vowels and update vowel string
        if (isVowel(ch))
        {
            nv++;
            vstr = vstr + ch;
        }

        // count consonants and update consonant
        // string
        else
        {
            nc++;
            cstr = cstr + ch;
        }
    }

    // no such string can be formed
    if (Math.abs(nv - nc) >= 2)
        return "no such string";

    // remove first character of vowel string
    // then create alternate string with
    // cstr[0...nc-1] and vstr[1...nv-1]
    if (nv > nc)
        return (vstr.charAt(0) + createAltStr(cstr, vstr, 1, nv));

    // remove first character of consonant string
    // then create alternate string with
    // vstr[0...nv-1] and cstr[1...nc-1]
    if (nc > nv)
        return (cstr.charAt(0) + createAltStr(vstr, cstr, 1, nc));

    // if both vowel and consonant
    // strings are of equal length
    // start creating string with consonant
    if (cstr.charAt(0) < vstr.charAt(0))
        return createAltStr(cstr, vstr, 0, nv);

    // start creating string with vowel
    return createAltStr(vstr, cstr, 0, nc);
}

// Driver code
public static void main(String args[])
{
    String str = "geeks";
    System.out.println(findAltStr(str));
}
}

// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python implementation of alternate vowel
# and consonant string

# 'ch' is vowel or not
def isVowel(ch):
    if(ch == 'a' or ch == 'e' or
       ch == 'i' or ch == 'o' or
       ch == 'u'):
        return True
    return False

# create alternate vowel and consonant string
# str1[0...l1-1] and str2[start...l2-1]
def createAltStr(str1, str2, start, l):
    finalStr = ""
    i = 0

    # first adding character of vowel/consonant
    # then adding character of consonant/vowel
    for j in range(start, l):
        finalStr = (finalStr + str1[i]) + str2[j]
        i + 1

    return finalStr

# function to find the required
# alternate vowel and consonant string
def findAltStr(str1):
    nv = 0
    nc = 0
    vstr = ""
    cstr = ""
    l = len(str1)
    for i in range(0, l):

        # count vowels and update vowel string
        if(isVowel(str1[i])):
            nv += 1
            vstr = vstr + str1[i]

        # count consonants and update
        # consonant string
        else:
            nc += 1
            cstr = cstr + str1[i]

    # no such string can be formed
    if(abs(nv - nc) >= 2):
        return "no such string"

    # remove first character of vowel string
    # then create alternate string with
    # cstr[0...nc-1] and vstr[1...nv-1]
    if(nv > nc):
        return (vstr[0] + createAltStr(cstr, vstr, 1, nv))

    # remove first character of consonant string
    # then create alternate string with
    # vstr[0...nv-1] and cstr[1...nc-1]
    if(nc > nv):
        return (cstr[0] + createAltStr(vstr, cstr, 1, nc))

    # if both vowel and consonant
    # strings are of equal length
    # start creating string with consonant
    if(cstr[0] < vstr[0]):
        return createAltStr(cstr, vstr, 0, nv)

    return createAltStr(vstr, cstr, 0, nc)

# Driver Code
if __name__ == "__main__":
    str1 = "geeks"
    print(findAltStr(str1))

# This code is contributed by Sairahul099
```

## C#

```
// C# implementation of alternate vowel and
// consonant string
using System;

class GFG
{

// 'ch' is vowel or not
static Boolean isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i' ||
            ch == 'o' || ch =='u')
        return true;
    return false;
}

// create alternate vowel and consonant string
// str1[0...l1-1] and str2[start...l2-1]
static String createAltStr(String str1, String str2,
                    int start, int l)
{
    String finalStr = "";

    // first adding character of vowel/consonant
    // then adding character of consonant/vowel
    for (int i = 0, j = start; j < l; i++, j++)
        finalStr = (finalStr + str1[i]) +
                                    str2[j];
    return finalStr;
}

// function to find the required
// alternate vowel and consonant string
static String findAltStr(String str)
{
    int nv = 0, nc = 0;
    String vstr = "", cstr = "";
    int l = str.Length;
    for (int i = 0; i < l; i++)
    {
        char ch = str[i];

        // count vowels and update vowel string
        if (isVowel(ch))
        {
            nv++;
            vstr = vstr + ch;
        }

        // count consonants and update consonant
        // string
        else
        {
            nc++;
            cstr = cstr + ch;
        }
    }

    // no such string can be formed
    if (Math.Abs(nv - nc) >= 2)
        return "no such string";

    // remove first character of vowel string
    // then create alternate string with
    // cstr[0...nc-1] and vstr[1...nv-1]
    if (nv > nc)
        return (vstr[0] + createAltStr(cstr, vstr, 1, nv));

    // remove first character of consonant string
    // then create alternate string with
    // vstr[0...nv-1] and cstr[1...nc-1]
    if (nc > nv)
        return (cstr[0] + createAltStr(vstr, cstr, 1, nc));

    // if both vowel and consonant
    // strings are of equal length
    // start creating string with consonant
    if (cstr[0] < vstr[0])
        return createAltStr(cstr, vstr, 0, nv);

    // start creating string with vowel
    return createAltStr(vstr, cstr, 0, nc);
}

// Driver code
public static void Main(String []args)
{
    String str = "geeks";
    Console.WriteLine(findAltStr(str));
}
}

// This code is contributed by Princi Singh
```

**输出:**

```
gekes
```

**时间复杂度:** O(n)，其中‘n’为弦的长度
本文由**阿尤什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。