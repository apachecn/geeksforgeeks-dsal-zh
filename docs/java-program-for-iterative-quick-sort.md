# 迭代快速排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-iterative-quick-sort/](https://www.geeksforgeeks.org/java-program-for-iterative-quick-sort/)

```
// Java implementation of iterative quick sort
class IterativeQuickSort {
    void swap(int arr[], int i, int j)
    {
        int t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
    }

    /* This function is same in both iterative and
       recursive*/
    int partition(int arr[], int l, int h)
    {
        int x = arr[h];
        int i = (l - 1);

        for (int j = l; j <= h - 1; j++) {
            if (arr[j] <= x) {
                i++;
                // swap arr[i] and arr[j]
                swap(arr, i, j);
            }
        }
        // swap arr[i+1] and arr[h]
        swap(arr, i + 1, h);
        return (i + 1);
    }

    // Sorts arr[l..h] using iterative QuickSort
    void QuickSort(int arr[], int l, int h)
    {
        // create auxiliary stack
        int stack[] = new int[h - l + 1];

        // initialize top of stack
        int top = -1;

        // push initial values in the stack
        stack[++top] = l;
        stack[++top] = h;

        // keep popping elements until stack is not empty
        while (top >= 0) {
            // pop h and l
            h = stack[top--];
            l = stack[top--];

            // set pivot element at it's proper position
            int p = partition(arr, l, h);

            // If there are elements on left side of pivot,
            // then push left side to stack
            if (p - 1 > l) {
                stack[++top] = l;
                stack[++top] = p - 1;
            }

            // If there are elements on right side of pivot,
            // then push right side to stack
            if (p + 1 < h) {
                stack[++top] = p + 1;
                stack[++top] = h;
            }
        }
    }

    // A utility function to print contents of arr
    void printArr(int arr[], int n)
    {
        int i;
        for (i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
    }

    // Driver code to test above
    public static void main(String args[])
    {
        IterativeQuickSort ob = new IterativeQuickSort();
        int arr[] = { 4, 3, 5, 2, 1, 3, 2, 3 };
        ob.QuickSort(arr, 0, arr.length - 1);
        ob.printArr(arr, arr.length);
    }
}
/*This code is contributed by Rajat Mishra */
```

**Output:**

```
1 2 2 3 3 3 4 5

```

上述递归快速排序的优化也可以应用于迭代版本。

1)分区过程在递归和迭代中是相同的。选择最佳轴心的相同技术也可以应用于迭代版本。

2)要减小堆栈大小，首先推小一半的索引。

3)当大小减少到实验计算的阈值以下时，使用插入排序。

更多详情请参考[迭代快速排序](https://www.geeksforgeeks.org/iterative-quick-sort/)整篇文章！