# 使用递归将字符串转换为整数

> 原文:[https://www . geesforgeks . org/convert-a-string-to-a-整数-使用递归/](https://www.geeksforgeeks.org/convert-a-string-to-an-integer-using-recursion/)

给定一个表示字符串的字符串 **str** ，任务是将给定的字符串转换成整数。
**例:**

> **输入:** str = "1234"
> **输出:** 1234
> **输入:** str = "0145"
> **输出:** 145

**方法:**写一个递归函数，取字符串的第一个数字，乘以适当的 10 次方，然后从第二个索引开始，将子字符串的递归结果相加。当传递的字符串由单个数字组成时，将出现终止条件。在这种情况下，返回由字符串表示的数字。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Recursive function to convert
// string to integer
int stringToInt(string str)
{

    // If the number represented as a string
    // contains only a single digit
    // then returns its value
    if (str.length() == 1)
        return (str[0] - '0');

    // Recursive call for the sub-string
    // starting at the second character
    double y = stringToInt(str.substr(1));

    // First digit of the number
    double x = str[0] - '0';

    // First digit multiplied by the
    // appropriate power of 10 and then
    // add the recursive result
    // For example, xy = ((x * 10) + y)
    x = x * pow(10, str.length() - 1) + y;
    return int(x);
}

// Driver code
int main()
{
    string str = "1235";
    cout << (stringToInt(str)) << endl;
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Recursive function to convert string to integer
    static int stringToInt(String str)
    {

        // If the number represented as a string
        // contains only a single digit
        // then returns its value
        if (str.length() == 1)
            return (str.charAt(0) - '0');

        // Recursive call for the sub-string
        // starting at the second character
        double y = stringToInt(str.substring(1));

        // First digit of the number
        double x = str.charAt(0) - '0';

        // First digit multiplied by the
        // appropriate power of 10 and then
        // add the recursive result
        // For example, xy = ((x * 10) + y)
        x = x * Math.pow(10, str.length() - 1) + y;
        return (int)(x);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "1235";
        System.out.print(stringToInt(str));
    }
}
```

## 蟒蛇 3

```

# Python3 implementation of the approach

# Recursive function to convert
# string to integer
def stringToInt(str):

    # If the number represented as a string
    # contains only a single digit
    # then returns its value
    if (len(str) == 1):
        return ord(str[0]) - ord('0');

    # Recursive call for the sub-string
    # starting at the second character
    y = stringToInt(str[1:]);

    # First digit of the number
    x = ord(str[0]) - ord('0');

    # First digit multiplied by the
    # appropriate power of 10 and then
    # add the recursive result
    # For example, xy = ((x * 10) + y)
    x = x * (10**(len(str) - 1)) + y;
    return int(x);

# Driver code
if __name__ == '__main__':
    str = "1235";
    print(stringToInt(str));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Recursive function to convert string to integer
    static int stringToInt(String str)
    {

        // If the number represented as a string
        // contains only a single digit
        // then returns its value
        if (str.Length == 1)
            return (str[0] - '0');

        // Recursive call for the sub-string
        // starting at the second character
        double y = stringToInt(str.Substring(1));

        // First digit of the number
        double x = str[0] - '0';

        // First digit multiplied by the
        // appropriate power of 10 and then
        // add the recursive result
        // For example, xy = ((x * 10) + y)
        x = x * Math.Pow(10, str.Length - 1) + y;
        return (int)(x);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "1235";
        Console.Write(stringToInt(str));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript implementation of the approach

    // Recursive function to convert string to integer
    function stringToInt(str)
    {

        // If the number represented as a string
        // contains only a single digit
        // then returns its value

        if (str.length == 1)
            return (str[0] - '0');

        // Recursive call for the sub-string
        // starting at the second character
        var y = stringToInt(str.substring(1));

        // First digit of the number
        var x = str[0] - '0';

        // First digit multiplied by the
        // appropriate power of 10 and then
        // add the recursive result
        // For example, xy = ((x * 10) + y)
        x = x * Math.pow(10, str.Length - 1) + y;

        return (x);
    }

    // Driver code

        var str = "1235".split()
        document.write(stringToInt(str));

</script>
```

**Output:** 

```
1235
```