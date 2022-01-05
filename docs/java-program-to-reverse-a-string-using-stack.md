# 使用堆栈反转字符串的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-reverse-a-string-use-stack/](https://www.geeksforgeeks.org/java-program-to-reverse-a-string-using-stack/)

[栈](https://www.geeksforgeeks.org/stack-class-in-java/)是遵循[后进先出](https://www.geeksforgeeks.org/lifo-last-in-first-out-approach-in-programming/)原则的线性数据结构，即最后插入的元素是最先出来的元素。

**方法:**

1.  Push characters into the data type character stack one by one.
2.  Eject the characters from the stack one by one until the stack becomes empty.
3.  Add pop-up elements to the character array.
4.  Convert a character array into a string.
5.  Returns the inverted string.

下面是上述方法的实现。

## 爪哇

T0T6】

#### 输出:

```
GeeksForGeeks <- Reverse -> skeeGroFskeeG
Hello World <- Reverse -> dlroW olleH

```

**时间复杂度:** O(n)，其中 n 是栈中的字符数。

**辅助空间:**堆的 O(n)。