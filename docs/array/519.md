# 最小化三个不同排序数组的`max(A[i], B[j], C[k]) – min(A[i], B[j], C[k])`

> 原文： [https://www.geeksforgeeks.org/minimize-maxai-bj-ck-minai-bj-ck-three-different-sorted-arrays/](https://www.geeksforgeeks.org/minimize-maxai-bj-ck-minai-bj-ck-three-different-sorted-arrays/)

给定三个排序数组`A`，`B`和`C`，它们的大小不一定相同。 计算任何三元组`A[i]`，`B[j]`，`C[k]`的最大数目和最小数目之间的最小绝对差，以使它们分别属于数组`A`，`B`和`C`，即最小化`max(A[i], B[j], C[k]) – min(A[i], B[j], C[k])`。

**示例**：

```
Input : A : [ 1, 4, 5, 8, 10 ]
        B : [ 6, 9, 15 ]
        C : [ 2, 3, 6, 6 ]
Output : 1
Explanation: When we select A[i] = 5
B[j] = 6, C[k] = 6, we get the minimum difference 
as max(A[i], B[j], C[k]) - min(A[i], B[j], C[k]))
= |6-5| = 1 

Input : A = [ 5, 8, 10, 15 ]
        B = [ 6, 9, 15, 78, 89 ]
        C = [ 2, 3, 6, 6, 8, 8, 10 ]
Output : 1
Explanation: When we select A[i] = 10
b[j] = 9, C[k] = 10.

```



从每个数组`A, B, C`中最大的元素开始。在随后的每个步骤中，都维护一个变量以更新答案。

在每一步中，减小差异的唯一可能方法是减小三个元素中的最大元素。

因此遍历包含此步骤中最大元素的数组中的下一个最大元素，并更新答案变量。

重复此步骤，直到包含最大元素的数组结束。

## C++ 

```cpp

// C++ code for above approach 
#include<bits/stdc++.h> 
using namespace std; 

int solve(int A[], int B[], int C[], int i, int j, int k) 
{  
        int min_diff, current_diff, max_term; 

        // calculating min difference from last 
        // index of lists 
        min_diff = Integer.MAX_VALUE; 

        while (i != -1 && j != -1 && k != -1)  
        { 
            current_diff = abs(max(A[i], max(B[j], C[k]))  
                            - min(A[i], min(B[j], C[k]))); 

            // checking condition 
            if (current_diff < min_diff) 
                min_diff = current_diff; 

            // calculating max term from list 
            max_term = max(A[i], max(B[j], C[k])); 

            // Moving to smaller value in the 
            // array with maximum out of three. 
            if (A[i] == max_term) 
                i -= 1; 
            else if (B[j] == max_term) 
                j -= 1; 
            else
                k -= 1; 
        } 

        return min_diff; 
    } 

    // Driver code 
    int main() 
    { 
        int D[] = { 5, 8, 10, 15 }; 
        int E[] = { 6, 9, 15, 78, 89 }; 
        int F[] = { 2, 3, 6, 6, 8, 8, 10 }; 
        int nD = sizeof(D) / sizeof(D[0]); 
        int nE = sizeof(E) / sizeof(E[0]); 
        int nF = sizeof(F) / sizeof(F[0]); 
        cout << solve(D, E, F, nD-1, nE-1, nF-1); 

        return 0;  
    } 

// This code is contributed by Ravi Maurya. 

```