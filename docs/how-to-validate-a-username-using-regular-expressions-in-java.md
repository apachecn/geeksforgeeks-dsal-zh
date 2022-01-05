# 如何在 Java 中使用正则表达式验证用户名

> 原文:[https://www . geesforgeks . org/如何使用 java 正则表达式验证用户名/](https://www.geeksforgeeks.org/how-to-validate-a-username-using-regular-expressions-in-java/)

给定一个代表用户名的字符串 **str** ，任务是在[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)的帮助下验证这个用户名。

如果满足以下所有约束，则用户名被视为有效:

*   用户名由 **6** 到 **30** 个字符组成。如果用户名
    少于 6 个字符或多于 30 个字符，则该用户名无效。
*   用户名只能包含字母数字字符和下划线(_)。字母数字字符描述由小写字符**【A–Z】**、大写字符**【A–Z】**和数字**【0–9】**组成的字符集。
*   用户名的第一个字符必须是字母字符，即小写字符 **【A–Z】**或大写字符**【A–Z】**。

**示例:**

> **输入:** str = "1Geeksforgeeks"
> **输出:**假
> **解释:**
> 给定的用户名无效，因为它以数字开头。
> 
> **输入:**str = " Geeksforgeeks _ 21 "
> **输出:**真
> **说明:**
> 给定的用户名满足上述所有条件。
> 
> **输入:** str = "Geeksforgeeks？10 _ 2A“
> **输出:**假
> **解释:**
> 给定的用户名无效，因为它包含无效字符“？”。

**方法:**想法是使用[正则表达式](https://www.geeksforgeeks.org/regular-expressions-in-java/)来验证给定的用户名是否有效。可以按照以下步骤计算答案:

1.  去拿绳子。
2.  Form a regular expression to validate the given string. According to the conditions, the regular expression can be formed in the following way:

    ```
    regex = "^[A-Za-z]\\w{5, 29}{content}quot;

    ```

    其中:

    *   “^”代表字符串起始字符。
    *   “[A-Za-z]”确保起始字符是小写或大写字母。
    *   " \\w{5，29} "表示检查以确保剩余的项是 word 项，包括下划线，直到它到达末尾并用$表示。
    *   “{5，29}”表示给我们的 6-30 个字符的约束减去预定义的第一个字符。
3.  将字符串与 Regex 匹配。在 Java 中，这可以使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。
4.  如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

```
// Java program to validate a username
// using Regular Expression or ReGex

import java.util.regex.*;

class GFG {

    // Function to validate the username
    public static boolean isValidUsername(String name)
    {

        // Regex to check valid username.
        String regex = "^[A-Za-z]\\w{5,29}{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the username is empty
        // return false
        if (name == null) {
            return false;
        }

        // Pattern class contains matcher() method
        // to find matching between given username
        // and regular expression.
        Matcher m = p.matcher(name);

        // Return if the username
        // matched the ReGex
        return m.matches();
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Test Case: 1
        String str1 = "Geeksforgeeks";
        System.out.println(isValidUsername(str1));

        // Test Case: 2
        String str3 = "1Geeksforgeeks";
        System.out.println(isValidUsername(str3));

        // Test Case: 3
        String str5 = "Ge";
        System.out.println(isValidUsername(str5));
    }
}
```

**Output:**

```
true
false
false

```