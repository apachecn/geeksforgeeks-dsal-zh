# 使给定二进制阵列交替所需的最小子阵列反转

> 原文:[https://www . geesforgeks . org/minimum-subarray-reverses-required-make-给定-binary-array-alternative/](https://www.geeksforgeeks.org/minimum-subarray-reversals-required-to-make-given-binary-array-alternating/)

给定由相等计数的 **0** s 和 **1** s 组成的二进制[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算使二进制阵列交替所需的最小数量的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)反转操作。在每个操作中，反转给定阵列的任何子阵列。

**示例:**

> **输入:** arr[] = { 1，1，1，0，1，0，0 }
> **输出:** 2
> **解释:**
> 反转子阵列{arr[1]，…，arr[5]}将 arr[]修改为{ 1，0，1，0，1，1，0，0 }
> 反转子阵列{arr[5]，arr[6]}将 arr[]修改为{ 1，0，1，0，1，0，1 因此，所需的输出为 2。
> 
> **输入:** arr[] = { 0，1，1，0 }
> **输出:** 1
> **解释:**
> 反转子阵列{arr[2]，…，arr[2]}将 arr[]修改为{ 0，1，0，1 }，这是交替的。因此，所需的输出为 1。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。其思想是对交替出现的阵列中没有出现在正确索引处的阵列元素进行计数，即对给定阵列中出现的连续相等元素进行计数。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntOp** ，以存储使给定阵列交替所需的子阵列反转操作的最小计数。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素**arr【I】**，检查它是否等于**arr【I+1】**。如果发现为真，则增加 **cntOp** 的值。
*   最后打印 **(cntOp + 1) / 2 的值。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum subarray reversal
// operations required to make array alternating
int minimumcntOperationReq(int arr[], int N)
{
    // Stores minimum count of operations
    // required to make array alternating
    int cntOp = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // If arr[i] is greater
        // than arr[i + 1]
        if (arr[i] == arr[i + 1]) {

            // Update cntOp
            cntOp++;
        }
    }

    return (cntOp + 1) / 2;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 1, 0, 1, 0, 0, 0 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minimumcntOperationReq(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count minimum subarray reversal
// operations required to make array alternating
static int minimumcntOperationReq(int arr[], int N)
{

    // Stores minimum count of operations
    // required to make array alternating
    int cntOp = 0;

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {

        // If arr[i] is greater
        // than arr[i + 1]
        if (arr[i] == arr[i + 1])
        {

            // Update cntOp
            cntOp++;
        }
    }
    return (cntOp + 1) / 2;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 1, 0, 1, 0, 0, 0 };
    int N = arr.length;

    System.out.print(minimumcntOperationReq(arr, N));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count minimum subarray
# reversal operations required to make
# array alternating
def minimumcntOperationReq(arr, N):

    # Stores minimum count of operations
    # required to make array alternating
    cntOp = 0

    # Traverse the array
    for i in range(N - 1):

        # If arr[i] is greater
        # than arr[i + 1]
        if (arr[i] == arr[i + 1]):

            # Update cntOp
            cntOp += 1

    return (cntOp + 1) // 2

# Driver Code
arr = [ 1, 1, 1, 0, 1, 0, 0, 0 ]

N = len(arr)

print(minimumcntOperationReq(arr, N))

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to count minimum subarray reversal
    // operations required to make array alternating
    static int minimumcntOperationReq(int[] arr, int N)
    {

        // Stores minimum count of operations
        // required to make array alternating
        int cntOp = 0;

        // Traverse the array
        for (int i = 0; i < N - 1; i++)
        {

            // If arr[i] is greater
            // than arr[i + 1]
            if (arr[i] == arr[i + 1])
            {

                // Update cntOp
                cntOp++;
            }
        }

        return (cntOp + 1) / 2;
    }

  // Driver code
  static void Main()
  {
        int[] arr = { 1, 1, 1, 0, 1, 0, 0, 0 };

        int N = arr.Length;

        Console.WriteLine(minimumcntOperationReq(arr, N));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to count minimum subarray reversal
// operations required to make array alternating
function minimumcntOperationReq(arr, N)
{

    // Stores minimum count of operations
    // required to make array alternating
    let cntOp = 0;

    // Traverse the array
    for(let i = 0; i < N - 1; i++)
    {

        // If arr[i] is greater
        // than arr[i + 1]
        if (arr[i] == arr[i + 1])
        {

            // Update cntOp
            cntOp++;
        }
    }
    return (cntOp + 1) / 2;
}

// Driver code
    let arr = [ 1, 1, 1, 0, 1, 0, 0, 0 ];
    let N = arr.length;
    document.write(Math.floor(minimumcntOperationReq(arr, N)));

    // This code is contributed by splevel62.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)