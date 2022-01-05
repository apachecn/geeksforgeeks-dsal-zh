# 两个偶数和字符串的字符对

> 原文:[https://www . geeksforgeeks . org/字符对-从两个带偶数和的字符串/](https://www.geeksforgeeks.org/character-pairs-from-two-strings-with-even-sum/)

给定两根弦 **s1** 和 **s2** 。任务是从第一个字符串中提取一个字符，从第二个字符串中提取一个字符，并检查两个字符的 ascii 值之和是否为偶数。打印此类对的总数。**注意**两个字符串都由小写英文字母组成。
**举例:**

> **输入:** s1 = "极客"，s2 = "代表"
> **输出:** 5
> 所有有效对为:
> (g，o) - > 103 + 111 = 214
> (e，o) - > 101 + 111 = 212
> (e，o) - > 101 + 111 = 212
> (k，o) - > 107 + 111

**进场:**

*   很明显，要使总和为偶数，两个 ascii 值必须都为偶数或都为奇数。
*   从第一个字符串计算奇数和偶数 ascii 值的总数。分别是 **a1** 和 **b1** 。
*   从第二个字符串计算奇数和偶数 ascii 值的总数。分别是 **a2** 和 **b2** 。
*   那么有效对的总数将是 **((a1 * a2) + (b1 * b2))** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the total number of valid pairs
int totalPairs(string s1, string s2)
{
    int a1 = 0, b1 = 0;

    // Count total number of even and odd
    // ascii values for string s1
    for (int i = 0; i < s1.length(); i++) {
        if (int(s1[i]) % 2 != 0)
            a1++;
        else
            b1++;
    }

    int a2 = 0, b2 = 0;

    // Count total number of even and odd
    // ascii values for string s2
    for (int i = 0; i < s2.length(); i++) {
        if (int(s2[i]) % 2 != 0)
            a2++;
        else
            b2++;
    }

    // Return total valid pairs
    return ((a1 * a2) + (b1 * b2));
}

// Driver code
int main()
{
    string s1 = "geeks", s2 = "for";
    cout << totalPairs(s1, s2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

    // Function to return the total number of valid pairs
    static int totalPairs(String s1, String s2)
    {
        int a1 = 0, b1 = 0;

        // Count total number of even and odd
        // ascii values for string s1
        for (int i = 0; i < s1.length(); i++)
        {
            if ((int)s1.charAt(i) % 2 != 0)
                a1++;
            else
                b1++;
        }

        int a2 = 0, b2 = 0;

        // Count total number of even and odd
        // ascii values for string s2
        for (int i = 0; i < s2.length(); i++)
        {
            if ((int)s2.charAt(i) % 2 != 0)
                a2++;
            else
                b2++;
        }

        // Return total valid pairs
        return ((a1 * a2) + (b1 * b2));
    }

    // Driver code
    public static void main(String []args)
    {

        String s1 = "geeks", s2 = "for";
        System.out.println(totalPairs(s1, s2));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the total
# number of valid pairs
def totalPairs(s1, s2) :

    a1 = 0; b1 = 0;

    # Count total number of even and 
    # odd ascii values for string s1
    for i in range(len(s1)) :
        if (ord(s1[i]) % 2 != 0) :
            a1 += 1;
        else :
            b1 += 1;

    a2 = 0 ; b2 = 0;

    # Count total number of even and odd
    # ascii values for string s2
    for i in range(len(s2)) :
        if (ord(s2[i]) % 2 != 0) :
            a2 += 1;
        else :
            b2 += 1;

    # Return total valid pairs
    return ((a1 * a2) + (b1 * b2));

# Driver code
if __name__ == "__main__" :

    s1 = "geeks";
    s2 = "for";

    print(totalPairs(s1, s2));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the total number of valid pairs
    static int totalPairs(String s1, String s2)
    {
        int a1 = 0, b1 = 0;

        // Count total number of even and odd
        // ascii values for string s1
        for (int i = 0; i < s1.Length; i++)
        {
            if ((int)s1[i] % 2 != 0)
                a1++;
            else
                b1++;
        }

        int a2 = 0, b2 = 0;

        // Count total number of even and odd
        // ascii values for string s2
        for (int i = 0; i < s2.Length; i++)
        {
            if ((int)s2[i] % 2 != 0)
                a2++;
            else
                b2++;
        }

        // Return total valid pairs
        return ((a1 * a2) + (b1 * b2));
    }

    // Driver code
    public static void Main(String []args)
    {

        String s1 = "geeks", s2 = "for";
        Console.WriteLine(totalPairs(s1, s2));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the total number of valid pairs
function totalPairs(s1, s2)
{
    var a1 = 0, b1 = 0;

    // Count total number of even and odd
    // ascii values for string s1
    for (var i = 0; i < s1.length; i++) {
        if ((s1[i].charCodeAt(0)) % 2 != 0)
            a1++;
        else
            b1++;
    }

    var a2 = 0, b2 = 0;

    // Count total number of even and odd
    // ascii values for string s2
    for (var i = 0; i < s2.length; i++) {
        if ((s2[i].charCodeAt(0)) % 2 != 0)
            a2++;
        else
            b2++;
    }

    // Return total valid pairs
    return ((a1 * a2) + (b1 * b2));
}

// Driver code
var s1 = "geeks", s2 = "for";
document.write( totalPairs(s1, s2));

</script>
```

**Output:** 

```
5
```