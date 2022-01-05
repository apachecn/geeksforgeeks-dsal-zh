# 线性搜索的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-linear-search/](https://www.geeksforgeeks.org/java-program-for-linear-search/)

**问题:**给定 n 个元素的数组 arr[]，编写一个函数在 arr[]中搜索给定的元素 x。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for linearly search x in arr[]. If x
// is present then return its location, otherwise
// return -1
class LinearSearch {
    // This function returns index of element x in arr[]
    static int search(int arr[], int n, int x)
    {
        for (int i = 0; i < n; i++) {
            // Return the index of the element if the element
            // is found
            if (arr[i] == x)
                return i;
        }

        // return -1 if the element is not found
        return -1;
    }

    public static void main(String[] args)
    {
        int[] arr = { 3, 4, 1, 7, 5 };
        int n = arr.length;

        int x = 4;

        int index = search(arr, n, x);
        if (index == -1)
            System.out.println("Element is not present in the array");
        else
            System.out.println("Element found at position " + index);
    }
}
```

**Output:**

```
Element found at position 1

```

上述算法的时间复杂度为 O(n)。

更多详情请参考[线性搜索](https://www.geeksforgeeks.org/linear-search/)整篇文章！