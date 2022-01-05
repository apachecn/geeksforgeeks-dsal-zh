# 如何在 Java 中删除字符串中的所有空格？

> 原文:[https://www . geesforgeks . org/如何从 java 字符串中删除所有空格/](https://www.geeksforgeeks.org/how-to-remove-all-white-spaces-from-a-string-in-java/)

给定一个带有空格的字符串，任务是使用 Java 内置方法删除字符串中的所有空格。

**示例:**

```
Input: str = "       Geeks     for    Geeks   "            
Output: GeeksforGeeks

Input:  str = "    A  Computer  Science   Portal"
Output: AComputerSciencePortal

```

要删除字符串中的所有空格，请使用带有两个参数的字符串类的 [`replaceAll()`](https://www.geeksforgeeks.org/java-lang-string-replace-java/) 方法，即

```
replaceAll("\\s", "");
```

，其中\\s 是 unicode 中的单个空格

**程序:**

```
class BlankSpace {
    public static void main(String[] args)
    {
        String str = "      Geeks     for    Geeks        ";

        // Call the replaceAll() method
        str = str.replaceAll("\\s", "");

        System.out.println(str);
    }
}
```

**Output:**

```
GeeksforGeeks

```