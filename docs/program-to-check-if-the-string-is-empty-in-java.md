# Java 中检查字符串是否为空的程序

> 原文:[https://www . geesforgeks . org/program-to-check-如果字符串在 java 中为空/](https://www.geeksforgeeks.org/program-to-check-if-the-string-is-empty-in-java/)

在 Java 中，给定一个字符串，任务是检查这个字符串是否为空。

**示例:**

```
Input: str = "" 
Output: True

Input: str = "GFG"
Output: False

```

**进场:**

*   获取要在字符串中检查的字符串
*   我们可以简单地使用字符串类
    **的 [isEmpty()方法检查字符串是否为空【语法:](https://www.geeksforgeeks.org/java-string-isempty-method-example/)**

    ```
    if (str.isEmpty())

    ```

*   如果上述条件为真，则打印为真。否则打印错误。

下面是上述方法的实现:

```
// Java Program to check if
// the String is empty in Java

class GFG {

    // Function to check if the String is empty
    public static boolean isStringEmpty(String str)
    {

        // check if the string is empty or not
        // using the isEmpty() method
        // and return the result
        if (str.isEmpty())
            return true;
        else
            return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "GeeksforGeeks";
        String str2 = "";

        System.out.println("Is string \"" + str1
                           + "\" empty? "
                           + isStringEmpty(str1));
        System.out.println("Is string \"" + str2
                           + "\" empty? "
                           + isStringEmpty(str2));
    }
}
```

**Output:**

```
Is string "GeeksforGeeks" empty? false
Is string "" empty? true

```