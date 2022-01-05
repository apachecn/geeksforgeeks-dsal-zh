# 交替上下字符串排序

> 原文:[https://www . geesforgeks . org/alternate-lower-upper-string-sort/](https://www.geeksforgeeks.org/alternate-lower-upper-string-sort/)

给定包含小写和大写字母的字符串。对其进行排序，使大小写字母以交替的方式出现，但以排序的方式出现。

**示例:**

```
Input : bAwutndekWEdkd
Output :AbEdWddekkntuw
Explanation:
Here we can see that letter ‘A’, ’E’, ’W’ are sorted 
as well as letters “b, d, d, d, e, k, k, n, t, u, w” are sorted 
but both appears alternately in the string as far as possible.

Input :abbfDDhGFBvdFDGBNDasZVDFjkb
Output :BaBaDbDbDbDdDfFhFjFkGsGvNVZ
```

1)计算一个数组中的小写字符数 lCount[]
2)计算另一个数组中的大写字符数 uCount[]
3)使用 lCount[]和 uCount[]修改字符串

## C++

```
// C++ program for unusul string sorting
#include <bits/stdc++.h>
using namespace std;
#define MAX 26

// Function for alternate sorting of string
void alternateSort(string& s)
{
    int n = s.length();

    // Count occurrences of individual lower case and
    // upper case characters
    int lCount[MAX] = { 0 }, uCount[MAX] = { 0 };
    for (int i = 0; i < n; i++) {
        if (isupper(s[i]))
            uCount[s[i] - 'A']++;
        else
            lCount[s[i] - 'a']++;
    }

    // Traverse through count arrays and one by one
    // pick characters.  Below loop takes O(n) time
    // considering the MAX is constant.
    int i = 0, j = 0, k = 0;
    while (k < n) {
        while (i < MAX && uCount[i] == 0)
            i++;
        if (i < MAX) {
            s[k++] = 'A' + i;
            uCount[i]--;
        }

        while (j < MAX && lCount[j] == 0)
            j++;
        if (j < MAX) {
            s[k++] = 'a' + j;
            lCount[j]--;
        }
    }
}

// Driver code
int main()
{
    string str = "bAwutndekWEdkd";
    alternateSort(str);
    cout << str << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// unusual string sorting
import java.util.*;
import java.lang.*;

public class GfG{

private final static int MAX = 100;

// Function for alternate
// sorting of string
public static String alternateSort(String s1)
{
    int n = s1.length();

    char[] s = s1.toCharArray();

    // Count occurrences of
    // individual lower case and
    // upper case characters
    int[] lCount = new int[MAX];
    int[] uCount = new int[MAX];

    for (int i = 0; i < n; i++) {

        if (Character.isUpperCase(s[i]))
            uCount[s[i] - 'A']++;
        else
            lCount[s[i] - 'a']++;
    }

    // Traverse through count
    // arrays and one by one
    // pick characters.
    // Below loop takes O(n) time
    // considering the MAX is constant.
    int i = 0, j = 0, k = 0;
    while (k < n)
    {

        while (i < MAX && uCount[i] == 0)
                i++;

        if (i < MAX) {
                s[k++] = (char)('A' + i);
                uCount[i]--;
            }

        while (j < MAX && lCount[j] == 0)
                j++;

        if (j < MAX) {
                s[k++] = (char)('a' + j);
                lCount[j]--;
            }
        }

        return (new String(s));
    }

// Driver function
public static void main(String argc[]){

    String str = "bAwutndekWEdkd";
    System.out.println(alternateSort(str));
}

}

// This code is contributed by Sagar Shukla
```

## C#

```
// C# program for unusual string sorting
using System;

public class GFG {

    private static int MAX = 100;

    // Function for alternate
    // sorting of string
    static String alternateSort(String s1)
    {
        int n = s1.Length;
        int l = 0, j = 0, k = 0;

        char[] s = s1.ToCharArray();

        // Count occurrences of
        // individual lower case and
        // upper case characters
        int[] lCount = new int[MAX];
        int[] uCount = new int[MAX];

        for (int i = 0; i < n; i++) {

            if (char.IsUpper(s[i]))
                uCount[s[i] - 'A']++;
            else
                lCount[s[i] - 'a']++;
        }

        // Traverse through count
        // arrays and one by one
        // pick characters.
        // Below loop takes O(n) time
        // considering the MAX is constant.

        while (k < n)
        {

            while (l < MAX && uCount[l] == 0)
                l++;

            if (l < MAX) {
                s[k++] = (char)('A' + l);
                uCount[l]--;
            }

            while (j < MAX && lCount[j] == 0)
                j++;

            if (j < MAX) {
                s[k++] = (char)('a' + j);
                lCount[j]--;
            }
        }

        return (new String(s));
    }

    // Driver function
    public static void Main()
    {
        String str = "bAwutndekWEdkd";

        Console.Write(alternateSort(str));
    }
}

// This code is contributed by parashar.
```

## 蟒蛇 3

```
# Python3 program for
# unusul string sorting
MAX = 26

# Function for alternate
# sorting of string
def alternateSort(s):

    n = len(s)

    # Count occurrences of
    # individual lower case and
       # upper case characters
    lCount = [0 for i in range(MAX)]
    uCount = [0 for i in range(MAX)]
    s = list(s)

    for i in range(n):
        if(s[i].isupper()):
            uCount[ord(s[i]) -
                   ord('A')] += 1
        else:
            lCount[ord(s[i]) -
                   ord('a')] += 1

    # Traverse through count
    # arrays and one by one
    # pick characters. Below
    # loop takes O(n) time
    # considering the MAX
    # is constant.
    i = 0
    j = 0
    k = 0

    while(k < n):
        while(i < MAX and
              uCount[i] == 0):
            i += 1
        if(i < MAX):
            s[k] = chr(ord('A') + i)
            k += 1
            uCount[i] -= 1
        while(j < MAX and
              lCount[j] == 0):
            j += 1
        if(j < MAX):
            s[k] = chr(ord('a') + j)
            k += 1
            lCount[j] -= 1

    print("".join(s))

# Driver code
str = "bAwutndekWEdkd"
alternateSort(str)

# This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
      // JavaScript program for unusual string sorting
      const MAX = 26;

      // Function for alternate
      // sorting of string
      function alternateSort(s1) {
        var n = s1.length;
        var l = 0, j = 0, k = 0;

        var s = s1.split("");

        // Count occurrences of
        // individual lower case and
        // upper case characters
        var lCount = new Array(MAX).fill(0);
        var uCount = new Array(MAX).fill(0);

        for (var i = 0; i < n; i++) {
          if (s[i] === s[i].toUpperCase())
            uCount[s[i].charCodeAt(0) - "A".charCodeAt(0)]++;
          else
              lCount[s[i].charCodeAt(0) - "a".charCodeAt(0)]++;
        }

        // Traverse through count
        // arrays and one by one
        // pick characters.
        // Below loop takes O(n) time
        // considering the MAX is constant.

        while (k < n) {
          while (l < MAX && uCount[l] === 0)
              l++;

          if (l < MAX) {
            s[k++] = String.fromCharCode("A".charCodeAt(0) + l);
            uCount[l]--;
          }

          while (j < MAX && lCount[j] === 0)
              j++;

          if (j < MAX) {
            s[k++] = String.fromCharCode("a".charCodeAt(0) + j);
            lCount[j]--;
          }
        }

        return s.join("");
      }

      // Driver function
      var str = "bAwutndekWEdkd";

      document.write(alternateSort(str));
</script>
```

**输出:**

```
AbEdWddekkntuw
```

**时间复杂度:** O(n)