# 检查给定的字符串是否与其在镜子中的反射相同

> 原文:[https://www . geeksforgeeks . org/check-如果给定字符串与其镜像中的反射相同/](https://www.geeksforgeeks.org/check-if-the-given-string-is-the-same-as-its-reflection-in-a-mirror/)

给定一个只包含大写英文字符的字符串 **S** 。任务是发现 **S** 是否和它在镜子里的倒影一样。
**例:**

```
Input: str = "AMA"
Output: YES
AMA is same as its reflection in the mirror.

Input: str = "ZXZ"
Output: NO
```

**方法:**字符串显然必须是回文，但仅此还不够。字符串中的所有字符都应该是对称的，这样它们的反射也是相同的。对称字符为 **AHIMOTUVWXY** 。

*   将对称字符存储在无序集中。
*   遍历字符串并检查字符串中是否存在任何非对称字符。如果是，则返回 false。
*   否则检查字符串是否是回文。如果字符串也是回文，则返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check reflection
bool isReflectionEqual(string s)
{
    // Symmetric characters
    unordered_set<char> symmetric = { 'A', 'H', 'I', 'M',
                        'O', 'T', 'U', 'V', 'W', 'X', 'Y' };

    int n = s.length();

    for (int i = 0; i < n; i++)
        // If any non-symmetric character is
        // present, the answer is NO
        if (symmetric.find(s[i]) == symmetric.end())
            return false;

    string rev = s;
    reverse(rev.begin(), rev.end());

    // Check if the string is a palindrome
    if (rev == s)
        return true;
    else
        return false;
}

// Driver code
int main()
{
    string s = "MYTYM";
    if (isReflectionEqual(s))
        cout << "YES";
    else
        cout << "NO";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

    static String Reverse(String s)
    {
        char[] charArray = s.toCharArray();
        reverse(charArray, 0, charArray.length - 1);
        return new String(charArray);
    }

    // Function to check reflection
    static boolean isReflectionEqual(String s)
    {
        HashSet<Character> symmetric = new HashSet<>();

        // Symmetric characters
        symmetric.add('A');
        symmetric.add('H');
        symmetric.add('I');
        symmetric.add('M');
        symmetric.add('O');
        symmetric.add('T');
        symmetric.add('U');
        symmetric.add('V');
        symmetric.add('W');
        symmetric.add('X');
        symmetric.add('Y');

        int n = s.length();

        // If any non-symmetric character is
        for (int i = 0; i < n; i++)

        // present, the answer is NO
        {
            if (symmetric.contains(s.charAt(i)) == false)
            {
                return false;
            }
        }

        String rev = s;
        s = Reverse(s);

        // Check if the String is a palindrome
        if (rev.equals(s))
        {
            return true;
        } else {
            return false;
        }
    }

    // Reverse the letters of the word
    static void reverse(char str[], int start, int end)
    {

        // Temporary variable to store character
        char temp;
        while (start <= end)
        {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "MYTYM";
        if (isReflectionEqual(s))
        {
            System.out.println("YES");
        }
        else
        {
            System.out.println("NO");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to check reflection
def isReflectionEqual(s):

    # Symmetric characters
    symmetric = dict()

    str1 = "AHIMOTUVWXY"

    for i in str1:
        symmetric[i] = 1

    n = len(s)

    for i in range(n):

        # If any non-symmetric character
        # is present, the answer is NO
        if (symmetric[s[i]] == 0):
            return False

    rev = s[::-1]

    # Check if the is a palindrome
    if (rev == s):
        return True
    else:
        return False

# Driver Code
s = "MYTYM"
if (isReflectionEqual(s)):
    print("YES")
else:
    print("NO")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic ;

class GFG
{

    static string Reverse( string s )
    {
        char[] charArray = s.ToCharArray();
        Array.Reverse( charArray );
        return new string( charArray );
    }

    // Function to check reflection
    static bool isReflectionEqual(string s)
    {
        HashSet<char> symmetric = new HashSet<char>();

        // Symmetric characters
        symmetric.Add('A');
        symmetric.Add('H');
        symmetric.Add('I');
        symmetric.Add('M');
        symmetric.Add('O');
        symmetric.Add('T');
        symmetric.Add('U');
        symmetric.Add('V');
        symmetric.Add('W');
        symmetric.Add('X');
        symmetric.Add('Y');

        int n = s.Length;

        for (int i = 0; i < n; i++)

            // If any non-symmetric character is
            // present, the answer is NO
            if (symmetric.Contains(s[i]) == false)
                return false;

        string rev = s;
        s = Reverse(s);

        // Check if the string is a palindrome
        if (rev == s)
            return true;
        else
            return false;
    }

    // Driver code
    static public void Main()
    {
        string s = "MYTYM";
        if (isReflectionEqual(s))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

    function Reverse(s)
    {
        let charArray = s.split("");
        reverse(charArray, 0, charArray.length - 1);
        return charArray.join("");
    }

    // Function to check reflection
    function isReflectionEqual(s)
    {
        let symmetric = new Set();

        // Symmetric characters
        symmetric.add('A');
        symmetric.add('H');
        symmetric.add('I');
        symmetric.add('M');
        symmetric.add('O');
        symmetric.add('T');
        symmetric.add('U');
        symmetric.add('V');
        symmetric.add('W');
        symmetric.add('X');
        symmetric.add('Y');

        let n = s.length;

        // If any non-symmetric character is
        for (let i = 0; i < n; i++)

        // present, the answer is NO
        {
            if (symmetric.has(s[i]) == false)
            {
                return false;
            }
        }

        let rev = s;
        s = Reverse(s);

        // Check if the String is a palindrome
        if (rev==(s))
        {
            return true;
        } else {
            return false;
        }
    }

    // Reverse the letters of the word
    function reverse(str,start,end)
    {
        // Temporary variable to store character
        let temp;
        while (start <= end)
        {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }

    // Driver code
    let s = "MYTYM";
        if (isReflectionEqual(s))
        {
            document.write("YES");
        }
        else
        {
            document.write("NO");
        }

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
YES
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)