# 未排序数组中第`K`个最小/最大元素 | 组合 3（最坏情况的线性时间）

> 原文： [https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)

我们建议阅读以下文章，作为此文章的先决条件。

[未排序数组中第`K`个最小/最大元素 | 系列 1](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)

[未排序数组中第`K`个最小/最大元素 | 系列 2（预期线性时间）](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)

给定一个数组和一个数字`k`，其中`k`小于数组的大小，我们需要找到给定数组中第`k`个最小的元素。 假定所有数组元素都是不同的。

**示例**：

```
Input: arr[] = {7, 10, 4, 3, 20, 15}
       k = 3
Output: 7

Input: arr[] = {7, 10, 4, 3, 20, 15}
       k = 4
Output: 10
```



在[之前的文章](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)中，我们讨论了一种预期的线性时间算法。 在这篇文章中，讨论了最坏情况的线性时间方法。 **此新方法中的想法类似于`quickSelect()`，我们通过选择以平衡方式对数组进行分割的枢轴来获得最坏情况的线性时间（一侧上的元素很少，而另一侧的元素很多）**。 在以平衡方式分割数组之后，我们采用与`quickSelect()`中相同的步骤来确定是在数据透视表的左侧还是右侧移动。

以下是完整的算法。

`kthSmallest(arr[0..n-1], k)`：

1.  将`arr[]`分成`⌈n/5⌉`个组，每个组的大小为 5，但最后一组的元素可能少于 5 个。

2.  对上面创建的`n / 5`个分组进行排序，并找到所有分组的中位数。 创建一个辅助数组`median[]`，并将所有`⌈n/5⌉`个组的中值存储在该中值数组中。

    递归调用此方法以找到中位数`[0..⌈n/5⌉-1]`。

3.  `medOfMed = kthSmallest(median [0..⌈n/5⌉-1]], ⌈n/10⌉)`。

4.  在`medOfMed`周围划分`arr[]`并获取其位置。

`pos = partition(arr, n, medOfMed)`。

5.  如果`pos == k`，则返回`medOfMed`。

6.  如果`pos k`，则返回`kthSmallest(arr[l..pos-1], k)`。

7.  如果`pos < k`返回`kthSmallest(arr[pos + 1..r], k-pos + 1-1)`。

在上述算法中，最后 3 个步骤与[先前文章](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)中的算法相同。 前四个步骤用于获得对数组进行分区的一个好方法（以确保枢轴两边没有太多元素）。

以下是上述算法的实现。

## C++ 

```cpp

// C++ implementation of worst case linear time algorithm 
// to find k'th smallest element 
#include<iostream> 
#include<algorithm> 
#include<climits> 

using namespace std; 

int partition(int arr[], int l, int r, int k); 

// A simple function to find median of arr[].  This is called 
// only for an array of size 5 in this program. 
int findMedian(int arr[], int n) 
{ 
    sort(arr, arr+n);  // Sort the array 
    return arr[n/2];   // Return middle element 
} 

// Returns k'th smallest element in arr[l..r] in worst case 
// linear time. ASSUMPTION: ALL ELEMENTS IN ARR[] ARE DISTINCT 
int kthSmallest(int arr[], int l, int r, int k) 
{ 
    // If k is smaller than number of elements in array 
    if (k > 0 && k <= r - l + 1) 
    { 
        int n = r-l+1; // Number of elements in arr[l..r] 

        // Divide arr[] in groups of size 5, calculate median 
        // of every group and store it in median[] array. 
        int i, median[(n+4)/5]; // There will be floor((n+4)/5) groups; 
        for (i=0; i<n/5; i++) 
            median[i] = findMedian(arr+l+i*5, 5); 
        if (i*5 < n) //For last group with less than 5 elements 
        { 
            median[i] = findMedian(arr+l+i*5, n%5);  
            i++; 
        }     

        // Find median of all medians using recursive call. 
        // If median[] has only one element, then no need 
        // of recursive call 
        int medOfMed = (i == 1)? median[i-1]: 
                                 kthSmallest(median, 0, i-1, i/2); 

        // Partition the array around a random element and 
        // get position of pivot element in sorted array 
        int pos = partition(arr, l, r, medOfMed); 

        // If position is same as k 
        if (pos-l == k-1) 
            return arr[pos]; 
        if (pos-l > k-1)  // If position is more, recur for left 
            return kthSmallest(arr, l, pos-1, k); 

        // Else recur for right subarray 
        return kthSmallest(arr, pos+1, r, k-pos+l-1); 
    } 

    // If k is more than number of elements in array 
    return INT_MAX; 
} 

void swap(int *a, int *b) 
{ 
    int temp = *a; 
    *a = *b; 
    *b = temp; 
} 

// It searches for x in arr[l..r], and partitions the array  
// around x. 
int partition(int arr[], int l, int r, int x) 
{ 
    // Search for x in arr[l..r] and move it to end 
    int i; 
    for (i=l; i<r; i++) 
        if (arr[i] == x) 
           break; 
    swap(&arr[i], &arr[r]); 

    // Standard partition algorithm 
    i = l; 
    for (int j = l; j <= r - 1; j++) 
    { 
        if (arr[j] <= x) 
        { 
            swap(&arr[i], &arr[j]); 
            i++; 
        } 
    } 
    swap(&arr[i], &arr[r]); 
    return i; 
} 

// Driver program to test above methods 
int main() 
{ 
    int arr[] = {12, 3, 5, 7, 4, 19, 26}; 
    int n = sizeof(arr)/sizeof(arr[0]), k = 3; 
    cout << "K'th smallest element is "
         << kthSmallest(arr, 0, n-1, k); 
    return 0; 
} 

```

## Java

```java
// Java implementation of worst  
// case linear time algorithm 
// to find k'th smallest element 
import java.util.*; 
  
class GFG  
{ 
  
// int partition(int arr[], int l, int r, int k); 
  
// A simple function to find median of arr[]. This is called 
// only for an array of size 5 in this program. 
static int findMedian(int arr[], int i,int n) 
{ 
    if(i <= n) 
        Arrays.sort(arr, i, n); // Sort the array 
    else
        Arrays.sort(arr, n, i); 
    return arr[n/2]; // Return middle element 
} 
  
// Returns k'th smallest element 
// in arr[l..r] in worst case 
// linear time. ASSUMPTION: ALL  
// ELEMENTS IN ARR[] ARE DISTINCT 
static int kthSmallest(int arr[], int l, int r, int k) 
{ 
    // If k is smaller than  
    // number of elements in array 
    if (k > 0 && k <= r - l + 1) 
    { 
        int n = r - l + 1 ; // Number of elements in arr[l..r] 
  
        // Divide arr[] in groups of size 5,  
        // calculate median of every group 
        //  and store it in median[] array. 
        int i; 
          
         // There will be floor((n+4)/5) groups; 
        int []median = new int[(n + 4) / 5]; 
        for (i = 0; i < n/5; i++) 
            median[i] = findMedian(arr,l + i * 5, 5); 
              
        // For last group with less than 5 elements 
        if (i*5 < n)  
        { 
            median[i] = findMedian(arr,l + i * 5, n % 5);  
            i++; 
        }  
  
        // Find median of all medians using recursive call. 
        // If median[] has only one element, then no need 
        // of recursive call 
        int medOfMed = (i == 1)? median[i - 1]: 
                                kthSmallest(median, 0, i - 1, i / 2); 
  
        // Partition the array around a random element and 
        // get position of pivot element in sorted array 
        int pos = partition(arr, l, r, medOfMed); 
  
        // If position is same as k 
        if (pos-l == k - 1) 
            return arr[pos]; 
        if (pos-l > k - 1) // If position is more, recur for left 
            return kthSmallest(arr, l, pos - 1, k); 
  
        // Else recur for right subarray 
        return kthSmallest(arr, pos + 1, r, k - pos + l - 1); 
    } 
  
    // If k is more than number of elements in array 
    return Integer.MAX_VALUE; 
} 
  
static int[] swap(int []arr, int i, int j) 
{ 
    int temp = arr[i]; 
    arr[i] = arr[j]; 
    arr[j] = temp; 
    return arr; 
} 
  
// It searches for x in arr[l..r], and  
// partitions the array around x. 
static int partition(int arr[], int l, 
                        int r, int x) 
{ 
    // Search for x in arr[l..r] and move it to end 
    int i; 
    for (i = l; i < r; i++) 
        if (arr[i] == x) 
        break; 
    swap(arr, i, r); 
  
    // Standard partition algorithm 
    i = l; 
    for (int j = l; j <= r - 1; j++) 
    { 
        if (arr[j] <= x) 
        { 
            swap(arr, i, j); 
            i++; 
        } 
    } 
    swap(arr, i, r); 
    return i; 
} 
  
// Driver code 
public static void main(String[] args) 
{ 
    int arr[] = {12, 3, 5, 7, 4, 19, 26}; 
    int n = arr.length, k = 3; 
    System.out.println("K'th smallest element is "
        + kthSmallest(arr, 0, n - 1, k)); 
} 
} 
  
// This code has been contributed by 29AjayKumar 
```

## Python3

```py
# Python3 implementation of worst case   
# linear time algorithm to find  
# k'th smallest element  
  
# Returns k'th smallest element in arr[l..r]  
# in worst case linear time.  
# ASSUMPTION: ALL ELEMENTS IN ARR[] ARE DISTINCT  
def kthSmallest(arr, l, r, k):  
      
    # If k is smaller than number of  
    # elements in array  
    if (k > 0 and k <= r - l + 1):  
          
        # Number of elements in arr[l..r]  
        n = r - l + 1
  
        # Divide arr[] in groups of size 5,  
        # calculate median of every group 
        # and store it in median[] array.  
        median = [] 
  
        i = 0
        while (i < n // 5): 
            median.append(findMedian(arr, l + i * 5, 5)) 
            i += 1
  
        # For last group with less than 5 elements  
        if (i * 5 < n): 
            median.append(findMedian(arr, l + i * 5,  
                                              n % 5)) 
            i += 1
  
        # Find median of all medians using recursive call.  
        # If median[] has only one element, then no need  
        # of recursive call 
        if i == 1: 
            medOfMed = median[i - 1] 
        else: 
            medOfMed = kthSmallest(median, 0,  
                                   i - 1, i // 2) 
  
        # Partition the array around a medOfMed 
        # element and get position of pivot  
        # element in sorted array  
        pos = partition(arr, l, r, medOfMed) 
  
        # If position is same as k  
        if (pos - l == k - 1):  
            return arr[pos]  
        if (pos - l > k - 1): # If position is more,  
                              # recur for left subarray  
            return kthSmallest(arr, l, pos - 1, k)  
  
        # Else recur for right subarray  
        return kthSmallest(arr, pos + 1, r,  
                           k - pos + l - 1)  
  
    # If k is more than the number of  
    # elements in the array  
    return 999999999999
  
def swap(arr, a, b):  
    temp = arr[a]  
    arr[a] = arr[b]  
    arr[b] = temp  
  
# It searches for x in arr[l..r],   
# and partitions the array around x.  
def partition(arr, l, r, x): 
    for i in range(l, r): 
        if arr[i] == x: 
            swap(arr, r, i) 
            break
  
    x = arr[r]  
    i = l  
    for j in range(l, r):  
        if (arr[j] <= x):  
            swap(arr, i, j)  
            i += 1
    swap(arr, i, r)  
    return i  
  
# A simple function to find  
# median of arr[] from index l to l+n 
def findMedian(arr, l, n): 
    lis = [] 
    for i in range(l, l + n): 
        lis.append(arr[i]) 
          
    # Sort the array  
    lis.sort() 
  
    # Return the middle element 
    return lis[n // 2] 
  
# Driver Code  
if __name__ == '__main__':  
  
    arr = [12, 3, 5, 7, 4, 19, 26]  
    n = len(arr)  
    k = 3
    print("K'th smallest element is",  
           kthSmallest(arr, 0, n - 1, k))  
  
# This code is contributed by Ashutosh450 
```

## C#

```cs
// C# implementation of worst  
// case linear time algorithm  
// to find k'th smallest element  
using System; 
  
class GFG  
{  
  
// int partition(int arr[], int l, int r, int k);  
  
// A simple function to find median of arr[]. This is called  
// only for an array of size 5 in this program.  
static int findMedian(int []arr, int i, int n)  
{  
    if(i <= n)  
        Array.Sort(arr, i, n); // Sort the array  
    else
        Array.Sort(arr, n, i);  
    return arr[n/2]; // Return middle element  
}  
  
// Returns k'th smallest element  
// in arr[l..r] in worst case  
// linear time. ASSUMPTION: ALL  
// ELEMENTS IN ARR[] ARE DISTINCT  
static int kthSmallest(int []arr, int l, 
                            int r, int k)  
{  
    // If k is smaller than  
    // number of elements in array  
    if (k > 0 && k <= r - l + 1)  
    {  
        int n = r - l + 1 ; // Number of elements in arr[l..r]  
  
        // Divide arr[] in groups of size 5,  
        // calculate median of every group  
        // and store it in median[] array.  
        int i;  
          
        // There will be floor((n+4)/5) groups;  
        int []median = new int[(n + 4) / 5];  
        for (i = 0; i < n/5; i++)  
            median[i] = findMedian(arr, l + i * 5, 5);  
              
        // For last group with less than 5 elements  
        if (i*5 < n)  
        {  
            median[i] = findMedian(arr,l + i * 5, n % 5);  
            i++;  
        }  
  
        // Find median of all medians using recursive call.  
        // If median[] has only one element, then no need  
        // of recursive call  
        int medOfMed = (i == 1)? median[i - 1]:  
                                kthSmallest(median, 0, i - 1, i / 2);  
  
        // Partition the array around a random element and  
        // get position of pivot element in sorted array  
        int pos = partition(arr, l, r, medOfMed);  
  
        // If position is same as k  
        if (pos-l == k - 1)  
            return arr[pos];  
        if (pos-l > k - 1) // If position is more, recur for left  
            return kthSmallest(arr, l, pos - 1, k);  
  
        // Else recur for right subarray  
        return kthSmallest(arr, pos + 1, r, k - pos + l - 1);  
    }  
  
    // If k is more than number of elements in array  
    return int.MaxValue;  
}  
  
static int[] swap(int []arr, int i, int j)  
{  
    int temp = arr[i];  
    arr[i] = arr[j];  
    arr[j] = temp;  
    return arr;  
}  
  
// It searches for x in arr[l..r], and  
// partitions the array around x.  
static int partition(int []arr, int l,  
                        int r, int x)  
{  
    // Search for x in arr[l..r] and move it to end  
    int i;  
    for (i = l; i < r; i++)  
        if (arr[i] == x)  
        break;  
    swap(arr, i, r);  
  
    // Standard partition algorithm  
    i = l;  
    for (int j = l; j <= r - 1; j++)  
    {  
        if (arr[j] <= x)  
        {  
            swap(arr, i, j);  
            i++;  
        }  
    }  
    swap(arr, i, r);  
    return i;  
}  
  
// Driver code  
public static void Main(String[] args)  
{  
    int []arr = {12, 3, 5, 7, 4, 19, 26};  
    int n = arr.Length, k = 3;  
    Console.WriteLine("K'th smallest element is "
        + kthSmallest(arr, 0, n - 1, k));  
}  
}  
  
// This code contributed by Rajput-Ji 
```

输出：

```
K'th smallest element is 5
```

时间复杂度：

上述算法的最坏情况下的时间复杂度是`O(n)`。 让我们分析所有步骤。

步骤 1）和 2）占用`O(n)`时间，因为找到大小为 5 的数组的中位数需要`O(1)`时间，并且有`n / 5`个大小为 5 的数组。
步骤 3）需要`T(n / 5)`时间。 步骤 4 是标准分区，花费`O(n)`时间。
有趣的步骤是 6）和 7）。 最多只能执行其中之一。 这些是递归步骤。 这些递归调用的最坏情况是多少？ 答案是大于`medOfMed`的最大元素数（在步骤 3 中获得）或小于`medOfMed`的最大元素数。

有多少个元素比`medOfMed`大，有几个小？
在步骤 2 中找到的中位数中至少有一半大于或等于`medOfMed`。 因此，除具有少于 5 个元素的一组外，`n / 5`个组中至少有一半贡献大于`medOfMed`的 3 个元素。 因此，大于`medOfMed`的元素数量至少是：

```
3 * (⌈1/2 * ⌈n/5⌉⌉ - 2) >= 3n/10 - 6
```

同样，小于`medOfMed`的元素数至少为`3n / 10 – 6`。在最坏的情况下，该函数最多重复出现`n –(3n / 10 – 6)`个，即`7n / 10 + 6`个元素。

请注意，`7n / 10 + 6 20 20`以及任何 80 个或更少元素的输入都需要`O(1)`时间。 因此，我们可以获得循环：

![](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-42a564283606e518df4cf0a87b81a0c5_l3.png)

我们通过替换显示运行时间是线性的。 假设对于某些常数`c`且所有`n > 80`的`T(n) cn`。将该归纳假设代入递归的右边，得出：

```
T(n)  <= cn/5 + c(7n/10 + 6) + O(n)
      <= cn/5 + c + 7cn/10 + 6c + O(n)
      <= 9cn/10 + 7c + O(n)
      <= cn, 
```

因为我们可以选择足够大的`c`，使得对于所有`n > 80`，`c(n / 10 – 7)`大于`O(n)`项描述的函数。因此，[最坏的运行时间是线性的](http://staff.ustc.edu.cn/~csli/graduate/algorithms/book6/chap10.htm)。

请注意，上述算法在最坏的情况下是线性的，但是此算法的常数非常高。 因此，该算法在实际情况下效果不佳，随机化的`quickSelect`效果更好，更可取。