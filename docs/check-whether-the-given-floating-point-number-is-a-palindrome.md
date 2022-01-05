# 检查给定的浮点数是否是回文

> 原文:[https://www . geesforgeks . org/check-给定的浮点数是否是回文/](https://www.geeksforgeeks.org/check-whether-the-given-floating-point-number-is-a-palindrome/)

给定一个浮点数 **N** ，任务是检查它是否是回文。

> **输入:**N = 123.321
> T3】输出:是
> T6】输入:N = 122.1
> T9】输出:否

**进场:**

*   首先，将给定的浮点数转换成字符数组。
*   初始化低到第一个索引和高到最后一个索引。
*   而低
    *   如果低位字符不等于高位字符，则退出并打印“否”。
    *   如果低位字符等于高位字符，则在递增低位和递减高位后继续…
*   如果上述循环成功完成，则打印“是”。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if num is palindrome
bool isPalindrome(float num)
{

    // Convert the given floating point number
    // into a string
    stringstream ss;
    ss << num;
    string s;
    ss >> s;

    // Pointers pointing to the first and
    // the last character of the string
    int low = 0;
    int high = s.size() - 1;

    while (low < high)
    {

        // Not a palindrome
        if (s[low] != s[high])
            return false;

        // Update the pointers
        low++;
        high--;
    }
    return true;
}

// Driver code
int main()
{
    float n = 123.321f;

    if (isPalindrome(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function that returns true if num is palindrome
    public static boolean isPalindrome(float num)
    {

        // Convert the given floating point number
        // into a string
        String s = String.valueOf(num);

        // Pointers pointing to the first and
        // the last character of the string
        int low = 0;
        int high = s.length() - 1;

        while (low < high) {

            // Not a palindrome
            if (s.charAt(low) != s.charAt(high))
                return false;

            // Update the pointers
            low++;
            high--;
        }

        return true;
    }

    // Driver code
    public static void main(String args[])
    {

        float n = 123.321f;

        if (isPalindrome(n))
            System.out.print("Yes");

        else
            System.out.print("No");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if num is palindrome
def isPalindrome(num) :

    # Convert the given floating point number
    # into a string
    s = str(num)

    # Pointers pointing to the first and
    # the last character of the string
    low = 0
    high = len(s) - 1

    while (low < high):

        # Not a palindrome
        if (s[low] != s[high]):
            return False

        # Update the pointers
        low += 1
        high -= 1

    return True

# Driver code
n = 123.321

if (isPalindrome(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true
    // if num is palindrome
    public static bool isPalindrome(float num)
    {

        // Convert the given floating point number
        // into a string
        string s = num.ToString();

        // Pointers pointing to the first and
        // the last character of the string
        int low = 0;
        int high = s.Length - 1;

        while (low < high)
        {

            // Not a palindrome
            if (s[low] != s[high])
                return false;

            // Update the pointers
            low++;
            high--;
        }
        return true;
    }

    // Driver code
    public static void Main()
    {
        float n = 123.321f;

        if (isPalindrome(n))
            Console.WriteLine("Yes");

        else
            Console.WriteLine("No");
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if num is palindrome
function isPalindrome(num)
{

    // Convert the given floating point number
    // into a string
    var s = num.toString();

    // Pointers pointing to the first and
    // the last character of the string
    var low = 0;
    var high = s.length - 1;

    while (low < high)
    {

        // Not a palindrome
        if (s[low] != s[high])
            return false;

        // Update the pointers
        low++;
        high--;
    }
    return true;
}

// Driver code
var n = 123.321;
if (isPalindrome(n))
    document.write( "Yes");
else
    document.write( "No");
</script>
```

**Output:** 

```
Yes
```

**时间复杂度** : O(N)。
**辅助空间** : O(1)。