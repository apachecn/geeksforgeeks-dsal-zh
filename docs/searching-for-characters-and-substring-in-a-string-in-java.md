# 在 Java 中搜索字符串中的字符和子字符串

> 原文:[https://www . geesforgeks . org/搜索 java 字符串中的字符和子字符串/](https://www.geeksforgeeks.org/searching-for-characters-and-substring-in-a-string-in-java/)

**字符串**从编程的角度来看是一个非常重要的方面，因为许多问题可以在字符串中被组织出来。理解弦乐有许多不同的概念和问题。现在这里将讨论不同的字符串处理方式，我们将在内置方法的帮助下处理字符串和子字符串字符，这是输入字符串的一部分，并且还提出了如下列出各种方式的逻辑:

### **在字符串中搜索字符**

**方式 1:** 索引(字符 c)

它搜索给定字符串中指定字符的索引。它从字符串的开头到结尾(从左到右)开始搜索，如果找到，则返回相应的索引，否则返回-1。

> **注意:**如果给定的字符串包含指定字符的多次出现，那么它返回指定字符的唯一第一次出现的索引。

**语法:**

```
int indexOf(char c)
// Accepts character as argument, Returns index of 
// the first occurrence of specified character 
```

**方式 2:**T2【最后一个索引(char c)

它从字符串末尾开始向后搜索，并在遇到指定字符时返回其索引。

**语法:**

```
public int lastIndexOf(char c)
// Accepts character as argument, Returns an 
// index of the last occurrence specified 
// character
```

**方式 3:** **索引(char c，int index rom)**

它从字符串中的指定索引开始向前搜索，并在遇到指定字符时返回相应的索引，否则返回-1。

> **注意:**返回的索引必须大于等于指定的索引。

**语法:**

```
public int IndexOf(char c, int indexFrom)
```

**参数:**

*   要搜索的字符
*   搜索位置的整数

**返回类型:**在前进方向上出现在指定索引处或之后的指定字符的索引。

**方式 4:负载指数(char c，int fromIndex)**

它从字符串中的指定索引开始向后搜索。并在遇到指定字符时返回相应的索引，否则返回-1。

> **注意:**返回的索引必须小于或等于指定的索引。

**语法:**

```
public int lastIndexOf(char c, int fromIndex)
```

**方式 6: charAt(int indexNumber)**

返回给定字符串中存在于指定索引处的字符。如果字符串中不存在指定的索引号，该方法将引发未检查的异常，即 StringIndexOutOfBoundsException。

**语法:**

```
char charAt(int indexNumber)
```

**示例:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Illustrate to Find a Character
// in the String

// Importing required classes
import java.io.*;

// Main class
class GFG {

    // Main driver method
    public static void main(String[] args)
    {

        // String in which a character to be searched.
        String str
            = "GeeksforGeeks is a computer science portal";

        // Returns index of first occurrence of character.
        int firstIndex = str.indexOf('s');
        System.out.println("First occurrence of char 's'"
                           + " is found at : "
                           + firstIndex);

        // Returns index of last occurrence specified
        // character.
        int lastIndex = str.lastIndexOf('s');
        System.out.println("Last occurrence of char 's' is"
                           + " found at : " + lastIndex);

        // Index of the first occurrence of specified char
        // after the specified index if found.
        int first_in = str.indexOf('s', 10);
        System.out.println("First occurrence of char 's'"
                           + " after index 10 : "
                           + first_in);

        int last_in = str.lastIndexOf('s', 20);
        System.out.println("Last occurrence of char 's'"
                           + " after index 20 is : "
                           + last_in);

        // gives ASCII value of character at location 20
        int char_at = str.charAt(20);
        System.out.println("Character at location 20: "
                           + char_at);

        // Note: If we uncomment it will throw
        // StringIndexOutOfBoundsException
        // char_at = str.charAt(50);
    }
}
```

**Output**

```
First occurrence of char 's' is found at : 4
Last occurrence of char 's' is found at : 28
First occurrence of char 's' after index 10 : 12
Last occurrence of char 's' after index 20 is : 15
Character at location 20: 111
```

**方式 7:在字符串中搜索子字符串**

上面提到的用于搜索字符串中的字符的方法也可以用于搜索字符串中的子字符串。

**例**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to illustrate to Find a Substring
// in the String

// Importing required classes
import java.io.*;

// Main class
class GFG {

    // Main driver method
    public static void main(String[] args)
    {

        // A string in which a substring
        // is to be searched
        String str
            = "GeeksforGeeks is a computer science portal";

        // Returns index of first occurrence of substring
        int firstIndex = str.indexOf("Geeks");

        System.out.println("First occurrence of char Geeks"
                           + " is found at : "
                           + firstIndex);

        // Returns index of last occurrence
        int lastIndex = str.lastIndexOf("Geeks");
        System.out.println(
            "Last occurrence of char Geeks is"
            + " found at : " + lastIndex);

        // Index of the first occurrence
        // after the specified index if found
        int first_in = str.indexOf("Geeks", 10);
        System.out.println("First occurrence of char Geeks"
                           + " after index 10 : "
                           + first_in);

        int last_in = str.lastIndexOf("Geeks", 20);
        System.out.println("Last occurrence of char Geeks "
                           + "after index 20 is : "
                           + last_in);
    }
}
```

**Output**

```
First occurrence of char Geeks is found at : 0
Last occurrence of char Geeks is found at : 8
First occurrence of char Geeks after index 10 : -1
Last occurrence of char Geeks after index 20 is : 8
```

**方式 8:** **包含(字符序列序列):**如果字符串包含指定的字符值序列，则返回真，否则返回假。它的参数指定要搜索的字符序列，如果 seq 为 null，则抛出 NullPointer 异常。

**语法:**

```
public boolean contains(CharSequence seq)
```

> **注意:** CharSequence 是一个由 string 类实现的接口，因此我们在 contains()方法中使用 String 作为参数。

**例**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Illustrate How to Find a Substring
// in the String using contains() Method

// Importing required classes
import java.io.*;
import java.lang.*;

// Class
class GFG {

    // Main driver method
    public static void main(String[] args)
    {
        // String in which substring
        // to be searched
        String test = "software";

        CharSequence seq = "soft";
        boolean bool = test.contains(seq);
        System.out.println("Found soft?: " + bool);

        // Returns true substring if found.
        boolean seqFound = test.contains("war");
        System.out.println("Found war? " + seqFound);

        // Returns true substring if found
        // otherwise return false
        boolean sqFound = test.contains("wr");
        System.out.println("Found wr?: " + sqFound);
    }
}
```

**Output**

```
Found soft?: true
Found war? true
Found wr?: false
```

**方式 9:匹配字符串开始和结束**

*   **布尔 startsWith(字符串):**如果字符串存在于给定字符串的开头，则返回 true，否则返回 false。
*   **布尔 startsWith(字符串，int indexNum):** 如果字符串存在于给定字符串的索引 indexNum 的开始处，则返回 true，否则返回 false。
*   **布尔结束开关(字符串):**如果字符串存在于给定字符串的结尾，则返回真，否则返回假。

**示例:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Match ofstart and endof a Substring

// Importing required classes
import java.io.*;

// Main class
class GFG {

    // Main driver method
    public static void main(String[] args)
    {
        // Input string in which substring
        // is to be searched
        String str
            = "GeeksforGeeks is a computer science portal";

        // Print and display commands
        System.out.println(str.startsWith("Geek"));
        System.out.println(str.startsWith("is", 14));
        System.out.println(str.endsWith("port"));
    }
}
```

**Output**

```
true
true
false
```

本文由 **Nitsdheerendra** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。