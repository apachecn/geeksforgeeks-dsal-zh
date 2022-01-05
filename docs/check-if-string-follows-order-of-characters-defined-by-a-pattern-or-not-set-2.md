# 检查字符串是否遵循模式定义的字符顺序|设置 2

> 原文:[https://www . geesforgeks . org/check-if-string-follow-order-of-characters-by-pattern-or-not-set-2/](https://www.geeksforgeeks.org/check-if-string-follows-order-of-characters-defined-by-a-pattern-or-not-set-2/)

给定输入字符串和模式，检查输入字符串中的字符是否遵循由模式中的字符确定的相同顺序。假设模式中没有任何重复的字符。
同一个问题的另一个解决方案发布在这里[。
**示例:**](https://www.geeksforgeeks.org/check-string-follows-order-characters-defined-pattern-not/) 

```
Input: string = "engineers rock", pattern = "er";
Output: true
All 'e' in the input string are before all 'r'.

Input: string = "engineers rock", pattern = "egr";
Output: false
There are two 'e' after 'g' in the input string.

Input: string = "engineers rock", pattern = "gsr";
Output: false
There are one 'r' before 's' in the input string.
```

这里的想法是将给定的字符串简化为给定的模式。对于模式中给出的字符，我们只保留字符串中对应的字符。在新字符串中，我们删除了连续重复的字符。修改后的字符串应该等于给定的模式。最后，我们将修改后的字符串与给定的模式进行比较，并相应地返回 true 或 false。
图解:

```
str = "bfbaeadeacc", pat[] = "bac"

1) Remove extra characters from str (characters
  that are not present in pat[]
str = "bbaaacc"   [f, e and d are removed]

3) Removed consecutive repeating occurrences of 
   characters
str = "bac"   

4) Since str is same as pat[], we return true
```

下面是上述步骤的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if characters of a string follow
// pattern defined by given pattern.
import java.util.*;

public class OrderOfCharactersForPattern
{
    public static boolean followsPattern(String str, String pattern)
    {
        // Insert all characters of pattern in a hash set,
        Set<Character> patternSet = neHashSet<>();
        for (int i=0; i<pattern.length(); i++)
            patternSet.add(pattern.charAt(i));

        // Build modified string (string with characters only from
        // pattern are taken)
        StringBuilder modifiedString = new StringBuilder(str);
        for (int i=str.length()-1; i>=0; i--)
            if (!patternSet.contains(modifiedString.charAt(i)))
                modifiedString.deleteCharAt(i);

        // Remove more than one consecutive occurrences of pattern
        // characters from modified string.
        for (int i=modifiedString.length()-1; i>0; i--)
            if (modifiedString.charAt(i) == modifiedString.charAt(i-1))
                modifiedString.deleteCharAt(i);

        // After above modifications, the length of modified string
        // must be same as pattern length
        if (pattern.length() != modifiedString.length())
            return false;

        // And pattern characters must also be same as modified string
        // characters
        for (int i=0; i<pattern.length(); i++)
            if (pattern.charAt(i) != modifiedString.charAt(i))
                return false;

        return true;
    }

    // Driver program
    int main()
    {
        String str = "engineers rock";
        String pattern = "er";
        System.out.println("Expected: true, Actual: " +
                           followsPattern(str, pattern));

        str = "engineers rock";
        pattern = "egr";
        System.out.println("Expected: false, Actual: " +
                          followsPattern(str, pattern));

        str = "engineers rock";
        pattern = "gsr";
        System.out.println("Expected: false, Actual: " +
                           followsPattern(str, pattern));

        str = "engineers rock";
        pattern = "eger";
        System.out.println("Expected: true, Actual: " +
                           followsPattern(str, pattern));

        return 0;
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if characters of
# a string follow pattern defined by given pattern.
def followsPattern(string, pattern):

    # Insert all characters of pattern in a hash set,
    patternSet = set()

    for i in range(len(pattern)):
        patternSet.add(pattern[i])

    # Build modified string (string with characters
    # only from pattern are taken)
    modifiedString = string
    for i in range(len(string) - 1, -1, -1):
        if not modifiedString[i] in patternSet:
            modifiedString = modifiedString[:i] + \
                             modifiedString[i + 1:]

    # Remove more than one consecutive occurrences
    # of pattern characters from modified string.
    for i in range(len(modifiedString) - 1, 0, -1):
        if modifiedString[i] == modifiedString[i - 1]:
            modifiedString = modifiedString[:i] + \
                             modifiedString[i + 1:]

    # After above modifications, the length of
    # modified string must be same as pattern length
    if len(pattern) != len(modifiedString):
        return False

    # And pattern characters must also be same
    # as modified string characters
    for i in range(len(pattern)):
        if pattern[i] != modifiedString[i]:
            return False
    return True

# Driver Code
if __name__ == "__main__":
    string = "engineers rock"
    pattern = "er"
    print("Expected: true, Actual:",
           followsPattern(string, pattern))

    string = "engineers rock"
    pattern = "egr"
    print("Expected: false, Actual:",
           followsPattern(string, pattern))

    string = "engineers rock"
    pattern = "gsr"
    print("Expected: false, Actual:",
           followsPattern(string, pattern))

    string = "engineers rock"
    pattern = "eger"
    print("Expected: true, Actual:",
           followsPattern(string, pattern))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to check if characters of a string follow
// pattern defined by given pattern.
using System;
using System.Collections.Generic;
using System.Text;

class GFG
{
    public static bool followsPattern(String str, String pattern)
    {
        // Insert all characters of pattern in a hash set,
        HashSet<char> patternSet = new HashSet<char>();
        for (int i = 0; i < pattern.Length; i++)
            patternSet.Add(pattern[i]);

        // Build modified string (string with characters
        // only from pattern are taken)
        StringBuilder modifiedString = new StringBuilder(str);
        for (int i = str.Length - 1; i >= 0; i--)
            if (!patternSet.Contains(modifiedString[i]))
                modifiedString.Remove(i, 1);

        // Remove more than one consecutive occurrences of pattern
        // characters from modified string.
        for (int i = modifiedString.Length - 1; i > 0; i--)
            if (modifiedString[i] == modifiedString[i - 1])
                modifiedString.Remove(i, 1);

        // After above modifications, the length of modified string
        // must be same as pattern length
        if (pattern.Length != modifiedString.Length)
            return false;

        // And pattern characters must also be same
        // as modified string characters
        for (int i = 0; i < pattern.Length; i++)
            if (pattern[i] != modifiedString[i])
                return false;

        return true;
    }

    // Driver program
    public static void Main(String[] args)
    {
        String str = "engineers rock";
        String pattern = "er";
        Console.WriteLine("Expected: true, Actual: " +
                        followsPattern(str, pattern));

        str = "engineers rock";
        pattern = "egr";
        Console.WriteLine("Expected: false, Actual: " +
                        followsPattern(str, pattern));

        str = "engineers rock";
        pattern = "gsr";
        Console.WriteLine("Expected: false, Actual: " +
                        followsPattern(str, pattern));

        str = "engineers rock";
        pattern = "eger";
        Console.WriteLine("Expected: true, Actual: " +
                        followsPattern(str, pattern));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to check if characters of a string follow
// pattern defined by given pattern.

function followsPattern(str, pattern)
{
    // Insert all characters of pattern in a hash set,
        let patternSet = new Set();
        for (let i=0; i<pattern.length; i++)
            patternSet.add(pattern[i]);

        // Build modified string (string with characters only from
        // pattern are taken)
        let modifiedString = (str).split("");
        for (let i=str.length-1; i>=0; i--)
            if (!patternSet.has(modifiedString[i]))
                modifiedString.splice(i,1);

        // Remove more than one consecutive occurrences of pattern
        // characters from modified string.
        for (let i=modifiedString.length-1; i>0; i--)
            if (modifiedString[i] == modifiedString[i-1])
                modifiedString.splice(i,1);

        // After above modifications, the length of modified string
        // must be same as pattern length
        if (pattern.length != modifiedString.length)
            return false;

        // And pattern characters must also be same as modified string
        // characters
        for (let i=0; i<pattern.length; i++)
            if (pattern[i] != modifiedString[i])
                return false;

        return true;
}

// Driver program
let str = "engineers rock";
let pattern = "er";
document.write("Expected: true, Actual: " +
                   followsPattern(str, pattern)+"<br>");

str = "engineers rock";
pattern = "egr";
document.write("Expected: false, Actual: " +
                   followsPattern(str, pattern)+"<br>");

str = "engineers rock";
pattern = "gsr";
document.write("Expected: false, Actual: " +
                   followsPattern(str, pattern)+"<br>");

str = "engineers rock";
pattern = "eger";
document.write("Expected: true, Actual: " +
                   followsPattern(str, pattern)+"<br>");

// This code is contributed by rag2127
</script>
```

**输出:**

```
Expected: true, Actual: true
Expected: false, Actual: false
Expected: false, Actual: false
Expected: true, Actual: true
```

**时间复杂度:**上述实现的时间复杂度实际上是 O(mn + n^2)，因为我们使用 deleteCharAt()来移除字符。我们可以优化上述解决方案，使其在线性时间内工作。我们可以创建一个空字符串，并只向其中添加所需的字符，而不是使用 deleteCharAr()。
StringBuilder 用于对输入字符串进行操作。这是因为 StringBuilder 是可变的，而 String 是不可变的对象。创建一个新的字符串需要 O(n)个空间，所以额外的空间就是 O(n)。
我们已经讨论了另外两种方法来解决这个问题。
[检查字符串是否遵循模式定义的字符顺序|集合 1](https://www.geeksforgeeks.org/check-string-follows-order-characters-defined-pattern-not/)
[检查字符串是否遵循模式定义的字符顺序|集合 3](https://www.geeksforgeeks.org/check-if-string-follows-order-of-characters-defined-by-a-pattern-or-not-set-3/)
本文由 **Lalit Ramesh Sirsikar** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。