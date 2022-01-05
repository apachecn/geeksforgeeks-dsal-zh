# 检查给定数组的元素是否可以重新排列，以便(arr[i] + i*K) % N = i 范围内 I 的所有值[0，N-1]

> 原文:[https://www . geesforgeks . org/check-if-给定数组的元素可以重新排列-arri-ik-n-I-for-all-values-in-I-range-0-n-1/](https://www.geeksforgeeks.org/check-if-elements-of-given-array-can-be-rearranged-such-that-arri-ik-n-i-for-all-values-of-i-in-range-0-n-1/)

给定一个由 **N** 正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是检查数组元素是否可以重新排列，使得**【0，N-1】**范围内 **i** 的所有值的 **(arr[i] + i*K) % N = i** 。

**示例:**

> **输入:** arr[] = {2，1，0}，K = 5
> **输出:**是
> **说明:**给定数组可以重新排列为{0，2，1}。因此，更新后的值变为{(0 + 0*5) % 3，(2 + 1*5) % 3，(1 + 2*5) % 3} = > {0%3，7%3，11%3} = > {0，1，2}数组中所有元素的索引都相等。
> 
> **输入:** arr[] = {1，1，1，1，1}，K = 5
> T3】输出:否

**天真方法:**给定的问题可以通过[生成给定数组的所有可能排列来解决](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)**arr【】**并检查是否存在满足给定标准的排列。

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以借助[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)使用[递归](https://www.geeksforgeeks.org/recursion/)进行优化。以下是解决给定问题的一些观察结果:

*   每个数组元素 **arr[i]** 被更新为 **(arr[i] + i*K) % N** 。因此，值 **arr[i] % N** 和 **i*K % N** 可以独立计算。
*   如果一个[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/) **A** 包含 **arr[i] % N** 的所有值，多集 **B** 包含 **A** 和 **B** 中所有值的 **i*K % N** 的所有值，并存储**【0，N-1】**中所有可能的元素组合如果结果集的大小为 **N** ，则可以按照所需的方式重新排列数组。

利用上述观察，可以通过以下步骤解决给定的问题:

*   为范围**【0，N-1】**中的所有 **i** 值创建一个包含所有**arr【I】% N**值的[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/) **A** 。
*   同样，创建一个多集 **B** 包含范围**【0，N-1】**内 **i** 的所有值的 **i*K % N** 的所有值。
*   创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)来迭代 **A** 和 **B** 中的所有整数对，在集合 **C** 中以 **N** 为模相加它们的和，并递归调用剩余的元素。
*   如果在任何时候，设定**C**T2 的大小= N ，返回**真**否则返回**假**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to generate all numbers in range
// [0, N-1] using the sum of elements
// in the multiset A and B mod N
bool isPossible(multiset<int> A,
                multiset<int> B,
                set<int> C, int N)
{
    // If no more pair of elements
    // can be selected
    if (A.size() == 0 || B.size() == 0) {

        // If the number of elements
        // in C = N, then return true
        if (C.size() == N) {
            return true;
        }

        // Otherwise return false
        else {
            return false;
        }
    }

    // Stores the value of final answer
    bool ans = false;

    // Iterate through all the pairs in
    // the given multiset A and B
    for (auto x : A) {
        for (auto y : B) {

            // Stores the set A without x
            multiset<int> _A = A;
            _A.erase(_A.find(x));

            // Stores the set B without y
            multiset<int> _B = B;
            _B.erase(_B.find(y));

            // Stores the set C with (x+y)%N
            set<int> _C = C;
            _C.insert((x + y) % N);

            // Recursive call
            ans = (ans
                   || isPossible(
                          _A, _B, _C, N));
        }
    }

    // Return Answer
    return ans;
}

// Function to check if it is possible
// to rearrange array elements such that
// (arr[i] + i*K) % N = i
void rearrangeArray(
    int arr[], int N, int K)
{
    // Stores the values of arr[] modulo N
    multiset<int> A;
    for (int i = 0; i < N; i++) {
        A.insert(arr[i] % N);
    }

    // Stores all the values of
    // i*K modulo N
    multiset<int> B;
    for (int i = 0; i < N; i++) {
        B.insert((i * K) % N);
    }

    set<int> C;

    // Print Answer
    if (isPossible(A, B, C, N)) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 0 };
    int K = 5;
    int N = sizeof(arr) / sizeof(arr[0]);

    rearrangeArray(arr, N, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible
# to generate all numbers in range
# [0, N-1] using the sum of elements
#+ in the multiset A and B mod N
def isPossible(A, B, C, N):

     # If no more pair of elements
    # can be selected
    if(len(A) == 0 or len(B) == 0):

         # If the number of elements
        # in C = N, then return true
        if(len(C) == N):
            return True

        # Otherwise return false
        else:
            return False

    # Stores the value of final answer
    ans = False
    for x in A:

        # Iterate through all the pairs in
        # the given multiset A and B
        for y in B:

           # Stores the set A without x
            _A = A
            _A.remove(x)

            # Stores the set A without y
            _B = B
            _B.remove(y)

             # Stores the set A without x+y%N
            _C = C
            _C.add((x+y) % N)

            # Recursive call
            ans = (ans or isPossible(_A, _B, _C, N))

    return ans

# Function to check if it is possible
# to rearrange array elements such that
# (arr[i] + i*K) % N = i
def rearrangeArray(arr, N, K):

   # Stores the values of arr[] modulo N
    A = []
    for i in range(N):
        A.append(arr[i] % N)
    A.sort()

     # Stores all the values of
    # i*K modulo N
    B = []
    for i in range(N):
        B.append((i*K) % N)
    B.sort()
    C = set()

    # Print Answer
    if isPossible(A, B, C, N):
        print("YES")
    else:
        print("NO")

# Driver code
arr = [1, 2, 0]
K = 5
N = len(arr)
rearrangeArray(arr, N, K)

# This code is contributed by parthmanchanda81
```

**Output:** 

```
YES
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*