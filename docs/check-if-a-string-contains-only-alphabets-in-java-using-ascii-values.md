# 使用 ASCII 值检查字符串是否只包含 Java 中的字母

> 原文:[https://www . geesforgeks . org/check-if-a-string-contains-only-alphabets-in-Java-using-ascii-values/](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-ascii-values/)

给定一个字符串，任务是检查一个字符串是否只包含字母，或者在 JAVA 中不使用 ASCII 值。

**示例:**

```
Input : GeeksforGeeks
Output : True

Input : Geeks4Geeks
Output : False

Input : null
Output : False

```

在本文中，使用字符串的 **ASCII 值逐个检查字符串的字符。**

**算法:**

1.  去拿绳子
2.  匹配字符串:
    *   检查字符串是否为空。如果为空，返回 false
    *   检查字符串是否为空。如果为空，则返回 false。
    *   如果字符串既不为空也不为空，则使用 ASCII 值逐个检查字符串字符的字母表。
3.  如果匹配，返回真

**伪代码:**

```
public static boolean isStringOnlyAlphabet(String str)
{
    if (str == null || str.equals("")) {
        return false;
    }
    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        if ((!(ch >= 'A' && ch <= 'Z'))
            && (!(ch >= 'a' && ch <= 'z'))) {
            return false;
        }
    }
    return true;
}
```

**程序:**检查只包含字母的字符串

```
// Java program to check if String contains only Alphabets
// using ASCII values

class GFG {

    // Function to check String for only Alphabets
    public static boolean isStringOnlyAlphabet(String str)
    {
        if (str == null || str.equals("")) {
            return false;
        }
        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            if ((!(ch >= 'A' && ch <= 'Z'))
                && (!(ch >= 'a' && ch <= 'z'))) {
                return false;
            }
        }
        return true;
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

**[使用 Lambda 表达式检查字符串是否只包含 Java 中的字母](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-lambda-expression/)**
**[使用 Regex](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-regex/)** 检查字符串是否只包含 Java 中的字母