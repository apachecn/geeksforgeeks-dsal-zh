# 查找最长公共前缀的最小移位

> 原文:[https://www . geesforgeks . org/find-最小移位-最长公共前缀/](https://www.geeksforgeeks.org/find-minimum-shift-longest-common-prefix/)

给你两个相同长度的字符串 str1 和 str2。在一次移位中，您可以将一个字符串(str2)旋转 1 个元素，使其第一个元素成为最后一个，第二个元素成为第一个，就像“abcd”在一次移位操作后会变成“bcda”。您必须找到从 str1 和 str2 获取最大长度的公共前缀所需的最小移位操作。
**例:**

```
Input : str1[] = "geeks", 
        str2 = "dgeek"
Output : Shift = 1, 
         Prefix = geek

Input : str1[] = "practicegeeks",
        str2 = "coderpractice"
Output : Shift = 5
         Prefix = practice
```

**天真方法:**逐个移位第二个字符串，并跟踪每个移位最长前缀的长度，总共有 n 个移位，对于每个移位，找到公共前缀的长度需要 O(n)个时间。因此，这种方法的总时间复杂度是 O(n^2).
**更好的方法:**如果我们在自身的末尾添加第二个字符串，即 **str2 = str2 + str2** ，那么就不需要分别为每个班次寻找前缀。现在，将 str2 添加到自身后，我们只需找到 str2 中存在的最长的 str1 前缀，该前缀在 str2 中的起始位置将给出所需的实际移位数。为了找到最长的前缀，我们可以使用 [KMP 模式搜索算法。](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)
所以，这样的话，我们的时间复杂度就会降低到只有 O(n)。

## C++

```
// CPP program to find longest common prefix
// after rotation of second string.
#include <bits/stdc++.h>
using namespace std;

// function for KMP search
void KMP(int m, int n, string str2, string str1)
{
    int pos = 0, len = 0;

    // preprocessing of longest proper prefix
    int p[m + 1];
    int k = 0;
    p[1] = 0;

    for (int i = 2; i <= n; i++) {
        while (k > 0 && str1[k] != str1[i - 1])
            k = p[k];
        if (str1[k] == str1[i - 1])
            ++k;
        p[i] = k;
    }

    // find out the longest prefix and position
    for (int j = 0, i = 0; i < m; i++) {
        while (j > 0 && str1[j] != str2[i])
            j = p[j];
        if (str1[j] == str2[i])
            j++;

        // for new position with longer prefix in str2
        // update pos and len
        if (j > len) {
            len = j;
            pos = i - j + 1;
        }
    }

    // print result
    cout << "Shift = " << pos << endl;
    cout << "Prefix = " << str1.substr(0, len);
}

// driver function
int main()
{
    string str1 = "geeksforgeeks";
    string str2 = "forgeeksgeeks";
    int n = str1.size();
    str2 = str2 + str2;
    KMP(2 * n, n, str2, str1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest common prefix
// after rotation of second string.

class GFG {

    // function for KMP search
    static void KMP(int m, int n,
                    String str2, String str1)
    {
        int pos = 0, len = 0;
        int []p = new int[m + 1];
        int k = 0;

        //p[1] = 0;
        char []ch1 = str1.toCharArray();
        char []ch2 = str2.toCharArray();

        for (int i = 2; i <= n; i++)
        {
            while (k > 0 && ch1[k] != ch1[i - 1])
                k = p[k];
            if (ch1[k] == ch1[i - 1])
                ++k;
            p[i] = k;
        }

        // find out the longest prefix and position
        for (int j = 0, i = 0; i < m; i++)
        {
            while (j > 0 && j < n && ch1[j] != ch2[i])
                j = p[j];
            if (j < n && ch1[j] == ch2[i])
                j++;

            // for new position with longer prefix in str2
            // update pos and len
            if (j > len)
            {
                len = j;
                pos = i - j + 1;
            }
        }

            // print result
            System.out.println("Shift = " + pos);
            System.out.println("Prefix = " +
                                str1.substring(0,len));
        }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "geeksforgeeks";
        String str2 = "forgeeksgeeks";
        int n = str1.length();
        str2 = str2 + str2;
        KMP(2 * n, n, str2, str1);
    }
}

// This code is contributed by Ita_c.
```

## 蟒蛇 3

```
# Python3 program to find longest common prefix
# after rotation of second string.

# function for KMP search
def KMP(m, n, str2, str1):

    pos = 0
    Len = 0

    # preprocessing of longest proper prefix
    p = [0 for i in range(m + 1)]
    k = 0

    for i in range(2, n + 1):
        while (k > 0 and str1[k] != str1[i - 1]):
            k = p[k]
        if (str1[k] == str1[i - 1]):
            k += 1
        p[i] = k

    # find out the longest prefix and position
    j = 0
    for i in range(m):
        while (j > 0 and j < n and str1[j] != str2[i]):
            j = p[j]
        if (j < n and str1[j] == str2[i]):
            j += 1

        # for new position with longer prefix
        # in str2 update pos and Len
        if (j > Len):
            Len = j
            pos = i - j + 1

    # prresult
    print("Shift = ", pos)
    print("Prefix = ", str1[:Len])

# Driver Code
str1 = "geeksforgeeks"
str2 = "forgeeksgeeks"
n = len(str1)
str2 = str2 + str2
KMP(2 * n, n, str2, str1)

# This code is contributed by Mohit kumar 29
```

## C#

```
// C# program to find longest common prefix
// after rotation of second string.
using System;

class GFG {

    // function for KMP search
    static void KMP(int m, int n,
                    String str2, String str1)
    {
        int pos = 0, len = 0;
        int []p = new int[m + 1];
        int k = 0;

        //p[1] = 0;
        char []ch1 = str1.ToCharArray();
        char []ch2 = str2.ToCharArray();

        for (int i = 2; i <= n; i++)
        {
            while (k > 0 && ch1[k] != ch1[i - 1])
                k = p[k];
            if (ch1[k] == ch1[i - 1])
                ++k;
            p[i] = k;
        }

        // find out the longest prefix and position
        for (int j = 0, i = 0; i < m; i++)
        {
            while (j > 0 && j < n && ch1[j] != ch2[i])
                j = p[j];
            if (j < n && ch1[j] == ch2[i])
                j++;

            // for new position with longer prefix in str2
            // update pos and len
            if (j > len)
            {
                len = j;
                pos = i - j + 1;
            }
        }

            // print result
            Console.WriteLine("Shift = " + pos);
            Console.WriteLine("Prefix = " +
                                str1.Substring(0,len));
        }

    // Driver code
    public static void Main(String[] args)
    {
        String str1 = "geeksforgeeks";
        String str2 = "forgeeksgeeks";
        int n = str1.Length;
        str2 = str2 + str2;
        KMP(2 * n, n, str2, str1);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to find longest common prefix
// after rotation of second string.

// function for KMP search
function KMP(m, n, str2, str1)
{
    var pos = 0, len = 0;

    // preprocessing of longest proper prefix
    var p = Array(m+1).fill(0);
    var k = 0;
    p[1] = 0;

    for (var i = 2; i <= n; i++) {
        while (k > 0 && str1[k] != str1[i - 1])
            k = p[k];
        if (str1[k] == str1[i - 1])
            ++k;
        p[i] = k;
    }

    // find out the longest prefix and position
    for (var j = 0, i = 0; i < m; i++) {
        while (j > 0 && str1[j] != str2[i])
            j = p[j];
        if (str1[j] == str2[i])
            j++;

        // for new position with longer prefix in str2
        // update pos and len
        if (j > len) {
            len = j;
            pos = i - j + 1;
        }
    }

    // print result
    document.write( "Shift = " + pos + "<br>");
    document.write( "Prefix = " + str1.substr(0, len));
}

// driver function
var str1 = "geeksforgeeks";
var str2 = "forgeeksgeeks";
var n = str1.length;
str2 = str2 + str2;
KMP(2 * n, n, str2, str1);

</script>
```

**输出:**

```
Shift = 8
Prefix = geeksforgeeks
```