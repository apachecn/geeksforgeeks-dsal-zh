# 外壳排序的 Java 程序

> 原文:[https://www.geeksforgeeks.org/java-program-for-shellsort/](https://www.geeksforgeeks.org/java-program-for-shellsort/)

在 shellSort 中，我们对数组 h 进行排序，得到一个大的 h 值。我们不断减少 h 的值，直到它变成 1。如果第 h 个元素的所有子列表都被排序，那么这个数组被称为 h 排序的。

```
// Java implementation of ShellSort
class ShellSort {
    /* An utility function to print array of size n*/
    static void printArray(int arr[])
    {
        int n = arr.length;
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    /* function to sort arr using shellSort */
    int sort(int arr[])
    {
        int n = arr.length;

        // Start with a big gap, then reduce the gap
        for (int gap = n / 2; gap > 0; gap /= 2) {
            // Do a gapped insertion sort for this gap size.
            // The first gap elements a[0..gap-1] are already
            // in gapped order keep adding one more element
            // until the entire array is gap sorted
            for (int i = gap; i < n; i += 1) {
                // add a[i] to the elements that have been gap
                // sorted save a[i] in temp and make a hole at
                // position i
                int temp = arr[i];

                // shift earlier gap-sorted elements up until
                // the correct location for a[i] is found
                int j;
                for (j = i; j >= gap && arr[j - gap] > temp; j -= gap)
                    arr[j] = arr[j - gap];

                // put temp (the original a[i]) in its correct
                // location
                arr[j] = temp;
            }
        }
        return 0;
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = { 12, 34, 54, 2, 3 };
        System.out.println("Array before sorting");
        printArray(arr);

        ShellSort ob = new ShellSort();
        ob.sort(arr);

        System.out.println("Array after sorting");
        printArray(arr);
    }
}
/*This code is contributed by Rajat Mishra */
```

**输出:**

```
Array before sorting
12 34 54 2 3 
Array after sorting
2 3 12 34 54

```

更多详情请参考[外壳排序](https://www.geeksforgeeks.org/shellsort/)完整文章！