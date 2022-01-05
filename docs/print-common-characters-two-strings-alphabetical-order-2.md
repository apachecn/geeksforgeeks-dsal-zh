# 按字母顺序打印两个字符串的常用字符

> 原文:[https://www . geesforgeks . org/print-common-characters-two-strings-字母顺序-2/](https://www.geeksforgeeks.org/print-common-characters-two-strings-alphabetical-order-2/)

给定两个字符串，按照[字典序](https://www.geeksforgeeks.org/lexicographic-permutations-of-string/)顺序打印所有常用字符。如果没有常用字母，打印-1。所有字母都是小写的。

**示例:**

```
Input : 
string1 : geeks
string2 : forgeeks
Output : eegks
Explanation: The letters that are common between 
the two strings are e(2 times), k(1 time) and 
s(1 time).
Hence the lexicographical output is "eegks"

Input : 
string1 : hhhhhello
string2 : gfghhmh
Output : hhh
```

想法是使用字符计数数组。
1)统计第一个和第二个字符串中从“a”到“z”的所有字符的出现次数。将这些计数存储在两个数组 a1[]和 a2[]中。
2)遍历 a1[]和 a2[](注意两者的大小都是 26)。对于每个索引 I，打印字符' a' + i 的次数等于 min(a1[i]，a2[i])。

下面是上述步骤的实现。

## C++

```
// C++ program to print common characters
// of two Strings in alphabetical order
#include<bits/stdc++.h>
using namespace std;

int main()
{
    string s1 = "geeksforgeeks";
    string s2 = "practiceforgeeks";

    // to store the count of
    // letters in the first string
    int a1[26] = {0};

    // to store the count of
    // letters in the second string
    int a2[26] = {0};
    int i , j;
    char ch;
    char ch1 = 'a';
    int k = (int)ch1, m;

    // for each letter present, increment the count
    for(i = 0 ; i < s1.length() ; i++)
    {
        a1[(int)s1[i] - k]++;
    }
    for(i = 0 ; i < s2.length() ; i++)
    {
        a2[(int)s2[i] - k]++;
    }

    for(i = 0 ; i < 26 ; i++)
    {
        // the if condition guarantees that
        // the element is common, that is,
        // a1[i] and a2[i] are both non zero
        // means that the letter has occurred
        // at least once in both the strings
        if (a1[i] != 0 and a2[i] != 0)
        {
            // print the letter for a number
            // of times that is the minimum
            // of its count in s1 and s2
            for(j = 0 ; j < min(a1[i] , a2[i]) ; j++)
            {
                m = k + i;
                ch = (char)(k + i);
                cout << ch;
            }
        }
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print common characters
// of two Strings in alphabetical order
import java.io.*;
import java.util.*;

// Function to find similar characters
public class Simstrings
{
    static final int MAX_CHAR = 26;

    static void printCommon(String s1, String s2)
    {
       // two arrays of length 26 to store occurrence
        // of a letters alphabetically for each string
        int[] a1 = new int[MAX_CHAR];
        int[] a2 = new int[MAX_CHAR];

        int length1 = s1.length();
        int length2 = s2.length();

        for (int i = 0 ; i < length1 ; i++)
           a1[s1.charAt(i) - 'a'] += 1;

        for (int i = 0 ; i < length2 ; i++)
           a2[s2.charAt(i) - 'a'] += 1;

        // If a common index is non-zero, it means
        // that the letter corresponding to that
        // index is common to both strings
        for (int i = 0 ; i < MAX_CHAR ; i++)
        {
            if (a1[i] != 0 && a2[i] != 0)
            {
                // Find the minimum of the occurrence
                // of the character in both strings and print
                // the letter that many number of times
                for (int j = 0 ; j < Math.min(a1[i], a2[i]) ; j++)
                    System.out.print(((char)(i + 'a')));
            }
        }
    }

    // Driver code
    public static void main(String[] args) throws IOException
    {
        String s1 = "geeksforgeeks", s2 = "practiceforgeeks";
        printCommon(s1, s2);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print common characters
# of two Strings in alphabetical order

# Initializing size of array
MAX_CHAR=26

# Function to find similar characters
def printCommon( s1, s2):
    # two arrays of length 26 to store occurrence
    # of a letters alphabetically for each string
    a1 = [0 for i in range(MAX_CHAR)]
    a2 = [0 for i in range(MAX_CHAR)]

    length1 = len(s1)
    length2 = len(s2)

    for i in range(0,length1):
        a1[ord(s1[i]) - ord('a')] += 1

    for i in range(0,length2):
        a2[ord(s2[i]) - ord('a')] += 1

    # If a common index is non-zero, it means
    # that the letter corresponding to that
    # index is common to both strings
    for i in range(0,MAX_CHAR):
        if (a1[i] != 0 and a2[i] != 0):

            # Find the minimum of the occurrence
            # of the character in both strings and print
            # the letter that many number of times
            for j in range(0,min(a1[i],a2[i])):
                ch = chr(ord('a')+i)
                print (ch, end='')

# Driver code
if __name__=="__main__":
    s1 = "geeksforgeeks"
    s2 = "practiceforgeeks"
    printCommon(s1, s2);

# This Code is contributed by Abhishek Sharma
```

## C#

```
// C# program to print common characters
// of two Strings in alphabetical order

using System;
// Function to find similar characters
public class Simstrings
{
    static int MAX_CHAR = 26;

    static void printCommon(string s1, string s2)
    {
       // two arrays of length 26 to store occurrence
        // of a letters alphabetically for each string
        int[] a1 = new int[MAX_CHAR];
        int[] a2 = new int[MAX_CHAR];

        int length1 = s1.Length;
        int length2 = s2.Length;

        for (int i = 0 ; i < length1 ; i++)
           a1[s1[i] - 'a'] += 1;

        for (int i = 0 ; i < length2 ; i++)
           a2[s2[i] - 'a'] += 1;

        // If a common index is non-zero, it means
        // that the letter corresponding to that
        // index is common to both strings
        for (int i = 0 ; i < MAX_CHAR ; i++)
        {
            if (a1[i] != 0 && a2[i] != 0)
            {
                // Find the minimum of the occurrence
                // of the character in both strings and print
                // the letter that many number of times
                for (int j = 0 ; j < Math.Min(a1[i], a2[i]) ; j++)
                    Console.Write(((char)(i + 'a')));
            }
        }
    }

    // Driver code
    public static void Main()
    {
        string s1 = "geeksforgeeks", s2 = "practiceforgeeks";
        printCommon(s1, s2);
    }
}
```

## java 描述语言

```
<script>
// Javascript program to print common characters
// of two Strings in alphabetical order

    let MAX_CHAR = 26;
    // Function to find similar characters
    function printCommon(s1,s2)
    {
        // two arrays of length 26 to store occurrence
        // of a letters alphabetically for each string
        let a1 = new Array(MAX_CHAR);
        let a2 = new Array(MAX_CHAR);
        for(let i=0;i<MAX_CHAR;i++)
        {
            a1[i]=0;
            a2[i]=0;
        }

        let length1 = s1.length;
        let length2 = s2.length;

        for (let i = 0 ; i < length1 ; i++)
           a1[s1[i].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;

        for (let i = 0 ; i < length2 ; i++)
           a2[s2[i].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;

        // If a common index is non-zero, it means
        // that the letter corresponding to that
        // index is common to both strings
        for (let i = 0 ; i < MAX_CHAR ; i++)
        {
            if (a1[i] != 0 && a2[i] != 0)
            {
                // Find the minimum of the occurrence
                // of the character in both strings and print
                // the letter that many number of times
                for (let j = 0 ; j < Math.min(a1[i], a2[i]) ; j++)
                    document.write((String.fromCharCode(i + 'a'.charCodeAt(0))));
            }
        }
    }

    // Driver code
    let s1 = "geeksforgeeks", s2 = "practiceforgeeks";
    printCommon(s1, s2);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
eeefgkors
```

**时间复杂度:**如果我们考虑 n =长度(更大的字符串)，那么这个算法以 **O(n)** 复杂度运行。