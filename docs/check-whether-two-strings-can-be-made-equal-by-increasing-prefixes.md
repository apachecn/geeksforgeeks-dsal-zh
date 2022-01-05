# 通过增加前缀

检查两个字符串是否可以相等

> 原文:[https://www . geeksforgeeks . org/check-两个字符串是否可以通过增加前缀来相等/](https://www.geeksforgeeks.org/check-whether-two-strings-can-be-made-equal-by-increasing-prefixes/)

在这个问题上我们必须检查。是否可以通过增加第一个字符串前缀的字符的 ASCII 值来使两个字符串相等。我们可以多次增加不同的前缀。
字符串仅由小写字母组成，不包含任何特殊字符。
**例:**

> **输入:**字符串 1 =“abcd”，字符串 2 =“bcdd”
> **输出:**是
> **说明:**字符串 1 可以通过将 string_1 的前缀增加 1，即“abcD”、“ABC”的前缀字符串的 ASCII 值增加 1，转换为字符串 2。
> 这样我们就可以把“abcd”转换成“bcdd”
> **输入:**字符串 1 =“ABCD”，字符串 2 =“bcdg”
> **输出:**否

**解决方法**只有当第一个字符串的所有 ASCII 值都小于或等于第二个字符串，并且字符的 ASCII 值之差按降序排列时，才可以通过增加第一个字符串前缀的 ASCII 值来使两个字符串相等。
因此我们将检查两个字符串是否相等，如果相等，那么我们将检查第一个字符串的所有 ASCII 值是否小于或等于第二个字符串，我们将创建一个差异数组，该数组将存储两个字符串的字符差异，并检查差异数组是否按降序排列，如果所有条件都满足，我们将打印“是”或“否”。

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// check whether the first string can be
// converted to the second string
// by increasing the ASCII value of prefix
// string of first string
bool find(string s1, string s2)
{
    // length of two strings
    int len = s1.length(), len_1 = s2.length();

    // If lengths are not equal
    if (len != len_1)
        return false;

    // store the difference of ASCII values
    int d[len] = { 0 };

    // difference of first element
    d[0] = s2[0] - s1[0];

    // traverse through the string
    for (int i = 1; i < len; i++) {

        // the ASCII value of the second string
        // should be greater than or equal to first
        // string, if it is violated return false.
        if (s1[i] > s2[i])
            return false;

        else {

            // store the difference of ASCII values
            d[i] = s2[i] - s1[i];
        }
    }

    // the difference of ASCII values should be
    // in descending order
    for (int i = 0; i < len - 1; i++) {

        // if the difference array is not in descending order
        if (d[i] < d[i + 1])
            return false;
    }

    // if all the ASCII values of characters of first string
    // is less than or equal to the second string
    // and the difference array is in descending
    // order, return true
    return true;
}

// Driver code
int main()
{
    // create two strings
    string s1 = "abcd", s2 = "bcdd";

    // check whether the first string can be
    // converted to the second string
    if (find(s1, s2))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG {

    // check whether the first string can be
    // converted to the second string
    // by increasing the ASCII value of prefix
    // string of first string
    static boolean find(String s1, String s2)
    {
        // length of two strings
        int len = s1.length(), len_1 = s2.length();

        // If lengths are not equal
        if (len != len_1)
        {
            return false;
        }

        // store the difference of ASCII values
        int d[] = new int[len];

        // difference of first element
        d[0] = s2.charAt(0) - s1.charAt(0);

        // traverse through the string
        for (int i = 1; i < len; i++)
        {

            // the ASCII value of the second string
            // should be greater than or equal to first
            // string, if it is violated return false.
            if (s1.charAt(i) > s2.charAt(i))
            {
                return false;
            }
            else
            {

                // store the difference of ASCII values
                d[i] = s2.charAt(i) - s1.charAt(i);
            }
        }

        // the difference of ASCII values should be
        // in descending order
        for (int i = 0; i < len - 1; i++)
        {

            // if the difference array is not in descending order
            if (d[i] < d[i + 1])
            {
                return false;
            }
        }

        // if all the ASCII values of characters  
        // of first string is less than or equal to  
        // the second string and the difference array 
        // is in descending order, return true
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        // create two strings
        String s1 = "abcd", s2 = "bcdd";

        // check whether the first string can be
        // converted to the second string
        if (find(s1, s2))
        {
            System.out.println("Yes");
        } else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// check whether the first string can be
// converted to the second string
// by increasing the ASCII value of prefix
// string of first string
public static bool find(string s1, string s2)
{
    // length of two strings
    int len = s1.Length, len_1 = s2.Length;

    // If lengths are not equal
    if (len != len_1)
        return false;

    // store the difference of ASCII values
    int []d = new int [len];

    // difference of first element
    d[0] = s2[0] - s1[0];

    // traverse through the string
    for (int i = 1; i < len; i++)
    {

        // the ASCII value of the second string
        // should be greater than or equal to first
        // string, if it is violated return false.
        if (s1[i] > s2[i])
            return false;

        else
        {

            // store the difference of ASCII values
            d[i] = s2[i] - s1[i];
        }
    }

    // the difference of ASCII values should be
    // in descending order
    for (int i = 0; i < len - 1; i++)
    {

        // if the difference array is not in descending order
        if (d[i] < d[i + 1])
            return false;
    }

    // if all the ASCII values of characters of first string
    // is less than or equal to the second string
    // and the difference array is in descending
    // order, return true
    return true;
}

// Driver code
public static void Main()
{
    // create two strings
    string s1 = "abcd", s2 = "bcdd";

    // check whether the first string can be
    // converted to the second string
    if (find(s1, s2))
        Console.WriteLine("Yes");
    else
        Console.WriteLine( "No");
}
}

// This code is contributed by SoM15242
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# check whether the first string can be
# converted to the second string
# by increasing the ASCII value of prefix
# string of first string
def find(s1, s2):

    # length of two strings
    len__ = len(s1)
    len_1 = len(s2)

    # If lengths are not equal
    if (len__ != len_1):
        return False

    # store the difference of ASCII values
    d = [0 for i in range(len__)]

    # difference of first element
    d[0] = ord(s2[0]) - ord(s1[0])

    # traverse through the string
    for i in range(1, len__, 1):

        # the ASCII value of the second string
        # should be greater than or equal to first
        # string, if it is violated return false.
        if (s1[i] > s2[i]):
            return False

        else:

            # store the difference of ASCII values
            d[i] = ord(s2[i]) - ord(s1[i])

    # the difference of ASCII values
    # should be in descending order
    for i in range(len__ - 1):

        # if the difference array is not
        # in descending order
        if (d[i] < d[i + 1]):
            return False

    # if all the ASCII values of characters of
    # first string is less than or equal to the
    # second string and the difference array is
    # in descending order, return true
    return True

# Driver code
if __name__ == '__main__':

    # create two strings
    s1 = "abcd"
    s2 = "bcdd"

    # check whether the first string can
    # be converted to the second string
    if (find(s1, s2)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Shashank_Sharma
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// check whether the first string can be
// converted to the second string
// by increasing the ASCII value of prefix
// string of first string
function find(s1, s2)
{
    // length of two strings
    var len = s1.length, len_1 = s2.length;

    // If lengths are not equal
    if (len != len_1)
        return false;

    // store the difference of ASCII values
    var d = Array(len).fill(0);

    // difference of first element
    d[0] = s2[0] - s1[0];

    // traverse through the string
    for (var i = 1; i < len; i++) {

        // the ASCII value of the second string
        // should be greater than or equal to first
        // string, if it is violated return false.
        if (s1[i] > s2[i])
            return false;

        else {

            // store the difference of ASCII values
            d[i] = s2[i] - s1[i];
        }
    }

    // the difference of ASCII values should be
    // in descending order
    for (var i = 0; i < len - 1; i++) {

        // if the difference array is not in descending order
        if (d[i] < d[i + 1])
            return false;
    }

    // if all the ASCII values of characters of first string
    // is less than or equal to the second string
    // and the difference array is in descending
    // order, return true
    return true;
}

// Driver code
// create two strings
var s1 = "abcd", s2 = "bcdd";
// check whether the first string can be
// converted to the second string
if (find(s1, s2))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(N)，其中 N 为 s1 字符串的长度

**辅助空格:** O(N)，其中 N 为 s1 字符串的长度