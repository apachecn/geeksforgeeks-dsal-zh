# 奇偶排序/砖块排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-奇数-偶数-sort-brick-sort/](https://www.geeksforgeeks.org/java-program-for-odd-even-sort-brick-sort/)

这基本上是[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)的变体。该算法分为两个阶段——奇数阶段和偶数阶段。该算法一直运行到数组元素被排序，并且在每次迭代中出现两个阶段——奇数阶段和偶数阶段。

在奇数阶段，我们对奇数索引元素执行冒泡排序，在偶数阶段，我们对偶数索引元素执行冒泡排序。

```
// Java Program to implement
// Odd-Even / Brick Sort
import java.io.*;

class GFG {
    public static void oddEvenSort(int arr[], int n)
    {
        boolean isSorted = false; // Initially array is unsorted

        while (!isSorted) {
            isSorted = true;
            int temp = 0;

            // Perform Bubble sort on odd indexed element
            for (int i = 1; i <= n - 2; i = i + 2) {
                if (arr[i] > arr[i + 1]) {
                    temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                    isSorted = false;
                }
            }

            // Perform Bubble sort on even indexed element
            for (int i = 0; i <= n - 2; i = i + 2) {
                if (arr[i] > arr[i + 1]) {
                    temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                    isSorted = false;
                }
            }
        }

        return;
    }
    public static void main(String[] args)
    {
        int arr[] = { 34, 2, 10, -9 };
        int n = arr.length;

        oddEvenSort(arr, n);
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");

        System.out.println(" ");
    }
}
// Code Contribute by Mohit Gupta_OMG <(0_o)>
```

**输出:**

```
-9 2 10 34

```

详情请参考[奇偶排序/砖块排序](https://www.geeksforgeeks.org/odd-even-sort-brick-sort/)整篇文章！