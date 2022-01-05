# 如何在不使用循环的情况下用 Java 打印数组

> 原文:[https://www . geesforgeks . org/如何在不使用循环的情况下打印 java 数组/](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/)

给定一个 Java 中的数组 arr，任务是打印这个数组的内容。

**Loop 方法:**首先想到的是写一个从 i = 0 到 n 的 for 循环，通过 arr[i]打印每个元素。

```
for(int i = 0; i < Array.length; i++)
        System.out.println(Array[i]);

```

本文讲述了如何在不使用任何循环的情况下，用 Java **打印这个数组。**

为此，我们将在 Java 的 [util 包中使用数组类](https://www.geeksforgeeks.org/java-util-package-java/)的 [toString()方法。这个方法帮助我们获取数组的字符串表示形式。借助 print()或 println()方法可以轻松打印该字符串。](https://www.geeksforgeeks.org/arrays-tostring-in-java-with-examples/)

**示例 1:** 本示例演示如何获取数组的字符串表示形式并打印该字符串表示形式。

```
// Java program to get the String
// representation of an array and print it

import java.io.*;
import java.util.*;

class GFG {
    public static void main(String[] args)
    {

        // Get the array
        int arr[]
            = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        // Get the String representation of array
        String stringArr = Arrays.toString(arr);

        // print the String representation
        System.out.println("Array: " + stringArr);
    }
}
```

**Output:**

```
Array: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```

**例 2:** 这个数组也可以不创建字符串直接打印。

```
// Java program to print an array
// without creating its String representation

import java.io.*;
import java.util.*;

class GFG {
    public static void main(String[] args)
    {

        // Get the array
        int arr[]
            = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        // Print the array
        System.out.println("Array: "
                           + Arrays.toString(arr));
    }
}
```

**Output:**

```
Array: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```