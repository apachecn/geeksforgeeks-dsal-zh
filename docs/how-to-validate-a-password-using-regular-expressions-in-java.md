# 如何在 Java 中使用正则表达式验证密码

> 原文:[https://www . geesforgeks . org/如何使用 java 正则表达式验证密码/](https://www.geeksforgeeks.org/how-to-validate-a-password-using-regular-expressions-in-java/)

给定一个密码，任务是在正则表达式的帮助下验证密码。
如果满足以下所有约束，则认为密码有效:

*   它至少包含 8 个字符，最多包含 20 个字符。
*   它至少包含一个数字。
*   它至少包含一个大写字母。
*   它至少包含一个小写字母。
*   它至少包含一个特殊字符，包括**！@#$% & *()-+=^** 。
*   它不包含任何空格。

**示例:**

> **输入:**Str = " Geeks @ portal 20 "
> T3】输出:真。
> **说明:**该密码满足上述所有约束。
> 
> **输入:**Str = " Geeksforgeeks "
> T3】输出:假。
> **说明:**包含大写和小写字母但不包含任何数字、特殊字符。
> 
> **输入:**Str = " Geeks @ portal 9 "
> T3】输出:假。
> **说明:**包含大写字母、小写字母、特殊字符、数字以及无效的空格。
> 
> **输入:**Str = " 12345 "
> T3】输出:假。
> **说明:**只包含数字，不包含大写字母、小写字母、特殊字符、8 个字符。

**方法:**这个问题可以用[正则表达式](https://www.geeksforgeeks.org/regular-expressions-in-java/)来解决。

1.  获取密码。
2.  Create a regular expression to check the password is valid or not as mentioned below:

    > **regex = "^(？=.*[0-9])(?=.*[a-z])(？=.*[A-Z])(？=.*[@#$%^ & -+=()])(？=\\S+$)。{8，20 } { content } # x201D**

    其中:

    *   **^** 代表字符串的起始字符。
    *   **(？=.*[0-9])** 代表一个数字必须至少出现一次。
    *   **(？=.*[a-z])** 代表小写字母必须至少出现一次。
    *   **(？=.*[A-Z])** 代表必须至少出现一次的大写字母。
    *   **(？=.*[@#$%^&-+=()】**代表必须至少出现一次的特殊字符。
    *   **(？=\\S+$)** 整个字符串中不允许有空格。
    *   **。{8，20}** 代表至少 8 个字符，最多 20 个字符。
    *   **$** 代表字符串的结尾。
3.  将给定的字符串与 Regex 匹配。在 java 中，这可以使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。
4.  如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

```
// Java program to validate
// the password using ReGex

import java.util.regex.*;
class GFG {

    // Function to validate the password.
    public static boolean
    isValidPassword(String password)
    {

        // Regex to check valid password.
        String regex = "^(?=.*[0-9])"
                       + "(?=.*[a-z])(?=.*[A-Z])"
                       + "(?=.*[@#$%^&+=])"
                       + "(?=\\S+$).{8,20}{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the password is empty
        // return false
        if (password == null) {
            return false;
        }

        // Pattern class contains matcher() method
        // to find matching between given password
        // and regular expression.
        Matcher m = p.matcher(password);

        // Return if the password
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "Geeks@portal20";
        System.out.println(isValidPassword(str1));

        // Test Case 2:
        String str2 = "Geeksforgeeks";
        System.out.println(isValidPassword(str2));

        // Test Case 3:
        String str3 = "Geeks@ portal9";
        System.out.println(isValidPassword(str3));

        // Test Case 4:
        String str4 = "1234";
        System.out.println(isValidPassword(str4));

        // Test Case 5:
        String str5 = "Gfg@20";
        System.out.println(isValidPassword(str5));

        // Test Case 6:
        String str6 = "geeks@portal20";
        System.out.println(isValidPassword(str6));
    }
}
```

**Output:**

```
true
false
false
false
false
false

```