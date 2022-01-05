# 将版本号与允许的大输入进行比较

> 原文:[https://www . geesforgeks . org/compare-version-numbers-large-inputs-allowed/](https://www.geeksforgeeks.org/compare-version-numbers-large-inputs-allowed/)

比较两个版本，版本 1 和版本 2。
如果版本 1 >版本 2 返回 1
如果版本 1 <版本 2 返回-1
如果版本 1 =版本 2 返回 0
版本字符串非空，仅包含数字和“.”性格。“.”字符不代表小数点，用于分隔数字序列。
版本排序示例。
0.1<1.1<1.2<1.13<1 . 13 . 4

**注意:**这里字符串中出现的数字可能很大，所以不要试图将这些数字
转换为无符号长整型。版本 1 = 1。58860 . 88888888861

**示例:**

```
Input :  version1 : 002.0005.12.3
         version2 : 2.5.12.3
Output : 0

Input : version1 : 451231654684151546847799885544662
        version2 : 1.256.24.5.5
Output : 1

Input : version1 : 1.21.20
        version2 : 1.21.25
Output : -1

Input : version1 : 1.2
        version2 : 1.2.0.0.0
Output : 0

Input : version1 : 1.2
        version2 : 1.0.1
Output : -1
```

我们在下面的帖子中讨论了一个解决方案。
[对比两个版本号](https://www.geeksforgeeks.org/compare-two-version-numbers/)

上面讨论的前一个解决方案有一些问题，例如，它不处理前导零，也不适用于大数字，因为版本号的各个部分都存储为 int。

在该解决方案中，解决了上述问题。我们同时遍历两个版本，并处理它们，直到两个版本都被完全遍历。将版本 1 和版本 2 的数字存储在不同的字符串中，即 substr_version1 和 substr_version2。比较这些子字符串，

如果 substr_version1 > substr _ version 2 的长度明显大于 substr _ version 1 的值，那么返回+1。类似的情况是当 substr _ version 2 > substr _ version 1 时，我们将返回-1。但是如果两个子串长度相似，那么
我们将不得不检查两个子串中的每个字符，然后比较这些字符，然后适当地返回结果。

## C++

```
// C++ program to compare two versions
#include <bits/stdc++.h>
using namespace std;

// Utility function to compare each substring
// of version1 and version2
int compareSubstr(char *substr_version1, char *substr_version2,
                  int len_substr_version1, int len_substr_version2)
{

    // If length of substring of version 1 is
    // greater then it means value of substr
    // of version1 is also greater
    if (len_substr_version1 > len_substr_version2)
        return 1;

    else if (len_substr_version1 < len_substr_version2)
        return -1;

    // When length of the substrings of
    // both versions is same.
    else
    {
        int i = 0, j = 0;

        // Compare each character of both substrings
        // and return accordingly.
        while (i < len_substr_version1)
        {
            if (substr_version1[i] < substr_version2[j])
                return -1;
            else if (substr_version1[i] > substr_version2[j])
                return 1;

            i++, j++;
        }
        return 0;
    }
}

// Function to compare two versions.
int compareVersion(char* version1, char* version2)
{
    int len_version1 = strlen(version1);
    int len_version2 = strlen(version2);

    char *substr_version1 = (char *)malloc(sizeof(char) * 1000);
    char *substr_version2 = (char *)malloc(sizeof(char) * 1000);   

    // Loop until both strings are exhausted.
    // and extract the substrings from version1
    // and version2
    int i = 0, j = 0;
    while (i < len_version1 || j < len_version2)
    {
        int p = 0, q = 0;

        // Skip the leading zeros in version1 string.
        while (version1[i] == '0')
            i++;

        // Skip the leading zeros in version2 string.
        while (version2[j] == '0')
            j++;

        // Extract the substring from version1.
        while (version1[i] != '.' && i < len_version1)       
            substr_version1[p++] = version1[i++];

        // Extract the substring from version2.
        while (version2[j] != '.' && j < len_version2)       
            substr_version2[q++] = version2[j++];   

        int res = compareSubstr(substr_version1,
                                substr_version2, p, q);

        // If res is either -1 or +1 then simply return.
        if (res)
            return res;

        i++;
        j++;
    }

    // Here both versions are exhausted it implicitly
    // means that both strings are equal.
    return 0;
}

// Driver code
int main()
{

    // Define Two versions.
    char version1[] = "1.2.032.45";
    char version2[] = "1.2.32.4";

    int res = compareVersion(version1, version2);

    cout << res << endl;

    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
/* C program to compare two versions */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// utility function to compare each substring of version1 and
// version2
 int compareSubstr(char *substr_version1, char *substr_version2,
                  int len_substr_version1, int len_substr_version2)
 {
     // if length of substring of version 1 is greater then
     // it means value of substr of version1 is also greater
     if (len_substr_version1 > len_substr_version2)
        return 1;

     else if (len_substr_version1 < len_substr_version2)
        return -1;

     // when length of the substrings of both versions is same.
     else
     {
        int i = 0, j = 0;

        // compare each character of both substrings and return
        // accordingly.
        while (i < len_substr_version1)
        {
            if (substr_version1[i] < substr_version2[j]) return -1;
            else if (substr_version1[i] > substr_version2[j]) return 1;
            i++, j++;
        }
        return 0;
     }
 }

// function to compare two versions.
int compareVersion(char* version1, char* version2)
{
    int len_version1 = strlen(version1);
    int len_version2 = strlen(version2);

    char *substr_version1 = (char *) malloc(sizeof(char) * 1000);
    char *substr_version2 = (char *) malloc(sizeof(char) * 1000);   

    // loop until both strings are exhausted.
    // and extract the substrings from version1 and version2
    int i = 0, j = 0;
    while (i < len_version1 || j < len_version2)
    {
        int p = 0, q = 0;

        // skip the leading zeros in version1 string.
        while (version1[i] == '0' )
           i++;

        // skip the leading zeros in version2 string.
        while (version2[j] == '0' )
           j++;

        // extract the substring from version1.
        while (version1[i] != '.' && i < len_version1)       
            substr_version1[p++] = version1[i++];

        //extract the substring from version2.
        while (version2[j] != '.' && j < len_version2)       
            substr_version2[q++] = version2[j++];   

        int res = compareSubstr(substr_version1,
                                substr_version2, p, q);

        // if res is either -1 or +1 then simply return.
        if (res)
            return res;
        i++;
        j++;
    }

    // here both versions are exhausted it implicitly
    // means that both strings are equal.
    return 0;
}

// Driver code.
int main()
{
    // Define Two versions.
    char version1[] = "1.2.032.45";
    char version2[] = "1.2.32.4";

    int res = compareVersion(version1, version2);

    printf("%d\n", res);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compare two versions
import java.io.*;

class GFG{

// utility function to compare each substring of
// version1 and version2
public static int compareSubstr(String substr_version1,
                                String substr_version2)
{
    int len_substr_version1 = substr_version1.length();
    int len_substr_version2 = substr_version1.length();

    // If length of substring of version 1 is greater
    // then it means value of substr of version1 is
    // also greater
    if (len_substr_version1 > len_substr_version2)
        return 1;
    else if (len_substr_version2 < len_substr_version1)
        return -1;

    // When length of the substrings of
    // both versions is same.
    int res = substr_version1.compareTo(
              substr_version2);

    if (res > 0) return 1;
    else if (res < 0) return -1;

    return 0;
}

// Function to compare two versions.
public static int compareVersion(String version1,
                                 String version2)
{
    String substr_version1[] = version1.split("[.]");
    String substr_version2[] = version2.split("[.]");

    int len_version1 = substr_version1.length;
    int len_version2 = substr_version2.length;
    int i = 0;
    int j = 0;

    // Loop until both strings are exhausted.
    // and extract the substrings from version1
    // and version2
    while (i < len_version1 || j < len_version2)
    {
        String x = "";
        String y = "";

        if (i < len_version1)
        {

            // Skip the leading zeros in
            // version1 string.
            if (substr_version1[i].charAt(0) == '0')
            {
                int len = substr_version1[i].length();
                int k = 0;

                while (k < len &&
                       substr_version1[i].charAt(k) == '0')
                {
                    k++;
                }
                x += substr_version1[i].substring(k);
            }
            else
                x += substr_version1[i];
        }

        if (j < len_version2)
        {

            // Skip the leading zeros in version2 string.
            if (substr_version2[i].charAt(0) == '0')
            {
                int len = substr_version2[i].length();
                int k = 0;

                while (k < len &&
                       substr_version2[i].charAt(k) == '0')
                {
                    k++;
                }
                y += substr_version2[i].substring(k);
            }
            else
                y = substr_version2[i];
        }

        // If res is either -1 or +1
        // then simply return.
        int res = compareSubstr(x, y);
        if (res != 0)
            return res;

        i++;
        j++;
    }

    // Here both versions are exhausted
    // it implicitly means that both
    // strings are equal.
    return 0;
}

// Driver code.
public static void main (String[] args)
{
    System.out.println(compareVersion("1.2.032.45",
                                      "1.2.32.4"));
}
}

// This code is contributed by naresh_saharan151
```

## C#

```
// C# program to compare two versions
using System;

public class GFG{

    // utility function to compare each Substring of
    // version1 and version2
    public static int compareSubstr(string substr_version1,
                                    string substr_version2)
    {
        int len_substr_version1 = substr_version1.Length;
        int len_substr_version2 = substr_version1.Length;

        // If length of Substring of version 1 is greater
        // then it means value of substr of version1 is
        // also greater
        if (len_substr_version1 > len_substr_version2)
            return 1;
        else if (len_substr_version2 < len_substr_version1)
            return -1;

        // When length of the Substrings of
        // both versions is same.
        int res = substr_version1.CompareTo(
                  substr_version2);

        if (res > 0) return -1;
        else if (res < 0) return 1;

        return 0;
    }

    // Function to compare two versions.
    public static int compareVersion(string version1,
                                     string version2)
    {
        string[] substr_version1 = version1.Split("[.]");
        string[] substr_version2 = version2.Split("[.]");

        int len_version1 = substr_version1.Length;
        int len_version2 = substr_version2.Length;
        int i = 0;
        int j = 0;

        // Loop until both strings are exhausted.
        // and extract the Substrings from version1
        // and version2
        while (i < len_version1 || j < len_version2)
        {
            string x = "";
            string y = "";

            if (i < len_version1)
            {

                // Skip the leading zeros in
                // version1 string.
                if (substr_version1[i][0] == '0')
                {
                    int len = substr_version1[i].Length;
                    int k = 0;

                    while (k < len &&
                           substr_version1[i][k] == '0')
                    {
                        k++;
                    }
                    x += substr_version1[i].Substring(k);
                }
                else
                    x += substr_version1[i];
            }

            if (j < len_version2)
            {

                // Skip the leading zeros in version2 string.
                if (substr_version2[i][0] == '0')
                {
                    int len = substr_version2[i].Length;
                    int k = 0;

                    while (k < len &&
                           substr_version2[i][k] == '0')
                    {
                        k++;
                    }
                    y += substr_version2[i].Substring(k);
                }
                else
                    y = substr_version2[i];
            }

            // If res is either -1 or +1
            // then simply return.
            int res = compareSubstr(x, y);
            if (res != 0)
                return res;

            i++;
            j++;
        }

        // Here both versions are exhausted
        // it implicitly means that both
        // strings are equal.
        return 0;
    }

    // Driver code.
    static public void Main (){
        Console.Write(compareVersion("1.2.032.45",
                                          "1.2.32.4"));
    }
}

// This code is contributed by shubhamsingh10
```

**输出:**

```
1
```

**时间复杂度:**O(2 * N)–>O(N)
这里最坏的情况是当两个版本相等时，因此在提取两个子串后，它们中的每一个将再次在 compareSubstr()函数中进行比较，该函数将复杂度提升到(2 * N)。

本文由[**<u>arshpreet soodan</u>**T5 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用](https://www.linkedin.com/in/arshpreet-soodan-717a5412a/)[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。