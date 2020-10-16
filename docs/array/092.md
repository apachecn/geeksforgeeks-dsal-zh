# 数组中两个元素的第`k`个最小绝对差

> 原文： [https://www.geeksforgeeks.org/k-th-smallest-absolute-difference-two-elements-array/](https://www.geeksforgeeks.org/k-th-smallest-absolute-difference-two-elements-array/)

给定一个大小为`n`的数组，其中包含正整数。 索引`i`和`j`处的值之间的绝对差为`|a[i] – a[j]|`。 有`n * (n-1) / 2`个这样的对，要求我们在所有这些对中打印第`k`个（`1 <= k <= n * (n-1) / 2`）最小的绝对差。

**示例**：

```
Input  : a[] = {1, 2, 3, 4}
         k = 3
Output : 1
The possible absolute differences are :
{1, 2, 3, 1, 2, 1}.
The 3rd smallest value among these is 1.

Input : n = 2
        a[] = {10, 10}
        k = 1
Output : 0

```



**朴素的方法**是找到`O(n ^ 2)`中所有`n * (n-1) / 2`个可能的绝对差并将它们存储在数组中。 然后对该数组进行排序，并打印该数组的第`k`个最小值。 这将花费时间`O(n ^ 2 + n ^ 2 * log(n ^ 2)) = O(n ^ 2 + 2 * n ^ 2 * log(n))`。

朴素的方法对于较大的`n`值（例如`n = 10 ^ 5`）不会有效。

**有效解决方案**基于二分搜索。

```
1) Sort the given array a[].
2) We can easily find the least possible absolute
   difference in O(n) after sorting. The largest
   possible difference will be a[n-1] - a[0] after
   sorting the array. Let low = minimum_difference
   and high = maximum_difference.
3) while low < high:
4)     mid = (low + high)/2
5)     if ((number of pairs with absolute difference
                                <= mid) < k):
6)        low = mid + 1
7)     else:
8)        high = mid
9) return low

```

我们需要一个函数，该函数可以有效地告诉我们差异< =中的对数。

由于对数组进行了排序，因此可以像下面这样完成此部分：

```
1) result = 0
2) for i = 0 to n-1:
3)     result = result + (upper_bound(a+i, a+n, a[i] + mid) - (a+i+1))
4) return result

```

[上界](https://www.geeksforgeeks.org/binary-search-functions-in-c-stl-binary_search-lower_bound-and-upper_bound/)是二分搜索的一种变体，它从`a[i]`到大于`[a] + mid`的`a[n-1]`返回指向第一个元素的指针。 让返回的指针为`j`。 然后`a[i] + mid < a[j]`。 因此，从中减去`a + i + 1`将得到与`a[i]`的差为`<= mid`的值的数量。 我们对所有从 0 到`n-1`的索引求和，并得到当前中值的答案。

## C++ 

```cpp

// C++ program to find k-th absolute difference 
// between two elements 
#include<bits/stdc++.h> 
using namespace std; 

// returns number of pairs with absolute difference 
// less than or equal to mid. 
int countPairs(int *a, int n, int mid) 
{ 
    int res = 0; 
    for (int i = 0; i < n; ++i) 

        // Upper bound returns pointer to position 
        // of next higher number than a[i]+mid in 
        // a[i..n-1]. We subtract (a + i + 1) from 
        // this position to count 
        res += upper_bound(a+i, a+n, a[i] + mid) - 
                                    (a + i + 1); 
    return res; 
} 

// Returns k-th absolute difference 
int kthDiff(int a[], int n, int k) 
{ 
    // Sort array 
    sort(a, a+n); 

    // Minimum absolute difference 
    int low = a[1] - a[0]; 
    for (int i = 1; i <= n-2; ++i) 
        low = min(low, a[i+1] - a[i]); 

    // Maximum absolute difference 
    int high = a[n-1] - a[0]; 

    // Do binary search for k-th absolute difference 
    while (low < high) 
    { 
        int mid = (low+high)>>1; 
        if (countPairs(a, n, mid) < k) 
            low = mid + 1; 
        else
            high = mid; 
    } 

    return low; 
} 

// Driver code 
int main() 
{ 
    int k = 3; 
    int a[] = {1, 2, 3, 4}; 
    int n = sizeof(a)/sizeof(a[0]); 
    cout << kthDiff(a, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program to find k-th absolute difference 
// between two elements 
import java.util.Scanner; 
import java.util.Arrays; 

class GFG 
{ 
    // returns number of pairs with absolute 
    // difference less than or equal to mid  
    static int countPairs(int[] a, int n, int mid) 
    { 
        int res = 0, value; 
        for(int i = 0; i < n; i++) 
        { 
            // Upper bound returns pointer to position 
            // of next higher number than a[i]+mid in 
            // a[i..n-1]. We subtract (ub + i + 1) from 
            // this position to count  
            int ub = upperbound(a, n, a[i]+mid); 
            res += (ub- (i-1)); 
        } 
        return res; 
    } 

    // returns the upper bound 
    static int upperbound(int a[], int n, int value) 
    { 
        int low = 0; 
        int high = n; 
        while(low < high) 
        { 
            final int mid = (low + high)/2; 
            if(value >= a[mid]) 
                low = mid + 1; 
            else
                high = mid; 
        } 

    return low; 
    } 

    // Returns k-th absolute difference 
    static int kthDiff(int a[], int n, int k) 
    { 
        // Sort array 
        Arrays.sort(a); 

        // Minimum absolute difference 
        int low = a[1] - a[0]; 
        for (int i = 1; i <= n-2; ++i) 
            low = Math.min(low, a[i+1] - a[i]); 

        // Maximum absolute difference 
        int high = a[n-1] - a[0]; 

        // Do binary search for k-th absolute difference 
        while (low < high) 
        { 
            int mid = (low + high) >> 1; 
            if (countPairs(a, n, mid) < k) 
                low = mid + 1; 
            else
                high = mid; 
        } 

        return low; 
    } 

    // Driver function to check the above functions 
    public static void main(String args[]) 
    { 
        Scanner s = new Scanner(System.in); 
        int k = 3; 
        int a[] = {1,2,3,4}; 
        int n = a.length; 
        System.out.println(kthDiff(a, n, k)); 
    } 

} 
// This code is contributed by nishkarsh146 

```

## Python3

```py

# Python3 program to find  
# k-th absolute difference  
# between two elements  
from bisect import bisect as upper_bound  

# returns number of pairs with  
# absolute difference less than  
# or equal to mid.  
def countPairs(a, n, mid):  
    res = 0
    for i in range(n):  

        # Upper bound returns pointer to position  
        # of next higher number than a[i]+mid in  
        # a[i..n-1]. We subtract (a + i + 1) from  
        # this position to count  
        res += upper_bound(a, a[i] + mid)  
    return res  

# Returns k-th absolute difference  
def kthDiff(a, n, k):  

    # Sort array  
    a = sorted(a)  

    # Minimum absolute difference  
    low = a[1] - a[0]  
    for i in range(1, n - 1):  
        low = min(low, a[i + 1] - a[i])  

    # Maximum absolute difference  
    high = a[n - 1] - a[0]  

    # Do binary search for k-th absolute difference  
    while (low < high):  
        mid = (low + high) >> 1
        if (countPairs(a, n, mid) < k):  
            low = mid + 1
        else:  
            high = mid  

    return low  

# Driver code  
k = 3
a = [1, 2, 3, 4]  
n = len(a)  
print(kthDiff(a, n, k))  

# This code is contributed by Mohit Kumar  

```

输出：

```
1

```

该算法的时间复杂度为`O(n * logn + n * logn * logn)`。 排序需要`O(n * logn)`。 之后，在低位和高位进行主要的二分搜索需要`O(n * logn * logn)`时间，因为每次对函数`int f(int c, int n, int * a)`的调用都需要时间`O(n * logn)`。

