# 用于二进制排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-bitonic-sort-2/](https://www.geeksforgeeks.org/java-program-for-bitonic-sort-2/)

**双音素序列**

如果一个序列先递增后递减，则称之为比通序列。换句话说，数组 arr[0..n-i]是 Bitonic，如果存在索引 I，其中 0<=i<=n-1

```
***x0 <= x1 …..<= xi  and  xi >= xi+1….. >= xn-1*** 
```

1.  按递增顺序排序的序列被认为是双音素的，递减部分为空。类似地，递减顺序被认为是 Bitonic，递增部分为空。
2.  双调和序列的旋转也是双调和的。

**双音素排序**

主要涉及两个步骤。

1.  形成双音序列(上面详细讨论过)。经过这一步，我们到达下图中的第四个阶段，即数组变成{3，4，7，8，6，5，2，1}
2.  从双音素序列创建一个排序序列:第一步后，前半部分按递增顺序排序，后半部分按递减顺序排序。
    我们将前半部分的第一个元素与后半部分的第一个元素进行比较，然后将前半部分的第二个元素与后半部分的第二个元素进行比较，以此类推。如果前半部分的元素较小，我们就交换元素。
    经过以上的比较和交换步骤，我们得到了数组中的两个双离子序列。见下图第五阶段。在第五阶段，我们有{3，4，2，1，6，5，7，8}。如果我们仔细观察这些元素，我们可以注意到有两个长度为 n/2 的双音素序列，使得第一个双音素序列{3，4，2，1}中的所有元素都小于第二个双音素序列{6，5，7，8}中的所有元素。
    我们在两个双离子序列中重复同样的过程，得到长度为 n/4 的四个双离子序列，使得最左边的双离子序列的所有元素都更小，最右边的所有元素都更小。见下图第六阶段，数组是{2，1，3，4，6，5，7，8}。
    如果我们再重复一次这个过程，我们会得到 8 个大小为 1 的 n/8 的双离子序列。因为所有这些双音素序列都是排序的，并且每个双音素序列都有一个元素，所以我们得到排序的数组。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program for Bitonic Sort. Note that this program
   works only when size of input is a power of 2\. */
public class BitonicSort {
    /* The parameter dir indicates the sorting direction,
       ASCENDING or DESCENDING; if (a[i] > a[j]) agrees
       with the direction, then a[i] and a[j] are
       interchanged. */
    void compAndSwap(int a[], int i, int j, int dir)
    {
        if ((a[i] > a[j] && dir == 1) || (a[i] < a[j] && dir == 0)) {
            // Swapping elements
            int temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
    }

    /* It recursively sorts a bitonic sequence in ascending
       order, if dir = 1, and in descending order otherwise
       (means dir=0). The sequence to be sorted starts at
       index position low, the parameter cnt is the number
       of elements to be sorted.*/
    void bitonicMerge(int a[], int low, int cnt, int dir)
    {
        if (cnt > 1) {
            int k = cnt / 2;
            for (int i = low; i < low + k; i++)
                compAndSwap(a, i, i + k, dir);
            bitonicMerge(a, low, k, dir);
            bitonicMerge(a, low + k, k, dir);
        }
    }

    /* This function first produces a bitonic sequence by
       recursively sorting its two halves in opposite sorting
       orders, and then  calls bitonicMerge to make them in
       the same order */
    void bitonicSort(int a[], int low, int cnt, int dir)
    {
        if (cnt > 1) {
            int k = cnt / 2;

            // sort in ascending order since dir here is 1
            bitonicSort(a, low, k, 1);

            // sort in descending order since dir here is 0
            bitonicSort(a, low + k, k, 0);

            // Will merge whole sequence in ascending order
            // since dir=1.
            bitonicMerge(a, low, cnt, dir);
        }
    }

    /*Caller of bitonicSort for sorting the entire array
      of length N in ASCENDING order */
    void sort(int a[], int N, int up)
    {
        bitonicSort(a, 0, N, up);
    }

    /* A utility function to print array of size n */
    static void printArray(int arr[])
    {
        int n = arr.length;
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    // Driver method
    public static void main(String args[])
    {
        int a[] = { 3, 7, 4, 8, 6, 2, 1, 5 };
        int up = 1;
        BitonicSort ob = new BitonicSort();
        ob.sort(a, a.length, up);
        System.out.println("\nSorted array");
        printArray(a);
    }
}
```

**Output:** 

```
Sorted array
1 2 3 4 5 6 7 8
```

更多详情请参考[双音素排序](https://www.geeksforgeeks.org/bitonic-sort/)整篇文章！