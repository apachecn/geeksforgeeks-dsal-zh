# 删除 Java 中字符串的第一个和最后一个字符

> 原文:[https://www . geesforgeks . org/remove-Java 中字符串的第一个和最后一个字符/](https://www.geeksforgeeks.org/remove-first-and-last-character-of-a-string-in-java/)

给定字符串 str，任务是编写 [Java](https://www.geeksforgeeks.org/java/) 程序，去掉字符串的第一个和最后一个字符，打印修改后的字符串。

**示例:**

> **输入:** str = "GeeksForGeeks"
> **输出:**eeksforgek
> **解释:**
> 给定字符串的第一个字符是‘G’，给定字符串的最后一个字符是‘s’。删除字符串的第一个和最后一个字符后，该字符串变成“eeksForGeek”。
> 
> **输入:** str = "Java"
> **输出:** av
> **解释:**
> 给定字符串的第一个字符是‘J’，给定字符串的最后一个字符是‘a’。删除字符串的第一个和最后一个字符后，该字符串变成“av”。

**方法 1:使用** [**String.substring()方法**](https://www.geeksforgeeks.org/substring-in-java/)

1.  想法是使用*字符串类*的*子字符串(*)方法删除字符串的第一个和最后一个字符。
2.  *子串(int beginIndex，int endIndex)方法*接受两个参数，第一个是*起始索引*，第二个是*结束索引*。
3.  字符串的第一个字符出现在索引*零*处，字符串的最后一个字符出现在字符串的索引*长度–1*处。
4.  使用 str.substring(1，str . length()–1)提取除第一个和最后一个字符之外的子字符串。
5.  现在，打印修改后的字符串。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove the first and
// the last character of a string

class GFG {

    // Function to remove the first and
    // the last character of a string
    public static String
    removeFirstandLast(String str)
    {

        // Removing first and last character
        // of a string using substring() method
        str = str.substring(1, str.length() - 1);

        // Return the modified string
        return str;
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given String str
        String str = "GeeksForGeeks";

        // Print the modified string
        System.out.print(
            removeFirstandLast(str));
    }
}
```

**Output:**

```
eeksForGeek

```

**方法二:使用**[**stringbuilder . delete charat()方法**](https://www.geeksforgeeks.org/stringbuilder-deletecharat-in-java-with-examples/)

1.  想法是使用 *StringBuilder 类*的 *deleteCharAt()* 方法删除字符串的第一个和最后一个字符。
2.  *deleteCharAt()* 方法接受一个参数作为要删除的字符的索引。
3.  使用*sb . delete charat(str . length()–1)删除字符串的最后一个字符。*
4.  使用 *sb.deleteCharAt(0)删除字符串的第一个字符。*
5.  现在，打印修改后的字符串。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove the first and
// the last character of a string

class GFG {

    // Function to remove the first and
    // the last character of a string
    public static String
    removeFirstandLast(String str)
    {

        // Creating a StringBuilder object
        StringBuilder sb = new StringBuilder(str);

        // Removing the last character
        // of a string
        sb.deleteCharAt(str.length() - 1);

        // Removing the first character
        // of a string
        sb.deleteCharAt(0);

        // Converting StringBuilder into a string
        // and return the modified string
        return sb.toString();
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given String str
        String str = "GeeksForGeeks";

        // Print the modified string
        System.out.println(
            removeFirstandLast(str));
    }
}
```

**Output:**

```
eeksForGeek

```

**方法三:使用** [**StringBuffer.delete()方法**](https://www.geeksforgeeks.org/stringbuffer-delete-method-in-java-with-examples/)

1.  想法是使用 *StringBuffer 类*的 *delete()* 方法删除字符串的第一个和最后一个字符。
2.  delete(start_point，int end_point)方法接受两个参数，第一个是 *start_point* ，第二个是 *end_point* ，删除参数中提到的范围形成的子串后返回字符串。
3.  使用*sb . delete(str.length()–1，str . length())删除字符串的最后一个字符。*
4.  使用*sb delete(0，1)删除字符串的第一个字符。*
5.  现在，打印修改后的字符串。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove the first and
// the last character of a string

class GFG {

    // Function to remove the first and
    // the last character of a string
    public static String
    removeFirstandLast(String str)
    {

        // Creating a StringBuffer object
        StringBuffer sb = new StringBuffer(str);

        // Removing the last character
        // of a string
        sb.delete(str.length() - 1, str.length());

        // Removing the first character
        // of a string
        sb.delete(0, 1);

        // Converting StringBuffer into
        // string & return modified string
        return sb.toString();
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given String str
        String str = "GeeksForGeeks";

        // Print the modified string
        System.out.println(
            removeFirstandLast(str));
    }
}
```

**Output:**

```
eeksForGeek

```