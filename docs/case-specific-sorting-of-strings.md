# 字符串的特定情况排序

> 原文:[https://www . geesforgeks . org/区分大小写字符串排序/](https://www.geeksforgeeks.org/case-specific-sorting-of-strings/)

给定字符串**字符串**由大写和小写字符组成。任务是分别对大写和小写字符进行排序，这样，如果原始字符串中的第 I 个位置有大写字符，则排序后不应有小写字符，反之亦然。

**示例:**

> **输入:**【str = " geeksforgeeks "
> **输出:**和【心电图】
> 
> **输入:**str = " eDefSR "
> T3】输出: eDefRS

**方法:**思想很简单，将小写字符和大写字符存储在两个不同的向量中，并对两个向量进行排序。然后使用排序后的向量得到排序后的字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sorted string
string getSortedString(string s, int n)
{

    // Vectors to store the lowercase
    // and uppercase characters
    vector<char> v1, v2;
    for (int i = 0; i < n; i++) {
        if (s[i] >= 'a' && s[i] <= 'z')
            v1.push_back(s[i]);
        if (s[i] >= 'A' && s[i] <= 'Z')
            v2.push_back(s[i]);
    }

    // Sort both the vectors
    sort(v1.begin(), v1.end());
    sort(v2.begin(), v2.end());
    int i = 0, j = 0;
    for (int k = 0; k < n; k++) {

        // If current character is lowercase
        // then pick the lowercase character
        // from the sorted list
        if (s[k] >= 'a' && s[k] <= 'z') {
            s[k] = v1[i];
            ++i;
        }

        // Else pick the uppercase character
        else if (s[k] >= 'A' && s[k] <= 'Z') {
            s[k] = v2[j];
            ++j;
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
import java.util.Collections;
import java.util.Vector;

class GFG{

// Function to return the sorted string
public static String getSortedString(StringBuilder s,
                                     int n)
{

    // Vectors to store the lowercase
    // and uppercase characters
    Vector<Character> v1 = new Vector<>();
    Vector<Character> v2 = new Vector<>();

    for(int i = 0; i < n; i++)
    {
        if (s.charAt(i) >= 'a' &&
            s.charAt(i) <= 'z')
            v1.add(s.charAt(i));

        if (s.charAt(i) >= 'A' &&
            s.charAt(i) <= 'z')
            v2.add(s.charAt(i));
    }

    // Sort both the vectors
    Collections.sort(v1);
    Collections.sort(v2);

    int i = 0, j = 0;

    for(int k = 0; k < n; k++)
    {

        // If current character is lowercase
        // then pick the lowercase character
        // from the sorted list
        if (s.charAt(k) > ='a' &&
            s.charAt(k) <= 'z')
        {
            s.setCharAt(k, v1.elementAt(i));
            ++i;
        }

        // Else pick the uppercase character
        else if (s.charAt(k) > ='A' &&
                 s.charAt(k) <= 'Z')
        {
            s.setCharAt(k, v2.elementAt(j));
            ++j;
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

# Function to return the sorted string
def getSortedString(s, n):

    # Vectors to store the lowercase
    # and uppercase characters
    v1=[]
    v2=[]
    for i in range(n):
        if (s[i] >= 'a' and s[i] <= 'z'):
            v1.append(s[i])
        if (s[i] >= 'A' and s[i] <= 'Z'):
            v2.append(s[i])

    # Sort both the vectors
    v1=sorted(v1)
    v2=sorted(v2)
    i = 0
    j = 0
    for k in range(n):

        # If current character is lowercase
        # then pick the lowercase character
        # from the sorted list
        if (s[k] >= 'a' and s[k] <= 'z'):
            s[k] = v1[i]
            i+=1

        # Else pick the uppercase character
        elif (s[k] >= 'A' and s[k] <= 'Z'):
            s[k] = v2[j]
            j+=1

    # Return the sorted string
    return "".join(s)

# Driver code
s = "gEeksfOrgEEkS"
ss=[i for i in s]
n = len(ss)

print(getSortedString(ss, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the sorted string
    public static String getSortedString(char[] s, 
                                         int n)
    {

        // Vectors to store the lowercase
        // and uppercase characters
        List<char> v1 = new List<char>();
        List<char> v2 = new List<char>();
        int i = 0;
        for (i = 0; i < n; i++)
        {
            if (s[i] > 'a' && s[i] <= 'z')
                v1.Add(s[i]);

            if (s[i] > 'A' && s[i] <= 'z')
                v2.Add(s[i]);
        }

        // Sort both the vectors
        v1.Sort();
        v2.Sort();
        int j = 0;
        i = 0;
        for (int k = 0; k < n; k++)
        {

            // If current character is lowercase
            // then pick the lowercase character
            // from the sorted list
            if (s[k] > 'a' && s[k] <= 'z')
            {
                s[k] = v1[i];
                ++i;
            }

            // Else pick the uppercase character
            else if (s[k] > 'A' && s[k] <= 'Z')
            {
                s[k] = v2[j];
                ++j;
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

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the sorted string
      function getSortedString(s, n) {
        // Vectors to store the lowercase
        // and uppercase characters
        var v1 = [];
        var v2 = [];
        var i = 0;
        for (i = 0; i < n; i++) {
          if (
            s[i].charCodeAt(0) > "a".charCodeAt(0) &&
            s[i].charCodeAt(0) <= "z".charCodeAt(0)
          )
            v1.push(s[i]);

          if (
            s[i].charCodeAt(0) > "A".charCodeAt(0) &&
            s[i].charCodeAt(0) <= "Z".charCodeAt(0)
          )
            v2.push(s[i]);
        }

        // Sort both the vectors
        console.log(v1);
        v1.sort();
        v2.sort();
        var j = 0;
        i = 0;
        for (var k = 0; k < n; k++) {
          // If current character is lowercase
          // then pick the lowercase character
          // from the sorted list
          if (
            s[k].charCodeAt(0) > "a".charCodeAt(0) &&
            s[k].charCodeAt(0) <= "z".charCodeAt(0)
          ) {
            s[k] = v1[i];
            ++i;
          }

          // Else pick the uppercase character
          else if (
            s[k].charCodeAt(0) > "A".charCodeAt(0) &&
            s[k].charCodeAt(0) <= "Z".charCodeAt(0)
          ) {
            s[k] = v2[j];
            ++j;
          }
        }

        // Return the sorted string
        return s.join("");
      }

      // Driver code
      var s = "gEeksfOrgEEkS";
      var n = s.length;
      document.write(getSortedString(s.split(""), n));
</script>
```

**Output**

```
eEfggkEkrEOsS
```

https://youtu . be/ICB 4 and EBN 9g