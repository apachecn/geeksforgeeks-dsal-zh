# 用于分类的 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-program-for-pigon hole-sort/](https://www.geeksforgeeks.org/java-program-for-pigeonhole-sort/)

[鸽子洞排序](https://en.wikipedia.org/wiki/Pigeonhole_sort)是一种排序算法，适用于元素数量和可能键值数量大致相同的元素列表排序。
需要 O( *n* + *Range* )时间，其中 n 为输入数组中的元素个数，【Range】为数组中可能的值个数。

**算法工作:**

1.  在数组中查找最小值和最大值。让最小值和最大值分别为“最小值”和“最大值”。还可以找到“最大-最小-1”的范围。
2.  建立一个与范围大小相同的初始空“文件箱”数组。
3.  访问数组中的每个元素，然后将每个元素放入它的文件夹中。元素 arr[i]被放入索引 arr[I]–min 处的孔中。
4.  按顺序在鸽子洞数组上开始循环，并将非空洞的元素放回原始数组中。

```
/* Java program to implement Pigeonhole Sort */

import java.lang.*;
import java.util.*;

public class GFG {
    public static void pigeonhole_sort(int arr[],
                                       int n)
    {
        int min = arr[0];
        int max = arr[0];
        int range, i, j, index;

        for (int a = 0; a < n; a++) {
            if (arr[a] > max)
                max = arr[a];
            if (arr[a] < min)
                min = arr[a];
        }

        range = max - min + 1;
        int[] phole = new int[range];
        Arrays.fill(phole, 0);

        for (i = 0; i < n; i++)
            phole[arr[i] - min]++;

        index = 0;

        for (j = 0; j < range; j++)
            while (phole[j]-- > 0)
                arr[index++] = j + min;
    }

    public static void main(String[] args)
    {
        GFG sort = new GFG();
        int[] arr = { 8, 3, 2, 7, 4, 6, 8 };

        System.out.print("Sorted order is : ");

        sort.pigeonhole_sort(arr, arr.length);

        for (int i = 0; i < arr.length; i++)
            System.out.print(arr[i] + " ");
    }
}

// Code contributed by Mohit Gupta_OMG <(0_o)>
```

**Output:**

```
Sorted order is : 2 3 4 6 7 8 8

```

详情请参考[整理](https://www.geeksforgeeks.org/pigeonhole-sort/)整篇文章！