# 根据给定条件每个数组元素必须添加的最小值

> 原文：[https://www.geeksforgeeks.org/minimum-value-by-which-each-array-element-must-be-added-as-per-given-conditions/](https://www.geeksforgeeks.org/minimum-value-by-which-each-array-element-must-be-added-as-per-given-conditions/)

给定 2 个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`A[]`和`B[]`和一个整数`M`。 任务是找到`X`的最小值，以便将数组的所有元素更改为`(arr[i] + X) % M`的所有元素频率`A[]`与`B[]`所有元素的频率相同。 如果找不到`X`的任何值，则打印 -1。

**示例**：

> **输入**：`M = 3, A[] = {0, 0, 2, 1}, B[] = {2, 0, 1, 1}`
> **输出**：1
> **说明**：
> 取`x = 1`时，数字将更改为：
>
> ```
> (0 + 1) % 3 = 1
> (0 + 1) % 3 = 1
> (2 + 1) % 3 = 0
> (1 + 1) % 3 = 2
> ```
> 
> 因此，在重新排列`1, 1, 0, 2`为`2, 0, 1, 1`，得到数组`B`。
>
> **输入**：`M = 887, A[] = {4625, 5469, 2038, 5916}, B[] = {744, 211, 795, 695}`
>
> **输出**：-1
>
> **说明**：
>
> 无法将`A[]`转换为`B[]`。

**方法**：`X`的可能值将在`[0, M]`范围内，与范围`M`之后的值将得出与对`M`取模相同的结果。以下是步骤：

1.  创建数组`B[]`的频率数组（例如`freqB[]`）。

2.  现在，在`[0, M]`范围内的所有可能值中迭代`X`，然后执行以下操作：

    *   对于上述范围内的每个`X`值，将数组`A[]`更新为`(arr[i] + X) %M`。

    *   创建数组`A[]`的频率数组（例如`freqA[]`）。

    *   如果数组`freqA[]`和`freqB[]`的频率相同，则打印`X`的值。

    *   否则检查`X`的另一个值。

3.  完成上述步骤后，如果找不到`X`的值，请打印 -1。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find minimum value of X 
int findX(int n, int m, 
          int ar1[], int ar2[]) 
{ 
    // Create a frequency array for B[] 
    int freq2[m] = { 0 }; 

    for (int i = 0; i < n; i++) { 
        freq2[ar2[i]]++; 
    } 

    // Intialize x = -1 
    int x = -1; 

    // Loop from [0 to m-1] 
    for (int i = 0; i < m; i++) { 

        int cnt = 0; 
        int freq1[m] = { 0 }; 

        // Create a frequency array 
        // for fixed x for all ar[i] 
        for (int j = 0; j < n; j++) { 

            freq1[(ar1[j] + i) % m]++; 
        } 

        bool flag = true; 

        // Comparing freq1[] and freq2[] 
        for (int k = 0; k < m; k++) { 

            if (freq1[k] != freq2[k]) { 
                flag = false; 
                break; 
            } 
        } 

        // If condition is satisfied 
        // then break out from loop 
        if (flag) { 
            x = i; 
            break; 
        } 
    } 

    // Return the answer 
    return x; 
} 

// Driver Code 
int main() 
{ 
    // Given value of M 
    int M = 3; 

    // Given arrays ar1[] and ar2[] 
    int ar1[] = { 0, 0, 2, 1 }; 
    int ar2[] = { 2, 0, 1, 1 }; 

    int N = sizeof arr1 / sizeof arr1[0]; 

    cout << findX(N, M, ar1, ar2) << '\n'; 

    return 0; 
} 

```

## Python3

```py

# Python3 program for  
# the above approach 

# Function to find  
# minimum value of X 
def findX(n, m,  
          ar1, ar2): 

    # Create a frequency  
    # array for B[] 
    freq2 = [0] * m 

    for i in range(n): 
        freq2[ar2[i]] += 1

    # Intialize x = -1 
    x = -1

    # Loop from [0 to m - 1] 
    for i in range(m): 
        cnt = 0
        freq1 = [0] * m 

        # Create a frequency array 
        # for fixed x for all ar[i] 
        for j in range(n): 
            freq1[(ar1[j] + i) % m] += 1

        flag = True

        # Comparing freq1[]  
        # and freq2[] 
        for k in range(m): 
            if (freq1[k] != freq2[k]): 
                flag = False
                break

        # If condition is satisfied 
        # then break out from loop 
        if (flag): 
            x = i 
            break

    # Return the answer 
    return x 

# Driver Code 
if __name__ == "__main__": 

    # Given value of M 
    M = 3

    # Given arrays ar1[]  
    # and ar2[] 
    ar1 = [0, 0, 2, 1] 
    ar2 = [2, 0, 1, 1] 

    N = len(ar1) 
    print (findX(N, M, ar1, ar2)) 

# This code is contributed by Chitranayal

```

**输出**： 

```
1

```

**时间复杂度**：`O(N * M)`，其中`N`是数组中*元素*的数量，`M`是一个整数。

**辅助空间**：`O(n)`。



* * *

* * *



