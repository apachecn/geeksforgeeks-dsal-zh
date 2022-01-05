# 气泡排序的 Java 程序

> 原文:[https://www.geeksforgeeks.org/java-program-for-bubble-sort/](https://www.geeksforgeeks.org/java-program-for-bubble-sort/)

冒泡排序是最简单的排序算法，如果相邻元素的顺序错误，可以通过重复交换它们来工作。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of Bubble Sort
class BubbleSort
{
    void bubbleSort(int arr[])
    {
        int n = arr.length;
        for (int i = 0; i < n-1; i++)
            for (int j = 0; j < n-i-1; j++)
                if (arr[j] > arr[j+1])
                {
                    // swap temp and arr[i]
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
    }

    /* Prints the array */
    void printArray(int arr[])
    {
        int n = arr.length;
        for (int i=0; i<n; ++i)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    // Driver method to test above
    public static void main(String args[])
    {
        BubbleSort ob = new BubbleSort();
        int arr[] = {64, 34, 25, 12, 22, 11, 90};
        ob.bubbleSort(arr);
        System.out.println("Sorted array");
        ob.printArray(arr);
    }
}
/* This code is contributed by Rajat Mishra */
```

更多详情请参考[气泡排序](https://www.geeksforgeeks.org/bubble-sort/)整篇文章！