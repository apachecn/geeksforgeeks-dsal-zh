# 要删除的最短子数组，以使所有 Array 元素唯一

> 原文：[https://www.geeksforgeeks.org/shortest-subarray-to-be-removed-to-make-all-array-elements-unique/](https://www.geeksforgeeks.org/shortest-subarray-to-be-removed-to-make-all-array-elements-unique/)

给定包含 **N** 个元素的数组 **arr []** ，任务是从给定数组中删除最小可能长度的子数组，以使所有其余元素成对区分。 打印子数组的最小可能长度。

**范例**：

> **输入**：N = 5，arr [] = {1、2、1、2、3}
> **输出**：2
> **说明**：
> 删除子数组{2，1}以使元素区分。
> 
> **输入**：N = 5，arr [] = {1,2,3,4,5}
> **输出**：0
> **说明**：
> 元素已经不同。

**朴素方法**：针对此问题的朴素方法是简单地检查所有可能的子数组，并找到最小的子数组的长度，然后删除该数组中所有元素成对区分的最小子数组。

**时间复杂度**：O（N <sup>3</sup> ）

**有效方法**：

*   令**和**为最小子数组的长度，该子数组从给定数组中删除时，使该数组的元素唯一。

*   我们可以很容易地观察到，如果在删除长度为 **ans** 的子数组后，所有数组元素都变得不同，则对于大于 **ans** 的所有值，此条件也成立。

*   这意味着该问题的解决方案是单调递增的函数，我们可以在答案上应用[二进制搜索](http://www.geeksforgeeks.org/binary-search/)。

*   现在，对于子数组的特定长度 **K** ，我们可以检查长度为 **K** 的所有子数组的前缀和后缀元素是否成对区分。

*   我们可以使用[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)来做到这一点。

*   使用[哈希图](https://www.geeksforgeeks.org/hashing-data-structure/)将元素的[频率存储在前缀和后缀中，向前移动窗口时，前缀的最后一个元素的递增频率和后缀的第一个元素的递减频率 。](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)

下面是上述方法的实现：

## C++

```cpp

// C++ program to make array elements  
// pairwise distinct by removing at most  
// one subarray of minimum length  

#include <bits/stdc++.h>  
using namespace std;  

// Function to check if elements of  
// Prefix and suffix of each sub array  
// of size K are pairwise distinct or not  
bool check(int a[], int n, int k)  
{  
    // Hash map to store frequencies of  
    // elements of prefix and suffix  
    map<int, int> m;  

    // Variable to store number of  
    // occurrences of an element other  
    // than one  
    int extra = 0;  

    // Adding frequency of elements of suffix  
    // to hash for subarray starting from first  
    // index  
    // There is no prefix for this sub array  
    for (int i = k; i < n; i++)  
        m[a[i]]++;  

    // Counting extra elements in current Hash  
    // map  
    for (auto x : m)  
        extra += x.second - 1;  

    // If there are no extra elements return  
    // true  
    if (extra == 0)  
        return true;  

    // Check for remaining sub arrays  

    for (int i = 1; i + k - 1 < n; i++) {  

        // First element of suffix is now  
        // part of subarray which is being  
        // removed so, check for extra elements  
        if (m[a[i + k - 1]] > 1)  
            extra--;  

        // Decrement frequency of first  
        // element of the suffix  
        m[a[i + k - 1]]--;  

        // Increment frequency of last  
        // element of the prefix  
        m[a[i - 1]]++;  

        // Check for extra elements  
        if (m[a[i - 1]] > 1)  
            extra++;  

        // If there are no extra elements  
        // return true  
        if (extra == 0)  
            return true;  
    }  

    return false;  
}  

// Function for calculating minimum  
// length of the subarray, which on  
// removing make all elements pairwise  
// distinct  
int minlength(int a[], int n)  
{  
    // Possible range of length of subarray  
    int lo = 0, hi = n + 1;  

    int ans = 0;  

    // Binary search to find minimum ans  
    while (lo < hi) {  

        int mid = (lo + hi) / 2;  

        if (check(a, n, mid)) {  
            ans = mid;  
            hi = mid;  
        }  
        else
            lo = mid + 1;  
    }  

    return ans;  
}  

// Driver code  
int main()  
{  
    int a[5] = { 1, 2, 1, 2, 3 };  

    int n = sizeof(a) / sizeof(int);  

    cout << minlength(a, n);  
}  

```

## Java

```java

// Java program to make array elements  
// pairwise distinct by removing at most  
// one subarray of minimum length  
import java.util.*; 
import java.lang.*; 

class GFG{ 

// Function to check if elements of  
// Prefix and suffix of each sub array  
// of size K are pairwise distinct or not  
static boolean check(int a[], int n, int k)  
{  

    // Hash map to store frequencies of  
    // elements of prefix and suffix  
    Map<Integer, Integer> m = new HashMap<>();  

    // Variable to store number of  
    // occurrences of an element other  
    // than one  
    int extra = 0;  

    // Adding frequency of elements of suffix  
    // to hash for subarray starting from first  
    // index  
    // There is no prefix for this sub array  
    for(int i = k; i < n; i++)  
        m.put(a[i], m.getOrDefault(a[i], 0) + 1);  

    // Counting extra elements in current Hash  
    // map  
    for(Integer x : m.values())  
        extra += x - 1;  

    // If there are no extra elements return  
    // true  
    if (extra == 0)  
        return true;  

    // Check for remaining sub arrays  
    for(int i = 1; i + k - 1 < n; i++) 
    {  

        // First element of suffix is now  
        // part of subarray which is being  
        // removed so, check for extra elements  
        if (m.get(a[i + k - 1]) > 1)  
            extra--;  

        // Decrement frequency of first  
        // element of the suffix  
        m.put(a[i + k - 1], 
        m.get(a[i + k - 1]) - 1);  

        // Increment frequency of last  
        // element of the prefix  
        m.put(a[i - 1], m.get(a[i - 1]) + 1);  

        // Check for extra elements  
        if (m.get(a[i - 1]) > 1)  
            extra++;  

        // If there are no extra elements  
        // return true  
        if (extra == 0)  
            return true;  
    }  
    return false;  
}  

// Function for calculating minimum  
// length of the subarray, which on  
// removing make all elements pairwise  
// distinct  
static int minlength(int a[], int n)  
{  

    // Possible range of length of subarray  
    int lo = 0, hi = n + 1;  

    int ans = 0;  

    // Binary search to find minimum ans  
    while (lo < hi) 
    {  
        int mid = (lo + hi) / 2;  

        if (check(a, n, mid)) 
        {  
            ans = mid;  
            hi = mid;  
        }  
        else
            lo = mid + 1;  
    }  
    return ans;  
} 

// Driver Code 
public static void main (String[] args)  
{ 
    int a[] = { 1, 2, 1, 2, 3 };  

    int n = a.length;  

    System.out.println(minlength(a, n));  
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program to make array elements  
# pairwise distinct by removing at most  
# one subarray of minimum length  
from collections import defaultdict  

# Function to check if elements of  
# Prefix and suffix of each sub array  
# of size K are pairwise distinct or not  
def check(a, n, k):  

    # Hash map to store frequencies of  
    # elements of prefix and suffix  
    m = defaultdict(int)  

    # Variable to store number of  
    # occurrences of an element other  
    # than one  
    extra = 0

    # Adding frequency of elements of suffix  
    # to hash for subarray starting from first  
    # index  
    # There is no prefix for this sub array  
    for i in range(k, n):  
        m[a[i]] += 1

    # Counting extra elements in current Hash  
    # map  
    for x in m:  
        extra += m[x] - 1

    # If there are no extra elements return  
    # true  
    if (extra == 0):  
        return True

    # Check for remaining sub arrays  
    for i in range(1, i + k - 1 < n):  

        # First element of suffix is now  
        # part of subarray which is being  
        # removed so, check for extra elements  
        if (m[a[i + k - 1]] > 1):  
            extra -= 1

        # Decrement frequency of first  
        # element of the suffix  
        m[a[i + k - 1]] -= 1

        # Increment frequency of last  
        # element of the prefix  
        m[a[i - 1]] += 1

        # Check for extra elements  
        if (m[a[i - 1]] > 1):  
            extra += 1

        # If there are no extra elements  
        # return true  
        if (extra == 0):  
            return True

    return False

# Function for calculating minimum  
# length of the subarray, which on  
# removing make all elements pairwise  
# distinct  
def minlength(a, n):  

    # Possible range of length of subarray  
    lo = 0
    hi = n + 1

    ans = 0

    # Binary search to find minimum ans  
    while (lo < hi):  
        mid = (lo + hi) // 2

        if (check(a, n, mid)):  
            ans = mid  
            hi = mid  
        else:  
            lo = mid + 1

    return ans  

# Driver code  
if __name__ == "__main__":  

    a = [ 1, 2, 1, 2, 3 ]  
    n = len(a)  

    print(minlength(a, n))  

# This code is contributed by chitranayal  

```

## C#

```cs

// C# program to make array elements  
// pairwise distinct by removing at most  
// one subarray of minimum length  
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to check if elements of  
// Prefix and suffix of each sub array  
// of size K are pairwise distinct or not  
static bool check(int []a, int n, int k)  
{  

    // Hash map to store frequencies of  
    // elements of prefix and suffix  
    Dictionary<int,  
               int> m = new Dictionary<int,  
                                       int>();  

    // Variable to store number of  
    // occurrences of an element other  
    // than one  
    int extra = 0;  

    // Adding frequency of elements of suffix  
    // to hash for subarray starting from first  
    // index  
    // There is no prefix for this sub array  
    for(int i = k; i < n; i++)  
        if(m.ContainsKey(a[i])) 
            m[a[i]] = m[a[i]] + 1; 
        else
            m.Add(a[i], 1);  

    // Counting extra elements in current Hash  
    // map  
    foreach(int x in m.Keys)  
        extra += m[x] - 1;  

    // If there are no extra elements return  
    // true  
    if (extra == 0)  
        return true;  

    // Check for remaining sub arrays  
    for(int i = 1; i + k - 1 < n; i++) 
    {  

        // First element of suffix is now  
        // part of subarray which is being  
        // removed so, check for extra elements  
        if (m[a[i + k - 1]] > 1)  
            extra--;  

        // Decrement frequency of first  
        // element of the suffix  
        m[a[i + k - 1]] = m[a[i + k - 1]] - 1;  

        // Increment frequency of last  
        // element of the prefix  
        m[a[i - 1]] = m[a[i - 1]] + 1;  

        // Check for extra elements  
        if (m[a[i - 1]] > 1)  
            extra++;  

        // If there are no extra elements  
        // return true  
        if (extra == 0)  
            return true;  
    }  
    return false;  
}  

// Function for calculating minimum  
// length of the subarray, which on  
// removing make all elements pairwise  
// distinct  
static int minlength(int []a, int n)  
{  

    // Possible range of length of subarray  
    int lo = 0, hi = n + 1;  

    int ans = 0;  

    // Binary search to find minimum ans  
    while (lo < hi) 
    {  
        int mid = (lo + hi) / 2;  

        if (check(a, n, mid)) 
        {  
            ans = mid;  
            hi = mid;  
        }  
        else
            lo = mid + 1;  
    }  
    return ans;  
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    int []a = { 1, 2, 1, 2, 3 };  
    int n = a.Length;  

    Console.WriteLine(minlength(a, n));  
} 
} 

// This code is contributed by Amit Katiyar  

```

**Output:** 

```
2

```

**时间复杂度**：*`O(N * log(N))`*，其中 N 是数组的大小。



* * *

* * *



