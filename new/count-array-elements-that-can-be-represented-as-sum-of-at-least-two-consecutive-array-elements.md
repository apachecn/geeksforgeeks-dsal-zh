# 对可以表示为至少两个连续数组元素之和的数组元素进行计数

> 原文：[https://www.geeksforgeeks.org/count-array-elements-that-can-be-represented-as-sum-of-at-least-two-consecutive-array-elements/](https://www.geeksforgeeks.org/count-array-elements-that-can-be-represented-as-sum-of-at-least-two-consecutive-array-elements/)

给定一个数组 **A []** ，该数组由 **[1，N]** 范围内的 **N** 个整数组成，任务是计算数组元素的数量（非 可以表示为两个或多个连续数组元素的总和。

**示例**：

> **输入**：a [] = {3，1，4，1，5，9，9，6，5}
> **输出**：5
> **说明 **：
> 满足条件的数组元素是：
> 4 = 3 +1
> 5 = 1 + 4 或 4 +1
> 9 = 3 +1 + 4 +1
> 6 = 1 + 5 或 1 + 4 +1
> 5 = 1 + 4 或 4 +1
> 
> **输入**：a [] = {1，1，1，1，1}
> **输出**：0
> **说明**：
> 否 存在这样的数组元素，可以将其表示为两个或更多连续元素的总和。

**朴素的方法**：[遍历每个元素的给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，找到所有可能的子数组的总和，并检查任何子数组的总和是否等于当前元素的总和。 如果发现是真的，则增加计数。 最后，打印获得的计数。

**时间复杂度**：O（n <sup>3</sup> ）

**辅助空间**：`O(1)`

**高效方法**：请按照以下步骤优化上述方法：

*   初始化数组 **cnt []** ，以存储每个数组元素的出现次数。

*   迭代所有长度至少为 2 的子数组，并保持当前子数组总和。

*   如果当前总和不超过 **N** ，则将 cnt [sum]添加到答案并设置 cnt [sum] = 0 以防止多次计数相同的元素。

*   最后，打印获得的总和。

下面是上述方法的实现：

## C++

```cpp

// C++ program for above approach  
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the number of 
// array elements that can be  
// represented as the sum of two  
// or more consecutive array elements 
int countElements(int a[], int n) 
{ 

    // Stores the frequencies 
    // of array elements 
    int cnt[n + 1] = {0}; 
    memset(cnt, 0, sizeof(cnt)); 

    // Stores required count 
    int ans = 0; 

    // Update frequency of 
    // each array element 
    for(int i = 0; i < n; i++) 
    { 
        ++cnt[a[i]]; 
    } 

    // Find sum of all subarrays 
    for(int l = 0; l < n; ++l) 
    { 
        int sum = 0; 

        for(int r = l; r < n; ++r) 
        { 
            sum += a[r]; 

            if (l == r) 
                continue; 

            if (sum <= n) 
            { 

                // Increment ans by cnt[sum] 
                ans += cnt[sum]; 

                // Reset cnt[sum] by 0 
                cnt[sum] = 0; 
            } 
        } 
    } 

    // Return ans 
    return ans; 
} 

// Driver Code 
int main() 
{ 

    // Given array 
    int a[] = { 1, 1, 1, 1, 1 }; 
    int N = sizeof(a) / sizeof(a[0]); 

    // Function call 
    cout << countElements(a, N); 
} 

// This code is contributed by Amit Katiyar

```

## Java

```java

// Java Program for above approach 

import java.util.*; 
class GFG { 

    // Function to find the number of array 
    // elements that can be represented as the sum 
    // of two or more consecutive array elements 
    static int countElements(int[] a, int n) 
    { 
        // Stores the frequencies 
        // of array elements 
        int[] cnt = new int[n + 1]; 

        // Stores required count 
        int ans = 0; 

        // Update frequency of 
        // each array element 
        for (int k : a) { 
            ++cnt[k]; 
        } 

        // Find sum of all subarrays 
        for (int l = 0; l < n; ++l) { 

            int sum = 0; 

            for (int r = l; r < n; ++r) { 
                sum += a[r]; 

                if (l == r) 
                    continue; 

                if (sum <= n) { 

                    // Increment ans by cnt[sum] 
                    ans += cnt[sum]; 

                    // Reset cnt[sum] by 0 
                    cnt[sum] = 0; 
                } 
            } 
        } 

        // Return ans 
        return ans; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        // Given array 
        int[] a = { 1, 1, 1, 1, 1 }; 

        // Function call 
        System.out.println( 
            countElements(a, a.length)); 
    } 
}

```

## Python3

```py

# Python3 program for above approach 

# Function to find the number of array 
# elements that can be represented as the sum 
# of two or more consecutive array elements 
def countElements(a, n): 

    # Stores the frequencies 
    # of array elements 
    cnt = [0] * (n + 1) 

    # Stores required count 
    ans = 0

    # Update frequency of 
    # each array element 
    for k in a: 
        cnt[k] += 1

    # Find sum of all subarrays 
    for l in range(n): 
        sum = 0

        for r in range(l, n): 
            sum += a[r] 

            if (l == r): 
                continue
            if (sum <= n): 

                # Increment ans by cnt[sum] 
                ans += cnt[sum] 

                # Reset cnt[sum] by 0 
                cnt[sum] = 0

    # Return ans 
    return ans 

# Driver Code 
if __name__ == '__main__': 

    # Given array 
    a = [ 1, 1, 1, 1, 1 ] 

    # Function call 
    print(countElements(a, len(a))) 

# This code is contributed by mohit kumar 29 

```

## C#

```cs

// C# program for above approach 
using System; 

class GFG{ 

// Function to find the number of array 
// elements that can be represented as the sum 
// of two or more consecutive array elements 
static int countElements(int[] a, int n) 
{ 

    // Stores the frequencies 
    // of array elements 
    int[] cnt = new int[n + 1]; 

    // Stores required count 
    int ans = 0; 

    // Update frequency of 
    // each array element 
    foreach(int k in a)  
    { 
        ++cnt[k]; 
    } 

    // Find sum of all subarrays 
    for(int l = 0; l < n; ++l) 
    { 
        int sum = 0; 

        for(int r = l; r < n; ++r) 
        { 
            sum += a[r]; 
            if (l == r) 
                continue; 

            if (sum <= n) 
            { 

                // Increment ans by cnt[sum] 
                ans += cnt[sum]; 

                // Reset cnt[sum] by 0 
                cnt[sum] = 0; 
            } 
        } 
    } 

    // Return ans 
    return ans; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 

    // Given array 
    int[] a = { 1, 1, 1, 1, 1 }; 

    // Function call 
    Console.WriteLine(countElements(a, a.Length)); 
} 
} 

// This code is contributed by Amit Katiyar 

```

**Output:** 

```
0

```

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(n)`



* * *

* * *



