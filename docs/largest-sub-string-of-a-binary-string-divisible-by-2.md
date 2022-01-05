# 可被 2 整除的二进制串中最大的子串

> 原文:[https://www . geesforgeks . org/最大二进制字符串子字符串可被 2 整除/](https://www.geeksforgeeks.org/largest-sub-string-of-a-binary-string-divisible-by-2/)

给定长度为 **N** 的二进制字符串 **str** ，任务是找到可被 **2** 整除的最长子字符串。如果不存在这样的子字符串，则打印 **-1** 。

**示例:**

> **输入:** str = "11100011"
> **输出:** 111000
> 可被 2 整除的最大子串为“111000”。
> **输入:** str = "1111"
> **输出:** -1
> 给定字符串
> 没有可被 2 整除的子字符串。

**天真的方法:**天真的方法是生成所有这样的子字符串，并检查它们是否能被 2 整除。这种方法的时间复杂度为 0(N<sup>3</sup>)。

**更好的方法:**一个简单的方法是从字符串末尾删除字符，而最后一个字符是 **1** 。当遇到 **0** 时，当前字符串将被 **2** 整除，因为它在 **0** 结束。这种方法的时间复杂度将是 O(N)。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the largest
// substring divisible by 2
string largestSubStr(string s)
{
    // While the last character of
    // the string is '1', pop it
    while (s.size() and s[s.size() - 1] == '1')
        s.pop_back();

    // If the original string had no '0'
    if (s.size() == 0)
        return "-1";
    else
        return s;
}

// Driver code
int main()
{
    string s = "11001";

    cout << largestSubStr(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the largest
    // substring divisible by 2
    static String largestSubStr(String s)
    {
        // While the last character of
        // the string is '1', pop it
        while (s.length() != 0 &&
               s.charAt(s.length() - 1) == '1')
            s = s.substring(0, s.length() - 1);

        // If the original string had no '0'
        if (s.length() == 0)
            return "-1";
        else
            return s;
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "11001";

        System.out.println(largestSubStr(s));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the largest
# substring divisible by 2
def largestSubStr(s) :

    # While the last character of
    # the string is '1', pop it
    while (len(s) and s[len(s) - 1] == '1') :
        s = s[:len(s) - 1];

    # If the original string had no '0'
    if (len(s) == 0) :
        return "-1";
    else :
        return s;

# Driver code
if __name__ == "__main__" :

    s = "11001";

    print(largestSubStr(s));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the largest
    // substring divisible by 2
    static string largestSubStr(string s)
    {
        // While the last character of
        // the string is '1', pop it
        while (s.Length != 0 &&
               s[s.Length - 1] == '1')
            s = s.Substring(0, s.Length - 1);

        // If the original string had no '0'
        if (s.Length == 0)
            return "-1";
        else
            return s;
    }

    // Driver code
    public static void Main ()
    {
        string s = "11001";

        Console.WriteLine(largestSubStr(s));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the largest
// substring divisible by 2
function largestSubStr(s)
{
    // While the last character of
    // the string is '1', pop it
    while (s.length && s[s.length - 1] == '1')
        s = s.substring(0,s.length-1);;

    // If the original string had no '0'
    if (s.length == 0)
        return "-1";
    else
        return s;
}

// Driver code
var s = "11001";
document.write( largestSubStr(s));

</script>
```

**Output:** 

```
1100
```