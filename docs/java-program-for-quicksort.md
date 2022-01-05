# 快速排序的 Java 程序

> 原文:[https://www.geeksforgeeks.org/java-program-for-quicksort/](https://www.geeksforgeeks.org/java-program-for-quicksort/)

像[合并排序](https://www.geeksforgeeks.org/merge-sort/)一样，快速排序是一种分治算法。它选取一个元素作为透视，并围绕选取的透视对给定数组进行分区。快速排序有许多不同的版本，它们以不同的方式选取轴心。

1.  始终选择第一个元素作为轴心。
2.  始终选择最后一个元素作为轴心(在下面实现)
3.  选择一个随机元素作为轴心。
4.  选择中线作为枢轴。

快速排序中的关键过程是分区()。分区的目标是，给定一个数组和数组的元素 x 作为轴心，将 x 放在排序数组中正确的位置，将所有较小的元素(小于 x)放在 x 之前，将所有较大的元素(大于 x)放在 x 之后。所有这些都应该在线性时间内完成。
**递归快速排序函数伪代码:**

```
/* low  --> Starting index,  high  --> Ending index */
quickSort(arr[], low, high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);  // Before pi
        quickSort(arr, pi + 1, high); // After pi
    }
}

```

```
// Java program for implementation of QuickSort
class QuickSort
{
    /* This function takes last element as pivot,
       places the pivot element at its correct
       position in sorted array, and places all
       smaller (smaller than pivot) to left of
       pivot and all greater elements to right
       of pivot */
    int partition(int arr[], int low, int high)
    {
        int pivot = arr[high]; 
        int i = (low-1); // index of smaller element
        for (int j=low; j<high; j++)
        {
            // If current element is smaller than or
            // equal to pivot
            if (arr[j] <= pivot)
            {
                i++;

                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high] (or pivot)
        int temp = arr[i+1];
        arr[i+1] = arr[high];
        arr[high] = temp;

        return i+1;
    }

    /* The main function that implements QuickSort()
      arr[] --> Array to be sorted,
      low  --> Starting index,
      high  --> Ending index */
    void sort(int arr[], int low, int high)
    {
        if (low < high)
        {
            /* pi is partitioning index, arr[pi] is 
              now at right place */
            int pi = partition(arr, low, high);

            // Recursively sort elements before
            // partition and after partition
            sort(arr, low, pi-1);
            sort(arr, pi+1, high);
        }
    }

    /* A utility function to print array of size n */
    static void printArray(int arr[])
    {
        int n = arr.length;
        for (int i=0; i<n; ++i)
            System.out.print(arr[i]+" ");
        System.out.println();
    }

    // Driver program
    public static void main(String args[])
    {
        int arr[] = {10, 7, 8, 9, 1, 5};
        int n = arr.length;

        QuickSort ob = new QuickSort();
        ob.sort(arr, 0, n-1);

        System.out.println("sorted array");
        printArray(arr);
    }
}
/*This code is contributed by Rajat Mishra */
```

详情请参考[快速排序](https://www.geeksforgeeks.org/quick-sort/)上的完整文章！