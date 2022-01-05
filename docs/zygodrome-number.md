# 合子号

> 原文:[https://www.geeksforgeeks.org/zygodrome-number/](https://www.geeksforgeeks.org/zygodrome-number/)

给定一个整数 **N** ，任务是检查 **N** 是否为合子号。

> **合子号**是一个数字，如果它是由相同数字的非平凡序列组成的。
> 例如:112233、7777333、1100 都是 10 号碱基的合子。

**示例:**

> **输入:**N = 1122
> T3】输出:是
> T6】输入:N = 26
> T9】输出:否

**做法:**思路是将数字转换为字符串，如果任意字符不等于上一个字符和下一个字符，则返回 false。因为第一个字符没有前一个字符，最后一个字符没有下一个字符，所以我们将在字符串的开头和结尾添加一个空格。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to check if N
// is an zygodrome number

#include <bits/stdc++.h>
using namespace std;

// Function to check if N
// is an zygodrome number
bool iszygodromeNum(int N)
{
    // convert N to string
    string s = to_string(N);

    // Adding a space at the
    // beginning and
    // end of the string
    s = ' ' + s + ' ';
    // Traverse the string
    for (int i = 1; i < s.size() - 1; i++) {
        // If any character is not same as
        // prev and next then return false
        if (s[i] != s[i - 1]
            && s[i] != s[i + 1]) {
            return false;
        }
    }
    return true;
}

// Driver code
int main()
{
    int n = 1122;
    if (iszygodromeNum(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if N
// is a zygodrome number
class GFG{

// Function to check if N
// is an zygodrome number
static boolean iszygodromeNum(int N)
{
    // convert N to string
    String s = Integer.toString(N);

    // Adding a space at the
    // beginning and
    // end of the string
    s = ' ' + s + ' ';

    // Traverse the string
    for (int i = 1; i < s.length() - 1; i++)
    {
        // If any character is not same as
        // prev and next then return false
        if (s.charAt(i) != s.charAt(i - 1) &&
            s.charAt(i) != s.charAt(i + 1))
        {
            return false;
        }
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int n = 1122;
    if (iszygodromeNum(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program implementation to check
# if N is an zygodrome number

# Function to check if N
# is an zygodrome number
def iszygodromeNum(N):

    # Convert N to string
    s = str(N);

    # Adding a space at the
    # beginning and
    # end of the string
    s = ' ' + s + ' ';

    # Traverse the string
    i = 1
    while i < len(s) - 1:

        # If any character is not same as
        # prev and next then return false
        if ((s[i] != s[i - 1]) and
            (s[i] != s[i + 1])):
            return False;

        i += 1

    return True;

# Driver code
if __name__ == '__main__':

    n = 1122;

    if iszygodromeNum(n):
        print("Yes")
    else:
        print("No")

# This code is contributed by jana_sayantan
```

## C#

```
// C# implementation to check if N
// is a zygodrome number
using System;
class GFG{

// Function to check if N
// is an zygodrome number
static bool iszygodromeNum(int N)
{
    // convert N to string
    String s = N.ToString();

    // Adding a space at the
    // beginning and
    // end of the string
    s = ' ' + s + ' ';

    // Traverse the string
    for (int i = 1; i < s.Length - 1; i++)
    {
        // If any character is not same as
        // prev and next then return false
        if (s[i] != s[i - 1] &&
            s[i] != s[i + 1])
        {
            return false;
        }
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    int n = 1122;
    if (iszygodromeNum(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation to check if N
// is a zygodrome number

    // Function to check if N
    // is an zygodrome number
    function iszygodromeNum( N)
    {

        // convert N to string
        let s = N.toString();

        // Adding a space at the
        // beginning and
        // end of the string
        s = ' ' + s + ' ';

        // Traverse the string
        for ( i = 1; i < s.length - 1; i++)
        {

            // If any letacter is not same as
            // prev and next then return false
            if (s[i] != s[i-1] && s[i] != s[i + 1])
            {
                return false;
            }
        }
        return true;
    }

    // Driver code
    let n = 1122;
    if (iszygodromeNum(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(log <sub>10</sub> n)