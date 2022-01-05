# 如何在 Java 中删除字符串中的所有非字母数字字符

> 原文:[https://www . geesforgeks . org/如何从 java 字符串中删除所有非字母数字字符/](https://www.geeksforgeeks.org/how-to-remove-all-non-alphanumeric-characters-from-a-string-in-java/)

给定一个字符串 **str** ，任务是从中删除所有非字母数字字符并打印修改后的字符。
**例:**

> **输入:** @！极客-为'极客，123
> T3】输出:极客 forgeeks 123
> T6】解释: at 符号(@)，感叹号(！)、破折号(-)、撇号(')和逗号(，)被删除。
> 
> **输入:** Geeks_for$ Geeks？{}[]
> **输出:**geeks forges
> **解释:**下划线(_)、美元符号($)、空格、问号(？)，大括号({})和方括号([])被删除。
> 
> **输入:**geesforgeeks 123
> **输出:**geesforgeeks 123
> **说明:**不需要删除任何字符，因为给定的字符串没有任何非字母数字字符。

**方法 1:使用 ASCII 值**
由于字母数字字符对于大写字母来说位于 ASCII 值范围[65，90]内，对于小写字母来说位于 ASCII 值范围[97，122]内，对于数字来说位于 ASCII 值范围[48，57]内。因此，逐字符遍历字符串并获取每个字符的 ASCII 值。如果 ASCII 值不在上述三个范围内，则该字符是非字母数字字符。因此，跳过这些字符，将其余字符添加到另一个字符串中并打印出来。

**方法 2:使用 String.replaceAll()**
非字母数字字符包括除字母和数字之外的所有字符**。可以是*感叹号(！)*，在*符号(@)* ，*逗号(，*，*问号(？)*、*冒号(:)*、*破折号(-)* 等以及特殊字符如*美元符号($)* 、*等号(=)* 、*加号(+)* 、*撇号(')*。**

**方法是使用 [String.replaceAll](https://www.geeksforgeeks.org/java-lang-string-replace-method-java/) 方法将所有非字母数字字符替换为空字符串。**

**下面是上述方法的实现:**

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to remove non-alphanumeric
// characters from a string
class GFG {

    // Function to remove non-alphanumeric
    // characters from string
    public static String
      removeNonAlphanumeric(String str)
    {
        // replace the given string
        // with empty string
        // except the pattern "[^a-zA-Z0-9]"
        str = str.replaceAll(
          "[^a-zA-Z0-9]", "");

        // return string
        return str;
    }

    // Driver Code
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 
          = "@!Geeks-for'Geeks, 123";
        System.out.println(
          removeNonAlphanumeric(str1));

        // Test Case 2:
        String str2 
          = "Geeks_for$ Geeks?{}[]";
        System.out.println(
          removeNonAlphanumeric(str2));

        // Test Case 3:
        String str3 
          = "GeeksforGeeks123";
        System.out.println(
          removeNonAlphanumeric(str3));
    }
}
```

****Output**

```
GeeksforGeeks123
GeeksforGeeks
GeeksforGeeks123

```** 

****方法 3:使用正则表达式**
另一种方法涉及使用[正则表达式](https://www.geeksforgeeks.org/regular-expressions-in-java/)。可以使用 regex***【^a-za-z0-9】***轻松过滤字符串。**