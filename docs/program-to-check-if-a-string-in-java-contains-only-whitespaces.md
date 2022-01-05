# 检查 Java 中字符串是否只包含空格的程序

> 原文:[https://www . geesforgeks . org/program-to-check-in-a-string-in-Java-contains-only-white spaces/](https://www.geeksforgeeks.org/program-to-check-if-a-string-in-java-contains-only-whitespaces/)

给定一个字符串，任务是在 Java 中检查这个字符串是否只包含空格或一些文本。

**示例:**

```
Input: str = "              " 
Output: True

Input: str = "GFG"
Output: False

```

**进场:**

*   获取要在字符串中检查的字符串
*   我们可以使用[字符串类](https://www.geeksforgeeks.org/string-class-in-java/)的[修剪()方法](https://www.geeksforgeeks.org/java-string-trim-method-example/)来移除字符串中的前导空格。
    **语法:**

```
str.trim()

```

*   然后我们可以使用[字符串类](https://www.geeksforgeeks.org/string-class-in-java/)的 [isEmpty()方法](https://www.geeksforgeeks.org/java-string-isempty-method-example/)来检查结果字符串是否为空。如果字符串只包含空格，那么这个方法将返回真
    **语法:**

    ```
    str.isEmpty()

    ```

    *   使用[方法链接](https://www.geeksforgeeks.org/method-chaining-in-java-with-examples/)将两种方法结合使用。

    ```
    str.trim().isEmpty();

    ```

    *   Print true if the above condition is true. Else print false.

    下面是上述方法的实现:

    ```
    // Java Program to check if
    // the String is not all whitespaces

    class GFG {

        // Function to check if the String is all whitespaces
        public static boolean isStringAllWhiteSpace(String str)
        {

            // Remove the leading whitespaces using trim()
            // and then check if this string is empty
            if (str.trim().isEmpty())
                return true;
            else
                return false;
        }

        // Driver code
        public static void main(String[] args)
        {
            String str1 = "GeeksforGeeks";
            String str2 = "              ";

            System.out.println("Is string [" + str1
                               + "] only whitespaces? "
                               + isStringAllWhiteSpace(str1));
            System.out.println("Is string [" + str2
                               + "] only whitespaces? "
                               + isStringAllWhiteSpace(str2));
        }
    }
    ```

    **Output:**

    ```
    Is string [GeeksforGeeks] only whitespaces? false
    Is string [              ] only whitespaces? true

    ```