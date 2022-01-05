# 作为同一字符串前缀的字符串的子字符串

> 原文:[https://www . geesforgeks . org/同一个字符串前缀的子字符串/](https://www.geeksforgeeks.org/sub-strings-of-a-string-that-are-prefix-of-the-same-string/)

给定一个字符串 **str** ，任务是统计给定字符串中所有可能的子字符串，这些子字符串是同一字符串的前缀。

**示例:**

> **输入:**str = " ababc "
> T3】输出: 7
> 所有可能的子串都是“a”、“ab”、“aba”、“abab”、“ababc”、“a”和“ab”
> 
> **输入:**str = " abdabc "
> T3】输出: 8

**方法:**逐字符遍历字符串，如果当前字符等于字符串的第一个字符，则从这里开始计数所有可能的子字符串，这些子字符串也是**字符串**的前缀，并将其添加到**计数**中。遍历完整字符串后，打印**计数**。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach
#include <iostream>
#include <string>
using namespace std;

// Function to return the
// count of sub-strings starting
// from startIndex that are
// also the prefixes of str
int subStringsStartingHere(string str, int n,
                            int startIndex)
{
    int count = 0, i = 1;
    while (i <= n)
    {
        if (str.substr(0,i) ==
                str.substr(startIndex, i))
        {
            count++;
        }
        else
            break;
        i++;
    }

    return count;
}

// Function to return the
// count of all possible sub-strings
// of str that are also the prefixes of str
int countSubStrings(string str, int n)
{
    int count = 0;
    for (int i = 0; i < n; i++)
    {

        // If current character is equal to
        // the starting character of str
        if (str[i] == str[0])
            count += subStringsStartingHere(str,
                                           n, i);
    }
    return count;
}

// Driver code
int main()
{
    string str = "abcda";
    int n = str.length();

    // Function Call
    cout << (countSubStrings(str, n));
}

// This code is contributed by harshvijeta0
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG
{

  // Function to return
  // the count of sub-strings starting
  // from startIndex that
  // are also the prefixes of str
  public static int subStringsStartingHere(
                                String str, int n,
                                    int startIndex)
  {
    int count = 0, i = startIndex + 1;
    while (i <= n)
    {
      if (str.startsWith(str.substring(
                                 startIndex, i)))
      {
        count++;
      }
      else
        break;
      i++;
    }
    return count;
  }

  // Function to return the
  // count of all possible sub-strings
  // of str that are also the prefixes of str
  public static int countSubStrings(String str,
                                         int n)
  {
    int count = 0;

    for (int i = 0; i < n; i++)
    {

      // If current character is equal to
      // the starting character of str
      if (str.charAt(i) == str.charAt(0))
        count += subStringsStartingHere(str, n, i);
    }

    return count;
  }

  // Driver code
  public static void main(String[] args)
  {
    String str = "ababc";
    int n = str.length();
    System.out.println(countSubStrings(str, n));
  }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# count of sub-strings starting
# from startIndex that are
# also the prefixes of string
def subStringsStartingHere(string, n,
                           startIndex):
    count = 0
    i = startIndex + 1

    while(i <= n) :
        if string.startswith(
                 string[startIndex : i]):
            count += 1
        else :
            break

        i += 1

    return count

# Function to return the
# count of all possible sub-strings
# of string that are also
# the prefixes of string
def countSubStrings(string, n) :
    count = 0

    for i in range(n) :

        # If current character is equal to 
        # the starting character of str
        if string[i] == string[0] :
            count += subStringsStartingHere(
                              string, n, i)

    return count

# Driver Code
if __name__ == "__main__" :

    string = "ababc"
    n = len(string)
    print(countSubStrings(string, n))

# this code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function to return the
    // count of sub-strings starting
    // from startIndex that
    // are also the prefixes of str
    static int subStringsStartingHere(
                               String str, int n,
                                   int startIndex)
    {
        int count = 0, i = startIndex + 1;
        while (i <= n) {
            if (str.StartsWith(str.Substring(
                  startIndex, i-startIndex)))
            {
                count++;
            }
            else
                break;
            i++;
        }

        return count;
    }

    // Function to return the
    // count of all possible sub-strings
    // of str that are also the prefixes of str
    static int countSubStrings(String str, int n)
    {
        int count = 0;

        for (int i = 0; i < n; i++) {

            // If current character is equal to
            // the starting character of str
            if (str[i] == str[0])
                count += subStringsStartingHere(
                                        str, n, i);
        }

        return count;
    }

    // Driver code
    static public void Main(String []args)
    {
        String str = "ababc";
        int n = str.Length;
        Console.WriteLine(countSubStrings(str, n));
    }
}
//contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the
// count of sub-strings starting
// from startIndex that are
// also the prefixes of str
function subStringsStartingHere(str, n,
                                startIndex)
{
    var count = 0, i = startIndex + 1;

    while (i <= n)
    {
        if (str.startsWith(
            str.substring(startIndex, i)))
        {
            count++;
        }
        else
            break;

        i++;
    }
    return count;
}

// Function to return the count of all
// possible sub-strings of str that are
// also the prefixes of str
function countSubStrings(str, n)
{
    var count = 0;
    for(var i = 0; i < n; i++)
    {

        // If current character is equal to
        // the starting character of str
        if (str[i] == str[0])
            count += subStringsStartingHere(str,
                                            n, i);
    }
    return count;
}

// Driver code
var str = "abcda";
var n = str.length;

// Function Call
document.write(countSubStrings(str, n));

// This code is contributed by rutvik_56

</script>
```

**Output**

```
6
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(1)

**有效方法:**

**先决条件:** [Z 算法](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)

**方法:**计算字符串的 z 数组，使得 z[i]存储从 I 开始的最长子字符串的长度，I 也是字符串 s 的前缀。然后，为了计数作为同一字符串前缀的字符串的所有可能的子字符串，我们只需要将 z 数组的所有值相加，因为匹配的子字符串的总数将等于最长子字符串的长度。

实施上述方法

## C++

```
#include <bits/stdc++.h>
using namespace std;

// returns an array z such that  z[i]
// stores length of the longest substring starting
// from i which is also a prefix of string s
vector<int> z_function(string s)
{
    int n = (int)s.length();
    vector<int> z(n);
    // consider a window [l,r]
    // which matches with prefix of s
    int l = 0, r = 0;
    z[0] = n;
    for (int i = 1; i < n; ++i) {
        // when i<=r, we make use of already computed z
        // value for some smaller index
        if (i <= r)
            z[i] = min(r - i + 1, z[i - l]);

        // if i>r nothing matches so we will calculate
        // z[i] using naive way.
        while (i + z[i] < n && s[z[i]] == s[i + z[i]])
            ++z[i];
        // update window size
        if (i + z[i] - 1 > r)
            l = i, r = i + z[i] - 1;
    }
    return z;
}

int main()
{
    string s = "abcda";

    int n = s.length();

    vector<int> z = z_function(s);

    // stores the count of
    // Sub-strings of a string that
    // are prefix of the same string
    int count = 0;

    for (auto x : z)
        count += x;

    cout << count << '\n';

    return 0;
}
```

## 蟒蛇 3

```
# returns an array z such that  z[i]
# stores length of the longest substarting
# from i which is also a prefix of s
def z_function(s):
    n = len(s)
    z=[0]*n
    # consider a window [l,r]
    # which matches with prefix of s
    l = 0; r = 0
    z[0] = n
    for i in range(1, n) :
        # when i<=r, we make use of already computed z
        # value for some smaller index
        if (i <= r):
            z[i] = min(r - i + 1, z[i - l])

        # if i>r nothing matches so we will calculate
        # z[i] using naive way.
        while (i + z[i] < n and s[z[i]] == s[i + z[i]]):
            z[i]+=1
        # update window size
        if (i + z[i] - 1 > r):
            l = i; r = i + z[i] - 1

    return z

if __name__ == '__main__':
    s = "abcda"

    n = len(s)

    z = z_function(s)

    # stores the count of
    # Sub-strings of a that
    # are prefix of the same string
    count = 0

    for x in z:
        count += x

    print(count)
```

**Output**

```
6
```

**时间复杂度:** O(n)

**辅助空间:** O(n)