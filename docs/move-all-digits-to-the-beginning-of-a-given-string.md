# 将所有数字移动到给定字符串的开头

> 原文:[https://www . geeksforgeeks . org/将所有数字移动到给定字符串的开头/](https://www.geeksforgeeks.org/move-all-digits-to-the-beginning-of-a-given-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是将字符串中的所有数字移动到字符串的开头。

**示例:**

> **输入:**S = " geeks 4 forgek s123 "
> **输出:**4123 geeks forgeks
> **解释:**
> 给定字符串包含数字 4、1、2 和 3。将所有数字移到字符串的开头会将字符串修改为“4123GeeksforGeeks”。
> 
> **输入:**S**= "**geekforgesks 1234 A com 56 计算机科学门户 7 al "
> T5】输出:1234567 geekforgesks A 计算机科学门户

**方法:**思路是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并维护两个字符串，一个字符串包含**数字**，另一个字符串包含**非数字字符**。最后，按照要求的顺序将两个字符串都附加到结果中。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to move all the digit
    // to the beginning of the string
    static void moveAllDigitAtBeginning(
        String str)
    {
        // Calculate the string length
        int len = str.length();

        // Stores the digits
        StringBuilder digits
            = new StringBuilder();

        // Stores the non-numeric character
        StringBuilder nonNumericCharacter
            = new StringBuilder();

        // Traverse the string and
        // check if there is a digit
        for (char c : str.toCharArray()) {

            // If character is a digit,
            // add it to the string digits
            if (c >= 48 && c <= 57) {
                digits.append(c);
            }

            // Otherwise, add it to the
            // string nonNumericCharacter
            else {
                nonNumericCharacter.append(c);
            }
        }

        // Append both the strings
        digits.append(
            nonNumericCharacter.toString());

        // Print the string
        System.out.print(
            digits.toString() + " ");
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given String str
        String str
            = "GeeksforGeeks123";
        moveAllDigitAtBeginning(str);
    }
}
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to move all the digit
// to the beginning of the string
function moveAllDigitAtBeginning(str)
{

    // Calculate the string length
    var len = str.length;

    // Stores the digits
    var digits = [];

    // Stores the non-numeric character
    var nonNumericCharacter = [];

    // Traverse the string and
    // check if there is a digit
    var temp = str.split("");
    for(const c of temp)
    {

        // If character is a digit,
        // add it to the string digits
        if (c.charCodeAt(0) >= 48 &&
            c.charCodeAt(0) <= 57)
        {
            digits.push(c);
        }

        // Otherwise, add it to the
        // string nonNumericCharacter
        else
        {
            nonNumericCharacter.push(c);
        }
    }

    // Append both the strings
    digits.push(nonNumericCharacter.join(""));

    // Print the string
    document.write(digits.join("") + " ");
}

// Driver Code

// Given String str
var str = "GeeksforGeeks123";
moveAllDigitAtBeginning(str);

// This code is contributed by rdtank

</script>
```

**Output:** 

```
123GeeksforGeeks
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

[**正则表达式**](https://www.geeksforgeeks.org/regular-expressions-in-java/) **基于方法:**给定的问题也可以使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)解决，用空字符串 **(" ")** 代替所有非数字字符，用空字符串 **(" ")** 代替所有数字字符。最后，连接字符串并打印结果。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to move all the digit
    // at the beginning of the string
    static void moveAllDigitAtBeginning(
        String str)
    {
        // Replace all the non-numeric
        // characters with " " and
        // replace all digits with " "
        String moveAllDigit = str.replaceAll("\\D+", "")
                              + str.replaceAll("\\d+", "");

        // Print the string
        System.out.println(moveAllDigit);
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given String str
        String str
            = "GeeksforGeeks1234";
        moveAllDigitAtBeginning(str);
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Text.RegularExpressions;
public class GFG
{

    // Function to move all the digit
    // at the beginning of the string
    static void moveAllDigitAtBeginning(
        String str)
    {

        // Replace all the non-numeric
        // characters with " " and
        // replace all digits with " "
        String moveAllDigit = Regex.Replace(str, "\\D+", "")
            +Regex.Replace(str, "\\d", "");

        // Print the string
        Console.WriteLine(moveAllDigit);
    }

    // Driver Code
    public static void Main(String []args)
    {

        // Given String str
        String str
            = "GeeksforGeeks1234";
        moveAllDigitAtBeginning(str);
    }
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
1234GeeksforGeeks
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)