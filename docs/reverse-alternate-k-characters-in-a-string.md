# 反转字符串中的 k 个交替字符

> 原文:[https://www . geesforgeks . org/reverse-alternate-k-characters in-a-string/](https://www.geeksforgeeks.org/reverse-alternate-k-characters-in-a-string/)

给定一个字符串 **str** 和一个整数 **k** ，任务是反转给定字符串的交替 **k** 字符。如果出现的字符少于 k，保持不变。
**举例:**

> **输入:** str = "geeksforgeeks "，k = 3
> **输出:** eegksfgroeeks
> **输入:** str = "abcde "，k = 2
> **输出:** bacde

**方法:**思路是先反转 **k** 字符，然后通过在索引中添加 **2 * k** 跳到下一个 **k** 字符，以此类推，直到修改完完整的字符串。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the string after
// reversing the alternate k characters
string revAlternateK(string s, int k, int len)
{

    for (int i = 0; i < s.size();) {

        // If there are less than k characters
        // starting from the current position
        if (i + k > len)
            break;

        // Reverse first k characters
        reverse(s.begin() + i, s.begin() + i + k);

        // Skip the next k characters
        i += 2 * k;
    }
    return s;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";
    int len = s.length();
    int k = 3;
    cout << revAlternateK(s, k, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the string after
// reversing the alternate k characters
static String revAlternateK(String s,
                            int k, int len)
{
    for (int i = 0; i < s.length();)
    {

        // If there are less than k characters
        // starting from the current position
        if (i + k > len)
            break;

        // Reverse first k characters
        s = s.substring(0, i) + new String(new StringBuilder(
            s.substring(i, i + k)).reverse()) +
            s.substring(i + k);

        // Skip the next k characters
        i += 2 * k;
    }
    return s;
}

// Driver code
public static void main(String[] args)
{
    String s = "geeksforgeeks";
    int len = s.length();
    int k = 3;
    System.out.println(revAlternateK(s, k, len));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the string after
# reversing the alternate k characters
def revAlternateK(s, k, Len):
    i = 0

    while(i < len(s)):

        # If there are less than k characters
        # starting from the current position
        if (i + k > Len):
            break

        # Reverse first k characters
        ss = s[i:i + k]
        s = s[:i]+ss[::-1]+s[i + k:]

        # Skip the next k characters
        i += 2 * k

    return s;

# Driver code

s = "geeksforgeeks"
Len = len(s)
k = 3
print(revAlternateK(s, k, Len))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the string after
// reversing the alternate k characters
static String revAlternateK(String s,
                            int k, int len)
{
    for (int i = 0; i < s.Length;)
    {

        // If there are less than k characters
        // starting from the current position
        if (i + k > len)
            break;

        // Reverse first k characters
        s = s.Substring(0, i) +
            reverse(s.Substring(i, k).ToCharArray(), 0, k - 1) +
            s.Substring(i + k);

        // Skip the next k characters
        i += 2 * k;
    }
    return s;
}
static String reverse(char []str, int start, int end)
{

    // Temporary variable to store character
    char temp;
    while (start <= end)
    {
        // Swapping the first and last character
        temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
    return String.Join("", str);
}

// Driver code
public static void Main(String[] args)
{
    String s = "geeksforgeeks";
    int len = s.Length;
    int k = 3;
    Console.WriteLine(revAlternateK(s, k, len));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the string after
// reversing the alternate k characters
function revAlternateK(s,k,len)
{
    for (let i = 0; i < s.length;)
    {

        // If there are less than k characters
        // starting from the current position
        if (i + k > len)
            break;

        // Reverse first k characters
        s = s.substring(0, i) + s.substring(i, i + k).split("").reverse().join("") +
            s.substring(i + k);

        // Skip the next k characters
        i += 2 * k;
    }
    return s;
}

// Driver code
let s = "geeksforgeeks";
let len = s.length;
let k = 3;
document.write(revAlternateK(s, k, len));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
eegksfgroeeks
```