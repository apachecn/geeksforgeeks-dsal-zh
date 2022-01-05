# 从给定的两个数组中找到子数组，使它们具有相等的和

> 原文:[https://www . geeksforgeeks . org/find-子数组-从给定的两个数组-这样它们就有相等的总和/](https://www.geeksforgeeks.org/find-sub-arrays-from-given-two-arrays-such-that-they-have-equal-sum/)

给定两个大小相等的数组 **A[]** 和 **B[]** ，即 **N** 包含从 **1** 到 **N** 的整数。任务是从给定的数组中找到子数组，使它们具有相等的和。打印这些子数组的索引。如果没有这样的子阵列，则打印 **-1** 。

**示例:**

> **输入:** A[] = {1，2，3，4，5}，B[] = {6，2，1，5，4}
> **输出:**
> 数组 1 中的索引:0，1，2
> 数组 2 中的索引:0
> A[0..2] = 1 + 2 + 3 = 6
> B[0] = 6
> 
> **输入:** A[] = {10，1}，B[] = {5，3}
> **输出:** -1
> 没有这样的子阵列。

**逼近:**让**A<sub>I</sub>T5】表示 **A** 中第一 I 元素之和**B<sub>j</sub>T11】表示 **B** 中第一 j 元素之和。不失一般性，我们假设**A<sub>n</sub><= B<sub>n</sub>**。
现为**B<sub>n</sub>T54】= A<sub>n</sub>T55】= A<sub>I</sub>T28】。所以对于每一个**A<sub>I</sub>T32】我们可以找到最小的 j 使得**A<sub>I</sub>T56】= B<sub>j</sub>T38】。对于每一个 I，我们都找到了区别
T40】B<sub>j</sub>–A<sub>I</sub>T45】。
如果差值为 0，那么我们就完成了，因为 **A** 中的 1 到 I 和 **B** 中的 1 到 j 具有相同的和。假设差值不为 0。那么差别一定在**【1，n-1】**的范围内。**********

> **证明:**
> 让 B<sub>j</sub>–A<sub>I</sub>T32】= n
> B<sub>j</sub>T33】= A<sub>I</sub>+n
> B<sub>j-1</sub>T34】= A<sub>I</sub>(由于 B 中的 jth 元素最多可以为 n 所以 B<sub>j</sub>T35】= B<sub>j
> 这是一个矛盾，因为我们假设 j 是最小的指数
> ，这样 B <sub>j</sub> > = A <sub>i</sub> 就是 j，所以我们的假设是错误的。
> 所以 B<sub>j</sub>–A<sub>I</sub>T37】n</sub>

现在有 n 个这样的差异(对应于每个指数)，但只有(n-1)个可能的值，所以至少两个指数会产生相同的差异(根据鸽子洞原理)。让**A<sub>j</sub>–B<sub>y</sub>= A<sub>I</sub>–B<sub>x</sub>**。重新排列后，我们得到**A<sub>j</sub>–A<sub>I</sub>= B<sub>y</sub>–B<sub>x</sub>**。所以需要的子阵列是 A 中的**【I+1，j】和 B 中的【x+1，y】**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the valid indices in the array
void printAns(int x, int y, int num)
{
    cout << "Indices in array " << num << " : ";
    for (int i = x; i < y; ++i) {
        cout << i << ", ";
    }
    cout << y << "\n";
}

// Function to find sub-arrays from two
// different arrays with equal sum
void findSubarray(int N, int a[], int b[], bool swap)
{

    // Map to store the indices in A and B
    // which produce the given difference
    std::map<int, pair<int, int> > index;
    int difference;
    index[0] = make_pair(-1, -1);
    int j = 0;
    for (int i = 0; i < N; ++i) {

        // Find the smallest j such that b[j] >= a[i]
        while (b[j] < a[i]) {
            j++;
        }
        difference = b[j] - a[i];

        // Difference encountered for the second time
        if (index.find(difference) != index.end()) {

            // b[j] - a[i] = b[idx.second] - a[idx.first]
            // b[j] - b[idx.second] = a[i] = a[idx.first]
            // So sub-arrays are a[idx.first+1...i] and b[idx.second+1...j]
            if (swap) {
                pair<int, int> idx = index[b[j] - a[i]];

                printAns(idx.second + 1, j, 1);
                printAns(idx.first + 1, i, 2);
            }
            else {
                pair<int, int> idx = index[b[j] - a[i]];
                printAns(idx.first + 1, i, 1);
                printAns(idx.second + 1, j, 2);
            }
            return;
        }

        // Store the indices for difference in the map
        index[difference] = make_pair(i, j);
    }

    cout << "-1";
}

// Utility function to calculate the
// cumulative sum of the array
void cumulativeSum(int arr[], int n)
{
    for (int i = 1; i < n; ++i)
        arr[i] += arr[i - 1];
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 4, 5 };
    int b[] = { 6, 2, 1, 5, 4 };
    int N = sizeof(a) / sizeof(a[0]);

    // Function to update the arrays
    // with their cumulative sum
    cumulativeSum(a, N);
    cumulativeSum(b, N);

    if (b[N - 1] > a[N - 1]) {
        findSubarray(N, a, b, false);
    }
    else {

        // Swap is true as a and b are swapped during
        // function call
        findSubarray(N, b, a, true);
    }

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# Function to print the valid indices in the array 
def printAns(x, y, num): 

    print("Indices in array", num, ":", end = " ") 
    for i in range(x, y):  
        print(i, end = ", ") 

    print(y) 

# Function to find sub-arrays from two 
# different arrays with equal sum 
def findSubarray(N, a, b, swap): 

    # Map to store the indices in A and B 
    # which produce the given difference 
    index = {} 
    difference, j = 0, 0 
    index[0] = (-1, -1)

    for i in range(0, N):  

        # Find the smallest j such that b[j] >= a[i] 
        while b[j] < a[i]:  
            j += 1 

        difference = b[j] - a[i] 

        # Difference encountered for the second time 
        if difference in index:  

            # b[j] - a[i] = b[idx.second] - a[idx.first] 
            # b[j] - b[idx.second] = a[i] = a[idx.first] 
            # So sub-arrays are a[idx.first+1...i] and b[idx.second+1...j] 
            if swap:  
                idx = index[b[j] - a[i]] 
                printAns(idx[1] + 1, j, 1) 
                printAns(idx[0] + 1, i, 2) 

            else:
                idx = index[b[j] - a[i]] 
                printAns(idx[0] + 1, i, 1) 
                printAns(idx[1] + 1, j, 2) 

            return 

        # Store the indices for difference in the map 
        index[difference] = (i, j) 

    print("-1") 

# Utility function to calculate the 
# cumulative sum of the array 
def cumulativeSum(arr, n): 

    for i in range(1, n): 
        arr[i] += arr[i - 1] 

# Driver code 
if __name__ == "__main__": 

    a = [1, 2, 3, 4, 5]  
    b = [6, 2, 1, 5, 4]  
    N = len(a) 

    # Function to update the arrays 
    # with their cumulative sum 
    cumulativeSum(a, N) 
    cumulativeSum(b, N) 

    if b[N - 1] > a[N - 1]:  
        findSubarray(N, a, b, False) 

    else:

        # Swap is true as a and b are 
        # swapped during function call 
        findSubarray(N, b, a, True) 

# This code is contributed by Rituraj Jain
```

**Output:**

```
Indices in array 1 : 0, 1, 2
Indices in array 2 : 0

```