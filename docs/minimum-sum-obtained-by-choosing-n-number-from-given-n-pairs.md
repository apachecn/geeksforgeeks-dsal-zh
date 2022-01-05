# 从给定的 N 对中选择 N 个数得到的最小和

> 原文:[https://www . geesforgeks . org/通过从给定的 n 对中选择 n 个数字获得的最小和/](https://www.geeksforgeeks.org/minimum-sum-obtained-by-choosing-n-number-from-given-n-pairs/)

给定整数对 **(A，B)** 的一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，其中 **N** 为偶数，任务是找到选择 **N** 元素的最小和，使得从所有对中选择的值 **A** 和 **B** 正好是 **(N/2)** 次。
**例:**

> **输入:** N = 4，arr[][] = { {7，20}，{300，50}，{30，200}，{30，20} }
> **输出:** 107
> **解释:**
> 从第一对中选择值-A = 7。
> 从第二对中选择值= 50。
> 从第三对中选择值-A = 30。
> 从第四对中选择值= 20。
> 最小和为 7 + 50 + 30 + 20 = 107。
> **输入:** N = 4，arr[][] = { {10，20}，{400，50}，{30，200}，{30，20} }
> **输出:** 110
> **解释:**
> 从第一对中选择值-A = 10。
> 从第二对中选择值= 50。
> 从第三对中选择值-A = 30。
> 从第 4 对中选择值= 20。
> 最小和为 10 + 50 + 30 + 20 = 110。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  对于给定数组中的每对 **(A，B)** ，将**(B–A)**的值和相应的索引存储在临时数组中(比如说 **temp[]** )。值**(B–A)**实际上定义了如果为每个元素选择 A 而不是 B，成本会最小化多少。
2.  目标是最小化总成本。因此，按降序对数组 **temp[]** 进行排序。
3.  通过选择 **A** 作为第一个 **N/2** 元素，从数组**temp【】**中选择第一个 **N/2** 元素，当选择 **A** 而不是 **B** 时，这些元素将具有最大的总和。
4.  对于剩余的 **N/2** 元素，选择 **B** ，因为值的总和可以最小化。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to choose the elements A
// and B such the sum of all elements
// is minimum
int minSum(int arr[][2], int n)
{

    // Create an array of pair to
    // store Savings and index
    pair<int, int> temp[n];

    // Traverse the given array of pairs
    for (int i = 0; i < 2 * n; i++) {

        // Sum minimized when A
        // is chosen over B for
        // i-th element.
        temp[i].first = arr[i][1]
                        - arr[i][0];

        // Store index for the
        // future reference.
        temp[i].second = i;
    }

    // Sort savings array in
    // non-increasing order.
    sort(temp, temp + 2 * n,
         greater<pair<int, int> >());

    // Storing result
    int res = 0;

    for (int i = 0; i < 2 * n; i++) {

        // First n elements choose
        // A and rest choose B
        if (i < n)
            res += arr[temp[i].second][0];
        else
            res += arr[temp[i].second][1];
    }

    // Return the final Sum
    return res;
}

// Driver Code
int main()
{
    // Given array of pairs
    int arr[4][2] = { { 7, 20 },
                      { 300, 50 },
                      { 30, 200 },
                      { 30, 20 } };

    // Function Call
    cout << minSum(arr, 2);
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to choose the elements A
# and B such the sum of all elements
# is minimum
def minSum(arr, n):

    # Create an array of pair to
    # store Savings and index
    temp = [None]*(2*n)

    # Traverse the given array of pairs
    for i in range(2 * n):

        # Sum minimized when A
        # is chosen over B for
        # i-th element.
        temp[i] = (arr[i][1] - arr[i][0], i)

    # Sort savings array in
    # non-increasing order.
    temp.sort(reverse=True)

    # Storing result
    res = 0

    for i in range(2 * n):

        # First n elements choose
        # A and rest choose B
        if (i < n):
            res += arr[temp[i][1]][0]
        else:
            res += arr[temp[i][1]][1]

    # Return the final Sum
    return res

# Driver Code
if __name__ == '__main__':
    # Given array of pairs
    arr = [[7, 20],
           [300, 50],
           [30, 200],
           [30, 20]]

    # Function Call
    print(minSum(arr, 2))
```

**Output:** 

```
107
```

**时间复杂度:***O(N * log(N))*
T5】辅助空间复杂度: *O(N)*