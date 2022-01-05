# 用于计数排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-计数程序-排序-2/](https://www.geeksforgeeks.org/java-program-for-counting-sort-2/)

[计数排序](http://en.wikipedia.org/wiki/Counting_sort)是一种基于特定范围之间的键的排序技术。它的工作原理是计算具有不同键值的对象的数量(某种散列法)。然后做一些算术来计算输出序列中每个对象的位置。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of Counting Sort
class CountingSort {
    void sort(char arr[])
    {
        int n = arr.length;

        // The output character array that will have sorted arr
        char output[] = new char[n];

        // Create a count array to store count of individual
        // characters and initialize count array as 0
        int count[] = new int[256];
        for (int i = 0; i < 256; ++i)
            count[i] = 0;

        // store count of each character
        for (int i = 0; i < n; ++i)
            ++count[arr[i]];

        // Change count[i] so that count[i] now contains actual
        // position of this character in output array
        for (int i = 1; i <= 255; ++i)
            count[i] += count[i - 1];

        // Build the output character array
        for (int i = 0; i < n; ++i) {
            output[count[arr[i]] - 1] = arr[i];
            --count[arr[i]];
        }

        // Copy the output array to arr, so that arr now
        // contains sorted characters
        for (int i = 0; i < n; ++i)
            arr[i] = output[i];
    }

    // Driver method
    public static void main(String args[])
    {
        CountingSort ob = new CountingSort();
        char arr[] = {'g', 'e', 'e', 'k', 's', 'f', 'o',
                      'r', 'g', 'e', 'e', 'k', 's' };

        ob.sort(arr);

        System.out.print("Sorted character array is ");
        for (int i = 0; i < arr.length; ++i)
            System.out.print(arr[i]);
    }
}
/*This code is contributed by Rajat Mishra */
```

**Output:** 

```
Sorted character array is eeeefggkkorss
```

详情请参考[计数排序](https://www.geeksforgeeks.org/counting-sort/)整篇文章！