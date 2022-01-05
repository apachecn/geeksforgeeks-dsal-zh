# 检查字符串是否代表十六进制数

> 原文:[https://www . geesforgeks . org/check-if-a-string-press-a-十六进制-number-or-not/](https://www.geeksforgeeks.org/check-if-a-string-represents-a-hexadecimal-number-or-not/)

给定一个长度为 **N** 的字母数字[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是检查给定的字符串是否代表一个[十六进制数](https://www.geeksforgeeks.org/program-to-convert-hexadecimal-number-to-binary/)。如果表示十六进制数，打印**是**。否则，打印**否**。

**示例:**

> **输入:** S = "BF57C"
> **输出:**是
> **解释:**
> 给定字符串的十进制表示= 783740
> 
> **输入:**S = " 58GK "
> T3】输出:否

**方法:**该方法基于以下思想:十六进制数的所有元素位于字符 **A 到 F** 之间或整数 **0 到 9** 之间。以下是解决问题的步骤:

1.  [迭代给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。
2.  检查字符串的每个字符是在字符 **A 到 F** 之间还是在 0 到 9 之间。
3.  如果发现为真，则打印**是**。
4.  否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the string
// represents a hexadecimal number
void checkHex(string s)
{

    // Size of string
    int n = s.length();

    // Iterate over string
    for(int i = 0; i < n; i++)
    {
        char ch = s[i];

        // Check if the character
        // is invalid
        if ((ch < '0' || ch > '9') &&
            (ch < 'A' || ch > 'F'))
        {
            cout << "No" << endl;
            return;
        }
    }

    // Print true if all
    // characters are valid
    cout << "Yes" << endl;
}

// Driver code    
int main()
{

    // Given string
    string s = "BF57C";

    // Function call
    checkHex(s);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;
import java.io.*;

class GFG {

    // Function to check if the string
    // represents a hexadecimal number
    public static void checkHex(String s)
    {
        // Size of string
        int n = s.length();

        // Iterate over string
        for (int i = 0; i < n; i++) {

            char ch = s.charAt(i);

            // Check if the character
            // is invalid
            if ((ch < '0' || ch > '9')
                && (ch < 'A' || ch > 'F')) {

                System.out.println("No");
                return;
            }
        }

        // Print true if all
        // characters are valid
        System.out.println("Yes");
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string
        String s = "BF57C";

        // Function Call
        checkHex(s);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to check if the string
# represents a hexadecimal number
def checkHex(s):

    # Iterate over string
    for ch in s:

        # Check if the character
        # is invalid
        if ((ch < '0' or ch > '9') and
            (ch < 'A' or ch > 'F')):

            print("No")
            return

    # Print true if all
    # characters are valid
    print("Yes")

# Driver Code

# Given string
s = "BF57C"

# Function call
checkHex(s)

# This code is contributed by extragornax
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to check if the string
// represents a hexadecimal number
public static void checkHex(String s)
{
  // Size of string
  int n = s.Length;

  // Iterate over string
  for (int i = 0; i < n; i++)
  {
    char ch = s[i];

    // Check if the character
    // is invalid
    if ((ch < '0' || ch > '9') &&
        (ch < 'A' || ch > 'F'))
    {
      Console.WriteLine("No");
      return;
    }
  }

  // Print true if all
  // characters are valid
  Console.WriteLine("Yes");
}

// Driver Code
public static void Main(String[] args)
{
  // Given string
  String s = "BF57C";

  // Function Call
  checkHex(s);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function to check if the string
// represents a hexadecimal number
function checkHex(s)
{

    // Size of string
    let n = s.length;

    // Iterate over string
    for(let i = 0; i < n; i++)
    {
        let ch = s[i];

        // Check if the character
        // is invalid
        if ((ch < '0' || ch > '9') &&
            (ch < 'A' || ch > 'F'))
        {
            document.write("No");
            return;
        }
    }

    // Print true if all
    // characters are valid
    document.write("Yes");
}

// Driver code

// Given string
let s = "BF57C";

// Function Call
checkHex(s);

// This code is contributed by souravghosh0416

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)