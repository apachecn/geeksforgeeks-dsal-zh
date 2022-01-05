# 检查给定字符串是否存在不包含任何单调子串的排列

> 原文:[https://www . geeksforgeeks . org/check-if-exists-a-arrange-of-给定字符串，其中不包含任何单调的子字符串/](https://www.geeksforgeeks.org/check-if-there-exists-a-permutation-of-given-string-which-doesnt-contain-any-monotonous-substring/)

给定一个由小写英文字母组成的字符串 **S** ，任务是检查字符串 **S** 的排列是否不包含任何单调的子字符串。

> 单调子串具有以下属性:
> 
> *   这种子串长度为 2。
> *   两个字符都是连续的，例如–“ab”、“cd”、“dc”、“zy”等。

**示例:**

> **输入:** S = "abcd"
> **输出:**是
> **说明:**
> 字符串 S 可以重新排列成“cadb”或“bdac”
> 
> **输入:**string =“aab”
> **输出:** No
> **解释:**
> 字符串的每个排列都包含一个单调的子串。

**方法:**想法是将字符分组到两个不同的桶中，其中一个桶包含位于偶数位置的字符，另一个桶包含位于奇数位置的字符。最后，检查两个组的拼接点是否不是单调的子串。

下面是上述方法的实现:

## C++

```
// C++ implementation such that there
// are no monotonous
// string in given string

#include <bits/stdc++.h>

using namespace std;

// Function to check a string doesn't
// contains a monotonous substring
bool check(string s)
{
    bool ok = true;

    // Loop to iterate over the string
    // and check that it doesn't contains
    // the monotonous substring
    for (int i = 0; i + 1 < s.size(); ++i)
        ok &= (abs(s[i] - s[i + 1]) != 1);
    return ok;
}

// Function to check that there exist
// a arrangement of string such that
// it doesn't contains monotonous substring
string monotonousString(string s)
{
    string odd = "", even = "";

    // Loop to group the characters
    // of the string into two buckets
    for (int i = 0; i < s.size(); ++i) {
        if (s[i] % 2 == 0)
            odd += s[i];
        else
            even += s[i];
    }

    // Sorting the two buckets
    sort(odd.begin(), odd.end());
    sort(even.begin(), even.end());

    // Condition to check if the
    // concatenation point doesn't
    // contains the monotonous string
    if (check(odd + even))
        return "Yes";
    else if (check(even + odd))
        return "Yes";
    return "No";
}

// Driver Code
int main()
{
    string str = "abcd";
    string ans;
    ans = monotonousString(str);
    cout << ans << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation such that there
// are no monotonous
// string in given string
import java.io.*;
import java.util.*;

class GFG{

// Function to check a string doesn't
// contains a monotonous substring
static boolean check(String s)
{
    boolean ok = true;

    // Loop to iterate over the string
    // and check that it doesn't contains
    // the monotonous substring
    for (int i = 0; i + 1 < s.length(); ++i)
        ok &= (Math.abs(s.charAt(i) -
                        s.charAt(i + 1)) != 1);
    return ok;
}

// Function to check that there exist
// a arrangement of string such that
// it doesn't contains monotonous substring
static String monotonousString(String s)
{
    String odd = "", even = "";

    // Loop to group the characters
    // of the string into two buckets
    for (int i = 0; i < s.length(); ++i)
    {
        if (s.charAt(i) % 2 == 0)
            odd += s.charAt(i);
        else
            even += s.charAt(i);
    }

    // Sorting the two buckets
    char oddArray[] = odd.toCharArray();
    Arrays.sort(oddArray);
    odd = new String(oddArray);

    char evenArray[] = even.toCharArray();
    Arrays.sort(evenArray);
    even = new String(evenArray);

    // Condition to check if the
    // concatenation point doesn't
    // contains the monotonous string
    if (check(odd + even))
        return "Yes";
    else if (check(even + odd))
        return "Yes";
    return "No";
}

// Driver Code
public static void main(String []args)
{
    String str = "abcd";
    String ans;
    ans = monotonousString(str);
    System.out.println( ans);
}
}

// This code is contributed by ChitraNayal
```

## 蟒蛇 3

```
# Python3 implementation such that there
# are no monotonous string in given string

# Function to check a string doesn't
# contains a monotonous substring
def check(s):

    ok = True

    # Loop to iterate over the string
    # and check that it doesn't contains
    # the monotonous substring
    for i in range(0, len(s) - 1, 1):
        ok = (ok & (abs(ord(s[i]) -
                        ord(s[i + 1])) != 1))
    return ok

# Function to check that there exist
# a arrangement of string such that
# it doesn't contains monotonous substring
def monotonousString(s):

    odd = ""
    even = ""

    # Loop to group the characters
    # of the string into two buckets
    for i in range(len(s)):

        if (ord(s[i]) % 2 == 0):
            odd += s[i]
        else:
            even += s[i]

    # Sorting the two buckets
    odd = list(odd)
    odd.sort(reverse = False)
    odd = str(odd)

    even = list(even)
    even.sort(reverse = False)
    even = str(even)

    # Condition to check if the
    # concatenation point doesn't
    # contains the monotonous string
    if (check(odd + even)):
        return "Yes"
    elif (check(even + odd)):
        return "Yes"

    return "No"

# Driver Code
if __name__ == '__main__':

    str1 = "abcd"
    ans = monotonousString(str1)

    print(ans)

# This code is contributed by Samarth
```

## C#

```
// C# implementation such that there
// are no monotonous
// string in given string
using System;

class GFG{

// Function to check a string doesn't
// contains a monotonous substring
static bool check(string s)
{
    bool ok = true;

    // Loop to iterate over the string
    // and check that it doesn't contains
    // the monotonous substring
    for(int i = 0; i + 1 < s.Length; ++i)
        ok &= (Math.Abs(s[i] -
                        s[i + 1]) != 1);

    return ok;
}

// Function to check that there exist
// a arrangement of string such that
// it doesn't contains monotonous substring
static string monotonousString(string s)
{
    string odd = "", even = "";

    // Loop to group the characters
    // of the string into two buckets
    for(int i = 0; i < s.Length; ++i)
    {
        if (s[i] % 2 == 0)
            odd += s[i];
        else
            even += s[i];
    }

    // Sorting the two buckets
    char []oddArray = odd.ToCharArray();
    Array.Sort(oddArray);
    odd = new String(oddArray);

    char []evenArray = even.ToCharArray();
    Array.Sort(evenArray);
    even = new String(evenArray);

    // Condition to check if the
    // concatenation point doesn't
    // contains the monotonous string
    if (check(odd + even))
        return "Yes";

    else if (check(even + odd))
        return "Yes";

    return "No";
}

// Driver Code
public static void Main(string []args)
{
    string str = "abcd";
    string ans;

    ans = monotonousString(str);

    Console.Write(ans);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation such that there
// are no monotonous
// string in given string

// Function to check a string doesn't
// contains a monotonous substring
function check(s)
{
    var ok = true;

    // Loop to iterate over the string
    // and check that it doesn't contains
    // the monotonous substring
    for (var i = 0; i + 1 < s.length; ++i)
        ok &= (Math.abs(s[i] - s[i + 1]) != 1);
    return ok;
}

// Function to check that there exist
// a arrangement of string such that
// it doesn't contains monotonous substring
function monotonousString(s)
{
    var odd = "", even = "";

    // Loop to group the characters
    // of the string into two buckets
    for (var i = 0; i < s.length; ++i) {
        if (s[i] % 2 == 0)
            odd += s[i];
        else
            even += s[i];
    }

    // Sorting the two buckets
    odd  = odd.split('').sort().join('');
    even = even.split('').sort().join('');

    // Condition to check if the
    // concatenation point doesn't
    // contains the monotonous string
    if (check(odd + even))
        return "Yes";
    else if (check(even + odd))
        return "Yes";
    return "No";
}

// Driver Code
var str = "abcd";
var ans;
ans = monotonousString(str);
document.write( ans );

</script>
```

**Output:** 

```
Yes
```