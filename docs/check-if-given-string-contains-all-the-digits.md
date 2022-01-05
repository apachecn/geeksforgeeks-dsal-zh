# 检查给定字符串是否包含所有数字

> 原文:[https://www . geesforgeks . org/check-if-给定字符串-包含所有数字/](https://www.geeksforgeeks.org/check-if-given-string-contains-all-the-digits/)

给定一个由字母数字字符组成的字符串 **str** ，任务是检查该字符串是否包含从 **1** 到 **9** 的所有数字。

**示例:**

> **输入:**str = " geeks 12345 for 69708 "
> **输出:**是
> 从 0 到 9 的所有数字都存在于给定的字符串中。
> 
> **输入:**str = " amazing 1234 "
> T3】输出:否

**方法:**创建一个频率数组来标记从 0 到 9 的每个数字的频率。最后，遍历频率数组，如果给定字符串中没有任何数字，那么答案将是“否”，否则答案将是“是”。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 10;

// Function that returns true
// if ch is a digit
bool isDigit(char ch)
{
    if (ch >= '0' && ch <= '9')
        return true;
    return false;
}

// Function that returns true
// if str contains all the
// digits from 0 to 9
bool allDigits(string str, int len)
{

    // To mark the present digits
    bool present[MAX] = { false };

    // For every character of the string
    for (int i = 0; i < len; i++) {

        // If the current character is a digit
        if (isDigit(str[i])) {

            // Mark the current digit as present
            int digit = str[i] - '0';
            present[digit] = true;
        }
    }

    // For every digit from 0 to 9
    for (int i = 0; i < MAX; i++) {

        // If the current digit is
        // not present in str
        if (!present[i])
            return false;
    }

    return true;
}

// Driver code
int main()
{
    string str = "Geeks12345for69708";
    int len = str.length();

    if (allDigits(str, len))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAX = 10;

// Function that returns true
// if ch is a digit
static boolean isDigit(char ch)
{
    if (ch >= '0' && ch <= '9')
        return true;
    return false;
}

// Function that returns true
// if str contains all the
// digits from 0 to 9
static boolean allDigits(String str, int len)
{

    // To mark the present digits
    boolean []present = new boolean[MAX];

    // For every character of the String
    for (int i = 0; i < len; i++)
    {

        // If the current character is a digit
        if (isDigit(str.charAt(i)))
        {

            // Mark the current digit as present
            int digit = str.charAt(i) - '0';
            present[digit] = true;
        }
    }

    // For every digit from 0 to 9
    for (int i = 0; i < MAX; i++)
    {

        // If the current digit is
        // not present in str
        if (!present[i])
            return false;
    }

    return true;
}

// Driver code
public static void main(String[] args)
{
    String str = "Geeks12345for69708";
    int len = str.length();

    if (allDigits(str, len))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 10

# Function that returns true
# if ch is a digit
def isDigit(ch):
    ch = ord(ch)
    if (ch >= ord('0') and ch <= ord('9')):
        return True
    return False

# Function that returns true
# if st contains all the
# digits from 0 to 9
def allDigits(st, le):

    # To mark the present digits
    present = [False for i in range(MAX)]

    # For every character of the string
    for i in range(le):

        # If the current character is a digit
        if (isDigit(st[i])):

            # Mark the current digit as present
            digit = ord(st[i]) - ord('0')
            present[digit] = True

    # For every digit from 0 to 9
    for i in range(MAX):

        # If the current digit is
        # not present in st
        if (present[i] == False):
            return False

    return True

# Driver code
st = "Geeks12345for69708"
le = len(st)

if (allDigits(st, le)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 10;

// Function that returns true
// if ch is a digit
static bool isDigit(char ch)
{
    if (ch >= '0' && ch <= '9')
        return true;
    return false;
}

// Function that returns true
// if str contains all the
// digits from 0 to 9
static bool allDigits(String str, int len)
{

    // To mark the present digits
    bool []present = new bool[MAX];

    // For every character of the String
    for (int i = 0; i < len; i++)
    {

        // If the current character is a digit
        if (isDigit(str[i]))
        {

            // Mark the current digit as present
            int digit = str[i] - '0';
            present[digit] = true;
        }
    }

    // For every digit from 0 to 9
    for (int i = 0; i < MAX; i++)
    {

        // If the current digit is
        // not present in str
        if (!present[i])
            return false;
    }

    return true;
}

// Driver code
public static void Main(String[] args)
{
    String str = "Geeks12345for69708";
    int len = str.Length;

    if (allDigits(str, len))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let MAX = 10;

// Function that returns true
// if ch is a digit
function isDigit(ch)
{
    if (ch >= '0' && ch <= '9')
        return true;
    return false;
}

// Function that returns true
// if str contains all the
// digits from 0 to 9
function allDigits(str, len)
{

    // To mark the present digits
    let present = Array.from({length: MAX}, (_, i) => 0);

    // For every character of the String
    for (let i = 0; i < len; i++)
    {

        // If the current character is a digit
        if (isDigit(str[i]))
        {

            // Mark the current digit as present
            let digit = str[i] - '0';
            present[digit] = true;
        }
    }

    // For every digit from 0 to 9
    for (let i = 0; i < MAX; i++)
    {

        // If the current digit is
        // not present in str
        if (!present[i])
            return false;
    }

    return true;
}

// Driver code

      let str = "Geeks12345for69708";
    let len = str.length;

    if (allDigits(str, len))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```