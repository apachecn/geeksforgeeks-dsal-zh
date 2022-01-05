# 查找最大长度奇数奇偶子串

> 原文:[https://www . geesforgeks . org/find-max-length-奇数-奇偶校验-substring/](https://www.geeksforgeeks.org/find-max-length-odd-parity-substring/)

给定一个二进制字符串 **str** ，任务是找到具有奇偶性的 **str** 的子字符串的最大长度。如果一个二进制字符串包含奇数个 **1** s，则称其为奇数奇偶校验。

**示例:**

> **输入:** str = "1001110"
> **输出:**6
> “001110”为有效子串。
> 
> **输入:**str = " 101101 "
> T3】输出: 5

**进场:**

1.  计算给定字符串中 **1** 的数量，并将其存储在变量 **cnt** 中。
2.  如果 **cnt = 0** ，则不存在奇数奇偶校验的子串，因此结果将是 **0** 。
3.  如果 **cnt** 是**奇数**，那么结果将是完整的字符串。
4.  现在对于 **cnt** 为**偶数**和**T12】0**的情况，所需的子串将从索引 **0** 开始，在最后一次出现 **1** 之前结束，或者在第一次出现 **1** 之后开始，在给定串的末尾结束。
5.  在上一步的两个子串中选择长度较大的一个。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

    // finds the index of character of string
    int indexOf(string s, char c, int i)
    {
        for(; i < s.length(); i++)
        if(s[i] == c)
        return i;

        return -1;
    }

    // finds the last index of character of string
    int lastIndexOf(string s,char c,int i)
    {
        for(; i >= 0; i--)
        if(s[i] == c)
            return i;

        return -1;
    }

    // Function to return the maximum
    // length of the sub-string which
    // contains odd number of 1s
    int maxOddParity(string str, int n)
    {

        // Find the count of 1s in
        // the given string
        int cnt = 0;
        for (int i = 0; i < n; i++)
            if (str[i] == '1')
                cnt++;

        // If there are only 0s in the string
        if (cnt == 0)
            return 0;

        // If the count of 1s is odd then
        // the complete string has odd parity
        if (cnt % 2 == 1)
            return n;

        // Index of the first and the second
        // occurrences of '1' in the string
        int firstOcc = indexOf(str,'1',0);
        int secondOcc = indexOf(str,'1', firstOcc + 1);

        // Index of the last and the second last
        // occurrences of '1' in the string
        int lastOcc = lastIndexOf(str,'1',str.length()-1);
        int secondLastOcc = lastIndexOf(str,'1', lastOcc - 1);

        // Result will the sub-string ending just
        // before the last occurrence of '1' or the
        // sub-string starting just after the first
        // occurrence of '1'
        // choose the one with the maximum length
        return max(lastOcc, n - firstOcc - 1);
    }

    // Driver code
    int main()
    {
        string str = "101101";
        int n = str.length();
        cout<<(maxOddParity(str, n));
    }

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to return the maximum
    // length of the sub-string which
    // contains odd number of 1s
    static int maxOddParity(String str, int n)
    {

        // Find the count of 1s in
        // the given string
        int cnt = 0;
        for (int i = 0; i < n; i++)
            if (str.charAt(i) == '1')
                cnt++;

        // If there are only 0s in the string
        if (cnt == 0)
            return 0;

        // If the count of 1s is odd then
        // the complete string has odd parity
        if (cnt % 2 == 1)
            return n;

        // Index of the first and the second
        // occurrences of '1' in the string
        int firstOcc = str.indexOf('1');
        int secondOcc = str.indexOf('1', firstOcc + 1);

        // Index of the last and the second last
        // occurrences of '1' in the string
        int lastOcc = str.lastIndexOf('1');
        int secondLastOcc = str.lastIndexOf('1', lastOcc - 1);

        // Result will the sub-string ending just
        // before the last occurrence of '1' or the
        // sub-string starting just after the first
        // occurrence of '1'
        // choose the one with the maximum length
        return Math.max(lastOcc, n - firstOcc - 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "101101";
        int n = str.length();
        System.out.print(maxOddParity(str, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# length of the sub-string which
# contains odd number of 1s
def maxOddParity(string, n):

    # Find the count of 1s in
    # the given string
    cnt = 0
    for i in range(n):
        if string[i] != '1':
            cnt += 1

    # If there are only 0s in the string
    if cnt == 0:
        return 0

    # If the count of 1s is odd then
    # the complete string has odd parity
    if cnt % 2 == 1:
        return n

    # Index of the first and the second
    # occurrences of '1' in the string
    firstOcc = string.index('1')
    secondOcc = string.index('1', firstOcc + 1)

    # Index of the last and the second last
    # occurrences of '1' in the string
    lastOcc = string.rindex('1')
    secondLastOcc = string.rindex('1', 0, lastOcc)

    # Result will the sub-string ending just
    # before the last occurrence of '1' or the
    # sub-string starting just after the first
    # occurrence of '1'
    # choose the one with the maximum length
    return max(lastOcc, n - firstOcc - 1)

# Driver Code
if __name__ == "__main__":
    string = "101101"
    n = len(string)
    print(maxOddParity(string, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the maximum
    // length of the sub-string which
    // contains odd number of 1s
    static int maxOddParity(String str, int n)
    {

        // Find the count of 1s in
        // the given string
        int cnt = 0;
        for (int i = 0; i < n; i++)
            if (str[i] == '1')
                cnt++;

        // If there are only 0s in the string
        if (cnt == 0)
            return 0;

        // If the count of 1s is odd then
        // the complete string has odd parity
        if (cnt % 2 == 1)
            return n;

        // Index of the first and the second
        // occurrences of '1' in the string
        int firstOcc = str.IndexOf('1');
        int secondOcc = str.IndexOf('1', firstOcc + 1);

        // Index of the last and the second last
        // occurrences of '1' in the string
        int lastOcc = str.LastIndexOf('1');
        int secondLastOcc = str.LastIndexOf('1', lastOcc - 1);

        // Result will the sub-string ending just
        // before the last occurrence of '1' or the
        // sub-string starting just after the first
        // occurrence of '1'
        // choose the one with the maximum length
        return Math.Max(lastOcc, n - firstOcc - 1);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "101101";
        int n = str.Length;
        Console.WriteLine(maxOddParity(str, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the maximum
// length of the sub-string which
// contains odd number of 1s
function maxOddParity(str, n)
{

    // Find the count of 1s in
    // the given string
    var cnt = 0;
    for(var i = 0; i < n; i++)
        if (str[i] == '1')
            cnt++;

    // If there are only 0s in the string
    if (cnt == 0)
        return 0;

    // If the count of 1s is odd then
    // the complete string has odd parity
    if (cnt % 2 == 1)
        return n;

    // Index of the first and the second
    // occurrences of '1' in the string
    var firstOcc = str.indexOf('1');
    var secondOcc = str.indexOf(
        '1', firstOcc + 1);

    // Index of the last and the second last
    // occurrences of '1' in the string
    var lastOcc = str.lastIndexOf('1');
    var secondLastOcc = str.lastIndexOf(
        '1', lastOcc - 1);

    // Result will the sub-string ending just
    // before the last occurrence of '1' or the
    // sub-string starting just after the first
    // occurrence of '1'
    // choose the one with the maximum length
    return Math.max(lastOcc, n - firstOcc - 1);
}

// Driver code
var str = "101101";
var n = str.length;

document.write(maxOddParity(str, n));

// This code is contributed by bunnyram19

</script>
```

**Output:** 

```
5
```