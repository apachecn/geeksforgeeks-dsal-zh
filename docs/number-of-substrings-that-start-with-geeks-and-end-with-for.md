# 以“极客”开头、以“for”结尾的子字符串数量

> 原文:[https://www . geeksforgeeks . org/以 geeks 开头和以 for 结尾的子字符串数量/](https://www.geeksforgeeks.org/number-of-substrings-that-start-with-geeks-and-end-with-for/)

给定一个由小写英文字母组成的字符串 **str** ，任务是找出以**“极客”**开头，以**“表示”**结尾的子字符串的数量。
**举例:**

> **输入:**str = " geeksforgeicks "
> **输出:**3
> “geeks for”“geeksforgeicks for”“geeks for”
> 是唯一有效的子字符串。
> **输入:**str = " geeks forgeeks "
> **输出:** 1

**天真的方法:**首先将计数器设置为 0，然后遍历字符串，每当遇到子字符串**“极客”**时，从下一个索引再次遍历字符串，并尝试找到“”的子字符串**。如果**“for”**存在，则递增计数器并最终打印。
**高效方法:**为子串**“极客”**和**“为”**设置两个计数器，比如 c1 和 c2。迭代时，每当遇到子串**“geeks”**时，递增 c1，每当遇到**“for”**时，设置 **c2 = c2 + c1** 。这是因为**“极客”**的每一次出现都会用当前找到的**做一个有效的子串来表示**。最后打印 **c2** 。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count
// of required substrings
int countSubStr(string s, int n)
{
    int c1 = 0, c2 = 0;

    // For every index of the string
    for (int i = 0; i < n; i++) {

        // If the substring starting at
        // the current index is "geeks"
        if (s.substr(i, 5) == "geeks")
            c1++;

        // If the substring is "for"
        if (s.substr(i, 3) == "for")
            c2 = c2 + c1;
    }

    return c2;
}

// Driver code
int main()
{
    string s = "geeksforgeeksisforgeeks";
    int n = s.size();

    cout << countSubStr(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count
    // of required substrings
    static int countSubStr(String s, int n)
    {
        int c1 = 0, c2 = 0;

        // For every index of the string
        for (int i = 0; i < n; i++)
        {

            // If the substring starting at
            // the current index is "geeks"
            if (i < n - 5 &&
                "geeks".equals(s.substring(i, i + 5)))
            {
                c1++;
            }

            // If the substring is "for"
            if (i < n - 3 &&
                "for".equals(s.substring(i, i + 3)))
            {
                c2 = c2 + c1;
            }
        }
        return c2;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geeksforgeeksisforgeeks";
        int n = s.length();
        System.out.println(countSubStr(s, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of required substrings
def countSubStr(s, n) :

    c1 = 0; c2 = 0;

    # For every index of the string
    for i in range(n) :

        # If the substring starting at
        # the current index is "geeks"
        if (s[i : i + 5] == "geeks") :
            c1 += 1;

        # If the substring is "for"
        if (s[i :i+ 3] == "for") :
            c2 = c2 + c1;

    return c2;

# Driver code
if __name__ == "__main__" :

    s = "geeksforgeeksisforgeeks";
    n = len(s);

    print(countSubStr(s, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

public class GFG
{

    // Function to return the count
    // of required substrings
    static int countSubStr(String s, int n)
    {
        int c1 = 0, c2 = 0;

        // For every index of the string
        for (int i = 0; i < n; i++)
        {

            // If the substring starting at
            // the current index is "geeks"
            if (i < n - 5 &&
                "geeks".Equals(s.Substring(i, 5)))
            {
                c1++;
            }

            // If the substring is "for"
            if (i < n - 3 &&
                "for".Equals(s.Substring(i, 3)))
            {
                c2 = c2 + c1;
            }
        }
        return c2;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "geeksforgeeksisforgeeks";
        int n = s.Length;
        Console.WriteLine(countSubStr(s, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count
// of required substrings
function countSubStr(s, n)
{
    var c1 = 0, c2 = 0;

    // For every index of the string
    for (var i = 0; i < n; i++) {

        // If the substring starting at
        // the current index is "geeks"
        if (s.substring(i, i+5) == "geeks")
            c1++;

        // If the substring is "for"
        if (s.substring(i,i+ 3) == "for")
            c2 = c2 + c1;
    }

    return c2;
}

// Driver code
var s = "geeksforgeeksisforgeeks";
var n = s.length;
document.write( countSubStr(s, n));

</script>
```

**Output:** 

```
3
```