# 检查一个字符串是否可以拆分成以 N 开头，后跟 N 个字符的子字符串

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-split-in-substrings-以-n 开头，后跟-n-characters/](https://www.geeksforgeeks.org/check-if-a-string-can-be-split-into-substrings-starting-with-n-followed-by-n-characters/)

给定一个字符串 **str** ，任务是检查它是否可以被分成子字符串，使得每个子字符串都以一个数值开始，后跟由该数字整数表示的多个字符。

**示例:**

> **输入:**str = " 4g12y 6hunter "
> **输出:**是
> **说明:**
> 子串“4g 12y”和“6 unter”满足给定条件
> 
> **输入:** str = "31ba2a"
> **输出:**否
> **说明:**
> 整个字符串不能拆分成所需类型的子字符串

**进场:**

*   检查不可能分割时的条件:
*   如果给定的字符串不以数字开头。
*   如果子字符串开头的整数大于剩余子字符串中后续字符的总数。
*   如果以上两个条件都不满足，答案肯定是可以的。因此递归地寻找子串。

下面是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given
// can be split into desired
// substrings
bool helper(string& s, int pos)
{
    // Length of the string
    int len = s.size();

    if (pos >= len)
        return true;

    if (!isdigit(s[pos]))
        return false;

    int num = 0;

    // Traverse the string
    for (int i = pos; i < len; i++) {

        // Extract the digit
        num = num * 10 + s[pos] - '0';

        // Check if the extracted number
        // does not exceed the remaining
        // length
        if (i + 1 + num > len)
            return false;

        // Check for the remaining
        // string
        if (helper(s, i + 1 + num))
            return true;
    }

    // If generating desired
    // substrings is not possible
    return false;
}

// Driver Code
int main()
{
    string s = "123abc4db1c";
    if (helper(s, 0))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the 
// above approach 
import java.util.*;

class GFG{

// Function to check if the given 
// can be split into desired 
// substrings 
public static boolean helper(String s, int pos) 
{ 

    // Length of the string 
    int len = s.length(); 

    if (pos >= len) 
        return true; 
    if (!Character.isDigit(s.charAt(pos)))
        return false; 

    int num = 0; 

    // Traverse the string 
    for(int i = pos; i < len; i++)
    {

       // Extract the digit 
       num = num * 10 + s.charAt(pos) - '0'; 

       // Check if the extracted number 
       // does not exceed the remaining 
       // length 
       if (i + 1 + num > len) 
           return false; 

       // Check for the remaining 
       // string 
       if (helper(s, i + 1 + num)) 
           return true; 
    } 

    // If generating desired 
    // substrings is not possible 
    return false; 
} 

// Driver code
public static void main (String[] args)
{
    String s = "123abc4db1c"; 

    if (helper(s, 0)) 
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function to check if the given
# can be split into desired
# substrings
def helper(s, pos):

    # Length of the string
    size = len(s)

    if(pos >= size):
        return True

    if(s[pos].isdigit() == False):
        return False

    num = 0

    # Traverse the string
    for i in range(pos, size):

        # Extract the digit
        num = num * 10 + ord(s[pos]) - 48

        # Check if the extracted number
        # does not exceed the remaining
        # length
        if (i + 1 + num > size):
            return False

        # Check for the remaining
        # string
        if (helper(s, i + 1 + num)):
            return True

    # If generating desired
    # substrings is not possible
    return False

# Driver Code
s = "123abc4db1c";

if (helper(s, 0)):
    print("Yes")
else:
    print("No")

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to implement the 
// above approach 
using System;

class GFG{

// Function to check if the given 
// can be split into desired 
// substrings 
public static bool helper(String s, int pos) 
{ 

    // Length of the string 
    int len = s.Length; 

    if (pos >= len) 
        return true; 
    if (!char.IsDigit(s[pos]))
        return false; 

    int num = 0; 

    // Traverse the string 
    for(int i = pos; i < len; i++)
    {

       // Extract the digit 
       num = num * 10 + s[pos] - '0'; 

       // Check if the extracted number 
       // does not exceed the remaining 
       // length 
       if (i + 1 + num > len) 
           return false; 

       // Check for the remaining 
       // string 
       if (helper(s, i + 1 + num)) 
           return true; 
    } 

    // If generating desired 
    // substrings is not possible 
    return false; 
} 

// Driver code
public static void Main(String[] args)
{
    String s = "123abc4db1c"; 

    if (helper(s, 0)) 
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by amal kumar choubey
```

**Output:**

```
Yes

```

 ***时间复杂度:**O(N)
T5】辅助空间: O(1)*