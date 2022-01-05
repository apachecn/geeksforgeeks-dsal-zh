# 给定字符串中出现的连续数字组成的数字总和

> 原文:[https://www . geesforgeks . org/由给定字符串中的连续数字组成的数字总和/](https://www.geeksforgeeks.org/sum-of-numbers-formed-by-consecutive-digits-present-in-a-given-string/)

给定一个由数字**【0–9】**和小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是计算字符串 **S** 中出现的连续数字序列所代表的所有数字的总和。

**示例:**

> **输入:** S = "11aa32bbb5"
> **输出:** : 48
> **说明:**
> 字符串 S 中出现的连续数字序列为{11，32，5}。
> 因此，总和= 11 + 32 + 5 = 48
> 
> **输入:**s = " 5an 63 ff2 "
> T3】输出: 70

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **curr** ，来存储当前的连续数字序列
*   [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。
*   如果当前字符不是数字，将 **curr** 的当前值加到最后的**答案**中。将**电流**复位至 **0** 。
*   否则，将当前数字追加到**电流**中。
*   最后，返回最终答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum of
// numbers formed by consecutive
// sequences of digits present in the string
int sumOfDigits(string s)
{
    // Stores consecutive digits
    // present in the string
    int curr = 0;

    // Stores the sum
    int ret = 0;

    // Iterate over characters
    // of the input string
    for (auto& ch : s) {

        // If current character is a digit
        if (isdigit(ch)) {

            // Append current digit to curr
            curr = curr * 10 + ch - '0';
        }
        else {

            // Add curr to sum
            ret += curr;

            // Reset curr
            curr = 0;
        }
    }

    ret += curr;
    return ret;
}

// Driver Code
int main()
{
    string S = "11aa32bbb5";
    cout << sumOfDigits(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to calculate the sum of
  // numbers formed by consecutive
  // sequences of digits present in the string
  static int sumOfDigits(String s)
  {

    // Stores consecutive digits
    // present in the string
    int curr = 0;

    // Stores the sum
    int ret = 0;

    // Iterate over characters
    // of the input string
    for(char ch : s.toCharArray())
    {

      // If current character is a digit
      if (ch >= 48 && ch <= 57)
      {

        // Append current digit to curr
        curr = curr * 10 + ch - '0';
      }
      else
      {

        // Add curr to sum
        ret += curr;

        // Reset curr
        curr = 0;
      }
    }
    ret += curr;
    return ret;
  }

  // Driver Code
  public static void main(String[] args)
  {
    String S = "11aa32bbb5";
    System.out.print(sumOfDigits(S));
  }
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the sum of
# numbers formed by consecutive
# sequences of digits present in the string
def sumOfDigits(s) :

    # Stores consecutive digits
    # present in the string
    curr = 0

    # Stores the sum
    ret = 0

    # Iterate over characters
    # of the input string
    for ch in s :

        # If current character is a digit
        if (ord(ch) >= 48 and ord(ch) <= 57) :

            # Append current digit to curr
            curr = curr * 10 + ord(ch) - ord('0')

        else :

            # Add curr to sum
            ret += curr

            # Reset curr
            curr = 0

    ret += curr
    return ret

# Driver Code

S = "11aa32bbb5"
print(sumOfDigits(S))

# This code is contributed by code_hunt.
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{

    // Function to calculate the sum of
    // numbers formed by consecutive
    // sequences of digits present in the string
    static int sumOfDigits(string s)
    {

        // Stores consecutive digits
        // present in the string
        int curr = 0;

        // Stores the sum
        int ret = 0;

        // Iterate over characters
        // of the input string
        foreach(char ch in s)
        {

            // If current character is a digit
            if (ch >= 48 && ch <= 57)
            {

                // Append current digit to curr
                curr = curr * 10 + ch - '0';
            }
            else
            {

                // Add curr to sum
                ret += curr;

                // Reset curr
                curr = 0;
            }
        }
        ret += curr;
        return ret;
    }

  // Driver code
  static void Main() {
    string S = "11aa32bbb5";
    Console.WriteLine(sumOfDigits(S));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to calculate the sum of
// numbers formed by consecutive
// sequences of digits present in the string
function sumOfDigits(s)
{
    // Stores consecutive digits
    // present in the string
    var curr = 0;

    // Stores the sum
    var ret = 0;

    // Iterate over characters
    // of the input string
    s.split('').forEach(ch => {

        // If current character is a digit
        if (parseInt(ch)) {

            // Append current digit to curr
            curr = curr * 10 + ch.charCodeAt(0) - '0'.charCodeAt(0);
        }
        else {

            // Add curr to sum
            ret += curr;

            // Reset curr
            curr = 0;
        }
    });

    ret += curr;
    return ret;
}

// Driver Code
var S = "11aa32bbb5";
document.write( sumOfDigits(S));

// This code is contributed by importantly.
</script>
```

**Output:** 

```
48
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)