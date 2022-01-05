# 找到给定字符串的所有字符相加而成的字符

> 原文:[https://www . geeksforgeeks . org/find-通过添加给定字符串的所有字符而制成的字符/](https://www.geeksforgeeks.org/find-the-character-made-by-adding-all-the-characters-of-the-given-string/)

给定一个由小写英文字母组成的字符串。任务是将所有字符值相加，即 **'a' = 1，' b' = 2，' c' = 3，…，' z' = 26** ，输出和值对应的字符。如果超过 26，则取总和% 26。
**例:**

> **输入:** str = "gfg"
> **输出:** t
> (g + f + g) = 7 + 6 + 7 = 20 和 t = 20
> **输入:** str = "极客"
> **输出:** u

**进场:**

1.  找到字符串所有字符的总和，并将其存储在变量 **sum** 中。
2.  如果**总和% 26 = 0** ，则打印**‘z’**。
3.  否则更新 **sum = sum % 26** 并打印 **(sum + 'a' + 1)** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required character
char getChar(string str)
{

    // To store the sum of the characters
    // of the given string
    int sum = 0;

    for (int i = 0; i < str.length(); i++) {

        // Add the current character to the sum
        sum += (str[i] - 'a' + 1);
    }

    // Return the required character
    if (sum % 26 == 0)
        return 'z';
    else {
        sum = sum % 26;
        return (char)('a' + sum - 1);
    }
}

// Driver code
int main()
{
    string str = "gfg";

    cout << getChar(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the required character
static char getChar(String str)
{

    // To store the sum of the characters
    // of the given string
    int sum = 0;

    for (int i = 0; i < str.length(); i++)
    {

        // Add the current character to the sum
        sum += (str.charAt(i) - 'a' + 1);
    }

    // Return the required character
    if (sum % 26 == 0)
        return 'z';
    else
    {
        sum = sum % 26;
        return (char)('a' + sum - 1);
    }
}

// Driver code
public static void main (String[] args)
{
    String str = "gfg";

    System.out.println(getChar(str));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required character
def getChar(strr):

    # To store the summ of the characters
    # of the given string
    summ = 0

    for i in range(len(strr)):

        # Add the current character to the summ
        summ += (ord(strr[i]) - ord('a') + 1)

    # Return the required character
    if (summ % 26 == 0):
        return ord('z')
    else:
        summ = summ % 26
        return chr(ord('a') + summ - 1)

# Driver code
strr = "gfg"

print(getChar(strr))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required character
static char getChar(String str)
{

    // To store the sum of the characters
    // of the given string
    int sum = 0;

    for (int i = 0; i < str.Length; i++)
    {

        // Add the current character to the sum
        sum += (str[i] - 'a' + 1);
    }

    // Return the required character
    if (sum % 26 == 0)
        return 'z';
    else
    {
        sum = sum % 26;
        return (char)('a' + sum - 1);
    }
}

// Driver code
public static void Main (String[] args)
{
    String str = "gfg";

    Console.WriteLine(getChar(str));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the required character
    function getChar(str)
    {

        // To store the sum of the characters
        // of the given string
        let sum = 0;

        for (let i = 0; i < str.length; i++)
        {

            // Add the current character to the sum
            sum += (str[i].charCodeAt() - 'a'.charCodeAt() + 1);
        }

        // Return the required character
        if (sum % 26 == 0)
            return 'z';
        else {
            sum = sum % 26;
            return String.fromCharCode('a'.charCodeAt() + sum - 1);
        }
    }

    let str = "gfg";
    document.write(getChar(str));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
t
```