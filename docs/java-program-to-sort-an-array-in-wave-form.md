# 以波形对数组进行排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序对波形数组进行排序/](https://www.geeksforgeeks.org/java-program-to-sort-an-array-in-wave-form/)

给定一个未排序的整数数组，将该数组排序为波浪式数组。数组“arr[0..如果 arr[0]> = arr[1]<= arr[2]>= arr[3]<= arr[4]>=…..

示例:

```
 Input:  arr[] = {10, 5, 6, 3, 2, 20, 100, 80}
 Output: arr[] = {10, 5, 6, 2, 20, 3, 100, 80} OR
                 {20, 5, 10, 2, 80, 6, 100, 3} OR
                 any other array that is in wave form

 Input:  arr[] = {20, 10, 8, 6, 4, 2}
 Output: arr[] = {20, 8, 10, 4, 6, 2} OR
                 {10, 8, 20, 2, 6, 4} OR
                 any other array that is in wave form

 Input:  arr[] = {2, 4, 6, 8, 10, 20}
 Output: arr[] = {4, 2, 8, 6, 20, 10} OR
                 any other array that is in wave form

 Input:  arr[] = {3, 6, 5, 10, 7, 20}
 Output: arr[] = {6, 3, 10, 5, 20, 7} OR
                 any other array that is in wave form

```

一个**简单的解决方法**就是使用排序。首先对输入数组进行排序，然后交换所有相邻的元素。
例如，让输入数组为{3，6，5，10，7，20}。排序后，我们得到{3，5，6，7，10，20}。交换相邻元素后，我们得到{5，3，7，6，20，10}。

下面是这种简单方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of naive method for sorting
// an array in wave form.
import java.util.*;

class SortWave
{
    // A utility method to swap two numbers.
    void swap(int arr[], int a, int b)
    {
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }

    // This function sorts arr[0..n-1] in wave form, i.e.,
    // arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4]..
    void sortInWave(int arr[], int n)
    {
        // Sort the input array
        Arrays.sort(arr);

        // Swap adjacent elements
        for (int i=0; i<n-1; i += 2)
            swap(arr, i, i+1);
    }

    // Driver method
    public static void main(String args[])
    {
        SortWave ob = new SortWave();
        int arr[] = {10, 90, 49, 2, 1, 5, 23};
        int n = arr.length;
        ob.sortInWave(arr, n);
        for (int i : arr)
            System.out.print(i + " ");
    }
}
/*This code is contributed by Rajat Mishra*/
```

**输出:**

```
2 1 10 5 49 23 90
```

如果像[合并排序](http://geeksquiz.com/merge-sort/)、[堆排序](http://geeksquiz.com/heap-sort/)这样的 O(nLogn)排序算法，..使用了 etc。
通过对给定数组进行单次遍历，可以在 **O(n)时间内完成。这个想法是基于这样一个事实，如果我们确保所有偶数位置(在索引 0，2，4，..)元素大于它们相邻的奇数元素，我们不需要担心奇数定位的元素。以下是一些简单的步骤。
1)遍历输入数组中所有偶数位置的元素，并执行以下操作。
…。a)如果当前元素小于前一个奇数元素，交换前一个和当前元素。
…。b)如果当前元素小于下一个奇数元素，则交换下一个和当前元素。**

下面是上述简单算法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(n) Java program to sort an input array in wave form
class SortWave
{
    // A utility method to swap two numbers.
    void swap(int arr[], int a, int b)
    {
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }

    // This function sorts arr[0..n-1] in wave form, i.e.,
    // arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4]....
    void sortInWave(int arr[], int n)
    {
        // Traverse all even elements
        for (int i = 0; i < n; i+=2)
        {
            // If current even element is smaller
            // than previous
            if (i>0 && arr[i-1] > arr[i] )
                swap(arr, i-1, i);

            // If current even element is smaller
            // than next
            if (i<n-1 && arr[i] < arr[i+1] )
                swap(arr, i, i + 1);
        }
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        SortWave ob = new SortWave();
        int arr[] = {10, 90, 49, 2, 1, 5, 23};
        int n = arr.length;
        ob.sortInWave(arr, n);
        for (int i : arr)
            System.out.print(i+" ");
    }
}
/*This code is contributed by Rajat Mishra*/
```

**输出:**

```
90 10 49 1 5 2 23

```

更多详情请参考[整理波形数组](https://www.geeksforgeeks.org/sort-array-wave-form-2/)整篇文章！

=>=>