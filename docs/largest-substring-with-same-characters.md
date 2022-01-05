# 相同字符的最大子串

> 原文:[https://www . geeksforgeeks . org/最大相同字符子串/](https://www.geeksforgeeks.org/largest-substring-with-same-characters/)

给定一根大小为 **N** 的绳子 **s** 。任务是找到由相同字符组成的最大子串
**示例:**

> **输入:**s =【abcddddeff】
> T3】输出: 5
> 子串为【ddddddd】
> T7】输入:s = aabceebee
> **输出:** 3

**方法:**
从左到右遍历字符串。取两个变量**和**以及**温度**。如果当前元素与前一个元素相同，则增加**温度**。如果当前元素不等于前一个元素，则使**温度**为 **1** 并更新 **ans** 。
以下是上述方法的实施:

## C++

```
// CPP program to find largest sub
// string with same characters
#include <bits/stdc++.h>
using namespace std;

// Function to find largest sub
// string with same characters
int Substring(string s)
{

    int ans = 1, temp = 1;

    // Traverse the string
    for (int i = 1; i < s.size(); i++) {
        // If character is same as
        // previous increment temp value
        if (s[i] == s[i - 1]) {
            ++temp;
        }
        else {
            ans = max(ans, temp);
            temp = 1;
        }
    }
    ans = max(ans, temp);

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    string s = "abcdddddeff";

    // Function call
    cout << Substring(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest sub
// string with same characters
import java.util.*;

class GFG
{

// Function to find largest sub
// string with same characters
static int Substring(String s)
{
    int ans = 1, temp = 1;

    // Traverse the string
    for (int i = 1; i < s.length(); i++)
    {
        // If character is same as
        // previous increment temp value
        if (s.charAt(i) == s.charAt(i - 1))
        {
            ++temp;
        }
        else
        {
            ans = Math.max(ans, temp);
            temp = 1;
        }
    }
    ans = Math.max(ans, temp);

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String s = "abcdddddeff";

    // Function call
    System.out.println(Substring(s));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find largest sub
# with same characters

# Function to find largest sub
# with same characters
def Substring(s):

    ans, temp = 1, 1

    # Traverse the string
    for i in range(1, len(s)):

        # If character is same as
        # previous increment temp value
        if (s[i] == s[i - 1]):
            temp += 1
        else:
            ans = max(ans, temp)
            temp = 1

    ans = max(ans, temp)

    # Return the required answer
    return ans

# Driver code
s = "abcdddddeff"

# Function call
print(Substring(s))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find largest sub
// string with same characters
using System;
class GFG
{

// Function to find largest sub
// string with same characters
static int Substring(String s)
{
    int ans = 1, temp = 1;

    // Traverse the string
    for (int i = 1; i < s.Length; i++)
    {
        // If character is same as
        // previous increment temp value
        if (s[i] == s[i - 1])
        {
            ++temp;
        }
        else
        {
            ans = Math.Max(ans, temp);
            temp = 1;
        }
    }
    ans = Math.Max(ans, temp);

    // Return the required answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String s = "abcdddddeff";

    // Function call
    Console.WriteLine(Substring(s));
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest sub
// string with same characters

// Function to find largest sub
// string with same characters
function Substring($s)
{
    $ans = 1;
    $temp = 1;

    // Traverse the string
    for ($i = 1; $i < strlen($s); $i++)
    {

        // If character is same as
        // previous increment temp value
        if ($s[$i] == $s[$i - 1])
        {
            ++$temp;
        }
        else
        {
            $ans = max($ans, $temp);
            $temp = 1;
        }
    }

    $ans = max($ans, $temp);

    // Return the required answer
    return $ans;
}

// Driver code
$s = "abcdddddeff";

// Function call
echo Substring($s);

// This code is contributed by Naman_Garg
?>
```

## java 描述语言

```
<script>

// Javascript program to find largest sub
// string with same characters

// Function to find largest sub
// string with same characters
function Substring(s)
{

    var ans = 1, temp = 1;

    // Traverse the string
    for (var i = 1; i < s.length; i++) {
        // If character is same as
        // previous increment temp value
        if (s[i] == s[i - 1]) {
            ++temp;
        }
        else {
            ans = Math.max(ans, temp);
            temp = 1;
        }
    }
    ans = Math.max(ans, temp);

    // Return the required answer
    return ans;
}

// Driver code
var s = "abcdddddeff";
// Function call
document.write( Substring(s));

</script>
```

**输出:**

```
5
```

**时间复杂度** : O(N)