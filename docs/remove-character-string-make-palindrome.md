# 从字符串中删除一个字符，使其成为回文

> 原文:[https://www . geesforgeks . org/remove-character-string-make-回文/](https://www.geeksforgeeks.org/remove-character-string-make-palindrome/)

给定一个字符串，我们需要检查在从这个字符串中删除一个字符后，是否有可能使这个字符串成为回文。

**示例:**

```
Input  : str = “abcba”
Output : Yes
we can remove character ‘c’ to make string palindrome

Input  : str = “abcbea”
Output : Yes
we can remove character ‘e’ to make string palindrome

Input : str = “abecbea”
It is not possible to make this string palindrome 
just by removing one character 
```

我们可以通过寻找错配的位置来解决这个问题。我们通过在两端保持两个指针来开始循环字符串，这两个指针在每次迭代后向中间位置移动，当我们发现不匹配时，这个迭代将停止，因为它只允许删除一个字符，我们在这里有两个选择，

不匹配时，删除左指针指向的字符或右指针指向的字符。
我们将检查这两种情况，请记住，由于我们已经从两侧遍历了相同数量的步骤，这个中间字符串也应该是删除一个字符后的回文，因此我们检查两个子字符串，一个通过删除左字符，一个通过删除右字符，如果其中一个是回文，那么我们可以通过删除相应的字符来制作完整的字符串回文，如果两个子字符串都不是回文，那么在给定的约束下不可能使完整的字符串成为回文。

## C++

```
// C/C++ program to check whether it is possible to make
// string palindrome by removing one character
#include <bits/stdc++.h>
using namespace std;

// Utility method to check if substring from low to high is
// palindrome or not.
bool isPalindrome(string::iterator low, string::iterator high)
{
    while (low < high)
    {
       if (*low != *high)
          return false;
       low++;
       high--;
    }
    return true;
}

// This method returns -1 if it is not possible to make string
// a palindrome. It returns -2 if string is already a palindrome.
// Otherwise it returns index of character whose removal can
// make the whole string palindrome.
int possiblePalinByRemovingOneChar(string str)
{
    //  Initialize low and right by both the ends of the string
    int low = 0, high = str.length() - 1;

    //  loop until low and high cross each other
    while (low < high)
    {
        // If both characters are equal then move both pointer
        // towards end
        if (str[low] == str[high])
        {
            low++;
            high--;
        }
        else
        {
            /*  If removing str[low] makes the whole string palindrome.
                We basically check if substring str[low+1..high] is
                palindrome or not. */
            if (isPalindrome(str.begin() + low + 1, str.begin() + high))
                return low;

            /*  If removing str[high] makes the whole string palindrome
                We basically check if substring str[low+1..high] is
                palindrome or not. */
            if (isPalindrome(str.begin() + low, str.begin() + high - 1))
                return high;

            return -1;
        }
    }

    //  We reach here when complete string will be palindrome
    //  if complete string is palindrome then return mid character
    return -2;
}

// Driver code to test above methods
int main()
{
    string str = "abecbea";
    int idx = possiblePalinByRemovingOneChar(str);
    if (idx == -1)
        cout << "Not Possible \n";
    else if (idx == -2)
        cout << "Possible without removing any character";
    else
        cout << "Possible by removing character"
             << " at index " << idx << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether
// it is possible to make string
// palindrome by removing one character
import java.util.*;

class GFG
{

    // Utility method to check if
    // substring from low to high is
    // palindrome or not.
    static boolean isPalindrome(String str,
                    int low, int high)
    {
        while (low < high)
        {
            if (str.charAt(low) != str.charAt(high))
                return false;
            low++;
            high--;
        }
        return true;
    }

    // This method returns -1 if it is
    // not possible to make string a palindrome.
    // It returns -2 if string is already
    // a palindrome. Otherwise it returns
    // index of character whose removal can
    // make the whole string palindrome.
    static int possiblePalinByRemovingOneChar(String str)
    {

        // Initialize low and right
        // by both the ends of the string
        int low = 0, high = str.length() - 1;

        // loop until low and
        // high cross each other
        while (low < high)
        {

            // If both characters are equal then
            // move both pointer towards end
            if (str.charAt(low) == str.charAt(high))
            {
                low++;
                high--;
            }
            else
            {

                /*
                * If removing str[low] makes the
                * whole string palindrome. We basically
                * check if substring str[low+1..high]
                * is palindrome or not.
                */
                if (isPalindrome(str, low + 1, high))
                    return low;

                /*
                * If removing str[high] makes the whole string
                * palindrome. We basically check if substring
                * str[low+1..high] is palindrome or not.
                */
                if (isPalindrome(str, low, high - 1))
                    return high;
                return -1;
            }
        }

        // We reach here when complete string
        // will be palindrome if complete string
        // is palindrome then return mid character
        return -2;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "abecbea";
        int idx = possiblePalinByRemovingOneChar(str);

        if (idx == -1)
            System.out.println("Not Possible");
        else if (idx == -2)
            System.out.println("Possible without " +
                        "removing any character");
        else
            System.out.println("Possible by removing" +
                            " character at index " + idx);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python program to check whether it is possible to make
# string palindrome by removing one character

# Utility method to check if substring from
# low to high is palindrome or not.
def isPalindrome(string: str, low: int, high: int) -> bool:
    while low < high:
        if string[low] != string[high]:
            return False
        low += 1
        high -= 1
    return True

# This method returns -1 if it
# is not possible to make string
# a palindrome. It returns -2 if
# string is already a palindrome.
# Otherwise it returns index of
# character whose removal can
# make the whole string palindrome.
def possiblepalinByRemovingOneChar(string: str) -> int:

    # Initialize low and right by
    # both the ends of the string
    low = 0
    high = len(string) - 1

    # loop until low and high cross each other
    while low < high:

        # If both characters are equal then
        # move both pointer towards end
        if string[low] == string[high]:
            low += 1
            high -= 1
        else:

            # If removing str[low] makes the whole string palindrome.
            # We basically check if substring str[low+1..high] is
            # palindrome or not.
            if isPalindrome(string, low + 1, high):
                return low

            # If removing str[high] makes the whole string palindrome
            # We basically check if substring str[low+1..high] is
            # palindrome or not
            if isPalindrome(string, low, high - 1):
                return high
            return -1

    # We reach here when complete string will be palindrome
    # if complete string is palindrome then return mid character
    return -2

# Driver Code
if __name__ == "__main__":

    string = "abecbea"
    idx = possiblepalinByRemovingOneChar(string)

    if idx == -1:
        print("Not possible")
    elif idx == -2:
        print("Possible without removing any character")
    else:
        print("Possible by removing character at index", idx)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to check whether
// it is possible to make string
// palindrome by removing one character
using System;
class GFG
{

    // Utility method to check if
    // substring from low to high is
    // palindrome or not.
    static bool isPalindrome(string str, int low, int high)
    {
        while (low < high)
        {
            if (str[low] != str[high])
                return false;
            low++;
            high--;
        }
        return true;
    }

    // This method returns -1 if it is
    // not possible to make string a palindrome.
    // It returns -2 if string is already
    // a palindrome. Otherwise it returns
    // index of character whose removal can
    // make the whole string palindrome.
    static int possiblePalinByRemovingOneChar(string str)
    {

        // Initialize low and right
        // by both the ends of the string
        int low = 0, high = str.Length - 1;

        // loop until low and
        // high cross each other
        while (low < high)
        {

            // If both characters are equal then
            // move both pointer towards end
            if (str[low] == str[high])
            {
                low++;
                high--;
            }
            else
            {

                /*
                * If removing str[low] makes the
                * whole string palindrome. We basically
                * check if substring str[low+1..high]
                * is palindrome or not.
                */
                if (isPalindrome(str, low + 1, high))
                    return low;

                /*
                * If removing str[high] makes the whole string
                * palindrome. We basically check if substring
                * str[low+1..high] is palindrome or not.
                */
                if (isPalindrome(str, low, high - 1))
                    return high;
                return -1;
            }
        }

        // We reach here when complete string
        // will be palindrome if complete string
        // is palindrome then return mid character
        return -2;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        string str = "abecbea";
        int idx = possiblePalinByRemovingOneChar(str);

        if (idx == -1)
            Console.Write("Not Possible");
        else if (idx == -2)
            Console.Write("Possible without " +
                        "removing any character");
        else
            Console.Write("Possible by removing" +
                            " character at index " + idx);
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program to check whether
// it is possible to make string
// palindrome by removing one character
// Utility method to check if
// substring from low to high is
// palindrome or not.
function isPalindrome(str, low, high)
    {
        while (low < high)
        {
            if (str.charAt(low) != str.charAt(high))
                return false;
            low++;
            high--;
        }
        return true;
    }

    // This method returns -1 if it is
    // not possible to make string a palindrome.
    // It returns -2 if string is already
    // a palindrome. Otherwise it returns
    // index of character whose removal can
    // make the whole string palindrome.
    function possiblePalinByRemovingOneChar(str)
    {

        // Initialize low and right
        // by both the ends of the string
        var low = 0, high = str.length - 1;

        // loop until low and
        // high cross each other
        while (low < high)
        {

            // If both characters are equal then
            // move both pointer towards end
            if (str.charAt(low) == str.charAt(high))
            {
                low++;
                high--;
            }
            else
            {

                /*
                * If removing str[low] makes the
                * whole string palindrome. We basically
                * check if substring str[low+1..high]
                * is palindrome or not.
                */
                if (isPalindrome(str, low + 1, high))
                    return low;

                /*
                * If removing str[high] makes the whole string
                * palindrome. We basically check if substring
                * str[low+1..high] is palindrome or not.
                */
                if (isPalindrome(str, low, high - 1))
                    return high;
                return -1;
            }
        }

        // We reach here when complete string
        // will be palindrome if complete string
        // is palindrome then return mid character
        return -2;
    }

    // Driver Code
        var str = "abecbea";
        var idx = possiblePalinByRemovingOneChar(str);

        if (idx == -1)
            document.write("Not Possible");
        else if (idx == -2)
            document.write("Possible without " +
                        "removing any character");
        else
            document.write("Possible by removing" +
                            " character at index " + idx);

// this code is contributed by shivanisinghss2110
</script>
```

**输出:**

```
Not Possible 
```

**时间复杂度:** O(N)

**空间复杂度:** O(1)

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。