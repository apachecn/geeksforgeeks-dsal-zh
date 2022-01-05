# 用于排序或排列排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-bogo sort-or-arrange-sort/](https://www.geeksforgeeks.org/java-program-for-bogosort-or-permutation-sort/)

BogoSort 也称为排列排序、愚蠢排序、缓慢排序、猎枪排序或猴子排序，是一种基于生成和测试范式的特别无效的算法。该算法连续生成输入的排列，直到找到一个排序的。( [Wiki](https://en.wikipedia.org/wiki/Bogosort) )
例如，如果使用 bogosort 对一副牌进行排序，它将包括检查该副牌是否有序，如果没有，则将该副牌抛向空中，随机捡起牌，并重复该过程直到该副牌被排序。

**伪代码:**

```
while not Sorted(list) do
    shuffle (list)
done
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement BogoSort
public class BogoSort {
    // Sorts array a[0..n-1] using Bogo sort
    void bogoSort(int[] a)
    {
        // if array is not sorted then shuffle the
        // array again
        while (isSorted(a) == false)
            shuffle(a);
    }

    // To generate permutation of the array
    void shuffle(int[] a)
    {
        // Math.random() returns a double positive
        // value, greater than or equal to 0.0 and
        // less than 1.0.
        for (int i = 0; i < a.length; i++)
            swap(a, i, (int)(Math.random() * i));
    }

    // Swapping 2 elements
    void swap(int[] a, int i, int j)
    {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }

    // To check if array is sorted or not
    boolean isSorted(int[] a)
    {
        for (int i = 1; i < a.length; i++)
            if (a[i] < a[i - 1])
                return false;
        return true;
    }

    // Prints the array
    void printArray(int[] arr)
    {
        for (int i = 0; i < arr.length; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    public static void main(String[] args)
    {
        // Enter array to be sorted here
        int[] a = { 3, 2, 5, 1, 0, 4 };
        BogoSort ob = new BogoSort();

        ob.bogoSort(a);

        System.out.print("Sorted array: ");
        ob.printArray(a);
    }
}
```

**Output:** 

```
Sorted array: 0 1 2 3 4 5
```

更多详情请参考 [BogoSort 或排列排序](https://www.geeksforgeeks.org/bogosort-permutation-sort/)整篇文章！