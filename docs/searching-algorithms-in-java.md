# Java 中的搜索算法

> 原文:[https://www.geeksforgeeks.org/searching-algorithms-in-java/](https://www.geeksforgeeks.org/searching-algorithms-in-java/)

搜索算法旨在检查元素或从存储元素的任何数据结构中检索元素。根据搜索操作的类型，这些算法一般分为两类:

1.  **顺序搜索:**在这种情况下，按顺序遍历列表或数组，并检查每个元素。例如:[线性搜索](https://www.geeksforgeeks.org/linear-search/)。
2.  **区间搜索:**这些算法是专门为在有序数据结构中搜索而设计的。这些类型的搜索算法比线性搜索高效得多，因为它们反复瞄准搜索结构的中心并将搜索空间分成两半。例如:[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。

[**【线性搜索】**](https://www.geeksforgeeks.org/linear-search/) **:** 思路是遍历给定数组**arr【】**找到元素所在的索引。以下是步骤:

*   让要搜索的元素为 **x** 。
*   从**arr【】**最左边的元素开始，逐一比较 **x** 和**arr【】**的各个元素。
*   如果 x 与某个元素匹配，则返回该**索引**。
*   如果 x 和柠檬不匹配，那么返回-1。

下面是 Java 中顺序搜索的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Linear Search

class GFG {

    // Function for linear search
    public static int search(int arr[], int x)
    {
        int n = arr.length;

        // Traverse array arr[]
        for (int i = 0; i < n; i++) {

            // If element found then
            // return that index
            if (arr[i] == x)
                return i;
        }
        return -1;
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given arr[]
        int arr[] = { 2, 3, 4, 10, 40 };

        // Element to search
        int x = 10;

        // Function Call
        int result = search(arr, x);
        if (result == -1)
            System.out.print(
                "Element is not present in array");
        else
            System.out.print("Element is present"
                             + " at index "
                             + result);
    }
}
```

**Output:** 

```
Element is present at index 3
```