# 检查字符串在 Java 中是否为空的程序

> 原文:[https://www . geesforgeks . org/program-to-check-如果字符串在 java 中为空/](https://www.geeksforgeeks.org/program-to-check-if-the-string-is-null-in-java/)

给定一个字符串，任务是在 Java 中检查这个字符串是否为空。

**示例:**

```
Input: str = null 
Output: True

Input: str = "GFG"
Output: False

```

**进场:**

*   获取要在字符串中检查的字符串
*   我们可以简单地使用 [==关系运算符](https://www.geeksforgeeks.org/java-relational-operators-with-examples/)将字符串与 Null 进行比较。
    **语法:**

    ```
    if(str == null)

    ```

*   如果上述条件为真，则打印为真。否则打印错误。

下面是上述方法的实现:

```
// Java Program to check if
// the String is Null in Java

class GFG {

    // Function to check if the String is Null
    public static boolean isStringNull(String str)
    {

        // Compare the string with null
        // using == relational operator
        // and return the result
        if (str == null)
            return true;
        else
            return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "GeeksforGeeks";
        String str2 = null;

        System.out.println("Is string [" + str1
                           + "] null? "
                           + isStringNull(str1));
        System.out.println("Is string [" + str2
                           + "] null? "
                           + isStringNull(str2));
    }
}
```

**Output:**

```
Is string [GeeksforGeeks] null? false
Is string [null] null? true

```