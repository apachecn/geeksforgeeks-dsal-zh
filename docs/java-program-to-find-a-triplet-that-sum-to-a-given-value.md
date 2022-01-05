# Java 程序寻找一个和给定值相加的三元组

> 原文:[https://www . geesforgeks . org/Java-program-to-find-a-triple-the-sum-to-a-给定值/](https://www.geeksforgeeks.org/java-program-to-find-a-triplet-that-sum-to-a-given-value/)

给定一个数组和值，找出数组中是否有一个三元组，其和等于给定值。如果数组中存在这样的三元组，则打印该三元组并返回 true。否则返回 false。

**例:**

> **输入:**数组= {12，3，4，1，6，9}，和= 24；
> **输出:** 12，3，9
> **说明:**数组中有一个三元组(12，3，9)存在
> ，其和为 24。
> **输入:**数组= {1，2，3，4，5}，和= 9
> **输出:** 5，3，1
> **说明:**数组中存在一个和为 9 的三元组(5，3，1)。

**<u>方法 1</u> :** 这是解决上述问题的天真方法。

*   **方法:**一个简单的方法是生成所有可能的三元组，并将每个三元组的总和与给定值进行比较。下面的代码使用三个嵌套循环实现了这个简单的方法。
*   **算法:**
    1.  给定一组长度 *n* 和一个总和 *s*
    2.  创建三个嵌套循环第一个循环从开始到结束(循环计数器 I)，第二个循环从 i+1 到结束(循环计数器 j)，第三个循环从 j+1 到结束(循环计数器 k)
    3.  这些循环的计数器表示三元组的 3 个元素的索引。
    4.  求 ith，jth 和 kth 元素的和。如果总和等于给定的总和。打印三联并断开。
    5.  如果没有三元组，则打印不存在三元组。
*   **实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a triplet
class FindTriplet {

    // returns true if there is triplet with sum equal
    // to 'sum' present in A[]. Also, prints the triplet
    boolean find3Numbers(int A[], int arr_size, int sum)
    {
        int l, r;

        // Fix the first element as A[i]
        for (int i = 0; i < arr_size - 2; i++) {

            // Fix the second element as A[j]
            for (int j = i + 1; j < arr_size - 1; j++) {

                // Now look for the third number
                for (int k = j + 1; k < arr_size; k++) {
                    if (A[i] + A[j] + A[k] == sum) {
                        System.out.print("Triplet is " + A[i] + ", " + A[j] + ", " + A[k]);
                        return true;
                    }
                }
            }
        }

        // If we reach here, then no triplet was found
        return false;
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        FindTriplet triplet = new FindTriplet();
        int A[] = { 1, 4, 45, 6, 10, 8 };
        int sum = 22;
        int arr_size = A.length;

        triplet.find3Numbers(A, arr_size, sum);
    }
}
```

**Output**

```
Triplet is 4, 10, 8
```

*   **复杂度分析:**
    *   **时间复杂度:** O(n <sup>3</sup> )。
        有三个嵌套循环遍历数组，因此时间复杂度为 O(n^3)
    *   **空间复杂度:** O(1)。
        因为不需要额外的空间。

**<u>方法二:</u>** 这种方法利用排序来增加代码的效率。

*   **方法:**通过对数组进行排序，可以提高算法的效率。这种高效的方法使用了[双指针技术](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/)。遍历数组并固定三元组的第一个元素。现在使用双指针算法来查找是否有一对的和等于 x–array[I]。两点算法需要线性时间，因此比嵌套循环更好。
*   **算法:**
    1.  给定数组排序。
    2.  循环数组并固定可能三元组的第一个元素，arr[i]。
    3.  然后固定两个指针，一个在 i + 1，另一个在 n–1。看看总数，
        1.  如果总和小于所需总和，则递增第一个指针。
        2.  否则，如果总和较大，减少结束指针以减少总和。
        3.  否则，如果两个指针上的元素之和等于给定的和，则打印三元组并断开。
*   **实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a triplet
class FindTriplet {

    // returns true if there is triplet with sum equal
    // to 'sum' present in A[]. Also, prints the triplet
    boolean find3Numbers(int A[], int arr_size, int sum)
    {
        int l, r;

        /* Sort the elements */
        quickSort(A, 0, arr_size - 1);

        /* Now fix the first element one by one and find the
           other two elements */
        for (int i = 0; i < arr_size - 2; i++) {

            // To find the other two elements, start two index variables
            // from two corners of the array and move them toward each
            // other
            l = i + 1; // index of the first element in the remaining elements
            r = arr_size - 1; // index of the last element
            while (l < r) {
                if (A[i] + A[l] + A[r] == sum) {
                    System.out.print("Triplet is " + A[i] + ", " + A[l] + ", " + A[r]);
                    return true;
                }
                else if (A[i] + A[l] + A[r] < sum)
                    l++;

                else // A[i] + A[l] + A[r] > sum
                    r--;
            }
        }

        // If we reach here, then no triplet was found
        return false;
    }

    int partition(int A[], int si, int ei)
    {
        int x = A[ei];
        int i = (si - 1);
        int j;

        for (j = si; j <= ei - 1; j++) {
            if (A[j] <= x) {
                i++;
                int temp = A[i];
                A[i] = A[j];
                A[j] = temp;
            }
        }
        int temp = A[i + 1];
        A[i + 1] = A[ei];
        A[ei] = temp;
        return (i + 1);
    }

    /* Implementation of Quick Sort
    A[] --> Array to be sorted
    si  --> Starting index
    ei  --> Ending index
     */
    void quickSort(int A[], int si, int ei)
    {
        int pi;

        /* Partitioning index */
        if (si < ei) {
            pi = partition(A, si, ei);
            quickSort(A, si, pi - 1);
            quickSort(A, pi + 1, ei);
        }
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        FindTriplet triplet = new FindTriplet();
        int A[] = { 1, 4, 45, 6, 10, 8 };
        int sum = 22;
        int arr_size = A.length;

        triplet.find3Numbers(A, arr_size, sum);
    }
}
```

**Output**

```
Triplet is 4, 8, 10
```

*   **复杂度分析:**
    *   **时间复杂度:** O(N^2).
        只有两个嵌套循环遍历数组，所以时间复杂度是 O(n^2).双指针算法需要 O(n)个时间，第一个元素可以使用另一个嵌套遍历来修复。
    *   **空间复杂度:** O(1)。
        因为不需要额外的空间。

**<u>方法 3</u> :** 这是一个基于哈希的解决方案。

*   **方法:**这种方法使用额外的空间，但比两点法简单。运行两个循环从开始到结束的外部循环和从 i+1 到结束的内部循环。创建一个 hashmap 或 set 来存储 i+1 到 j-1 之间的元素。所以如果给定的和是 x，检查集合中是否有一个数等于 x–arr[I]–arr[j]。如果是，打印三份。

*   **算法:**
    1.  从头到尾遍历数组。(循环计数器 I)
    2.  创建一个 HashMap 或集合来存储唯一的对。
    3.  从 i+1 到数组末尾运行另一个循环。(循环计数器 j)
    4.  如果集合中有一个元素等于 x-arr[i]–arr[j]，则打印三元组(arr[I]、arr[j]、x-arr[i]-arr[j])并断开
    5.  在集合中插入 jth 元素。
*   **实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a triplet using Hashing
import java.util.*;

class GFG {

    // returns true if there is triplet
    // with sum equal to 'sum' present
    // in A[]. Also, prints the triplet
    static boolean find3Numbers(int A[],
                                int arr_size, int sum)
    {
        // Fix the first element as A[i]
        for (int i = 0; i < arr_size - 2; i++) {

            // Find pair in subarray A[i+1..n-1]
            // with sum equal to sum - A[i]
            HashSet<Integer> s = new HashSet<Integer>();
            int curr_sum = sum - A[i];
            for (int j = i + 1; j < arr_size; j++) 
            {
                if (s.contains(curr_sum - A[j])) 
                {
                    System.out.printf("Triplet is %d, 
                                        %d, %d", A[i],
                                      A[j], curr_sum - A[j]);
                    return true;
                }
                s.add(A[j]);
            }
        }

        // If we reach here, then no triplet was found
        return false;
    }

    /* Driver code */
    public static void main(String[] args)
    {
        int A[] = { 1, 4, 45, 6, 10, 8 };
        int sum = 22;
        int arr_size = A.length;

        find3Numbers(A, arr_size, sum);
    }
}

// This code has been contributed by 29AjayKumar
```

**输出:**

```
Triplet is 4, 8, 10
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(N)

更多细节请参考[整篇文章找到一个和给定值](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/)的三元组！