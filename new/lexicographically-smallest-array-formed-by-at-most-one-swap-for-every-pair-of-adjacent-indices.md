# 由每对相邻索引对最多进行一次交换形成的词典上最小的数组

> 原文：[https://www.geeksforgeeks.org/lexicographically-smallest-array-formed-by-at-most-one-swap-for-every-pair-of-adjacent-indices/](https://www.geeksforgeeks.org/lexicographically-smallest-array-formed-by-at-most-one-swap-for-every-pair-of-adjacent-indices/)

给定长度为`N`的数组`A[]`，任务是通过为每个索引交换相邻元素至少一次来找到字典上最小的数组。 因此，对于任何索引：

`0 <= K < N-1`

最多允许`A[K]`和`A[K + 1]`之间进行一次交换。


> **输入**：`A[] = {3, 2, 1, 4}`
>
> **输出**：`1 3 2 4`
>
> **说明**：执行以下交换操作：
>
> 交换`A[1]`和`A[2]`，现在`A[] = {3, 1, 2, 4}`
>
> 交换`A[0]`和`A[1]`，现在`A[] = {1, 3, 2, 4}`
>
> 由于已经交换了`A[1]`和`A[2]`，因此无法进行进一步的交换。
>
> **输入**：`A[] = {2, 1, 4, 3, 6, 5}`
>
> **输出**：`1 2 3 4 5 6`
>
> **解释**：执行以下交换：
>
> 交换`A[0]`和`A[1]`，现在`A[] = {1, 2, 4, 4, 3, 6, 5}`
>
> 交换`A[2]`和`A[3]`，现在`A[] = {1, 2, 3, 4, 6, 5}`
>
> 交换`A[4]`和`A[5]`，现在`A[] = {1, 2, 3 , 4, 5, 6}`

**方法**：

为解决上述问题，我们可以应用**贪婪方法**。 我们知道最多可以执行`N – 1`个交换，以使给定的数组尽可能的小。

*   创建一个**计数器**变量，并使用`N-1`和一个哈希映射表进行初始化以存储执行的交换。

*   从当前索引开始查找最小元素的位置。

*   现在向后执行交换，直到到达当前元素位置。

*   还要检查当前交换是否可行，并在每次交换时也将计数器递减。

*   最后打印所需的数组。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the 
// lexicographically smallest 
// array by at most single swap 
// for every pair of adjacent indices 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the 
// lexicographically smallest array 
void findSmallestArray(int A[], int n) 
{ 
    // maximum swaps possible 
    int count = n - 1; 

    // hash to store swaps performed 
    map<pair<int, int>, int> mp; 

    for (int i = 0; i < n && count > 0; ++i) { 

        // let current element be 
        // the minimum possible 
        int mn = A[i], pos = i; 

        // Find actual position of 
        // the minimum element 
        for (int j = i + 1; j < n; ++j) { 

            // Update minimum element and 
            // its position 
            if (A[j] < mn) { 
                mn = A[j]; 
                pos = j; 
            } 
        } 

        // Perform swaps if possible 
        while (pos > i && count > 0 
               && !mp[{ pos - 1, pos }]) { 

            // Insert current swap in hash 
            mp[{ pos - 1, pos }] = 1; 

            swap(A[pos], A[pos - 1]); 
            --pos; 
            --count; 
        } 
    } 

    // print the required array 
    for (int i = 0; i < n; ++i) 
        cout << A[i] << " "; 
} 

// Driver code 
int main() 
{ 

    int A[] = { 2, 1, 4, 3, 6, 5 }; 
    int n = sizeof(A) / sizeof(A[0]); 

    findSmallestArray(A, n); 

    return 0; 
} 

```

## Python3

```py

# Python3 implementation to find the 
# lexicographically smallest array by 
# at most single swap for every pair 
# of adjacent indices 

# Function to find the 
# lexicographically smallest array 
def findSmallestArray(A, n): 

    # Maximum swaps possible 
    count = n - 1

    # Hash to store swaps performed 
    mp = {''} 

    for i in range(0, n): 
        if(count <= 0): 
            break; 

        # Let current element be 
        # the minimum possible 
        mn = A[i] 
        pos = i 

        # Find actual position of 
        # the minimum element 
        for j in range(i + 1, n): 

            # Update minimum element  
            # and its position 
            if (A[j] < mn): 
                mn = A[j] 
                pos = j 

        # Perform swaps if possible 
        while (pos > i and count > 0 and 
             ((pos - 1, pos) not in mp)): 

            # Insert current swap in hash 
            mp.add((pos - 1, pos)) 

            A[pos], A[pos - 1] = A[pos - 1], A[pos] 
            pos -= 1
            count -= 1

    # Print the required array 
    for i in range(0, n): 
        print(A[i], end = " ") 

# Driver code 
A = [ 2, 1, 4, 3, 6, 5 ] 
n = len(A) 

findSmallestArray(A, n) 

# This code is contributed by Sanjit_Prasad 

```

**输出**： 

```
1 2 3 4 5 6

```

**时间复杂度**：`O(N ^ 2)`。



* * *

* * *



