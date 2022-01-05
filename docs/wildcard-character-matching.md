# 字符串匹配，其中一个字符串包含通配符

> 原文:[https://www.geeksforgeeks.org/wildcard-character-matching/](https://www.geeksforgeeks.org/wildcard-character-matching/)

给定两个字符串，其中第一个字符串可能包含通配符，第二个字符串是普通字符串。编写一个函数，如果两个字符串匹配，则返回 true。以下是第一个字符串中允许的通配符。

```
* --> Matches with 0 or more instances of any character or set of characters.
? --> Matches with any one character.
```

比如“g*ks”匹配“极客”匹配。又串“葛？ks*”与“geeksforgeeks”匹配(注意第一个字符串末尾的“*”)。但是“g*k”与“gee”不匹配，因为字符“k”不在第二个字符串中。

## C++

```
// A C program to match wild card characters
#include <stdio.h>
#include <stdbool.h>

// The main function that checks if two given strings
// match. The first string may contain wildcard characters
bool match(char *first, char * second)
{
    // If we reach at the end of both strings, we are done
    if (*first == '\0' && *second == '\0')
        return true;

    // Make sure that the characters after '*' are present
    // in second string. This function assumes that the first
    // string will not contain two consecutive '*'
    if (*first == '*' && *(first+1) != '\0' && *second == '\0')
        return false;

    // If the first string contains '?', or current characters
    // of both strings match
    if (*first == '?' || *first == *second)
        return match(first+1, second+1);

    // If there is *, then there are two possibilities
    // a) We consider current character of second string
    // b) We ignore current character of second string.
    if (*first == '*')
        return match(first+1, second) || match(first, second+1);
    return false;
}

// A function to run test cases
void test(char *first, char *second)
{  match(first, second)? puts("Yes"): puts("No"); }

// Driver program to test above functions
int main()
{
    test("g*ks", "geeks"); // Yes
    test("ge?ks*", "geeksforgeeks"); // Yes
    test("g*k", "gee");  // No because 'k' is not in second
    test("*pqrs", "pqrst"); // No because 't' is not in first
    test("abc*bcd", "abcdhghgbcd"); // Yes
    test("abc*c?d", "abcd"); // No because second must have 2
                             // instances of 'c'
    test("*c*d", "abcd"); // Yes
    test("*?c*d", "abcd"); // Yes
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to match wild card characters
class GFG
{

// The main function that checks if
// two given strings match. The first string
// may contain wildcard characters
static boolean match(String first, String second)
{

    // If we reach at the end of both strings,
    // we are done
    if (first.length() == 0 && second.length() == 0)
        return true;

    // Make sure that the characters after '*'
    // are present in second string.
    // This function assumes that the first
    // string will not contain two consecutive '*'
    if (first.length() > 1 && first.charAt(0) == '*' &&
                              second.length() == 0)
        return false;

    // If the first string contains '?',
    // or current characters of both strings match
    if ((first.length() > 1 && first.charAt(0) == '?') ||
        (first.length() != 0 && second.length() != 0 &&
         first.charAt(0) == second.charAt(0)))
        return match(first.substring(1),
                     second.substring(1));

    // If there is *, then there are two possibilities
    // a) We consider current character of second string
    // b) We ignore current character of second string.
    if (first.length() > 0 && first.charAt(0) == '*')
        return match(first.substring(1), second) ||
               match(first, second.substring(1));
    return false;
}

// A function to run test cases
static void test(String first, String second)
{
    if (match(first, second))
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main(String[] args)
{
    test("g*ks", "geeks"); // Yes
    test("ge?ks*", "geeksforgeeks"); // Yes
    test("g*k", "gee"); // No because 'k' is not in second
    test("*pqrs", "pqrst"); // No because 't' is not in first
    test("abc*bcd", "abcdhghgbcd"); // Yes
    test("abc*c?d", "abcd"); // No because second must have 2
                            // instances of 'c'
    test("*c*d", "abcd"); // Yes
    test("*?c*d", "abcd"); // Yes
}
}

// This code is contributed by
// sanjeev2552
```

## 计算机编程语言

```
# Python program to match wild card characters

# The main function that checks if two given strings match.
# The first string may contain wildcard characters
def match(first, second):

    # If we reach at the end of both strings, we are done
    if len(first) == 0 and len(second) == 0:
        return True

    # Make sure that the characters after '*' are present
    # in second string. This function assumes that the first
    # string will not contain two consecutive '*'
    if len(first) > 1 and first[0] == '*' and  len(second) == 0:
        return False

    # If the first string contains '?', or current characters
    # of both strings match
    if (len(first) > 1 and first[0] == '?') or (len(first) != 0
        and len(second) !=0 and first[0] == second[0]):
        return match(first[1:],second[1:]);

    # If there is *, then there are two possibilities
    # a) We consider current character of second string
    # b) We ignore current character of second string.
    if len(first) !=0 and first[0] == '*':
        return match(first[1:],second) or match(first,second[1:])

    return False

# A function to run test cases
def test(first, second):
    if match(first, second):
        print "Yes"
    else:
        print "No"

# Driver program
test("g*ks", "geeks") # Yes
test("ge?ks*", "geeksforgeeks") # Yes
test("g*k", "gee") # No because 'k' is not in second
test("*pqrs", "pqrst") # No because 't' is not in first
test("abc*bcd", "abcdhghgbcd") # Yes
test("abc*c?d", "abcd") # No because second must have 2 instances of 'c'
test("*c*d", "abcd") # Yes
test("*?c*d", "abcd") # Yes

# This code is contributed by BHAVYA JAIN and ROHIT SIKKA
```

## C#

```
// C# program to match wild card characters
using System;

class GFG
{

// The main function that checks if
// two given strings match. The first string
// may contain wildcard characters
static bool match(String first, String second)
{

    // If we reach at the end of both strings,
    // we are done
    if (first.Length == 0 && second.Length == 0)
        return true;

    // Make sure that the characters after '*'
    // are present in second string.
    // This function assumes that the first
    // string will not contain two consecutive '*'
    if (first.Length > 1 && first[0] == '*' &&
                              second.Length == 0)
        return false;

    // If the first string contains '?',
    // or current characters of both strings match
    if ((first.Length > 1 && first[0] == '?') ||
        (first.Length != 0 && second.Length != 0 &&
         first[0] == second[0]))
        return match(first.Substring(1),
                     second.Substring(1));

    // If there is *, then there are two possibilities
    // a) We consider current character of second string
    // b) We ignore current character of second string.
    if (first.Length > 0 && first[0] == '*')
        return match(first.Substring(1), second) ||
               match(first, second.Substring(1));
    return false;
}

// A function to run test cases
static void test(String first, String second)
{
    if (match(first, second))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main(String[] args)
{
    test("g*ks", "geeks"); // Yes
    test("ge?ks*", "geeksforgeeks"); // Yes
    test("g*k", "gee"); // No because 'k' is not in second
    test("*pqrs", "pqrst"); // No because 't' is not in first
    test("abc*bcd", "abcdhghgbcd"); // Yes
    test("abc*c?d", "abcd"); // No because second must have 2
                            // instances of 'c'
    test("*c*d", "abcd"); // Yes
    test("*?c*d", "abcd"); // Yes
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to match wild card characters

// The main function that checks if
// two given strings match. The first string
// may contain wildcard characters
function match(first, second)
{

    // If we reach at the end of both strings,
    // we are done
    if (first.length == 0 && second.length == 0)
        return true;

    // Make sure that the characters after '*'
    // are present in second string.
    // This function assumes that the first
    // string will not contain two consecutive '*'
    if (first.length > 1 && first[0] == '*' &&
        second.length == 0)
        return false;

    // If the first string contains '?',
    // or current characters of both strings match
    if ((first.length > 1 && first[0] == '?') ||
        (first.length != 0 && second.length != 0 &&
         first[0] == second[0]))
        return match(first.substring(1),
                     second.substring(1));

    // If there is *, then there are two possibilities
    // a) We consider current character of second string
    // b) We ignore current character of second string.
    if (first.length > 0 && first[0] == '*')
        return match(first.substring(1), second) ||
               match(first, second.substring(1));

    return false;
}

// A function to run test cases
function test(first, second)
{
    if (match(first, second))
       document.write("Yes" + "<br>");
    else
       document.write("No" + "<br>");
}

// Driver code
test("g*ks", "geeks"); // Yes
test("ge?ks*", "geeksforgeeks"); // Yes
test("g*k", "gee"); // No because 'k' is not in second
test("*pqrs", "pqrst"); // No because 't' is not in first
test("abc*bcd", "abcdhghgbcd"); // Yes
test("abc*c?d", "abcd"); // No because second must have 2
                        // instances of 'c'
test("*c*d", "abcd"); // Yes
test("*?c*d", "abcd"); // Yes

// This code is contributed by SoumikMondal

</script>
```

**输出:**

```
Yes
Yes
No
No
Yes
No
Yes
Yes

```

**练习**
**1)** 在上面的解决方案中，第一个字符串的所有非通配符必须有第二个字符串，第二个字符串的所有字符必须与第一个字符串的普通字符或通配符匹配。扩展上述解决方案，使其像其他[模式搜索解决方案](https://www.geeksforgeeks.org/tag/pattern-searching/)一样工作，其中第一个字符串是模式，第二个字符串是文本，我们应该以秒为单位打印第一个字符串的所有出现。
**2)** 写一个模式搜索函数哪里有“？”的意思相同，但“*”表示该字符在“*”之前出现了 0 次或更多次。例如，如果第一个字符串是' a*b '，则它与' aaab '匹配，但与' abb '不匹配。
本文由 [Vishal Chaudhary](https://www.facebook.com/vishal.cs.bits) 编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。