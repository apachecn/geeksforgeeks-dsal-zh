# 生成给定数组中相同索引元素的按位“或”和等于 K 的数组

> 原文:[https://www . geeksforgeeks . org/生成一个数组，该数组具有给定数组等于 k 的相同索引元素的按位或和/](https://www.geeksforgeeks.org/generate-an-array-having-sum-of-bitwise-or-of-same-indexed-elements-with-given-array-equal-to-k/)

给定一个由 **N** 个整数和一个整数 **K、**组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是[打印生成的数组](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/)，使得生成的数组与给定数组的相同索引元素的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)之和等于**K。**如果不可能生成这样的数组，则打印**“-1”。**

**示例:**

> **输入:** arr[] = {6，6，6，6}，K = 34
> **输出:** 15 7 6 6
> **解释:**
> 数组{6，6，6，6}和{15，7，6，6}的同索引元素的按位异或为:
> 6 | 15 = 15
> 6 | 7 = 7
> 6 | 6 = 6
> 6 | 6 = 6【T13
> 
> **输入:** arr[] = {1，2，3，4}，K = 32
> T3】输出: 23 2 3 4

**进场:** 按照以下步骤解决问题:

*   首先，[计算数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**arr【】**的和，并将其存储在一个变量中，比如**和。**
*   初始化一个[向量< int >](https://www.geeksforgeeks.org/vector-in-cpp-stl/) ，比如 **B，**来存储结果数组。
*   将 **K** 的值更新为**K = K–总和。**
*   如果 **K** 小于 **0** ，打印 **-1。**
*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并执行以下操作:
    *   初始化一个变量，比如 **curr，**来存储结果数组的元素。
    *   遍历当前数组元素的位。
    *   检查当前位是否置位， **2 <sup>j</sup> ≤ K** 是否置位。如果发现为真，则更新 **curr** 为 **curr = curr | (1 < < j)** 和**K = K–(1<<j)。**
    *   现在，将 **curr** 推入矢量**b**
*   [如果 **K** 为 **0** ，则打印矢量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **B** 。否则，打印 **-1。**

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the resultant array
void constructArr(int A[], int N, int K)
{
    // Stores the sum of the array
    int sum = 0;

    // Calculate sum of the array
    for (int i = 0; i < N; i++) {
        sum += A[i];
    }

    // If sum > K
    if (sum > K) {

        // Not possible to
        // construct the array
        cout << -1 << "\n";
        return;
    }

    // Update K
    K -= sum;

    // Stores the resultant array
    vector<int> B;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores the current element
        int curr = A[i];

        for (int j = 32; j >= 0 and K; j--) {

            // If jth bit is not set and
            // value of 2^j is less than K
            if ((curr & (1LL << j)) == 0
                and (1LL << j) <= K) {

                // Update curr
                curr |= (1LL << j);

                // Update K
                K -= (1LL << j);
            }
        }

        // Push curr into B
        B.push_back(curr);
    }

    // If K is greater than 0
    if (!K) {

        // Print the vector B
        for (auto it : B) {
            cout << it << " ";
        }
        cout << "\n";
    }

    // Otherwise
    else {
        cout << "-1"
             << "\n";
    }
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 2, 3, 4 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given input
    int K = 32;

    // Function call to print
    // the required array
    constructArr(arr, N, K);
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to print the resultant array
def constructArr(A, N, K):

    # Stores the sum of the array
    sum = 0

    # Calculate sum of the array
    for i in range(N):
        sum += A[i]

    # If sum > K
    if (sum > K):

        # Not possible to
        # construct the array
        print(-1)
        return

    # Update K
    K -= sum

    # Stores the resultant array
    B = []

    # Traverse the array
    for i in range(N):

        # Stores the current element
        curr = A[i]
        j = 32

        while(j >= 0 and K>0):

            # If jth bit is not set and
            # value of 2^j is less than K
            if ((curr & (1 << j)) == 0 and (1 << j) <= K):

                # Update curr
                curr |= (1 << j)

                # Update K
                K -= (1 << j)
            j -= 1

        # Push curr into B
        B.append(curr)

    # If K is greater than 0
    if (K == 0):
        # Print the vector B
        for it in B:
            print(it,end=" ")
        print("\n",end = "")

    # Otherwise
    else:
        print("-1")

# Driver Code
if __name__ == '__main__':
    # Input
    arr = [1, 2, 3, 4]

    # Size of the array
    N = len(arr)

    # Given input
    K = 32

    # Function call to print
    # the required array
    constructArr(arr, N, K)

# This code is contributed by ipg2016107.
```

**Output:** 

```
23 2 3 4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)