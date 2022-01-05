# 通过替换将数字字符串修改为平衡括号

> 原文:[https://www . geesforgeks . org/modify-a-numeric-string-to-balanced-by-replacements/](https://www.geeksforgeeks.org/modify-a-numeric-string-to-a-balanced-parentheses-by-replacements/)

给定一个仅由字符**“1”、“2”**和**“3”**组成的数字[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是用一个开括号(**(**)或一个闭括号(**)**)替换字符，这样新形成的字符串就变成了[一个平衡的括号序列](https://www.geeksforgeeks.org/check-if-given-parentheses-expression-is-balanced-or-not/)。

***注意:**一个字符的所有出现都必须用相同的括号替换。*

**示例:**

> **输入:** S = "1123"
> **输出:**是，(()
> **解释:**将字符“1”的出现替换为“(”、“2”替换为“)”和“3”替换为“)”。因此，得到的括号序列是”(())，这是平衡的。
> 
> **输入:**S = " 1121 "
> T3】输出:否

**方法:**给定的问题可以基于以下观察来解决:

*   对于[平衡括号序列](https://www.geeksforgeeks.org/check-if-given-parentheses-expression-is-balanced-or-not/)，第一个和最后一个字符必须分别为**打开**和**关闭**括号。所以**第一个和最后一个字符应该是不同的。**
*   如果一个字符串的**第一个**和**最后一个**字符相同，那么就不可能得到一个平衡的括号序列。
*   如果一个字符串的第一个**和最后一个**字符不同，则分别由**打开**和**关闭**括号来代替。第三个**字符由**打开**或**关闭**支架代替。******
*   对于剩余的**第三个**字符，逐一检查两种替换方式。
*   如果第三个**剩余字符的两个替换都不能构成一个平衡的括号序列，那么就不可能构成一个平衡的括号序列。**

按照以下步骤解决给定的问题:

*   检查字符串 **S** 的**第一个**和**最后一个**字符是否等于**。如果发现是真的，则打印**“否”**并返回。**
*   **初始化两个变量，比如 **cntforOpen** 和 **cntforClose** ，来存储开括号和闭括号的计数。**
*   **[迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并执行以下操作:

    *   如果当前字符与字符串的第一个字符相同，则递增 **cntforOpen。**
    *   如果当前字符与字符串的最后一个字符相同，则递减 **cntforOpen。**
    *   对于剩余的第三个字符，递增 **cntforOpen** ，即将该字符替换为**(“**)。
    *   如果在任何时刻 **cntforOpen** 被发现为负，则不能获得平衡的括号序列。** 
*   **同样，使用 **cntforClose** 变量进行检查，即将第三个字符替换为 **')'** 。**
*   **如果以上两种方法都没有生成平衡括号序列，则打印**“否”**。否则，打印**“是”。****

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if the given
// string can be converted to a
// balanced bracket sequence or not
void balBracketSequence(string str)
{
    int n = str.size();

    // Check if the first and
    // last characters are equal
    if (str[0]
        == str[n - 1])

    {
        cout << "No" << endl;
    }
    else {

        // Initialize two variables to store
        // the count of open and closed brackets
        int cntForOpen = 0, cntForClose = 0;
        int check = 1;
        for (int i = 0; i < n; i++) {

            // If the current character is
            // same as the first character
            if (str[i] == str[0])
                cntForOpen++;

            // If the current character is
            // same as the last character
            else if (str[i] == str[n - 1])
                cntForOpen--;
            else
                cntForOpen++;

            // If count of open brackets
            // becomes less than 0
            if (cntForOpen < 0) {
                check = 0;
                break;
            }
        }
        if (check && cntForOpen == 0) {
            cout << "Yes, ";

            // Print the new string
            for (int i = 0; i < n; i++) {
                if (str[i] == str[n - 1])
                    cout << ')';
                else
                    cout << '(';
            }
            return;
        }
        else {
            for (int i = 0; i < n; i++) {

                // If the current character is
                // same as the first character
                if (str[i] == str[0])
                    cntForClose++;
                else
                    cntForClose--;

                // If bracket sequence
                // is not balanced
                if (cntForClose
                    < 0) {
                    check = 0;
                    break;
                }
            }

            // Check for unbalanced
            // bracket sequence
            if (check
                && cntForClose
                       == 0) {
                cout << "Yes, ";

                // Print the sequence
                for (int i = 0; i < n;
                     i++) {
                    if (str[i] == str[0])
                        cout << '(';
                    else
                        cout << ')';
                }
                return;
            }
        }
        cout << "No";
    }
}

// Driver Code
int main()
{
    // Given Input
    string str = "123122";

    // Function Call
    balBracketSequence(str);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if the given
// string can be converted to a
// balanced bracket sequence or not
static void balBracketSequence(String str)
{
    int n = str.length();

    // Check if the first and
    // last characters are equal
    if (str.charAt(0)
        == str.charAt(n - 1))

    {
        System.out.println("No");
    }
    else {

        // Initialize two variables to store
        // the count of open and closed brackets
        int cntForOpen = 0, cntForClose = 0;
        int check = 1;
        for (int i = 0; i < n; i++) {

            // If the current character is
            // same as the first character
            if (str.charAt(i) == str.charAt(0))
                cntForOpen++;

            // If the current character is
            // same as the last character
            else if (str.charAt(i) == str.charAt(n - 1))
                cntForOpen -= 1;
            else
                cntForOpen += 1;

            // If count of open brackets
            // becomes less than 0
            if (cntForOpen < 0) {
                check = 0;
                break;
            }
        }
        if (check != 0 && cntForOpen == 0) {
            System.out.print("Yes, ");

            // Print the new string
            for (int i = 0; i < n; i++) {
                if (str.charAt(i) == str.charAt(n - 1))
                    System.out.print(')');
                else
                   System.out.print('(');
            }
            return;
        }
        else {
            for (int i = 0; i < n; i++) {

                // If the current character is
                // same as the first character
                if (str.charAt(i) == str.charAt(0))
                    cntForClose++;
                else
                    cntForClose--;

                // If bracket sequence
                // is not balanced
                if (cntForClose
                    < 0) {
                    check = 0;
                    break;
                }
            }

            // Check for unbalanced
            // bracket sequence
            if (check != 0
                && cntForClose
                       == 0) {
                System.out.print("Yes, ");

                // Print the sequence
                for (int i = 0; i < n;
                     i++) {
                    if (str.charAt(i) == str.charAt(0))
                       System.out.print('(');
                    else
                        System.out.print(')');
                }
                return;
            }
        }
        System.out.print("No");
    }
}

// Driver Code
public static void main(String args[])
{
    // Given Input
    String str = "123122";

    // Function Call
    balBracketSequence(str);
}
}

// This code is contributed by ipg2016107.
```

## **蟒蛇 3**

```
# Python program for the above approach;
# Function to check if the given
# string can be converted to a
# balanced bracket sequence or not
def balBracketSequence(str):
    n = len(str)

    # Check if the first and
    # last characters are equal
    if (str[0] == str[n - 1]):
        print("No", end="")
    else:

        # Initialize two variables to store
        # the count of open and closed brackets
        cntForOpen = 0
        cntForClose = 0
        check = 1

        for i in range(n):

            # If the current character is
            # same as the first character
            if (str[i] == str[0]):
                cntForOpen += 1

            # If the current character is
            # same as the last character
            elif str[i] == str[n - 1] :
                cntForOpen -= 1
            else:
                cntForOpen += 1

            # If count of open brackets
            # becomes less than 0
            if (cntForOpen < 0):
                check = 0
                break

        if (check and cntForOpen == 0):
            print("Yes, ", end="")

            # Print the new string
            for i in range(n):
                if (str[i] == str[n - 1]):
                    print(')', end="")
                else:
                    print('(', end="")

            return

        else:
            for i in range(n):

                # If the current character is
                # same as the first character
                if (str[i] == str[0]):
                    cntForClose += 1
                else:
                    cntForClose -= 1

                # If bracket sequence
                # is not balanced
                if (cntForClose < 0):
                    check = 0
                    break

            # Check for unbalanced
            # bracket sequence
            if (check and cntForClose == 0):
                print("Yes, ", end="")

                # Print the sequence
                for i in range(n):
                    if (str[i] == str[0]):
                        print('(', end="") 
                    else:
                        print(')', end="")

                return

        print("NO", end="")

# Driver Code

# Given Input
str = "123122"

# Function Call
balBracketSequence(str)

# This code is contributed by gfgking
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if the given
// string can be converted to a
// balanced bracket sequence or not
static void balBracketSequence(string str)
{
    int n = str.Length;

    // Check if the first and
    // last characters are equal
    if (str[0] == str[n - 1])
    {
        Console.Write("No");
    }
    else
    {

        // Initialize two variables to store
        // the count of open and closed brackets
        int cntForOpen = 0, cntForClose = 0;
        int check = 1;

        for(int i = 0; i < n; i++)
        {

            // If the current character is
            // same as the first character
            if (str[i] == str[0])
                cntForOpen++;

            // If the current character is
            // same as the last character
            else if (str[i] == str[n - 1])
                cntForOpen--;
            else
                cntForOpen++;

            // If count of open brackets
            // becomes less than 0
            if (cntForOpen < 0)
            {
                check = 0;
                break;
            }
        }
        if (check != 0 && cntForOpen == 0)
        {
            Console.Write("Yes, ");

            // Print the new string
            for(int i = 0; i < n; i++)
            {
                if (str[i] == str[n - 1])
                    Console.Write(')');
                else
                    Console.Write('(');
            }
            return;
        }
        else
        {
            for(int i = 0; i < n; i++)
            {

                // If the current character is
                // same as the first character
                if (str[i] == str[0])
                    cntForClose++;
                else
                    cntForClose--;

                // If bracket sequence
                // is not balanced
                if (cntForClose < 0)
                {
                    check = 0;
                    break;
                }
            }

            // Check for unbalanced
            // bracket sequence
            if (check != 0 && cntForClose == 0)
            {
                Console.Write("Yes, ");

                // Print the sequence
                for(int i = 0; i < n; i++)
                {
                    if (str[i] == str[0])
                        Console.Write('(');
                    else
                        Console.Write(')');
                }
                return;
            }
        }
        Console.Write("No");
    }
}

// Driver Code
public static void Main()
{

    // Given Input
    string str = "123122";

    // Function Call
    balBracketSequence(str);
}
}

// This code is contributed by sanjoy_62
```

## **java 描述语言**

```
<script>

        // JavaScript program for the above approach;
// Function to check if the given
// string can be converted to a
// balanced bracket sequence or not
function balBracketSequence(str)
{
    let n = str.length;

    // Check if the first and
    // last characters are equal
    if (str[0]
        == str[n - 1])

    {
        document.write( "No");
    }
    else {

        // Initialize two variables to store
        // the count of open and closed brackets
        let cntForOpen = 0, cntForClose = 0;
        let check = 1;
        for (let i = 0; i < n; i++) {

            // If the current character is
            // same as the first character
            if (str[i] == str[0])
                cntForOpen++;

            // If the current character is
            // same as the last character
            else if (str[i] == str[n - 1])
                cntForOpen--;
            else
                cntForOpen++;

            // If count of open brackets
            // becomes less than 0
            if (cntForOpen < 0) {
                check = 0;
                break;
            }
        }
        if (check && cntForOpen == 0) {
            document.write("Yes, ");

            // Print the new string
            for (let i = 0; i < n; i++) {
                if (str[i] == str[n - 1])
                    document.write(')');
                else
                    document.write('(');
            }
            return;
        }
        else {
            for (let i = 0; i < n; i++) {

                // If the current character is
                // same as the first character
                if (str[i] == str[0])
                    cntForClose++;
                else
                    cntForClose--;

                // If bracket sequence
                // is not balanced
                if (cntForClose
                    < 0) {
                    check = 0;
                    break;
                }
            }

            // Check for unbalanced
            // bracket sequence
            if (check
                && cntForClose
                       == 0) {
                document.write("Yes, ");

                // Print the sequence
                for (let i = 0; i < n;
                     i++) {
                    if (str[i] == str[0])
                        document.write('(');
                    else
                        document.write(')');
                }
                return;
            }
        }
       document.write("NO") ;
    }
}

// Driver Code

    // Given Input
    let str = "123122";

    // Function Call
    balBracketSequence(str);

   // This code is contributed by Potta Lokesh
    </script>
```

****Output:** 

```
Yes, ()(())
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**