# `Q`操作后包含所有唯一元素的最小长度子数组

> 原文：[https://www.geeksforgeeks.org/minimum-length-subarray-containing-all-unique-elements-after-q-operations/](https://www.geeksforgeeks.org/minimum-length-subarray-containing-all-unique-elements-after-q-operations/)

给定大小为`N`的数组，该数组最初包含所有元素为`0`，并且给出一个`Q`查询，其中查询的范围为`[L, R]`。 任务是通过向`Q`查询的`[L, R]`范围内的每个元素添加`1`来修改数组，然后打印最小长度的大小 包含所有唯一元素的子数组。

**注意**：基于 1 的索引在`[L, R]`范围内使用。

**示例**：

> **输入**：`N = 6, Q[4][] = {{1, 3}, {4, 6}, {3, 4}, {3, 3}}`
>
> **输出**：3
>
> **说明**：
>
> 初始数组：`arr[] = {0, 0, 0, 0, 0, 0}`
>
> 查询 1：更新后的`arr[] = {1, 1, 1, 0, 0, 0}`。
>
> 查询 2：更新后的`arr[] = {1, 1, 1, 1, 1, 1}`。
>
> 查询 3：更新后的`arr[] = {1, 1, 2, 2, 1, 1}`。
>
> 查询 4：更新后的`arr[] = {1, 1, 3, 2, 1, 1}`。
>
> 子数组`{1, 3, 2}`是包含所有唯一元素的最小子数组。 因此，答案是 3。
> 
> **输入**：`N = 8, Q[6][] = {{1, 4}, {3, 4}, {4, 5}, {5, 5}, {7, 8},  {8, 8}}`
>
> **输出**：4
>
> **说明**：
>
> 处理完所有查询后，该数组变为`{1, 1, 2, 3,  2, 0, 1, 2}`。
>
> 子数组`{3, 2, 0, 1}`是包含所有唯一元素的最小子数组。 因此，答案是 4。

**方法**：这个想法是针对此问题使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[双指针](https://www.geeksforgeeks.org/two-pointers-technique/)的概念。

*   可以通过在索引`L`处将数组的值递增 1，并在索引`R + 1`处将值递减 1 来计算查询后的最终数组。

```
Processing of a Query:
arr[L] += 1
arr[R + 1] -= 1

```

*   最后，计算数组的[前缀总和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，以计算查询后的最终数组。 然后使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)获得包含所有唯一元素的最小长度子数组。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the 
// minimum size subarray containing 
// all unique elements after processing 
// the array for K queries of ranges 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find minimum size subarray 
// of all array elements 
int subarrayLength(int A[], int R[][2], 
                   int N, int M) 
{ 

    // Updating the array after 
    // processing each query 
    for (int i = 0; i < M; ++i) { 

        int l = R[i][0], r = R[i][1] + 1; 

        // Making it to 0-indexing 
        l--; 
        r--; 

        // Prefix sum array concept is used 
        // to obtain the count array 
        A[l]++; 

        if (r < N) 
            A[r]--; 
    } 

    // Iterating over the array 
    // to get the final array 
    for (int i = 1; i < N; ++i) { 
        A[i] += A[i - 1]; 
    } 

    // Variable to get count 
    // of all unique elements 
    int count = 0; 

    // Hash to maintain perviously 
    // occured elements 
    unordered_set<int> s; 

    // Loop to find the all 
    // unique elements 
    for (int i = 0; i < N; ++i) { 
        if (s.find(A[i]) == s.end()) 
            count++; 

        s.insert(A[i]); 
    } 

    // array to maintain counter 
    // of encountered elements 
    vector<int> repeat(count + 1, 0); 

    // variable to store answer 
    int ans = N; 

    // Using two pointers approach 
    int counter = 0, left = 0, right = 0; 

    while (right < N) { 

        int cur_element = A[right]; 
        repeat[cur_element] += 1; 

        // Increment counter 
        // if occured once 
        if (repeat[cur_element] == 1) 
            ++counter; 

        // when all unique 
        // elements are found 
        while (counter == count) { 

            // update answer with 
            // minimum size 
            ans = min(ans, right - left + 1); 

            // decrement count of 
            // elements from left 
            cur_element = A[left]; 
            repeat[cur_element] -= 1; 
            ++left; 

            // decrement counter 
            if (repeat[cur_element] == 0) 
                --counter; 
        } 

        ++right; 
    } 
    return ans; 
} 

// Driver code 
int main() 
{ 
    int N = 8, queries = 6; 
    int Q[][2] 
        = { 
            { 1, 4 }, { 3, 4 }, { 4, 5 }, 
            { 5, 5 }, { 7, 8 }, { 8, 8 } 
          }; 

    int A[N] = { 0 }; 

    cout << subarrayLength(A, Q, N, queries); 

    return 0; 
} 

```

## Java

```java

// Java implementation to find the 
// minimum size subarray containing 
// all unique elements after processing 
// the array for K queries of ranges 
import java.util.*; 
class GFG{ 

// Function to find minimum size subarray 
// of all array elements 
static int subarrayLength(int A[], int R[][], 
                          int N, int M) 
{ 
    // Updating the array after 
    // processing each query 
    for (int i = 0; i < M; ++i)  
    { 
        int l = R[i][0], r = R[i][1] + 1; 

        // Making it to 0-indexing 
        l--; 
        r--; 

        // Prefix sum array concept is used 
        // to obtain the count array 
        A[l]++; 

        if (r < N) 
            A[r]--; 
    } 

    // Iterating over the array 
    // to get the final array 
    for (int i = 1; i < N; ++i)  
    { 
        A[i] += A[i - 1]; 
    } 

    // Variable to get count 
    // of all unique elements 
    int count = 0; 

    // Hash to maintain perviously 
    // occured elements 
    HashSet<Integer> s = new HashSet<Integer>(); 

    // Loop to find the all 
    // unique elements 
    for (int i = 0; i < N; ++i)  
    { 
        if (!s.contains(A[i])) 
            count++; 
        s.add(A[i]); 
    } 

    // array to maintain counter 
    // of encountered elements 
    int []repeat = new int[count + 1]; 

    // variable to store answer 
    int ans = N; 

    // Using two pointers approach 
    int counter = 0, left = 0, right = 0; 

    while (right < N)  
    { 
        int cur_element = A[right]; 
        repeat[cur_element] += 1; 

        // Increment counter 
        // if occured once 
        if (repeat[cur_element] == 1) 
            ++counter; 

        // when all unique 
        // elements are found 
        while (counter == count)  
        { 
            // update answer with 
            // minimum size 
            ans = Math.min(ans,  
                           right - left + 1); 

            // decrement count of 
            // elements from left 
            cur_element = A[left]; 
            repeat[cur_element] -= 1; 
            ++left; 

            // decrement counter 
            if (repeat[cur_element] == 0) 
                --counter; 
        } 

        ++right; 
    } 
    return ans; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int N = 8, queries = 6; 
    int Q[][] = {{ 1, 4 }, { 3, 4 }, { 4, 5 }, 
                 { 5, 5 }, { 7, 8 }, { 8, 8 }}; 
    int A[] = new int[N]; 
    System.out.print(subarrayLength(A, Q,  
                                    N, queries)); 
} 
} 

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 implementation to find the 
# minimum size subarray containing 
# all unique elements after processing 
# the array for K queries of ranges 

# Function to find minimum size subarray 
# of all array elements 
def subarrayLength(A, R, N, M): 

    # Updating the array after 
    # processing each query 
    for i in range(M): 

        l = R[i][0] 
        r = R[i][1] + 1

        # Making it to 0-indexing 
        l -= 1
        r -= 1

        # Prefix sum array concept is used 
        # to obtain the count array 
        A[l] += 1

        if (r < N): 
            A[r] -= 1

    # Iterating over the array 
    # to get the final array 
    for i in range(1 , N): 
        A[i] += A[i - 1] 

    # Variable to get count 
    # of all unique elements 
    count = 0

    # Hash to maintain perviously 
    # occured elements 
    s = [] 

    # Loop to find the all 
    # unique elements 
    for i in range(N): 
        if (A[i] not in s): 
            count += 1

        s.append(A[i]) 

    # Array to maintain counter 
    # of encountered elements 
    repeat = [0] * (count + 1) 

    # Variable to store answer 
    ans = N 

    # Using two pointers approach 
    counter, left, right = 0, 0, 0

    while (right < N): 

        cur_element = A[right] 
        repeat[cur_element] += 1

        # Increment counter 
        # if occured once 
        if (repeat[cur_element] == 1): 
            counter += 1

        # When all unique 
        # elements are found 
        while (counter == count): 

            # update answer with 
            # minimum size 
            ans = min(ans, right - left + 1) 

            # Decrement count of 
            # elements from left 
            cur_element = A[left] 
            repeat[cur_element] -= 1
            left += 1

            # Decrement counter 
            if (repeat[cur_element] == 0): 
                counter -= 1

        right += 1

    return ans 

# Driver code 
if __name__ == "__main__": 

    N , queries = 8 , 6
    Q = [ [ 1, 4 ], [ 3, 4 ], [ 4, 5 ], 
          [ 5, 5 ], [ 7, 8 ], [ 8, 8 ] ] 

    A = [0] * N 
    print(subarrayLength(A, Q, N, queries)) 

# This code is contributed by chitranayal 

```

## C#

```cs

// C# implementation to find the 
// minimum size subarray containing 
// all unique elements after processing 
// the array for K queries of ranges 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find minimum size subarray 
// of all array elements 
static int subarrayLength(int []A, int [,]R, 
                          int N, int M) 
{ 

    // Updating the array after 
    // processing each query 
    for(int i = 0; i < M; ++i)  
    { 
        int l = R[i, 0], r = R[i, 1] + 1; 

        // Making it to 0-indexing 
        l--; 
        r--; 

        // Prefix sum array concept is used 
        // to obtain the count array 
        A[l]++; 

        if (r < N) 
            A[r]--; 
    } 

    // Iterating over the array 
    // to get the readonly array 
    for(int i = 1; i < N; ++i)  
    { 
        A[i] += A[i - 1]; 
    } 

    // Variable to get count 
    // of all unique elements 
    int count = 0; 

    // Hash to maintain perviously 
    // occured elements 
    HashSet<int> s = new HashSet<int>(); 

    // Loop to find the all 
    // unique elements 
    for(int i = 0; i < N; ++i)  
    { 
        if (!s.Contains(A[i])) 
            count++; 

        s.Add(A[i]); 
    } 

    // Array to maintain counter 
    // of encountered elements 
    int []repeat = new int[count + 1]; 

    // Variable to store answer 
    int ans = N; 

    // Using two pointers approach 
    int counter = 0, left = 0, right = 0; 

    while (right < N)  
    { 
        int cur_element = A[right]; 
        repeat[cur_element] += 1; 

        // Increment counter 
        // if occured once 
        if (repeat[cur_element] == 1) 
            ++counter; 

        // When all unique 
        // elements are found 
        while (counter == count)  
        { 

            // Update answer with 
            // minimum size 
            ans = Math.Min(ans,  
                           right - left + 1); 

            // Decrement count of 
            // elements from left 
            cur_element = A[left]; 
            repeat[cur_element] -= 1; 
            ++left; 

            // Decrement counter 
            if (repeat[cur_element] == 0) 
                --counter; 
        } 
        ++right; 
    } 
    return ans; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int N = 8, queries = 6; 
    int [,]Q = { { 1, 4 }, { 3, 4 }, { 4, 5 }, 
                 { 5, 5 }, { 7, 8 }, { 8, 8 } }; 
    int []A = new int[N]; 

    Console.Write(subarrayLength(A, Q,  
                                 N, queries)); 
} 
} 

// This code is contributed by Amit Katiyar

```

**输出**： 

```
4

```

**时间复杂度**：`O(n)`。



* * *

* * *



