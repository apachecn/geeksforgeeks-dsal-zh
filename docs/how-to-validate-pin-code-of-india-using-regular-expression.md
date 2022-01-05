# 如何使用正则表达式

验证印度的 pin 码

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证印度 pin 码/](https://www.geeksforgeeks.org/how-to-validate-pin-code-of-india-using-regular-expression/)

给定一个从 **0 到 9** 的正数**字符串**，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查该数字是否有效 **pin 码**。

> 印度的有效个人识别码必须满足以下条件。
> 
> 1.  只能是六位数。
> 2.  不应该从零开始。
> 3.  pin 码的第一个数字必须从 1 到 9。
> 4.  pin 码的下五位数字的范围可以从 0 到 9。
> 5.  它应该只允许一个空格，但是在三位数之后，虽然这是可选的。

**示例:**

> **输入:** num = "132103"
> **输出:**真
> **说明:**
> 给定的数满足上述所有条件。
> 
> **输入:** num = "201 305"
> **输出:**真
> **说明:**
> 给定的数满足上述所有条件。
> 
> **输入:** num = "014205"
> **输出:**假
> **说明:**
> 给定的数字以零开始，因此不是印度的有效 pin 码。
> 
> **输入:** num = "1473598"
> **输出:**假
> **说明:**
> 给定的数字包含 7 位数字，因此不是印度的有效 pin 码。

**方法:**这个问题可以用正则表达式来解决。

1.拿到号码。

2.如下所述，创建一个正则表达式来验证印度的 pin 码:

```

regex = "^[1-9]{1}[0-9]{2}\\s{0, 1}[0-9]{3}{content}quot;;
```

其中:

*   **^** 代表数字的开始。
*   **[1-9]{1}** 代表从 1 到 9 的 pin 码的起始数字。
*   **[0-9]{2}** 表示 pin 码中从 0 到 9 范围内的下两位数字。
*   **\\s{0，1}** 表示 pin 码中可能出现一次或永远不会出现的空白。
*   **[0-9]{3}** 表示 0 到 9 范围内的 pin 码的最后三位数字。
*   **$** 代表数字的结束。

3.用正则表达式匹配给定的数字，在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。

4.如果数字与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现。

## C++

```
// C++ program to validate the pin code
// of India using Regular Expression.
#include <bits/stdc++.h>
using namespace std;

// Function to validate the pin code of India.
bool isValidPinCode(string pinCode)
{

    // Regex to check valid pin code of India.
    const regex pattern("^[1-9]{1}[0-9]{2}\\s{0,1}[0-9]{3}{content}quot;);

    // If the pin code is empty
    // return false
    if (pinCode.empty())
    {
        return false;
    }

    // Return true if the pin code
    // matched the ReGex
    if (regex_match(pinCode, pattern))
    {
        return true;
    }
    else
    {
        return false;
    }
}

void print(bool n)
{
    if (n == 0)
    {
        cout << "False" << endl;
    }
    else
    {
        cout << "True" << endl;
    }
}

// Driver Code.
int main()
{

    // Test Case 1:
    string num1 = "132103";
    cout << num1 + ": ";
    print(isValidPinCode(num1));

    // Test Case 2:
    string num2 = "201 305";
    cout << num2 + ": ";
    print(isValidPinCode(num2));

    // Test Case 3:
    string num3 = "014205";
    cout << num3 + ": ";
    print(isValidPinCode(num3));

    // Test Case 4:
    string num4 = "1473598";
    cout << num4 + ": ";
    print(isValidPinCode(num4));

    return 0;
}

// This code is contributed by nirajgusain5
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate the pin code
// of India using Regular Expression.

import java.util.regex.*;

class GFG {

    // Function to validate the pin code of India.
    public static boolean isValidPinCode(String pinCode)
    {

        // Regex to check valid pin code of India.
        String regex
            = "^[1-9]{1}[0-9]{2}\\s{0,1}[0-9]{3}{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the pin code is empty
        // return false
        if (pinCode == null) {
            return false;
        }

        // Pattern class contains matcher() method
        // to find matching between given pin code
        // and regular expression.
        Matcher m = p.matcher(pinCode);

        // Return if the pin code
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String num1 = "132103";
        System.out.println(
            num1 + ": "
            + isValidPinCode(num1));

        // Test Case 2:
        String num2 = "201 305";
        System.out.println(
            num2 + ": "
            + isValidPinCode(num2));

        // Test Case 3:
        String num3 = "014205";
        System.out.println(
            num3 + ": "
            + isValidPinCode(num3));

        // Test Case 4:
        String num4 = "1473598";
        System.out.println(
            num4 + ": "
            + isValidPinCode(num4));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate the 
# pin code of India using Regular
# Expression.
import re

# Function to validate the pin code
# of India.
def isValidPinCode(pinCode):

    # Regex to check valid pin code
    # of India.
    regex = "^[1-9]{1}[0-9]{2}\\s{0,1}[0-9]{3}{content}quot;;

    # Compile the ReGex
    p = re.compile(regex);

    # If the pin code is empty
    # return false
    if (pinCode == ''):
        return False;

    # Pattern class contains matcher() method
    # to find matching between given pin code
    # and regular expression.
    m = re.match(p, pinCode);

    # Return True if the pin code
    # matched the ReGex else False
    if m is None:
        return False
    else:
        return True

# Driver code
if __name__ == "__main__":

    # Test case 1
    num1 = "132103";
    print(num1, ": ", isValidPinCode(num1));

    # Test case 2:
    num2 = "201 305";
    print(num2, ": ", isValidPinCode(num2));

    # Test case 3:
    num3 = "014205";
    print(num3, ": ", isValidPinCode(num3));

    # Test case 4:
    num4 = "1473598";
    print(num4, ": ", isValidPinCode(num4));

# This code is contributed by AnkitRai01
```

**Output:** 

```
132103: true
201 305: true
014205: false
1473598: false
```