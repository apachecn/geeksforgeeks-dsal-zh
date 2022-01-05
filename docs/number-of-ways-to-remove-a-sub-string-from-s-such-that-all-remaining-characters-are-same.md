# 从 S 中移除子字符串以使所有剩余字符相同的方法数量

> 原文:[https://www . geeksforgeeks . org/从 s 中移除子字符串的方法数，以便所有剩余字符都相同/](https://www.geeksforgeeks.org/number-of-ways-to-remove-a-sub-string-from-s-such-that-all-remaining-characters-are-same/)

给定一个仅由小写英文字母组成的字符串 **str** ，任务是计算从 **str** 中精确删除一个子字符串的方法数量，以便所有剩余的字符都相同。
**注意:**在**字符串**中至少有两个不同的字符，我们也可以去掉整个字符串。
**举例:**

> **输入:** str = "abaa"
> **输出:** 6
> 我们可以移除以下子字符串以满足给定条件:
> str[0:1]、str[0:2]、str[0:3]、str[1:1]、str[1:2]和 str[1:3]
> **输入:**str = " geeksforgeks "
> **输出:** 3
> 我们移除完整字符串。
> 除了第一个，我们全部移除。
> 我们移除除最后一个
> 以外的所有

**进场:**

*   将字符串中相同字符的**前缀**和**后缀**的**长度**存储在变量 **count_left** 和 **count_right** 中。
*   很明显，这个前缀和后缀不会重叠，因为**字符串**中至少有两个不同的字符。
*   现在有两种情况:
    *   当**str[0]= str[n–1]**时，前缀的每个字符(包括前缀结束后的字符)将作为子字符串的起始字符，后缀的每个字符(包括后缀开始前的字符)将作为子字符串的结束字符。因此，总的有效子串将是**计数=(计数 _ 左+ 1) *(计数 _ 右+ 1)** 。
    *   当 **str[0]！= str[n–1]**。然后**计数=计数 _ 左+计数 _ 右+ 1** 。

以下是上述方法的实现:

## C++

```
// C++ program to count number of ways of
// removing a substring from a string such
// that all remaining characters are equal
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of ways
// of removing a sub-string from s such
// that all the remaining characters are same
int no_of_ways(string s)
{
    int n = s.length();

    // To store the count of prefix and suffix
    int count_left = 0, count_right = 0;

    // Loop to count prefix
    for (int i = 0; i < n; ++i) {
        if (s[i] == s[0]) {
            ++count_left;
        }
        else
            break;
    }

    // Loop to count suffix
    for (int i = n - 1; i >= 0; --i) {
        if (s[i] == s[n - 1]) {
            ++count_right;
        }
        else
            break;
    }

    // First and last characters of the
    // string are same
    if (s[0] == s[n - 1])
        return ((count_left + 1) * (count_right + 1));

    // Otherwise
    else
        return (count_left + count_right + 1);
}

// Driver function
int main()
{
    string s = "geeksforgeeks";
    cout << no_of_ways(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways of
// removing a substring from a string such
// that all remaining characters are equal
import java.util.*;

class solution
{

// Function to return the number of ways
// of removing a sub-string from s such
// that all the remaining characters are same
static int no_of_ways(String s)
{
    int n = s.length();

    // To store the count of prefix and suffix
    int count_left = 0, count_right = 0;

    // Loop to count prefix
    for (int i = 0; i < n; ++i) {
        if (s.charAt(i) == s.charAt(0)) {
            ++count_left;
        }
        else
            break;
    }

    // Loop to count suffix
    for (int i = n - 1; i >= 0; --i) {
        if (s.charAt(i) == s.charAt(n - 1)) {
            ++count_right;
        }
        else
            break;
    }

    // First and last characters of the
    // string are same
    if (s.charAt(0) == s.charAt(n - 1))
        return ((count_left + 1) * (count_right + 1));

    // Otherwise
    else
        return (count_left + count_right + 1);
}

// Driver function
public static void main(String args[])
{
    String s = "geeksforgeeks";
    System.out.println(no_of_ways(s));

}
}
```

## 蟒蛇 3

```
# Python 3 program to count number of
# ways of removing a substring from a
# string such that all remaining
# characters are equal

# Function to return the number of
# ways of removing a sub-string from
# s such that all the remaining
# characters are same
def no_of_ways(s):
    n = len(s)

    # To store the count of
    # prefix and suffix
    count_left = 0
    count_right = 0

    # Loop to count prefix
    for i in range(0, n, 1):
        if (s[i] == s[0]):
            count_left += 1
        else:
            break

    # Loop to count suffix
    i = n - 1
    while(i >= 0):
        if (s[i] == s[n - 1]):
            count_right += 1
        else:
            break

        i -= 1

    # First and last characters of
    # the string are same
    if (s[0] == s[n - 1]):
        return ((count_left + 1) *
                (count_right + 1))

    # Otherwise
    else:
        return (count_left + count_right + 1)

# Driver Code
if __name__ == '__main__':
    s = "geeksforgeeks"
    print(no_of_ways(s))

# This code is contributed by
# Sahil_shelengia
```

## C#

```
// C# program to count number of ways of
// removing a substring from a string such
// that all remaining characters are equal
using System;

class GFG
{

// Function to return the number of ways
// of removing a sub-string from s such
// that all the remaining characters are same
static int no_of_ways(string s)
{
    int n = s.Length;

    // To store the count of prefix and suffix
    int count_left = 0, count_right = 0;

    // Loop to count prefix
    for (int i = 0; i < n; ++i)
    {
        if (s[i] == s[0])
        {
            ++count_left;
        }
        else
            break;
    }

    // Loop to count suffix
    for (int i = n - 1; i >= 0; --i)
    {
        if (s[i] == s[n - 1])
        {
            ++count_right;
        }
        else
            break;
    }

    // First and last characters of the
    // string are same
    if (s[0] == s[n - 1])
        return ((count_left + 1) *
                (count_right + 1));

    // Otherwise
    else
        return (count_left + count_right + 1);
}

// Driver Code
public static void Main()
{
    string s = "geeksforgeeks";
    Console.WriteLine(no_of_ways(s));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of ways of
// removing a substring from a string such
// that all remaining characters are equal

// Function to return the number of ways
// of removing a sub-string from $s such
// that all the remaining characters are same
function no_of_ways($s)
{
    $n = strlen($s);

    // To store the count of prefix and suffix
    $count_left = 0;
    $count_right = 0;

    // Loop to count prefix
    for ($i = 0; $i < $n; ++$i)
    {
        if ($s[$i] == $s[0])
        {
            ++$count_left;
        }
        else
            break;
    }

    // Loop to count suffix
    for ($i = $n - 1; $i >= 0; --$i)
    {
        if ($s[$i] == $s[$n - 1])
        {
            ++$count_right;
        }
        else
            break;
    }

    // First and last characters of the
    // string are same
    if ($s[0] == $s[$n - 1])
        return (($count_left + 1) *
                ($count_right + 1));

    // Otherwise
    else
        return ($count_left + $count_right + 1);
}

// Driver Code
$s = "geeksforgeeks";
echo no_of_ways($s);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

    // JavaScript program to count number of ways of
    // removing a substring from a string such
    // that all remaining characters are equal

    // Function to return the number of ways
    // of removing a sub-string from s such
    // that all the remaining characters are same
    function no_of_ways(s)
    {
        let n = s.length;

        // To store the count of prefix and suffix
        let count_left = 0, count_right = 0;

        // Loop to count prefix
        for (let i = 0; i < n; ++i)
        {
            if (s[i] == s[0])
            {
                ++count_left;
            }
            else
                break;
        }

        // Loop to count suffix
        for (let i = n - 1; i >= 0; --i)
        {
            if (s[i] == s[n - 1])
            {
                ++count_right;
            }
            else
                break;
        }

        // First and last characters of the
        // string are same
        if (s[0] == s[n - 1])
            return ((count_left + 1) *
                    (count_right + 1));

        // Otherwise
        else
            return (count_left + count_right + 1);
    }

    let s = "geeksforgeeks";
    document.write(no_of_ways(s));

</script>
```

**Output:** 

```
3
```