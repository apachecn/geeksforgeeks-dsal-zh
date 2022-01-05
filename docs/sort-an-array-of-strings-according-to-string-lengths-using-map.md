# 使用地图

根据字符串长度对字符串数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-按字符串长度排列字符串-使用映射/](https://www.geeksforgeeks.org/sort-an-array-of-strings-according-to-string-lengths-using-map/)

给定一个字符串数组，我们需要使用[映射数据结构](https://www.geeksforgeeks.org/map-interface-java-examples/)按照字符串长度的递增顺序对数组进行排序。

**示例:**

> **输入:**str[]= {“GeeksforGeeks”，“我”，“来自”，“am”}
> **输出:**我来自 geesforgeeks
> 
> **输入:** str[] = {“你”、“是”、“漂亮”、“在看”}
> **输出:**你在看漂亮

**方法:**给定的方法是使用[树形图](https://www.geeksforgeeks.org/treemap-in-java/)的 Java

*   取一个包含字符串长度的[树形图](https://www.geeksforgeeks.org/treemap-in-java/)作为键，取一个与键长度相同的[字符串的](https://www.geeksforgeeks.org/strings-in-java/)[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)。
*   由于我们知道一个[树图](https://www.geeksforgeeks.org/treemap-in-java/)已经被排序，所以在插入到[树图](https://www.geeksforgeeks.org/treemap-in-java/)之后，我们再次从[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)中一个接一个地获取值(T4】字符串到[字符串](https://www.geeksforgeeks.org/strings-in-java/)数组[中。](https://www.geeksforgeeks.org/java-gq/arrays-gq/)

下面是上述方法的实现:

```
// Java program to sort an Array of
// Strings according to their lengths
// using Map

import java.util.*;
import java.util.Map.Entry;
import java.io.*;

public class GFG {

    // Function to Sort the array of string
    // according to lengths using Map
    static String[] sort(String[] str, int n)
    {
        TreeMap<Integer, ArrayList<String> > map
            = new TreeMap<Integer, ArrayList<String> >();

        for (int i = 0; i < n; i++) {

            map.putIfAbsent(str[i].length(),
                            new ArrayList<String>());
            map.get(str[i].length()).add(str[i]);
        }

        int temp = 0;

        for (Entry<Integer, ArrayList<String> >
                 e : map.entrySet()) {

            for (int i = 0; i < e.getValue().size(); i++) {

                str[temp] = e.getValue().get(i);
                temp++;
            }
        }
        return str;
    }

    // Function to print the sorted array of string
    static void printArraystring(String str[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(str[i] + " ");
    }

    // Driver function
    public static void main(String args[])
    {
        String[] arr = { "GeeksforGeeks",
                         "I", "from", "am" };
        int n = arr.length;

        // Function to perform sorting
        arr = sort(arr, n);

        // Calling the function to print result
        printArraystring(arr, n);
    }
}
```

**Output:**

```
I am from GeeksforGeeks

```