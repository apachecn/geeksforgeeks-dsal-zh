# 检查一个二进制字符串是否在任何地方都连续出现两次

> 原文:[https://www . geesforgeks . org/check-if-a-binary-string-with-two-continuous-everything-one-everything/](https://www.geeksforgeeks.org/check-if-a-binary-string-has-two-consecutive-occurrences-of-one-everywhere/)

给定仅由字符**【a】**和**【b】**组成的字符串 **str** ，任务是检查该字符串是否有效。在有效字符串中，每组连续的 **b** 必须具有长度 **2** ，并且必须出现在字符 **'a'** 出现的 **1 或更多**之后，即**“ABBA”**是有效的子字符串，但是**“abbb”**和 **aba** 不是。如果字符串有效，打印 **1** ，否则打印 **-1** 。

**示例:**

> **输入:**str = " abbaabbaba "
> T3】输出: 1
> 
> **输入:**str = " abbaabab "
> T3】输出: -1

**方法:**找出串中每一个出现的**【b】**，检查它是否是子串**【abb】**的一部分。如果任一子串条件失败，则打印 **-1** ，否则打印 **1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns 1 if str is valid
bool isValidString(string str, int n)
{
    // Index of first appearance of 'b'
    int index = find(str.begin(),      
                     str.end(), 'b') -
                     str.begin();

    // If str starts with 'b'
    if (index == 0)
        return false;

    // While 'b' occurs in str
    while (index <= n - 1)
    {
        // If 'b' doesn't appear after an 'a'
        if (str[index - 1] != 'a')
            return false;

        // If 'b' is not succeeded by another 'b'
        if (index + 1 < n && str[index + 1] != 'b')
            return false;

        // If sub-string is of the type "abbb"
        if (index + 2 < n && str[index + 2] == 'b')
            return false;

        // If str ends with a single b
        if (index == n - 1)
            return false;

        index = find(str.begin() + index + 2,
                     str.end(), 'b') - str.begin();
    }
    return true;
}

// Driver code
int main()
{
    string str = "abbaaabbabba";
    int n = str.length();
    isValidString(str, n) ? cout
                << "true" : cout << "false";
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns 1 if str is valid
    private static boolean isValidString(String str, int n)
    {

        // Index of first appearance of 'b'
        int index = str.indexOf("b");

        // If str starts with 'b'
        if (index == 0)
            return false;

        // While 'b' occurs in str
        while (index != -1) {

            // If 'b' doesn't appear after an 'a'
            if (str.charAt(index - 1) != 'a')
                return false;

            // If 'b' is not succeeded by another 'b'
            if (index + 1 < n && str.charAt(index + 1) != 'b')
                return false;

            // If sub-string is of the type "abbb"
            if (index + 2 < n && str.charAt(index + 2) == 'b')
                return false;

            // If str ends with a single b
            if (index == n - 1)
                return false;

            index = str.indexOf("b", index + 2);
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "abbaaabbabba";
        int n = str.length();
        System.out.println(isValidString(str, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns 1 if str is valid
def isValidString(str, n):

    # Index of first appearance of 'b'
    idx = str.find("b")

    # If str starts with 'b'
    if (idx == 0):
        return False

    # While 'b' occurs in str
    while (idx != -1):

        # If 'b' doesn't appear after an 'a'
        if (str[idx - 1] != 'a'):
            return False

        # If 'b' is not succeeded by another 'b'
        if (idx + 1 < n and str[idx + 1] != 'b'):
            return False

        # If sub-string is of the type "abbb"
        if (idx + 2 < n and str[idx + 2] == 'b'):
            return False

        # If str ends with a single b
        if (idx == n - 1):
            return False

        idx = str.find("b", idx + 2)

    return True

# Driver code
if __name__ == "__main__":

    str = "abbaaabbabba"
    n = len(str)
    print(isValidString(str, n))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns 1 if str is valid
    private static bool isValidString(string str, int n)
    {

        // Index of first appearance of 'b'
        int index = str.IndexOf("b");

        // If str starts with 'b'
        if (index == 0)
            return false;

        // While 'b' occurs in str
        while (index != -1)
        {

            // If 'b' doesn't appear after an 'a'
            if (str[index - 1] != 'a')
                return false;

            // If 'b' is not succeeded by another 'b'
            if (index + 1 < n && str[index + 1] != 'b')
                return false;

            // If sub-string is of the type "abbb"
            if (index + 2 < n && str[index + 2] == 'b')
                return false;

            // If str ends with a single b
            if (index == n - 1)
                return false;

            index = str.IndexOf("b", index + 2);
        }
        return true;
    }

    // Driver code
    public static void Main()
    {
        string str = "abbaaabbabba";
        int n = str.Length;
        Console.WriteLine(isValidString(str, n));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns 1 if str is valid
function isValidString(str,n)
{
        // Index of first appearance of 'b'
        let index = str.indexOf("b");

        // If str starts with 'b'
        if (index == 0)
            return false;

        // While 'b' occurs in str
        while (index != -1) {

            // If 'b' doesn't appear after an 'a'
            if (str[index - 1] != 'a')
                return false;

            // If 'b' is not succeeded by another 'b'
            if (index + 1 < n && str[index + 1] != 'b')
                return false;

            // If sub-string is of the type "abbb"
            if (index + 2 < n && str[index + 2] == 'b')
                return false;

            // If str ends with a single b
            if (index == n - 1)
                return false;

            index = str.indexOf("b", index + 2);
        }
        return true;
}

// Driver code
let str = "abbaaabbabba";
let n = str.length;
document.write(isValidString(str, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
true
```