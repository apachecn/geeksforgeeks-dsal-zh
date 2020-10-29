# 最长子数组，不超过 K 个不同元素

> 原文：[https://www.geeksforgeeks.org/longest-subarray-not-k-distinct-elements/](https://www.geeksforgeeks.org/longest-subarray-not-k-distinct-elements/)

给定 N 个元素和一个数字 K，找到最长不超过 K 个不同元素的子数组（它可以少于 K 个）

**示例**：

```
Input : arr[] = {1, 2, 3, 4, 5}
            k = 6 
Output : 1 2 3 4 5 
Explanation: The whole array has only 5 
distinct elements which is less than k, 
so we print the array itself.

Input: arr[] = {6, 5, 1, 2, 3, 2, 1, 4, 5}
           k = 3
Output: 1 2 3 2 1, 
The output is the longest subarray with 3
distinct elements.

```

**朴素的方法**将遍历数组，并对每个子数组使用散列，并检查不超过 K 个不同元素的最长子数组。

**有效方法**使用*两个指针*的概念，其中我们维护一个散列来计数元素的出现。 我们从头开始，一直计数不同的元素，直到数量超过 k。 一旦它超过 K，我们就开始从子数组开始的地方开始减少哈希中元素的数量，并随着子数组的减少而减少我们的长度，从而指针向右移动。 我们不断删除元素，直到再次获得 k 个不同的元素。 我们继续这个过程，直到我们再次拥有超过 k 个不同的元素，并在此之前保持左指针不变。 如果新的子数组长度大于前一个子数组的长度，我们将根据其更新开始和结束。

## C++

```cpp

// CPP program to find longest subarray with 
// k or less distinct elements. 
#include <bits/stdc++.h> 
using namespace std; 

// function to print the longest sub-array 
void longest(int a[], int n, int k) 
{ 
    unordered_map<int, int> freq; 

    int start = 0, end = 0, now = 0, l = 0; 
    for (int i = 0; i < n; i++) { 

        // mark the element visited 
        freq[a[i]]++; 

        // if its visited first time, then increase 
        // the counter of distinct elements by 1 
        if (freq[a[i]] == 1) 
            now++; 

        // When the counter of distinct elements 
        // increases from k, then reduce it to k 
        while (now > k) { 

            // from the left, reduce the number of 
            // time of visit 
            freq[a[l]]--; 

            // if the reduced visited time element 
            // is not present in further segment 
            // then decrease the count of distinct 
            // elements 
            if (freq[a[l]] == 0) 
                now--; 

            // increase the subsegment mark 
            l++; 
        } 

        // check length of longest sub-segment 
        // when greater then previous best 
        // then change it 
        if (i - l + 1 >= end - start + 1) 
            end = i, start = l; 
    } 

    // print the longest sub-segment 
    for (int i = start; i <= end; i++) 
        cout << a[i] << " "; 
} 

// driver program to test the above function 
int main() 
{ 
    int a[] = { 6, 5, 1, 2, 3, 2, 1, 4, 5 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int k = 3; 
    longest(a, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program to find longest subarray with 
// k or less distinct elements. 
import java.util.*; 

class GFG 
{ 

// function to print the longest sub-array 
static void longest(int a[], int n, int k) 
{ 
    int[] freq = new int[7]; 

    int start = 0, end = 0, now = 0, l = 0; 
    for (int i = 0; i < n; i++) 
    { 

        // mark the element visited 
        freq[a[i]]++; 

        // if its visited first time, then increase 
        // the counter of distinct elements by 1 
        if (freq[a[i]] == 1) 
            now++; 

        // When the counter of distinct elements 
        // increases from k, then reduce it to k 
        while (now > k) 
        { 

            // from the left, reduce the number of 
            // time of visit 
            freq[a[l]]--; 

            // if the reduced visited time element 
            // is not present in further segment 
            // then decrease the count of distinct 
            // elements 
            if (freq[a[l]] == 0) 
                now--; 

            // increase the subsegment mark 
            l++; 
        } 

        // check length of longest sub-segment 
        // when greater then previous best 
        // then change it 
        if (i - l + 1 >= end - start + 1) 
        { 
            end = i; 
            start = l; 
        } 
    } 

    // print the longest sub-segment 
    for (int i = start; i <= end; i++) 
        System.out.print(a[i]+" "); 
} 

// Driver code 
public static void main(String args[]) 
{ 
    int a[] = { 6, 5, 1, 2, 3, 2, 1, 4, 5 }; 
    int n = a.length; 
    int k = 3; 
    longest(a, n, k); 
} 
} 

// This code is contributed by 
// Surendra_Gangwar 

```

## Python 3

```

# Python 3 program to find longest  
# subarray with k or less distinct elements. 

# function to print the longest sub-array 
def longest(a, n, k): 

    freq = [0] * n 

    start = 0
    end = 0
    now = 0
    l = 0
    for i in range(n): 

        # mark the element visited 
        freq[a[i]] += 1

        # if its visited first time, then increase 
        # the counter of distinct elements by 1 
        if (freq[a[i]] == 1): 
            now += 1

        # When the counter of distinct elements 
        # increases from k, then reduce it to k 
        while (now > k) : 

            # from the left, reduce the number  
            # of time of visit 
            freq[a[l]] -= 1

            # if the reduced visited time element 
            # is not present in further segment 
            # then decrease the count of distinct 
            # elements 
            if (freq[a[l]] == 0): 
                now -= 1

            # increase the subsegment mark 
            l += 1

        # check length of longest sub-segment 
        # when greater then previous best 
        # then change it 
        if (i - l + 1 >= end - start + 1): 
            end = i 
            start = l 

    # print the longest sub-segment 
    for i in range(start, end + 1): 
        print(a[i], end = " ") 

# Driver Code 
if __name__ == "__main__": 

    a = [ 6, 5, 1, 2, 3,  
             2, 1, 4, 5 ] 
    n = len(a) 
    k = 3
    longest(a, n, k) 

# This code is contributed 
# by ChitraNayal 

```

## C#

```cs

// C# program to find longest subarray with 
// k or less distinct elements. 
using System; 

class GFG 
{ 

// function to print the longest sub-array 
static void longest(int []a, int n, int k) 
{ 
    int[] freq = new int[7]; 

    int start = 0, end = 0, now = 0, l = 0; 
    for (int i = 0; i < n; i++) 
    { 

        // mark the element visited 
        freq[a[i]]++; 

        // if its visited first time, then increase 
        // the counter of distinct elements by 1 
        if (freq[a[i]] == 1) 
            now++; 

        // When the counter of distinct elements 
        // increases from k, then reduce it to k 
        while (now > k) 
        { 

            // from the left, reduce the number of 
            // time of visit 
            freq[a[l]]--; 

            // if the reduced visited time element 
            // is not present in further segment 
            // then decrease the count of distinct 
            // elements 
            if (freq[a[l]] == 0) 
                now--; 

            // increase the subsegment mark 
            l++; 
        } 

        // check length of longest sub-segment 
        // when greater then previous best 
        // then change it 
        if (i - l + 1 >= end - start + 1) 
        { 
            end = i; 
            start = l; 
        } 
    } 

    // print the longest sub-segment 
    for (int i = start; i <= end; i++) 
        Console.Write(a[i]+" "); 
} 

// Driver code 
public static void Main(String []args) 
{ 
    int []a = { 6, 5, 1, 2, 3, 2, 1, 4, 5 }; 
    int n = a.Length; 
    int k = 3; 
    longest(a, n, k); 
} 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
1 2 3 2 1 

```

**时间复杂度**：`O(n)`

本文由 [**Striver**](https://www.facebook.com/raja.vikramaditya.7) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

