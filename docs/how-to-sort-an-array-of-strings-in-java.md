# 如何在 Java 中对字符串数组进行排序

> 原文:[https://www . geesforgeks . org/如何在 java 中对字符串数组进行排序/](https://www.geeksforgeeks.org/how-to-sort-an-array-of-strings-in-java/)

**字符串数组**

要在 Java 中对字符串数组进行排序，我们可以使用 [Arrays.sort()](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/) 函数。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A sample Java program to
// sort an array of strings
// in ascending and descending
// orders using Arrays.sort().

import java.util.Arrays;
import java.util.Collections;

public class SortExample {
    public static void main(String[] args)
    {
        String arr[] = { "practice.geeksforgeeks.org",
                         "quiz.geeksforgeeks.org",
                         "code.geeksforgeeks.org" };

        // Sorts arr[] in ascending order
        Arrays.sort(arr);
        System.out.printf("Modified arr[] : \n%s\n\n",
                          Arrays.toString(arr));

        // Sorts arr[] in descending order
        Arrays.sort(arr, Collections.reverseOrder());

        System.out.printf("Modified arr[] : \n%s\n\n",
                          Arrays.toString(arr));
    }
}
```

**Output:** 

修改后的 arr[]:

修改后的 arr[]:
[code.geeksforgeeks.org practice.geeksforgeeks.org 问答]

**字符串数组列表**

如果我们有一个[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)来排序，我们可以使用 [Collections.sort()](https://www.geeksforgeeks.org/collections-sort-java-examples/)

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A sample Java program to sort
// an arrayList of strings
// in ascending and descending
// orders using Collections.sort().

import java.util.ArrayList;
import java.util.Collections;

public class SortExample {
    public static void main(String[] args)
    {
        ArrayList<String> al = new ArrayList<String>();
        al.add("practice.geeksforgeeks.org");
        al.add("quiz.geeksforgeeks.org");
        al.add("code.geeksforgeeks.org");

        // Sorts ArrayList in ascending order
        Collections.sort(al);
        System.out.println(
            "Modified ArrayList : \n" + al);

        // Sorts arr[] in descending order
        Collections.sort(al,
                         Collections.reverseOrder());

        System.out.println(
            "Modified ArrayList : \n" + al);
    }
}
```

**Output:** 

修改后的数组列表:

修改后的数组列表: