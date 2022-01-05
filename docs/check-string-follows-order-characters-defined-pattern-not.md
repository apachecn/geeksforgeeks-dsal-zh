# 检查字符串是否遵循模式定义的字符顺序|设置 1

> 原文:[https://www . geesforgeks . org/check-string-follow-order-characters-defined-pattern-not/](https://www.geeksforgeeks.org/check-string-follows-order-characters-defined-pattern-not/)

给定输入字符串和模式，检查输入字符串中的字符是否遵循由模式中的字符确定的相同顺序。假设模式中没有任何重复的字符。
**例:**

```
Input: 
string = "engineers rock"
pattern = "er";
Output: true
Explanation: 
All 'e' in the input string are before all 'r'.

Input: 
string = "engineers rock"
pattern = "egr";
Output: false
Explanation: 
There are two 'e' after 'g' in the input string.

Input: 
string = "engineers rock"
pattern = "gsr";
Output: false
Explanation: 
There are one 'r' before 's' in the input string.
```

想法很简单。对于模式字符串中的每对(x，y)连续字符，我们会找到输入字符串中 x 的最后一次出现和 y 的第一次出现。对于任何一对，如果字符 x 的最后一次出现在字符 y 的第一次出现之后，我们返回 false。检查模式字符串中的每对连续字符就足够了。例如，如果我们考虑模式中的三个连续字符，比如 x，y 和 z，如果(x，y)和(y，z)返回 true，这意味着(x，z)也是 true。
以下是上述思路的实现–

## C++

```
// C++ program check if characters in the input string
// follows the same order as determined by characters
// present in the given pattern
#include <iostream>
using namespace std;

// Function to check if characters in the input string
// follows the same order as determined by characters
// present in the given pattern
bool checkPattern(string str, string pattern)
{
    // len stores length of the given pattern
    int len = pattern.length();

    // if length of pattern is more than length of
    // input string, return false;
    if (str.length() < len)
        return false;

    for (int i = 0; i < len - 1; i++)
    {
        // x, y are two adjacent characters in pattern
        char x = pattern[i];
        char y = pattern[i + 1];

        // find index of last occurrence of character x
        // in the input string
        size_t last = str.find_last_of(x);

        // find index of first occurrence of character y
        // in the input string
        size_t first = str.find_first_of(y);

        // return false if x or y are not present in the
        // input string OR last occurrence of x is after
        // the first occurrence of y in the input string
        if (last == string::npos || first == 
            string::npos || last > first)   
        return false;
    }

    // return true if string matches the pattern
    return true;
}

// Driver code
int main()
{
    string str = "engineers rock";
    string pattern = "gsr";

    cout << boolalpha << checkPattern(str, pattern);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program check if characters in the input string
// follows the same order as determined by characters
// present in the given pattern

class GFG
{

    // Function to check if characters in the input string
    // follows the same order as determined by characters
    // present in the given pattern
    static boolean checkPattern(String str, String pattern)
    {
        // len stores length of the given pattern
        int len = pattern.length();

        // if length of pattern is more than length of
        // input string, return false;
        if (str.length() < len)
        {
            return false;
        }

        for (int i = 0; i < len - 1; i++)
        {
            // x, y are two adjacent characters in pattern
            char x = pattern.charAt(i);
            char y = pattern.charAt(i + 1);

            // find index of last occurrence of character x
            // in the input string
            int last = str.lastIndexOf(x);

            // find index of first occurrence of character y
            // in the input string
            int first = str.indexOf(y);

            // return false if x or y are not present in the
            // input string OR last occurrence of x is after
            // the first occurrence of y in the input string
            if (last == -1 || first
                    == -1 || last > first)
            {
                return false;
            }
        }

        // return true if string matches the pattern
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "engineers rock";
        String pattern = "gsr";

        System.out.println(checkPattern(str, pattern));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program check if characters in
# the input string follows the same order
# as determined by characters present in
# the given pattern

# Function to check if characters in the
# input string follows the same order as
# determined by characters present
# in the given pattern
def checkPattern(string, pattern):

    # len stores length of the given pattern
    l = len(pattern)

    # if length of pattern is more than length
    # of input string, return false;
    if len(string) < l:
        return False

    for i in range(l - 1):

        # x, y are two adjacent characters in pattern
        x = pattern[i]
        y = pattern[i + 1]

        # find index of last occurrence of
        # character x in the input string
        last = string.rindex(x)

        # find index of first occurrence of
        # character y in the input string
        first = string.index(y)

        # return false if x or y are not present
        # in the input string OR last occurrence of
        # x is after the first occurrence of y
        # in the input string
        if last == -1 or first == -1 or last > first:
            return False

    # return true if
    # string matches the pattern
    return True

# Driver Code
if __name__ == "__main__":
    string = "engineers rock"
    pattern = "gsr"
    print(checkPattern(string, pattern))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program check if characters in the input string
// follows the same order as determined by characters
// present in the given pattern
using System;

class GFG
{

    // Function to check if characters in the input string
    // follows the same order as determined by characters
    // present in the given pattern
    static Boolean checkPattern(String str, String pattern)
    {
        // len stores length of the given pattern
        int len = pattern.Length;

        // if length of pattern is more than length of
        // input string, return false;
        if (str.Length < len)
        {
            return false;
        }

        for (int i = 0; i < len - 1; i++)
        {
            // x, y are two adjacent characters in pattern
            char x = pattern[i];
            char y = pattern[i+1];

            // find index of last occurrence of character x
            // in the input string
            int last = str.LastIndexOf(x);

            // find index of first occurrence of character y
            // in the input string
            int first = str.IndexOf(y);

            // return false if x or y are not present in the
            // input string OR last occurrence of x is after
            // the first occurrence of y in the input string
            if (last == -1 || first
                    == -1 || last > first)
            {
                return false;
            }
        }

        // return true if string matches the pattern
        return true;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "engineers rock";
        String pattern = "gsr";

        Console.WriteLine(checkPattern(str, pattern));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
      // JavaScript program check if characters in the input string
      // follows the same order as determined by characters
      // present in the given pattern
      // Function to check if characters in the input string
      // follows the same order as determined by characters
      // present in the given pattern
      function checkPattern(str, pattern) {
        // len stores length of the given pattern
        var len = pattern.length;

        // if length of pattern is more than length of
        // input string, return false;
        if (str.length < len) {
          return false;
        }

        for (var i = 0; i < len - 1; i++) {
          // x, y are two adjacent characters in pattern
          var x = pattern[i];
          var y = pattern[i + 1];

          // find index of last occurrence of character x
          // in the input string
          var last = str.lastIndexOf(x);

          // find index of first occurrence of character y
          // in the input string
          var first = str.indexOf(y);

          // return false if x or y are not present in the
          // input string OR last occurrence of x is after
          // the first occurrence of y in the input string
          if (last === -1 || first === -1 || last > first) {
            return false;
          }
        }

        // return true if string matches the pattern
        return true;
      }

      // Driver code
      var str = "engineers rock";
      var pattern = "gsr";

      document.write(checkPattern(str, pattern));

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
false
```

我们已经讨论了另外两种方法来解决这个问题。
[检查字符串是否遵循模式定义的字符顺序|第 2 集](https://www.geeksforgeeks.org/check-if-string-follows-order-of-characters-defined-by-a-pattern-or-not-set-2/)
[检查字符串是否遵循模式定义的字符顺序|第 3 集](https://www.geeksforgeeks.org/check-if-string-follows-order-of-characters-defined-by-a-pattern-or-not-set-3/)
本文由 **Aditya Goel** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。