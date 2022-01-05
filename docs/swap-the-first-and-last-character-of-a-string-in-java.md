# 在 Java 中交换字符串的第一个和最后一个字符

> 原文:[https://www . geesforgeks . org/swap-Java 中字符串的第一个和最后一个字符/](https://www.geeksforgeeks.org/swap-the-first-and-last-character-of-a-string-in-java/)

给定字符串 **str** ，任务是编写一个 [Java](https://www.geeksforgeeks.org/java/) 程序来交换给定字符串的第一个和最后一个字符，并打印修改后的字符串。

**示例:**

> **输入:**str = " geeks forgeeks "
> T3】输出: seeksForGeekG
> **解释:**给定字符串的第一个字符是‘G’，给定字符串的最后一个字符是‘s’。我们交换字符“G”和“s”，并打印修改后的字符串。
> 
> **输入:** str = "Java"
> **输出:** aavJ
> **解释:**给定字符串的第一个字符是‘J’，给定字符串的最后一个字符是‘a’。我们交换字符“J”和“a”，并打印修改后的字符串。

**方法 1–使用** [**弦长()方法**](https://www.geeksforgeeks.org/java-string-tochararray-example/)

1.  获取要交换第一个和最后一个字符的字符串。
2.  检查字符串是否只有一个字符，然后返回字符串。
3.  将给定的字符串转换为字符数组。
4.  使用临时变量交换字符串的第一个和最后一个字符。
5.  现在，打印修改后的字符串。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function that swap first and
    // the last character of a string
    public static String
    swapFirstAndLast(String str)
    {

        // Check if the string has only
        // one character then return
        // the string
        if (str.length() < 2)
            return str;

        // Converting the string into
        // a character array
        char[] ch = str.toCharArray();

        // Swapping first and the last
        // character of a string
        char temp = ch[0];
        ch[0] = ch[ch.length - 1];
        ch[ch.length - 1] = temp;

        // Converting character to
        // string and return
        return String.valueOf(ch);
    }

    // Driver Code
    public static void
    main(String args[])
    {
        // Given String str
        String str = "GeeksForGeeks";

        // Function Call
        System.out.println(
            swapFirstAndLast(str));
    }
}
```

**Output:**

```
seeksForGeekG

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**方法 2–使用**[**stringbuilder . setcharat()方法**](https://www.geeksforgeeks.org/stringbuilder-setcharat-in-java-with-examples/) **:**

1.  获取要交换的第一个和最后一个字符的字符串。
2.  检查字符串是否只有一个字符，然后返回字符串。
3.  使用作为参数传递的给定字符串创建一个 [*字符串生成器*对象](https://www.geeksforgeeks.org/stringbuilder-class-in-java-with-examples/)。
4.  将字符串的最后一个字符设置在索引 0 处。
5.  在最后一个索引处设置字符串的第一个字符。
6.  现在，打印修改后的字符串。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function that swap first and
    // the last character of a string
    public static String
    swapFirstAndLast(String str)
    {

        // Check if the string has only
        // one character then return
        // the string
        if (str.length() < 2)
            return str;

        // Creating a StringBuilder object
        // with given string
        StringBuilder sb
            = new StringBuilder(str);

        // Finding the first character
        // of the string
        char first = sb.charAt(0);

        // Set last character at index zero
        sb.setCharAt(0,
                     sb.charAt(sb.length() - 1));

        // Set first character at last index
        sb.setCharAt(sb.length() - 1,
                     first);

        // Converting StringBuilder to
        // String and return
        return sb.toString();
    }

    // Driver Code
    public static void
    main(String args[])
    {
        // Given String str
        String str = "GeeksForGeeks";

        // Print the modified string
        System.out.println(
            swapFirstAndLast(str));
    }
}
```

**Output:**

```
seeksForGeekG

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**方法 3–使用** [**字符串()方法**](https://www.geeksforgeeks.org/substring-in-java/)

1.  获取要交换的第一个和最后一个字符的字符串。
2.  检查字符串是否只有一个字符，然后返回字符串。
3.  提取字符串的最后一个字符。
4.  提取字符串的第一个字符。
5.  在中间字符之间连接最后一个字符和第一个字符。
6.  现在，打印修改后的字符串。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function that swap the first and
    // the last character of a string
    public static String
    swapFirstAndLast(String str)
    {
        // Check if the string has only
        // one character then return
        // the string
        if (str.length() < 2)
            return str;

        // Concatenate last character
        // and first character between
        // middle characters of string
        return (str.substring(str.length() - 1)
                + str.substring(1, str.length() - 1)
                + str.substring(0, 1));
    }

    // Driver Code
    public static void
    main(String args[])
    {
        // Given String str
        String str = "GeeksForGeeks";

        // Function Call
        System.out.println(
            swapFirstAndLast(str));
    }
}
```

**Output:**

```
seeksForGeekG

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)