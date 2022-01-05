# 使用 Lambda 表达式

检查字符串是否只包含 Java 中的字母

> 原文:[https://www . geesforgeks . org/check-if-a-string-contains-only-alphabets-in-Java-using-lambda-expression/](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-lambda-expression/)

给定一个字符串，任务是检查一个字符串是否只包含字母。

**示例:**

```
Input : GeeksforGeeks
Output : True

Input : Geeks4Geeks
Output : False

Input : null
Output : False

```

思路是使用【字符类】的 *isLetter()方法。*

**算法:**

1.  去拿绳子
2.  匹配字符串:
    *   检查字符串是否为空。如果为空，返回 false
    *   检查字符串是否为空。如果为空，则返回 false。
    *   如果字符串既不为空也不为空，
        则使用 Lambda 表达式字符::isLetter()进行检查。
3.  如果匹配，返回真

**伪代码:**

```
public static boolean isStringOnlyAlphabet(String str)
{
    return ((!str.equals(""))
            && (str != null)
            && (str.chars().allMatch(Character::isLetter)));
}
```

**程序:**检查字符串是否只包含字母。

```
// Java program to check if String contains only Alphabets
// using Lambda Expression

class GFG {

    // Function to check String for only Alphabets
    public static boolean isStringOnlyAlphabet(String str)
    {
        return ((str != null)
                && (!str.equals(""))
                && (str.chars().allMatch(Character::isLetter)));
    }

    // Main method
    public static void main(String[] args)
    {

        // Checking for True case
        System.out.println("Test Case 1:");

        String str1 = "GeeksforGeeks";
        System.out.println("Input: " + str1);
        System.out.println("Output: " + isStringOnlyAlphabet(str1));

        // Checking for String with numeric characters
        System.out.println("\nTest Case 2:");

        String str2 = "Geeks4Geeks";
        System.out.println("Input: " + str2);
        System.out.println("Output: " + isStringOnlyAlphabet(str2));

        // Checking for null String
        System.out.println("\nTest Case 3:");

        String str3 = null;
        System.out.println("Input: " + str3);
        System.out.println("Output: " + isStringOnlyAlphabet(str3));

        // Checking for empty String
        System.out.println("\nTest Case 4:");

        String str4 = "";
        System.out.println("Input: " + str4);
        System.out.println("Output: " + isStringOnlyAlphabet(str4));
    }
}
```

**Output:**

```
Test Case 1:
Input: GeeksforGeeks
Output: true

Test Case 2:
Input: Geeks4Geeks
Output: false

Test Case 3:
Input: null
Output: false

Test Case 4:
Input: 
Output: false

```

**[使用 ASCII 值检查字符串是否只包含 Java 中的字母](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-ascii-values/)**
**[使用 Regex](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-regex/)** 检查字符串是否只包含 Java 中的字母