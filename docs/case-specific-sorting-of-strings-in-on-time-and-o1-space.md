# 在 O(n)时间和 O(1)空间中字符串的特定情况排序

> 原文:[https://www . geeksforgeeks . org/case-specific-on-time-and-O1-space 字符串排序/](https://www.geeksforgeeks.org/case-specific-sorting-of-strings-in-on-time-and-o1-space/)

给定一个由大写和小写字符组成的字符串 **str** 。任务是分别对大写和小写字符进行排序，这样如果原始字符串中的第 **i <sup>第</sup>T5】个位置有一个大写字符，则排序后它不应该有一个小写字符，反之亦然。
**举例:**** 

> **输入:**输入:输入:
> 输出:输出:
> 输出

**方法:**取两个数组 lower[]和 upper[]存储给定字符串中所有小写和大写字符的频率，然后再次遍历该字符串，对于遇到的每个小写字符，使用 lower[]数组将其替换为可用的最小小写字符，并使用 upper[]数组替换大写字符。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 26

// Function to return the sorted string
string getSortedString(string s, int n)
{

    // To store the frequencies of the
    // lowercase and the uppercase
    // characters in the given string
    int lower[MAX] = { 0 };
    int upper[MAX] = { 0 };

    for (int i = 0; i < n; i++) {

        // If current character is lowercase then
        // increment its frequency in
        // the lower[] array
        if (islower(s[i]))
            lower[s[i] - 'a']++;

        // Else increment in the upper[] array
        else if (isupper(s[i]))
            upper[s[i] - 'A']++;
    }

    // Pointers that point to the smallest lowercase
    // and the smallest uppercase characters
    // respectively in the given string
    int i = 0, j = 0;
    while (i < MAX && lower[i] == 0)
        i++;

    while (j < MAX && upper[j] == 0)
        j++;

    // For every character in the given string
    for (int k = 0; k < n; k++) {

        // If the current character is lowercase
        // then replace it with the smallest
        // lowercase character available
        if (islower(s[k])) {
            while (lower[i] == 0)
                i++;
            s[k] = (char)(i + 'a');

            // Decrement the frequency
            // of the used character
            lower[i]--;
        }

        // Else replace it with the smallest
        // uppercase character available
        else if (isupper(s[k])) {
            while (upper[j] == 0)
                j++;
            s[k] = (char)(j + 'A');

            // Decrement the frequency
            // of the used character
            upper[j]--;
        }
    }

    // Return the sorted string
    return s;
}

// Driver code
int main()
{
    string s = "gEeksfOrgEEkS";
    int n = s.length();

    cout << getSortedString(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.lang.Character;

class GFG
{

    static int MAX = 26;

    public static String getSortedString(StringBuilder s, int n)
    {

        // To store the frequencies of the
        // lowercase and the uppercase
        // characters in the given string
        int[] lower = new int[MAX];
        int[] upper = new int[MAX];

        for (int i = 0; i < n; i++)
        {

            // If current character is lowercase then
            // increment its frequency in
            // the lower[] array
            if (Character.isLowerCase(s.charAt(i)))
                lower[s.charAt(i) - 'a']++;

            // Else increment in the upper[] array
            else if (Character.isUpperCase(s.charAt(i)))
                upper[s.charAt(i) - 'A']++;
        }

        // Pointers that point to the smallest lowercase
        // and the smallest uppercase characters
        // respectively in the given string
        int i = 0, j = 0;
        while (i < MAX && lower[i] == 0)
            i++;

        while (j < MAX && upper[j] == 0)
            j++;

        // For every character in the given string
        for (int k = 0; k < n; k++)
        {

            // If the current character is lowercase
            // then replace it with the smallest
            // lowercase character available
            if (Character.isLowerCase(s.charAt(k)))
            {
                while (lower[i] == 0)
                    i++;
                s.setCharAt(k, (char) (i + 'a'));

                // Decrement the frequency
                // of the used character
                lower[i]--;
            }

            // Else replace it with the smallest
            // uppercase character available
            else if (Character.isUpperCase(s.charAt(k)))
            {
                while (upper[j] == 0)
                    j++;
                s.setCharAt(k, (char) (j + 'A'));

                // Decrement the frequency
                // of the used character
                upper[j]--;
            }
        }

        // Return the sorted string
        return s.toString();
    }

    // Driver code
    public static void main(String[] args)
    {
        StringBuilder s = new StringBuilder("gEeksfOrgEEkS");
        int n = s.length();
        System.out.println(getSortedString(s, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 26

# Function to return the sorted string
def getSortedString(s, n) :

    # To store the frequencies of the
    # lowercase and the uppercase
    # characters in the given string
    lower = [ 0 ] * MAX;
    upper = [ 0 ] * MAX;

    for i in range(n) :

        # If current character is lowercase then
        # increment its frequency in
        # the lower[] array
        if (s[i].islower()) :
            lower[ord(s[i]) - ord('a')] += 1;

        # Else increment in the upper[] array
        elif (s[i].isupper()) :
            upper[ord(s[i]) - ord('A')] += 1;

    # Pointers that point to the smallest lowercase
    # and the smallest uppercase characters
    # respectively in the given string
    i = 0; j = 0;
    while (i < MAX and lower[i] == 0) :
        i += 1;

    while (j < MAX and upper[j] == 0) :
        j += 1;

    # For every character in the given string
    for k in range(n) :

        # If the current character is lowercase
        # then replace it with the smallest
        # lowercase character available
        if (s[k].islower()) :
            while (lower[i] == 0) :
                i += 1;
            s[k] = chr(i + ord('a'));

            # Decrement the frequency
            # of the used character
            lower[i] -= 1;

        # Else replace it with the smallest
        # uppercase character available
        elif (s[k].isupper()) :
            while (upper[j] == 0) :
                j += 1;
            s[k] = chr(j + ord('A'));

            # Decrement the frequency
            # of the used character
            upper[j] -= 1;

    # Return the sorted string
    return "".join(s);

# Driver code
if __name__ == "__main__" :
    s = "gEeksfOrgEEkS";
    n = len(s);

    print(getSortedString(list(s), n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MAX = 26;

    // Function to return the sorted string
    static string getSortedString(char[] s, int n)
    {

        // To store the frequencies of the
        // lowercase and the uppercase
        // characters in the given string
        int[] lower = new int[MAX];
        int[] upper = new int[MAX];
        int i = 0, j = 0;
        for (i = 0; i < n; i++)
        {

            // If current character is lowercase then
            // increment its frequency in
            // the lower[] array
            if (char.IsLower(s[i]))
                lower[s[i] - 'a']++;

            // Else increment in the upper[] array
            else if (char.IsUpper(s[i]))
                upper[s[i] - 'A']++;
        }

        // Pointers that point to the smallest lowercase
        // and the smallest uppercase characters
        // respectively in the given string
        i = 0;
        while (i < MAX && lower[i] == 0)
            i++;

        while (j < MAX && upper[j] == 0)
            j++;

        // For every character in the given string
        for (int k = 0; k < n; k++)
        {

            // If the current character is lowercase
            // then replace it with the smallest
            // lowercase character available
            if (char.IsLower(s[k]))
            {
                while (lower[i] == 0)
                    i++;
                s[k] = (char)(i + 'a');

                // Decrement the frequency
                // of the used character
                lower[i]--;
            }

            // Else replace it with the smallest
            // uppercase character available
            else if (char.IsUpper(s[k]))
            {
                while (upper[j] == 0)
                    j++;
                s[k] = (char)(j + 'A');

                // Decrement the frequency
                // of the used character
                upper[j]--;
            }
        }

        // Return the sorted string
        return String.Join("", s);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "gEeksfOrgEEkS";
        int n = s.Length;
        Console.WriteLine(getSortedString(s.ToCharArray(), n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 26;

// Function to return the sorted string
function getSortedString(s, n)
{

    // To store the frequencies of the
    // lowercase and the uppercase
    // characters in the given string
    var lower = Array(MAX).fill(0);
    var upper = Array(MAX).fill(0);

    for (var i = 0; i < n; i++) {

        // If current character is lowercase then
        // increment its frequency in
        // the lower[] array
        if ((s[i]) == s[i].toLowerCase())
            lower[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // Else increment in the upper[] array
        else if (s[i] = s[i].toUpperCase())
            upper[s[i].charCodeAt(0) - 'A'.charCodeAt(0)]++;
    }

    // Pointers that point to the smallest lowercase
    // and the smallest uppercase characters
    // respectively in the given string
    var i = 0, j = 0;
    while (i < MAX && lower[i] == 0)
        i++;

    while (j < MAX && upper[j] == 0)
        j++;

    // For every character in the given string
    for (var k = 0; k < n; k++) {

        // If the current character is lowercase
        // then replace it with the smallest
        // lowercase character available
        if (s[k] == s[k].toLowerCase()) {
            while (lower[i] == 0)
                i++;
            s[k] = String.fromCharCode(i + 'a'.charCodeAt(0));

            // Decrement the frequency
            // of the used character
            lower[i]--;
        }

        // Else replace it with the smallest
        // uppercase character available
        else if (s[k] == s[k].toUpperCase()) {
            while (upper[j] == 0)
                j++;
            s[k] = String.fromCharCode(j + 'A'.charCodeAt(0));

            // Decrement the frequency
            // of the used character
            upper[j]--;
        }
    }

    // Return the sorted string
    return s.join('');
}

// Driver code
var s = "gEeksfOrgEEkS";
var n = s.length;
document.write( getSortedString(s.split(''), n));

</script>
```

**Output:** 

```
eEfggkEkrEOsS
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)