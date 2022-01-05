# 给定一个排序和旋转数组的 Java 程序，查找是否有一对给定和的数组

> 原文:[https://www . geeksforgeeks . org/Java-给定排序和旋转数组的程序-如果有给定和的对就查找/](https://www.geeksforgeeks.org/java-program-for-given-a-sorted-and-rotated-array-find-if-there-is-a-pair-with-a-given-sum/)

给定一个排序后围绕未知点旋转的数组。查找数组中是否有一对和为“x”的数组。可以假设数组中的所有元素都是不同的。

**示例:**

```
Input: arr[] = {11, 15, 6, 8, 9, 10}, x = 16
Output: true
There is a pair (6, 10) with sum 16

Input: arr[] = {11, 15, 26, 38, 9, 10}, x = 35
Output: true
There is a pair (26, 9) with sum 35

Input: arr[] = {11, 15, 26, 38, 9, 10}, x = 45
Output: false
There is no pair with sum 45.
```

我们已经讨论了排序数组的 [O(n)解(参见方法 1 的步骤 2、3 和 4)](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)。我们也可以将此解决方案扩展到旋转阵列。其思想是首先找到数组中最大的元素，它也是轴点，紧接着最大的元素是最小的元素。一旦我们有了索引最大和最小的元素，我们就使用类似的中间相遇算法(如方法 1 中的[所讨论的)来查找是否有一对。这里唯一的新东西是使用模块化算法以循环方式递增和递减索引。](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)

以下是上述想法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a pair with a given 
// sum in a sorted and rotated array
class PairInSortedRotated
{
    // This function returns true if arr[0..n-1] 
    // has a pair with sum equals to x.
    static boolean pairInSortedRotated(int arr[], 
                                    int n, int x)
    {
        // Find the pivot element
        int i;
        for (i = 0; i < n - 1; i++)
            if (arr[i] > arr[i+1])
                break;

        int l = (i + 1) % n; // l is now index of                                          
                            // smallest element

        int r = i;       // r is now index of largest 
                         //element

        // Keep moving either l or r till they meet
        while (l != r)
        {
             // If we find a pair with sum x, we
             // return true
             if (arr[l] + arr[r] == x)
                  return true;

             // If current pair sum is less, move 
             // to the higher sum
             if (arr[l] + arr[r] < x)
                  l = (l + 1) % n;

             else  // Move to the lower sum side
                  r = (n + r - 1) % n;
        }
        return false;
    }

    /* Driver program to test above function */
    public static void main (String[] args)
    {
        int arr[] = {11, 15, 6, 8, 9, 10};
        int sum = 16;
        int n = arr.length;

        if (pairInSortedRotated(arr, n, sum))
            System.out.print("Array has two elements" +
                             " with sum 16");
        else
            System.out.print("Array doesn't have two" + 
                             " elements with sum 16 ");
    }
}
/*This code is contributed by Prakriti Gupta*/
```

**输出:**

```
Array has two elements with sum 16
```

上述解的时间复杂度为 O(n)。使用这里讨论的二分搜索法方法，可以将寻找枢轴的步骤优化为 0(Logn)。

**如何统计所有和为 x 的对？**
分步算法是:

1.  找到排序和旋转数组的轴心元素。透视元素是数组中最大的元素。最小的元素将与其相邻。
2.  使用两个指针(比如左和右)，左指针指向最小的元素，右指针指向最大的元素。
3.  求两个指针指向的元素的和。
4.  如果总和等于 x，则递增计数。如果总和小于 x，则要增加总和，请通过以旋转方式递增来将左指针移动到下一个位置。如果总和大于 x，则要减少总和，请以旋转方式递减，将右指针移动到下一个位置。
5.  重复步骤 3 和 4，直到左指针不等于右指针，或者直到左指针不等于右指针–1。
6.  打印最终计数。

下面是上述算法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find 
// number of pairs with 
// a given sum in a sorted 
// and rotated array.
import java.io.*;

class GFG
{

// This function returns
// count of number of pairs
// with sum equals to x.
static int pairsInSortedRotated(int arr[], 
                                int n, int x)
{
    // Find the pivot element. 
    // Pivot element is largest 
    // element of array.
    int i;
    for (i = 0; i < n - 1; i++)
        if (arr[i] > arr[i + 1])
            break;

    // l is index of
    // smallest element.
    int l = (i + 1) % n; 

    // r is index of 
    // largest element.
    int r = i;

    // Variable to store
    // count of number
    // of pairs.
    int cnt = 0;

    // Find sum of pair 
    // formed by arr[l] 
    // and arr[r] and 
    // update l, r and 
    // cnt accordingly.
    while (l != r)
    {
        // If we find a pair with 
        // sum x, then increment 
        // cnt, move l and r to 
        // next element.
        if (arr[l] + arr[r] == x)
        {
            cnt++;

            // This condition is required 
            // to be checked, otherwise 
            // l and r will cross each 
            // other and loop will never 
            // terminate.
            if(l == (r - 1 + n) % n)
            {
                return cnt;
            }

            l = (l + 1) % n;
            r = (r - 1 + n) % n;
        }

        // If current pair sum 
        // is less, move to 
        // the higher sum side.
        else if (arr[l] + arr[r] < x)
            l = (l + 1) % n;

        // If current pair sum 
        // is greater, move 
        // to the lower sum side.
        else
            r = (n + r - 1) % n;
    }

    return cnt;
}

// Driver Code
public static void main (String[] args) 
{
    int arr[] = {11, 15, 6, 7, 9, 10};
    int sum = 16;
    int n = arr.length;

    System.out.println(
            pairsInSortedRotated(arr, n, sum));
}
}

// This code is contributed by ajit
```

**输出:**

```
2
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
此方法由 [Nikhil Jindal](https://www.linkedin.com/in/nikhil-jindal-b1212812b/) 提出。

**练习:**
1)扩展上述解决方案，使其适用于允许重复的阵列。
本文由**希曼舒·古普塔**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息

更多细节请参考[整篇文章给定一个排序和旋转的数组，看看是否有一对给定和的](https://www.geeksforgeeks.org/given-a-sorted-and-rotated-array-find-if-there-is-a-pair-with-a-given-sum/)！