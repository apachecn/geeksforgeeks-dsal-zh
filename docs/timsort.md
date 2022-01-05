# TimSort

> 哎哎哎:# t0]https://www . geeksforgeeks . org/timsort/

[](https://en.wikipedia.org/wiki/Timsort)**是基于[插入排序](https://www.geeksforgeeks.org/insertion-sort/)和[合并排序](https://www.geeksforgeeks.org/iterative-merge-sort/)的排序算法。**

1.  **一个稳定的排序算法在 O(n ^ Log n)时间内工作**
2.  **用于 Java 的 Arrays.sort()以及 Python 的 sorted()和 sort()。**
3.  **首先使用插入排序对小块进行排序，然后使用合并排序合并小块。**

**我们将数组分成称为**运行**的块。我们使用插入排序逐一对这些运行进行排序，然后使用合并排序中使用的组合函数合并这些运行。如果数组的大小小于游程，则数组仅通过使用插入排序进行排序。运行的大小可以从 32 到 64 不等，具体取决于阵列的大小。请注意，当子阵列的大小为 2 的幂时，合并函数表现良好。这个想法是基于这样一个事实，即插入排序对小数组表现良好。**

**以下实施细节:**

*   **我们认为游程长度为 32。**
*   **我们一个接一个地分拣大小相等的碎片**
*   **在对单个片段进行分类后，我们将它们逐一合并。每次迭代后，我们将合并子阵列的大小加倍。**

## **C++**

```
// C++ program to perform TimSort.
#include<bits/stdc++.h>
using namespace std;
const int RUN = 32;

// This function sorts array from left index to
// to right index which is of size atmost RUN
void insertionSort(int arr[], int left, int right)
{
    for (int i = left + 1; i <= right; i++)
    {
        int temp = arr[i];
        int j = i - 1;
        while (j >= left && arr[j] > temp)
        {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = temp;
    }
}

// Merge function merges the sorted runs
void merge(int arr[], int l, int m, int r)
{

    // Original array is broken in two parts
    // left and right array
    int len1 = m - l + 1, len2 = r - m;
    int left[len1], right[len2];
    for (int i = 0; i < len1; i++)
        left[i] = arr[l + i];
    for (int i = 0; i < len2; i++)
        right[i] = arr[m + 1 + i];

    int i = 0;
    int j = 0;
    int k = l;

    // After comparing, we
    // merge those two array
    // in larger sub array
    while (i < len1 && j < len2)
    {
        if (left[i] <= right[j])
        {
            arr[k] = left[i];
            i++;
        }
        else
        {
            arr[k] = right[j];
            j++;
        }
        k++;
    }

    // Copy remaining elements of left, if any
    while (i < len1)
    {
        arr[k] = left[i];
        k++;
        i++;
    }

    // Copy remaining element of right, if any
    while (j < len2)
    {
        arr[k] = right[j];
        k++;
        j++;
    }
}

// Iterative Timsort function to sort the
// array[0...n-1] (similar to merge sort)
void timSort(int arr[], int n)
{

    // Sort individual subarrays of size RUN
    for (int i = 0; i < n; i+=RUN)
        insertionSort(arr, i, min((i+RUN-1),
                                    (n-1)));

    // Start merging from size RUN (or 32).
    // It will merge
    // to form size 64, then 128, 256
    // and so on ....
    for (int size = RUN; size < n;
                             size = 2*size)
    {

        // pick starting point of
        // left sub array. We
        // are going to merge
        // arr[left..left+size-1]
        // and arr[left+size, left+2*size-1]
        // After every merge, we
        // increase left by 2*size
        for (int left = 0; left < n;
                             left += 2*size)
        {

            // find ending point of
            // left sub array
            // mid+1 is starting point
            // of right sub array
            int mid = left + size - 1;
            int right = min((left + 2*size - 1),
                                            (n-1));

            // merge sub array arr[left.....mid] &
            // arr[mid+1....right]
              if(mid < right)
                merge(arr, left, mid, right);
        }
    }
}

// Utility function to print the Array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d  ", arr[i]);
    printf("\n");
}

// Driver program to test above function
int main()
{
    int arr[] = {-2, 7, 15, -14, 0, 15, 0, 7, -7,
                       -4, -13, 5, 8, -14, 12};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Given Array is\n");
    printArray(arr, n);

    // Function Call
    timSort(arr, n);

    printf("After Sorting Array is\n");
    printArray(arr, n);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to perform TimSort.
class GFG
{

    static int MIN_MERGE = 32;

    public static int minRunLength(int n)
    {
        assert n >= 0;

        // Becomes 1 if any 1 bits are shifted off
        int r = 0;
        while (n >= MIN_MERGE)
        {
            r |= (n & 1);
            n >>= 1;
        }
        return n + r;
    }

    // This function sorts array from left index to
    // to right index which is of size atmost RUN
    public static void insertionSort(int[] arr, int left,
                                     int right)
    {
        for (int i = left + 1; i <= right; i++)
        {
            int temp = arr[i];
            int j = i - 1;
            while (j >= left && arr[j] > temp)
            {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = temp;
        }
    }

    // Merge function merges the sorted runs
    public static void merge(int[] arr, int l,
                                 int m, int r)
    {
        // Original array is broken in two parts
        // left and right array
        int len1 = m - l + 1, len2 = r - m;
        int[] left = new int[len1];
        int[] right = new int[len2];
        for (int x = 0; x < len1; x++)
        {
            left[x] = arr[l + x];
        }
        for (int x = 0; x < len2; x++)
        {
            right[x] = arr[m + 1 + x];
        }

        int i = 0;
        int j = 0;
        int k = l;

        // After comparing, we merge those two array
        // in larger sub array
        while (i < len1 && j < len2)
        {
            if (left[i] <= right[j])
            {
                arr[k] = left[i];
                i++;
            }
            else {
                arr[k] = right[j];
                j++;
            }
            k++;
        }

        // Copy remaining elements
        // of left, if any
        while (i < len1)
        {
            arr[k] = left[i];
            k++;
            i++;
        }

        // Copy remaining element
        // of right, if any
        while (j < len2)
        {
            arr[k] = right[j];
            k++;
            j++;
        }
    }

    // Iterative Timsort function to sort the
    // array[0...n-1] (similar to merge sort)
    public static void timSort(int[] arr, int n)
    {
        int minRun = minRunLength(MIN_MERGE);

        // Sort individual subarrays of size RUN
        for (int i = 0; i < n; i += minRun)
        {
            insertionSort(arr, i,
                          Math.min((i + MIN_MERGE - 1), (n - 1)));
        }

        // Start merging from size
        // RUN (or 32). It will
        // merge to form size 64,
        // then 128, 256 and so on
        // ....
        for (int size = minRun; size < n; size = 2 * size)
        {

            // Pick starting point
            // of left sub array. We
            // are going to merge
            // arr[left..left+size-1]
            // and arr[left+size, left+2*size-1]
            // After every merge, we
            // increase left by 2*size
            for (int left = 0; left < n;
                                 left += 2 * size)
            {

                // Find ending point of left sub array
                // mid+1 is starting point of right sub
                // array
                int mid = left + size - 1;
                int right = Math.min((left + 2 * size - 1),
                                     (n - 1));

                // Merge sub array arr[left.....mid] &
                // arr[mid+1....right]
                  if(mid < right)
                    merge(arr, left, mid, right);
            }
        }
    }

    // Utility function to print the Array
    public static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.print("\n");
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { -2, 7,  15,  -14, 0, 15,  0, 7,
                      -7, -4, -13, 5,   8, -14, 12 };
        int n = arr.length;
        System.out.println("Given Array is");
        printArray(arr, n);

        timSort(arr, n);

        System.out.println("After Sorting Array is");
        printArray(arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program to perform basic timSort
MIN_MERGE = 32

def calcMinRun(n):
    """Returns the minimum length of a
    run from 23 - 64 so that
    the len(array)/minrun is less than or
    equal to a power of 2.

    e.g. 1=>1, ..., 63=>63, 64=>32, 65=>33,
    ..., 127=>64, 128=>32, ...
    """
    r = 0
    while n >= MIN_MERGE:
        r |= n & 1
        n >>= 1
    return n + r

# This function sorts array from left index to
# to right index which is of size atmost RUN
def insertionSort(arr, left, right):
    for i in range(left + 1, right + 1):
        j = i
        while j > left and arr[j] < arr[j - 1]:
            arr[j], arr[j - 1] = arr[j - 1], arr[j]
            j -= 1

# Merge function merges the sorted runs
def merge(arr, l, m, r):

    # original array is broken in two parts
    # left and right array
    len1, len2 = m - l + 1, r - m
    left, right = [], []
    for i in range(0, len1):
        left.append(arr[l + i])
    for i in range(0, len2):
        right.append(arr[m + 1 + i])

    i, j, k = 0, 0, l

    # after comparing, we merge those two array
    # in larger sub array
    while i < len1 and j < len2:
        if left[i] <= right[j]:
            arr[k] = left[i]
            i += 1

        else:
            arr[k] = right[j]
            j += 1

        k += 1

    # Copy remaining elements of left, if any
    while i < len1:
        arr[k] = left[i]
        k += 1
        i += 1

    # Copy remaining element of right, if any
    while j < len2:
        arr[k] = right[j]
        k += 1
        j += 1

# Iterative Timsort function to sort the
# array[0...n-1] (similar to merge sort)
def timSort(arr):
    n = len(arr)
    minRun = calcMinRun(n)

    # Sort individual subarrays of size RUN
    for start in range(0, n, minRun):
        end = min(start + minRun - 1, n - 1)
        insertionSort(arr, start, end)

    # Start merging from size RUN (or 32). It will merge
    # to form size 64, then 128, 256 and so on ....
    size = minRun
    while size < n:

        # Pick starting point of left sub array. We
        # are going to merge arr[left..left+size-1]
        # and arr[left+size, left+2*size-1]
        # After every merge, we increase left by 2*size
        for left in range(0, n, 2 * size):

            # Find ending point of left sub array
            # mid+1 is starting point of right sub array
            mid = min(n - 1, left + size - 1)
            right = min((left + 2 * size - 1), (n - 1))

            # Merge sub array arr[left.....mid] &
            # arr[mid+1....right]
            if mid < right:
                merge(arr, left, mid, right)

        size = 2 * size

# Driver program to test above function
if __name__ == "__main__":

    arr = [-2, 7, 15, -14, 0, 15, 0,
           7, -7, -4, -13, 5, 8, -14, 12]

    print("Given Array is")
    print(arr)

    # Function Call
    timSort(arr)

    print("After Sorting Array is")
    print(arr)
    # [-14, -14, -13, -7, -4, -2, 0, 0,
           5, 7, 7, 8, 12, 15, 15]
```

## **C#**

```
// C# program to perform TimSort.
using System;

class GFG
{
    public const int RUN = 32;

    // This function sorts array from left index to
    // to right index which is of size atmost RUN
    public static void insertionSort(int[] arr,
                                int left, int right)
    {
        for (int i = left + 1; i <= right; i++)
        {
            int temp = arr[i];
            int j = i - 1;
            while (j >= left && arr[j] > temp)
            {
                arr[j+1] = arr[j];
                j--;
            }
            arr[j+1] = temp;
        }
    }

    // merge function merges the sorted runs
    public static void merge(int[] arr, int l,
                                   int m, int r)
    {
        // original array is broken in two parts
        // left and right array
        int len1 = m - l + 1, len2 = r - m;
        int[] left = new int[len1];
        int[] right = new int[len2];
        for (int x = 0; x < len1; x++)
            left[x] = arr[l + x];
        for (int x = 0; x < len2; x++)
            right[x] = arr[m + 1 + x];

        int i = 0;
        int j = 0;
        int k = l;

        // After comparing, we merge those two array
        // in larger sub array
        while (i < len1 && j < len2)
        {
            if (left[i] <= right[j])
            {
                arr[k] = left[i];
                i++;
            }
            else
            {
                arr[k] = right[j];
                j++;
            }
            k++;
        }

        // Copy remaining elements
        // of left, if any
        while (i < len1)
        {
            arr[k] = left[i];
            k++;
            i++;
        }

        // Copy remaining element
        // of right, if any
        while (j < len2)
        {
            arr[k] = right[j];
            k++;
            j++;
        }
    }

    // Iterative Timsort function to sort the
    // array[0...n-1] (similar to merge sort)
    public static void timSort(int[] arr, int n)
    {

        // Sort individual subarrays of size RUN
        for (int i = 0; i < n; i+=RUN)
            insertionSort(arr, i,
                         Math.Min((i+RUN-1), (n-1)));

        // Start merging from size RUN (or 32).
        // It will merge
        // to form size 64, then
        // 128, 256 and so on ....
        for (int size = RUN; size < n;
                                 size = 2*size)
        {

            // Pick starting point of
            // left sub array. We
            // are going to merge
            // arr[left..left+size-1]
            // and arr[left+size, left+2*size-1]
            // After every merge, we increase
            // left by 2*size
            for (int left = 0; left < n;
                                  left += 2*size)
            {

                // Find ending point of left sub array
                // mid+1 is starting point of
                // right sub array
                int mid = left + size - 1;
                int right = Math.Min((left +
                                    2*size - 1), (n-1));

                // Merge sub array arr[left.....mid] &
                // arr[mid+1....right]
                  if(mid < right)
                    merge(arr, left, mid, right);
            }
        }
    }

    // Utility function to print the Array
    public static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
        Console.Write("\n");
    }

    // Driver program to test above function
    public static void Main()
    {
        int[] arr = {-2, 7, 15, -14, 0, 15, 0,
                   7, -7, -4, -13, 5, 8, -14, 12};
        int n = arr.Length;
        Console.Write("Given Array is\n");
        printArray(arr, n);

        // Function Call
        timSort(arr, n);

        Console.Write("After Sorting Array is\n");
        printArray(arr, n);
    }   
}

//This code is contributed by DrRoot_
```

## **java 描述语言**

```
<script>

// Javascript program to perform TimSort.
let MIN_MERGE = 32;

function minRunLength(n)
{

    // Becomes 1 if any 1 bits are shifted off
    let r = 0;
    while (n >= MIN_MERGE)
    {
        r |= (n & 1);
        n >>= 1;
    }
    return n + r;
}

// This function sorts array from left index to
// to right index which is of size atmost RUN
function insertionSort(arr,left,right)
{
    for(let i = left + 1; i <= right; i++)
    {
        let temp = arr[i];
        let j = i - 1;

        while (j >= left && arr[j] > temp)
        {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = temp;
    }
}

// Merge function merges the sorted runs
function merge(arr, l, m, r)
{

    // Original array is broken in two parts
    // left and right array
    let len1 = m - l + 1, len2 = r - m;
    let left = new Array(len1);
    let right = new Array(len2);
    for(let x = 0; x < len1; x++)
    {
        left[x] = arr[l + x];
    }
    for(let x = 0; x < len2; x++)
    {
        right[x] = arr[m + 1 + x];
    }

    let i = 0;
    let j = 0;
    let k = l;

    // After comparing, we merge those two
    // array in larger sub array
    while (i < len1 && j < len2)
    {
        if (left[i] <= right[j])
        {
            arr[k] = left[i];
            i++;
        }
        else
        {
            arr[k] = right[j];
            j++;
        }
        k++;
    }

    // Copy remaining elements
    // of left, if any
    while (i < len1)
    {
        arr[k] = left[i];
        k++;
        i++;
    }

    // Copy remaining element
    // of right, if any
    while (j < len2)
    {
        arr[k] = right[j];
        k++;
        j++;
    }
}

// Iterative Timsort function to sort the
// array[0...n-1] (similar to merge sort)
function  timSort(arr, n)
{
    let minRun = minRunLength(MIN_MERGE);

    // Sort individual subarrays of size RUN
    for(let i = 0; i < n; i += minRun)
    {
        insertionSort(arr, i, Math.min(
            (i + MIN_MERGE - 1), (n - 1)));
    }

    // Start merging from size
    // RUN (or 32). It will
    // merge to form size 64,
    // then 128, 256 and so on
    // ....
    for(let size = minRun; size < n; size = 2 * size)
    {

        // Pick starting point
        // of left sub array. We
        // are going to merge
        // arr[left..left+size-1]
        // and arr[left+size, left+2*size-1]
        // After every merge, we
        // increase left by 2*size
        for(let left = 0; left < n;
                          left += 2 * size)
        {

            // Find ending point of left sub array
            // mid+1 is starting point of right sub
            // array
            let mid = left + size - 1;
            let right = Math.min((left + 2 * size - 1),
                                    (n - 1));

            // Merge sub array arr[left.....mid] &
            // arr[mid+1....right]
            if(mid < right)
                merge(arr, left, mid, right);
        }
    }
}

// Utility function to print the Array
function printArray(arr,n)
{
    for(let i = 0; i < n; i++)
    {
        document.write(arr[i] + " ");
    }
    document.write("<br>");
}

// Driver code
let arr = [ -2, 7, 15, -14, 0, 15, 0, 7,
            -7, -4, -13, 5, 8, -14, 12 ];
let n = arr.length;
document.write("Given Array is<br>");
printArray(arr, n);
timSort(arr, n);

document.write("After Sorting Array is<br>");
printArray(arr, n);

// This code is contributed by rag2127

</script>
```

****输出:****

```
Given Array is
-2, 7, 15, -14, 0, 15, 0, 7, -7, -4, -13, 5, 8, -14, 12
After Sorting Array is
-14  -14  -13  -7  -4  -2  0  0  5  7  7  8  12  15  15
```

****参考文献:**
[https://SVN . python . org/project/python/trunk/Objects/list sort . txt](https://svn.python.org/projects/python/trunk/Objects/listsort.txt)
[https://en . Wikipedia . org/wiki/Timsort # Minimum _ size _ . 28 minrun . 29](https://en.wikipedia.org/wiki/Timsort#Minimum_size_.28minrun.29)
本文由 [Aditya Kumar](https://www.linkedin.com/in/aditya-kumar-837315100/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。**