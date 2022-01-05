# 检查给定的二进制字符串是否符合给定的条件

> 原文:[https://www . geesforgeks . org/check-if-given-binary-string-跟在-then-given-condition-or-not/](https://www.geeksforgeeks.org/check-if-given-binary-string-follows-then-given-condition-or-not/)

给定二进制字符串 **str** ，任务是检查给定字符串是否符合以下条件:

*   字符串以**‘1’**开头。
*   每个**‘1’**后面是空字符串(**“**)、**‘1’**或**“00”**。
*   每个**“00”**后面是空串(**“**)、**“1”**。

如果给定字符串符合上述标准，则打印**“有效字符串”**否则打印**“无效字符串”**。
**例:**

> **输入:** str = "1000"
> **输出:**假
> **解释:**
> 给定的字符串以“1”开头，后面是“00”，后面是“1”，这不是给定的标准。
> 因此，给定的字符串是“无效字符串”。
> **输入:** str = "1111"
> **输出:**真
> **解释:**
> 给定的字符串以 1 开头，有 1 后跟所有的 1。
> 因此，给定的字符串是“有效字符串”。

**方法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)。以下是步骤:

1.  检查第 0 <sup>个</sup>字符是否为**‘1’**。如果不是 **'1'** ，则返回 false，因为字符串不符合条件 1。
2.  要检查满足第二个条件的字符串，使用 C++中的 [substr()](https://www.geeksforgeeks.org/substring-in-cpp/) 函数递归调用从第一个索引开始的字符串。
3.  要检查满足第三个条件的字符串，首先需要检查字符串长度是否大于 2。如果是，则检查第一和第二索引处是否存在**‘0’**。如果是，则递归调用从第三个索引开始的字符串。
4.  在任何递归调用中，如果字符串为空，那么我们已经遍历了满足所有给定条件的完整字符串，并打印**“有效字符串”**。
5.  在任何递归调用中，如果给定条件不满足，则停止该递归并打印**“无效字符串”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// string follows rules or not
bool checkrules(string s)
{
    if (s.length() == 0)
        return true;

    // Check for the first condition
    if (s[0] != '1')
        return false;

    // Check for the third condition
    if (s.length() > 2) {
        if (s[1] == '0' && s[2] == '0')
            return checkrules(s.substr(3));
    }

    // Check for the second condition
    return checkrules(s.substr(1));
}

// Driver Code
int main()
{
    // Given String str
    string str = "1111";

    // Function Call
    if (checkrules(str)) {
        cout << "Valid String";
    }
    else {
        cout << "Invalid String";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if the
// String follows rules or not
static boolean checkrules(String s)
{
    if (s.length() == 0)
        return true;

    // Check for the first condition
    if (s.charAt(0) != '1')
        return false;

    // Check for the third condition
    if (s.length() > 2)
    {
        if (s.charAt(1) == '0' &&
            s.charAt(2) == '0')
            return checkrules(s.substring(3));
    }

    // Check for the second condition
    return checkrules(s.substring(1));
}

// Driver Code
public static void main(String[] args)
{

    // Given String str
    String str = "1111";

    // Function call
    if (checkrules(str))
    {
        System.out.print("Valid String");
    }
    else
    {
        System.out.print("Invalid String");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the
# string follows rules or not
def checkrules(s):

    if len(s) == 0:
        return True

    # Check for the first condition
    if s[0] != '1':
        return False

    # Check for the third condition
    if len(s) > 2:
        if s[1] == '0' and s[2] == '0':
            return checkrules(s[3:])

    # Check for the second condition
    return checkrules(s[1:])

# Driver code
if __name__ == '__main__':

    # Given string
    s = '1111'

    # Function call
    if checkrules(s):
        print('valid string')
    else:
        print('invalid string')

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the
// String follows rules or not
static bool checkrules(String s)
{
    if (s.Length == 0)
        return true;

    // Check for the first condition
    if (s[0] != '1')
        return false;

    // Check for the third condition
    if (s.Length > 2)
    {
        if (s[1] == '0' &&
            s[2] == '0')
            return checkrules(s.Substring(3));
    }

    // Check for the second condition
    return checkrules(s.Substring(1));
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String str = "1111";

    // Function call
    if (checkrules(str))
    {
        Console.Write("Valid String");
    }
    else
    {
        Console.Write("Invalid String");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the
// string follows rules or not
function checkrules(s)
{
    if (s.length == 0)
        return true;

    // Check for the first condition
    if (s[0] != '1')
        return false;

    // Check for the third condition
    if (s.length > 2) {
        if (s[1] == '0' && s[2] == '0')
            return checkrules(s.substring(3));
    }

    // Check for the second condition
    return checkrules(s.substring(1));
}

// Driver Code
// Given String str
var str = "1111";
// Function Call
if (checkrules(str)) {
    document.write( "Valid String");
}
else {
    document.write( "Invalid String");
}

</script>
```

**Output:** 

```
Valid String
```

**时间复杂度:** *O(N)* ，其中 N 为字符串长度。
**辅助空间:** *O(1)* 。