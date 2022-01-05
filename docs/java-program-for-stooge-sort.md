# 用于傀儡排序的 Java 程序

> 原文:[https://www.geeksforgeeks.org/java-program-for-stooge-sort/](https://www.geeksforgeeks.org/java-program-for-stooge-sort/)

Stooge 排序是一种递归排序算法。其定义如下(用于升序排序)。

```
Step 1 : If value at index 0 is greater than
         value at last index, swap them.
Step 2:  Recursively,
       a) Stooge sort the initial 2/3rd of the array.
       b) Stooge sort the last 2/3rd of the array.
       c) Stooge sort the initial 2/3rd again to confirm.

```

```
// Java program to implement stooge sort
import java.io.*;

public class stooge
{
    // Function to implement stooge sort
    static void stoogesort(int arr[], int l, int h)
    {
        if (l >= h)
           return;

        // If first element is smaller
        // than last,swap them
        if (arr[l] > arr[h])
        {
            int t = arr[l];
            arr[l] = arr[h];
            arr[h] = t;
        }

        // If there are more than 2 elements in
        // the array
        if (h-l+1 > 2)
        {
            int t = (h-l+1) / 3;

            // Recursively sort first 2/3 elements
            stoogesort(arr, l, h-t);

            // Recursively sort last 2/3 elements
            stoogesort(arr, l+t, h);

            // Recursively sort first 2/3 elements
            // again to confirm
            stoogesort(arr, l, h-t);
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = {2, 4, 5, 3, 1};
        int n = arr.length;

        stoogesort(arr, 0, n-1);

        for (int i=0; i < n; i++)
             System.out.print(arr[i] + " ");
    }
}
// Code Contributed by Mohit Gupta_OMG <(0_o)>
```

**输出:**

```
1 2 3 4 5 

```

更多详情请参考[走狗排序](https://www.geeksforgeeks.org/stooge-sort/)整篇文章！