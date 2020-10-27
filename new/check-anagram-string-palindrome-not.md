# 检查字符串的任何字谜是否回文

我们给出了一个字谜字符串，我们必须检查它是否可以做成回文。
**示例：**

```
Input : geeksforgeeks 
Output : No
There is no palindrome anagram of 
given string

Input  : geeksgeeks
Output : Yes
There are palindrome anagrams of
given string. For example kgeesseegk

```

此问题基本上与[相同。检查给定字符串的字符是否可以重新排列以形成回文](https://www.geeksforgeeks.org/check-characters-given-string-can-rearranged-form-palindrome/)。 我们可以使用 count 数组在 O（n）时间内完成此操作。 以下是详细步骤。
1）创建一个字母大小的计数数组，通常为 256。将计数数组的所有值初始化为 0。
2）遍历给定的字符串并递增每个字符的计数。
3）遍历计数数组，如果计数数组有多个奇数，则返回 false。 否则，返回 true。

## C++

```cpp

#include <iostream>
using namespace std;
#define NO_OF_CHARS 256

/* function to check whether characters of a string
   can form a palindrome */
bool canFormPalindrome(string str)
{
    // Create a count array and initialize all
    // values as 0
    int count[NO_OF_CHARS] = { 0 };

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    for (int i = 0; str[i]; i++)
        count[str[i]]++;

    // Count odd occurring characters
    int odd = 0;
    for (int i = 0; i < NO_OF_CHARS; i++) {
        if (count[i] & 1)
            odd++;

        if (odd > 1)
            return false;
    }

    // Return true if odd count is 0 or 1,
    return true;
}

/* Driver program to test to print printDups*/
int main()
{
    canFormPalindrome("geeksforgeeks") ? cout << "Yes\n" : cout << "No\n";
    canFormPalindrome("geeksogeeks") ? cout << "Yes\n" : cout << "No\n";
    return 0;
}

```

## Java

```java

// Java program to Check if any anagram
// of a string is palindrome or not
public class GFG {
    static final int NO_OF_CHARS = 256;

    /* function to check whether characters of
      a string can form a palindrome */
    static boolean canFormPalindrome(String str)
    {
        // Create a count array and initialize
        // all values as 0
        int[] count = new int[NO_OF_CHARS];

        // For each character in input strings,
        // increment count in the corresponding
        // count array
        for (int i = 0; i < str.length(); i++)
            count[str.charAt(i)]++;

        // Count odd occurring characters
        int odd = 0;
        for (int i = 0; i < NO_OF_CHARS; i++) {
            if ((count[i] & 1) != 0)
                odd++;

            if (odd > 1)
                return false;
        }

        // Return true if odd count is 0 or 1,
        return true;
    }

    /* Driver program to test to print printDups*/
    public static void main(String args[])
    {
        System.out.println(canFormPalindrome("geeksforgeeks")
                               ? "Yes"
                               : "No");
        System.out.println(canFormPalindrome("geeksogeeks")
                               ? "Yes"
                               : "No");
    }
}
// This code is contributed by Sumit Ghosh

```

## 蟒蛇

```

NO_OF_CHARS = 256

""" function to check whether characters of a string
   can form a palindrome """
def canFormPalindrome(string):

    # Create a count array and initialize all 
    # values as 0
    count = [0 for i in range(NO_OF_CHARS)]

    # For each character in input strings,
    # increment count in the corresponding
    # count array
    for i in string:
        count[ord(i)] += 1

    # Count odd occurring characters
    odd = 0
    for i in range(NO_OF_CHARS):
        if (count[i] & 1):
            odd += 1

        if (odd > 1):
            return False

    # Return true if odd count is 0 or 1, 
    return True

# Driver program to test to print printDups
if(canFormPalindrome("geeksforgeeks")):
    print "Yes"
else:
    print "No"
if(canFormPalindrome("geeksogeeks")):
    print "Yes"
else:
    print "NO"

# This code is contributed by Sachin Bisht

```

## C#

```cs

// C# program to Check if any anagram
// of a string is palindrome or not
using System;

public class GFG {

    static int NO_OF_CHARS = 256;

    /* function to check whether 
    characters of a string can form
    a palindrome */
    static bool canFormPalindrome(string str)
    {

        // Create a count array and
        // initialize all values as 0
        int[] count = new int[NO_OF_CHARS];

        // For each character in input
        // strings, increment count in
        // the corresponding count array
        for (int i = 0; i < str.Length; i++)
            count[str[i]]++;

        // Count odd occurring characters
        int odd = 0;
        for (int i = 0; i < NO_OF_CHARS; i++) {
            if ((count[i] & 1) != 0)
                odd++;

            if (odd > 1)
                return false;
        }

        // Return true if odd count
        // is 0 or 1,
        return true;
    }

    // Driver program
    public static void Main()
    {
        Console.WriteLine(
            canFormPalindrome("geeksforgeeks")
                              ? "Yes" : "No");

        Console.WriteLine(
            canFormPalindrome("geeksogeeks")
                              ? "Yes" : "No");
    }
}

// This code is contributed by vt_m.

```

**输出：**

```
No
Yes

```

本文由 **Rishabh Jain** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

