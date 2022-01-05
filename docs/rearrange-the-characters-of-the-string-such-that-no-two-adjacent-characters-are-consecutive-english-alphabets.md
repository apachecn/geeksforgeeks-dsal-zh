# 重新排列字符串的字符，使得没有两个相邻的字符是连续的英文字母

> 原文:[https://www . geeksforgeeks . org/重新排列字符串中的字符，使得没有两个相邻的字符是连续的英文字母/](https://www.geeksforgeeks.org/rearrange-the-characters-of-the-string-such-that-no-two-adjacent-characters-are-consecutive-english-alphabets/)

给定字符串**大小为 **N** 的字符串**由小写英文字母组成。任务是找到字符串中字符的排列方式，使得在英文字母中没有两个相邻的字符是相邻的。如果有多个答案，打印其中任何一个。如果这样的安排是不可能的，那么打印-1。
**例:**

> **输入:** str = "aabcd"
> **输出:** bdaac
> 英文字母中没有相邻的两个字符是相邻的。
> **输入:** str = "aab"
> **输出:** -1

**方法:**遍历字符串并将所有奇数位置的字符存储在一个字符串中**奇数**和偶数位置的字符存储在另一个字符串中**偶数**，即两个字符串中每两个连续的字符在 ASCII 值上的绝对差异至少为 2。然后[整理](https://www.geeksforgeeks.org/sort-c-stl/)两根琴弦。现在，如果连接**(偶数+奇数)**或**(奇数+偶数)**中的任何一个有效，则打印有效的排列，否则不可能以所需的方式重新排列字符串。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the
// current arrangement is valid
bool check(string s)
{
    for (int i = 0; i + 1 < s.size(); ++i)
        if (abs(s[i] - s[i + 1]) == 1)
            return false;
    return true;
}

// Function to rearrange the characters of
// the string such that no two neighbours
// in the English alphabets appear together
void Rearrange(string str)
{
    // To store the odd and the
    // even positioned characters
    string odd = "", even = "";

    // Traverse through the array
    for (int i = 0; i < str.size(); ++i) {
        if (str[i] % 2 == 0)
            even += str[i];
        else
            odd += str[i];
    }

    // Sort both the strings
    sort(odd.begin(), odd.end());
    sort(even.begin(), even.end());

    // Check possibilities
    if (check(odd + even))
        cout << odd + even;
    else if (check(even + odd))
        cout << even + odd;
    else
        cout << -1;
}

// Driver code
int main()
{
    string str = "aabcd";

    Rearrange(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function that returns true if the
    // current arrangement is valid
    static boolean check(String s)
    {
        for (int i = 0; i + 1 < s.length(); ++i)
        {
            if (Math.abs(s.charAt(i) -
                         s.charAt(i + 1)) == 1)
            {
                return false;
            }
        }
        return true;
    }

    // Function to rearrange the characters of
    // the string such that no two neighbours
    // in the English alphabets appear together
    static void Rearrange(String str)
    {

        // To store the odd and the
        // even positioned characters
        String odd = "", even = "";

        // Traverse through the array
        for (int i = 0; i < str.length(); ++i)
        {
            if (str.charAt(i) % 2 == 0)
            {
                even += str.charAt(i);
            }
            else
            {
                odd += str.charAt(i);
            }
        }

        // Sort both the strings
        odd = sort(odd);
        even = sort(even);

        // Check possibilities
        if (check(odd + even))
        {
            System.out.print(odd + even);
        }
        else if (check(even + odd))
        {
            System.out.print(even + odd);
        }
        else
        {
            System.out.print(-1);
        }
    }

    // Method to sort a string alphabetically
    public static String sort(String inputString)
    {
        // convert input string to char array
        char tempArray[] = inputString.toCharArray();

        // sort tempArray
        Arrays.sort(tempArray);

        // return new sorted string
        return new String(tempArray);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "aabcd";

        Rearrange(str);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the
# current arrangement is valid
def check(s):

    for i in range(len(s) - 1):
        if (abs(ord(s[i]) -
                ord(s[i + 1])) == 1):
            return False
    return True

# Function to rearrange the characters
# of the such that no two neighbours
# in the English alphabets appear together
def Rearrange(Str):

    # To store the odd and the
    # even positioned characters
    odd, even = "",""

    # Traverse through the array
    for i in range(len(Str)):
        if (ord(Str[i]) % 2 == 0):
            even += Str[i]
        else:
            odd += Str[i]

    # Sort both the Strings
    odd = sorted(odd)
    even = sorted(even)

    # Check possibilities
    if (check(odd + even)):
        print("".join(odd + even))
    elif (check(even + odd)):
        print("".join(even + odd))
    else:
        print(-1)

# Driver code
Str = "aabcd"

Rearrange(Str)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if the
    // current arrangement is valid
    static Boolean check(String s)
    {
        for (int i = 0; i + 1 < s.Length; ++i)
        {
            if (Math.Abs(s[i] -
                         s[i + 1]) == 1)
            {
                return false;
            }
        }
        return true;
    }

    // Function to rearrange the characters of
    // the string such that no two neighbours
    // in the English alphabets appear together
    static void Rearrange(String str)
    {

        // To store the odd and the
        // even positioned characters
        String odd = "", even = "";

        // Traverse through the array
        for (int i = 0; i < str.Length; ++i)
        {
            if (str[i] % 2 == 0)
            {
                even += str[i];
            }
            else
            {
                odd += str[i];
            }
        }

        // Sort both the strings
        odd = sort(odd);
        even = sort(even);

        // Check possibilities
        if (check(odd + even))
        {
            Console.Write(odd + even);
        }
        else if (check(even + odd))
        {
            Console.Write(even + odd);
        }
        else
        {
            Console.Write(-1);
        }
    }

    // Method to sort a string alphabetically
    public static String sort(String inputString)
    {
        // convert input string to char array
        char []tempArray = inputString.ToCharArray();

        // sort tempArray
        Array.Sort(tempArray);

        // return new sorted string
        return new String(tempArray);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "aabcd";

        Rearrange(str);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach

      // Function that returns true if the
      // current arrangement is valid
      function check(s) {
        for (var i = 0; i + 1 < s.length; ++i)
        {
          if (Math.abs(s[i].charCodeAt(0) -
          s[i + 1].charCodeAt(0)) === 1)
          {
            return false;
          }
        }
        return true;
      }

      // Function to rearrange the characters of
      // the string such that no two neighbours
      // in the English alphabets appear together
      function Rearrange(str) {
        // To store the odd and the
        // even positioned characters
        var odd = "",
          even = "";

        // Traverse through the array
        for (var i = 0; i < str.length; ++i) {
          if (str[i].charCodeAt(0) % 2 === 0) {
            even += str[i];
          } else {
            odd += str[i];
          }
        }

        // Sort both the strings
        odd.split("").sort((a, b) => a - b);
        even.split("").sort((a, b) => a - b);

        // Check possibilities
        if (check(odd + even)) {
          document.write(odd + even);
        } else if (check(even + odd)) {
          document.write(even + odd);
        } else {
          document.write(-1);
        }
      }

      // Driver code
      var str = "aabcd";
      Rearrange(str);

</script>
```

**Output:** 

```
bdaac
```