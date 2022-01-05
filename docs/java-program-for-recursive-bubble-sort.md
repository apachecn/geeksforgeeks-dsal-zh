# 递归冒泡排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-recursive-bubble-sort/](https://www.geeksforgeeks.org/java-program-for-recursive-bubble-sort/)

**背景:**
[【冒泡排序】](https://www.geeksforgeeks.org/bubble-sort/)是最简单的排序算法，如果相邻元素的顺序不对，就重复交换相邻元素。
以下是迭代冒泡排序算法:

```
// Iterative Bubble Sort
bubbleSort(arr[], n)
{
  for (i = 0; i < n-1; i++)      

     // Last i elements are already in place   
     for (j = 0; j  arr[j+1])
         swap(arr[j], arr[j+1]);
} 
```

**递归思想。**

1.  基本情况:如果数组大小为 1，则返回。
2.  做一遍正常的冒泡排序。此过程修复了当前子阵列的最后一个元素。
3.  除了当前子阵列的最后一个元素之外的所有元素重复出现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for recursive implementation
// of Bubble sort

import java.util.Arrays;

public class GFG
{
    // A function to implement bubble sort
    static void bubbleSort(int arr[], int n)
    {
        // Base case
        if (n == 1)
            return;

        // One pass of bubble sort. After
        // this pass, the largest element
        // is moved (or bubbled) to end.
        for (int i=0; i<n-1; i++)
            if (arr[i] > arr[i+1])
            {
                // swap arr[i], arr[i+1]
                int temp = arr[i];
                arr[i] = arr[i+1];
                arr[i+1] = temp;
            }

        // Largest element is fixed,
        // recur for remaining array
        bubbleSort(arr, n-1);
    }

    // Driver Method
    public static void main(String[] args)
    {
        int arr[] = {64, 34, 25, 12, 22, 11, 90};

        bubbleSort(arr, arr.length);

        System.out.println("Sorted array : ");
        System.out.println(Arrays.toString(arr));
    }
}
```

更多详情请参考[递归冒泡排序](https://www.geeksforgeeks.org/recursive-bubble-sort/)整篇文章！