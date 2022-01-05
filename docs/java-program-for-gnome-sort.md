# 【Gnome 排序的 Java 程序

> 原文:[https://www.geeksforgeeks.org/java-program-for-gnome-sort/](https://www.geeksforgeeks.org/java-program-for-gnome-sort/)

**算法步骤**

1.  如果你在数组的开始，那么转到右边的元素(从 arr[0]到 arr[1])。
2.  如果当前数组元素大于或等于前一个数组元素，则向右移动一步

```
                   if (arr[i] >= arr[i-1])
                      i++;

```

3.  如果当前数组元素小于前一个数组元素，则交换这两个元素并向后退一步

```
                       if (arr[i] < arr[i-1])
                       {
                           swap(arr[i], arr[i-1]);
                           i--;
                       }

```

4.  重复步骤 2)和 3)，直到“I”到达数组的末尾(即“n-1”)
5.  如果到达数组的末尾，则停止并对数组进行排序。

```
// Java Program to implement Gnome Sort

import java.util.Arrays;
public class GFG {
    static void gnomeSort(int arr[], int n)
    {
        int index = 0;

        while (index < n) {
            if (index == 0)
                index++;
            if (arr[index] >= arr[index - 1])
                index++;
            else {
                int temp = 0;
                temp = arr[index];
                arr[index] = arr[index - 1];
                arr[index - 1] = temp;
                index--;
            }
        }
        return;
    }

    // Driver program to test above functions.
    public static void main(String[] args)
    {
        int arr[] = { 34, 2, 10, -9 };

        gnomeSort(arr, arr.length);

        System.out.print("Sorted sequence after applying Gnome sort: ");
        System.out.println(Arrays.toString(arr));
    }
}

// Code Contributed by Mohit Gupta_OMG
```

**Output:**

```
Sorted sequence after applying Gnome sort: [-9, 2, 10, 34]

```

要了解 **Arrays.toString()** ，请参考:
[https://www . geeksforgeeks . org/arrays-tostring-in-Java-with-examples/](https://www.geeksforgeeks.org/arrays-tostring-in-java-with-examples/)

详情请参考 [Gnome Sort](https://www.geeksforgeeks.org/gnome-sort-a-stupid-one/) 上的完整文章！