# 3 向合并排序

> 原文:[https://www.geeksforgeeks.org/3-way-merge-sort/](https://www.geeksforgeeks.org/3-way-merge-sort/)

先决条件–[合并排序](https://www.geeksforgeeks.org/merge-sort/)

合并排序包括递归地将数组分成两部分，排序，最后合并它们。合并排序的一种变体叫做 3 路合并排序，我们不是把数组分成 2 部分，而是把它分成 3 部分。
合并排序递归地将数组分解成一半大小的子数组。类似地，3 向合并排序将数组分解为三分之一大小的子数组。

**例:** 

```
Input  : 45, -2, -45, 78, 30, -42, 10, 19 , 73, 93 
Output : -45 -42 -2 10 19 30 45 73 78 93 

Input  : 23, -19
Output : -19  23

```

## C++

```
// C++ Program to perform 3 way Merge Sort
#include <bits/stdc++.h>
using namespace std;

/* Merge the sorted ranges [low, mid1), [mid1,mid2) 
and [mid2, high) mid1 is first midpoint 
index in overall range to merge mid2 is second 
midpoint index in overall range to merge*/
void merge(int gArray[], int low, int mid1, 
           int mid2, int high, int destArray[]) 
{ 
    int i = low, j = mid1, k = mid2, l = low; 

    // choose smaller of the smallest in the three ranges 
    while ((i < mid1) && (j < mid2) && (k < high)) 
    { 
        if(gArray[i] < gArray[j])
        {
            if(gArray[i] < gArray[k])
            {
                destArray[l++] = gArray[i++];
            }
            else
            {
                destArray[l++] = gArray[k++];
            }
        }
        else
        {
            if(gArray[j] < gArray[k])
            {
                destArray[l++] = gArray[j++];
            }
            else
            {
                destArray[l++] = gArray[k++];
            }
        }
    } 

    // case where first and second ranges
    // have remaining values 
    while ((i < mid1) && (j < mid2)) 
    { 
        if(gArray[i] < gArray[j])
        {
            destArray[l++] = gArray[i++];
        }
        else
        {
            destArray[l++] = gArray[j++];
        }
    } 

    // case where second and third ranges
    // have remaining values 
    while ((j < mid2) && (k < high)) 
    { 
        if(gArray[j] < gArray[k])
        {
            destArray[l++] = gArray[j++];
        }
        else
        {
            destArray[l++] = gArray[k++];
        } 
    } 

    // case where first and third ranges have 
    // remaining values 
    while ((i < mid1) && (k < high)) 
    { 
        if(gArray[i] < gArray[k])
        {
            destArray[l++] = gArray[i++];
        }
        else
        {
            destArray[l++] = gArray[k++];
        } 
    } 

    // copy remaining values from the first range 
    while (i < mid1) 
        destArray[l++] = gArray[i++]; 

    // copy remaining values from the second range 
    while (j < mid2) 
        destArray[l++] = gArray[j++]; 

    // copy remaining values from the third range 
    while (k < high) 
        destArray[l++] = gArray[k++]; 
} 

/* Performing the merge sort algorithm on the 
given array of values in the rangeof indices 
[low, high). low is minimum index, high is 
maximum index (exclusive) */
void mergeSort3WayRec(int gArray[], int low,
                      int high, int destArray[]) 
{ 
    // If array size is 1 then do nothing 
    if (high - low < 2) 
        return; 

    // Splitting array into 3 parts 
    int mid1 = low + ((high - low) / 3); 
    int mid2 = low + 2 * ((high - low) / 3) + 1; 

    // Sorting 3 arrays recursively 
    mergeSort3WayRec(destArray, low, mid1, gArray); 
    mergeSort3WayRec(destArray, mid1, mid2, gArray); 
    mergeSort3WayRec(destArray, mid2, high, gArray); 

    // Merging the sorted arrays 
    merge(destArray, low, mid1, mid2, high, gArray); 
}

void mergeSort3Way(int gArray[], int n) 
{ 
    // if array size is zero return null 
    if (n == 0) 
        return; 

    // creating duplicate of given array 
    int fArray[n]; 

    // copying alements of given array into 
    // duplicate array 
    for (int i = 0; i < n; i++) 
        fArray[i] = gArray[i]; 

    // sort function 
    mergeSort3WayRec(fArray, 0, n, gArray); 

    // copy back elements of duplicate array 
    // to given array 
    for (int i = 0; i < n; i++) 
        gArray[i] = fArray[i]; 
} 

// Driver Code
int main()
{
    int data[] = {45, -2, -45, 78, 30, 
                 -42, 10, 19, 73, 93};
    mergeSort3Way(data,10);
    cout << "After 3 way merge sort: ";
    for (int i = 0; i < 10; i++)
    {
        cout << data[i] << " ";
    }
    return 0;
}

// This code is contributed by Rashmi Kumari
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform 3 way Merge Sort
import java.util.*;
public class MergeSort3Way
{
    // Function  for 3-way merge sort process
    public static void mergeSort3Way(Integer[] gArray)
    {
        // if array of size is zero returns null
        if (gArray == null)
            return;

        // creating duplicate of given array
        Integer[] fArray = new Integer[gArray.length];

        // copying alements of given array into
        // duplicate array
        for (int i = 0; i < fArray.length; i++)
            fArray[i] = gArray[i];

        // sort function
        mergeSort3WayRec(fArray, 0, gArray.length, gArray);

        // copy back elements of duplicate array
        // to given array
        for (int i = 0; i < fArray.length; i++)
            gArray[i] = fArray[i];
    }

    /* Performing the merge sort algorithm on the
       given array of values in the rangeof indices
       [low, high).  low is minimum index, high is
       maximum index (exclusive) */
    public static void mergeSort3WayRec(Integer[] gArray,
                  int low, int high, Integer[] destArray)
    {
        // If array size is 1 then do nothing
        if (high - low < 2)
            return;

        // Splitting array into 3 parts
        int mid1 = low + ((high - low) / 3);
        int mid2 = low + 2 * ((high - low) / 3) + 1;

        // Sorting 3 arrays recursively
        mergeSort3WayRec(destArray, low, mid1, gArray);
        mergeSort3WayRec(destArray, mid1, mid2, gArray);
        mergeSort3WayRec(destArray, mid2, high, gArray);

        // Merging the sorted arrays
        merge(destArray, low, mid1, mid2, high, gArray);
    }

    /* Merge the sorted ranges [low, mid1), [mid1,
       mid2) and [mid2, high) mid1 is first midpoint
       index in overall range to merge mid2 is second
       midpoint index in overall range to merge*/
    public static void merge(Integer[] gArray, int low,
                           int mid1, int mid2, int high,
                                   Integer[] destArray)
    {
        int i = low, j = mid1, k = mid2, l = low;

        // choose smaller of the smallest in the three ranges
        while ((i < mid1) && (j < mid2) && (k < high))
        {
            if (gArray[i].compareTo(gArray[j]) < 0)
            {
                if (gArray[i].compareTo(gArray[k]) < 0)
                    destArray[l++] = gArray[i++];

                else
                    destArray[l++] = gArray[k++];
            }
            else
            {
                if (gArray[j].compareTo(gArray[k]) < 0)
                    destArray[l++] = gArray[j++];
                else
                    destArray[l++] = gArray[k++];
            }
        }

        // case where first and second ranges have
        // remaining values
        while ((i < mid1) && (j < mid2))
        {
            if (gArray[i].compareTo(gArray[j]) < 0)
                destArray[l++] = gArray[i++];
            else
                destArray[l++] = gArray[j++];
        }

        // case where second and third ranges have
        // remaining values
        while ((j < mid2) && (k < high))
        {
            if (gArray[j].compareTo(gArray[k]) < 0)
                destArray[l++] = gArray[j++];

            else
                destArray[l++] = gArray[k++];
        }

        // case where first and third ranges have
        // remaining values
        while ((i < mid1) && (k < high))
        {
            if (gArray[i].compareTo(gArray[k]) < 0)
                destArray[l++] = gArray[i++];
            else
                destArray[l++] = gArray[k++];
        }

        // copy remaining values from the first range
        while (i < mid1)
            destArray[l++] = gArray[i++];

        // copy remaining values from the second range
        while (j < mid2)
            destArray[l++] = gArray[j++];

        // copy remaining values from the third range
        while (k < high)
            destArray[l++] = gArray[k++];
    }

    // Driver function
    public static void main(String args[])
    {
        // test case of values
        Integer[] data = new Integer[] {45, -2, -45, 78,
                               30, -42, 10, 19, 73, 93};
        mergeSort3Way(data);

        System.out.println("After 3 way merge sort: ");
        for (int i = 0; i < data.length; i++)
            System.out.print(data[i] + " ");
    }
}
```

**Output:**

```
After 3 way merge sort: 
-45 -42 -2 10 19 30 45 73 78 93 
```

在这里，我们首先将数据数组的内容复制到另一个名为 fArray 的数组中。然后，通过寻找将数组分成 3 部分的中点对数组进行排序，并分别对每个数组调用排序函数。递归的基本情况是当数组的大小为 1 时，它从函数返回。然后开始合并数组，最后排序后的数组将在 fArray 中，并被复制回 gArray。

**时间复杂度**:在双向归并排序的情况下我们得到方程:T(n) = 2T(n/2) + O(n)
同样，在三向归并排序的情况下我们得到方程:T(n) = 3T(n/3) + O(n)
通过使用[大师方法](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)求解，我们得到它的复杂度为 **O(n log <sub>3</sub> n】。**。虽然与 [2 路合并排序](https://www.geeksforgeeks.org/merge-sort/)相比，时间复杂度看起来更低，但实际花费的时间可能会变得更长，因为合并函数中的比较次数变得更多。请参考[为什么二分搜索法优于三元搜索？](https://www.geeksforgeeks.org/binary-search-preferred-ternary-search/)详见。

**类似文章:**
[3 路快速排序](https://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/)

本文由 **Pavan Gopal Rayapati** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。