# 将不平衡的括号序列转换为平衡的序列

> 原文:[https://www . geesforgeks . org/convert-a-不平衡-括号-序列-a-平衡-序列/](https://www.geeksforgeeks.org/convert-an-unbalanced-bracket-sequence-to-a-balanced-sequence/)

给定一个不平衡的括号序列**'(****)'**，通过在字符串的开头加上最小数量的**'(**)和在字符串的结尾加上 **')'** ，将其转换成一个平衡序列。

**示例:**

> **输入:**str =()))()”
> T3】输出:“((()))(”
> 
> **输入:**str =())()(())()))“
> **输出:**”(((())())()()))”

**进场:**

*   让我们假设，每当我们遇到开括号时，深度增加一，当遇到闭括号时，深度减少一。
*   在 minDep 中找到最大负深度，并在开头加上 **'('** )这个数字。
*   然后循环新的序列，找到字符串末尾需要的**)**的数量并相加。
*   最后，返回字符串。

以下是该方法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return balancedBrackets string
string balancedBrackets(string str)
{
    // Initializing dep to 0
    int dep = 0;

    // Stores maximum negative depth
    int minDep = 0;

    for (int i = 0; i < str.length(); i++)
    {
        if (str[i] == '(')
            dep++;
        else
            dep--;

        // if dep is less than minDep
        if (minDep > dep)
            minDep = dep;
    }

    // if minDep is less than 0 then there
    // is need to add '(' at the front
    if (minDep < 0)
    {
        for (int i = 0; i < abs(minDep); i++)
            str = '(' + str;
    }

    // Reinitializing to check the updated string
    dep = 0;

    for (int i = 0; i < str.length(); i++)
    {
        if (str[i] == '(')
            dep++;
        else
            dep--;
    }

    // if dep is not 0 then there
    // is need to add ')' at the back
    if (dep != 0)
    {
        for (int i = 0; i < dep; i++)
            str = str + ')';
    }
    return str;
}

// Driver code
int main()
{
    string str = ")))()";
    cout << balancedBrackets(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return balancedBrackets string
    static String balancedBrackets(String str)
    {
        // Initializing dep to 0
        int dep = 0;

        // Stores maximum negative depth
        int minDep = 0;

        for (int i = 0; i < str.length(); i++)
        {
            if (str.charAt(i) == '(')
                dep++;
            else
                dep--;

            // if dep is less than minDep
            if (minDep > dep)
                minDep = dep;
        }

        // if minDep is less than 0 then there
        // is need to add '(' at the front
        if (minDep < 0)
        {
            for (int i = 0; i < Math.abs(minDep); i++)
                str = '(' + str;
        }

        // Reinitializing to check the updated string
        dep = 0;

        for (int i = 0; i < str.length(); i++)
        {
            if (str.charAt(i) == '(')
                dep++;
            else
                dep--;
        }

        // if dep is not 0 then there
        // is need to add ')' at the back
        if (dep != 0)
        {
            for (int i = 0; i < dep; i++)
                str = str + ')';
        }
        return str;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = ")))()";
        System.out.println(balancedBrackets(str));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return balancedBrackets String

def balancedBrackets(Str):

    # Initializing dep to 0
    dep = 0

    # Stores maximum negative depth
    minDep = 0

    for i in Str:
        if (i == '('):
            dep += 1
        else:
            dep -= 1

        # if dep is less than minDep
        if (minDep > dep):
            minDep = dep

    # if minDep is less than 0 then there
    # is need to add '(' at the front
    if (minDep < 0):
        for i in range(abs(minDep)):
            Str = '(' + Str

    # Reinitializing to check the updated String
    dep = 0

    for i in Str:
        if (i == '('):
            dep += 1
        else:
            dep -= 1

    # if dep is not 0 then there
    # is need to add ')' at the back
    if (dep != 0):
        for i in range(dep):
            Str = Str + ')'

    return Str

# Driver code
Str = ")))()"
print(balancedBrackets(Str))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return balancedBrackets string
    static string balancedBrackets(string str)
    {
        // Initializing dep to 0
        int dep = 0;

        // Stores maximum negative depth
        int minDep = 0;

        for (int i = 0; i < str.Length; i++)
        {
            if (str[i] == '(')
                dep++;
            else
                dep--;

            // if dep is less than minDep
            if (minDep > dep)
                minDep = dep;
        }

        // if minDep is less than 0 then there
        // is need to add '(' at the front
        if (minDep < 0)
        {
            for (int i = 0; i < Math.Abs(minDep); i++)
                str = '(' + str;
        }

        // Reinitializing to check the updated string
        dep = 0;

        for (int i = 0; i < str.Length; i++)
        {
            if (str[i] == '(')
                dep++;
            else
                dep--;
        }

        // if dep is not 0 then there
        // is need to add ')' at the back
        if (dep != 0)
        {
            for (int i = 0; i < dep; i++)
                str = str + ')';
        }
        return str;
    }

    // Driver code
    public static void Main()
    {
        String str = ")))()";
        Console.WriteLine(balancedBrackets(str));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return balancedBrackets string
      function balancedBrackets(str) {
        // Initializing dep to 0
        var dep = 0;

        // Stores maximum negative depth
        var minDep = 0;

        for (var i = 0; i < str.length; i++) {
          if (str[i] === "(") dep++;
          else dep--;

          // if dep is less than minDep
          if (minDep > dep) minDep = dep;
        }

        // if minDep is less than 0 then there
        // is need to add '(' at the front
        if (minDep < 0) {
          for (var i = 0; i < Math.abs(minDep); i++) str = "(" + str;
        }

        // Reinitializing to check the updated string
        dep = 0;

        for (var i = 0; i < str.length; i++) {
          if (str[i] === "(") dep++;
          else dep--;
        }

        // if dep is not 0 then there
        // is need to add ')' at the back
        if (dep !== 0) {
          for (var i = 0; i < dep; i++) str = str + ")";
        }
        return str;
      }

      // Driver code
      var str = ")))()";
      document.write(balancedBrackets(str));
    </script>
```

**Output**

```
((()))()
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)