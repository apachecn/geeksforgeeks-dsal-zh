# 求[1，N]的排列，使得(arr[i]！= i+1)并且 arr[i]和(i+1)之间的绝对差之和最小

> 原文:[https://www . geeksforgeeks . org/find-1-n 的排列-这样-arri-i1-和-arri-和-i1-之间的绝对差之和最小/](https://www.geeksforgeeks.org/find-permutation-of-1-n-such-that-arri-i1-and-sum-of-absolute-difference-between-arri-and-i1-is-minimum/)

给定一个正整数 **N** ，任务是找到第一个 **N** 自然数的[排列，比如说**arr【】**这样 **(arr[i]！= I+1)****arr【I】**与 **(i + 1)** 的绝对差之和为**最小值**。](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)

**示例:**

> **输入:** N = 4
> **输出:** 2 1 4 3
> **解释:**
> 考虑排列{2，1，4，3}，现在，和为 ABS(2–1)+ABS(1–2)+ABS(4–3)+ABS(3–4)= 1+1+1+1 = 4，最小。
> 
> **输入:**N = 7
> T3】输出: 2 1 4 3 6 7 5

**天真方法:**解决给定问题的最简单方法是[生成第一个 **N**](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/) [自然数](https://www.geeksforgeeks.org/natural-numbers/)的所有可能排列，并打印出满足给定标准的排列。

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过观察这样的事实来优化，即结果[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)可以通过交换交替的相邻[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)来形成，以便允许新位置具有**arr【I】**和 **(i +1)** 之间的绝对差的最小和。如果 **N** 大于 **1** 且 **N** 为奇数，则最后一个元素可以被置换的第二个最后一个或第三个最后一个元素交换。按照以下步骤解决给定的问题:

*   初始化一个数组，说 **arr[]** ，第一个 N 个自然数按升序排列。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将所有相邻元素交换为**交换** ( **arr[i]，arr[I–1])**。
*   现在，如果 **N** 的值大于 **1** 和 **N** 为奇数，则**交换(arr[N–1]，arr[N–2])**。
*   完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 作为结果排列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

// Function to generate the permutation
// of the first N natural numbers having
// sum of absolute difference between
// element and indices as minimum
#include <iostream>
using namespace std;

void swap(int& a, int& b)
{
    int temp = a;
    a = b;
    b = temp;
}

void findPermutation(int N)
{

    // Initialize array arr[] from 1 to N
    int arr[N];
    for (int i = 0; i < N; i++) {
        arr[i] = i + 1;
    }
    for (int i = 1; i < N; i += 2) {

      // Swap alternate positions
        swap(arr[i], arr[i - 1]);
    }

  // Check N is greater than 1 and
    // N is odd
    if (N % 2 == 1 && N > 1) {

      // Swapping last two positions
        swap(arr[N - 1], arr[N - 2]);
    }

   // Print the permutation
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int N = 7;
    findPermutation(N);
    return 0;
}

// This code is contributed by Parth Manchanda
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

// Function to generate the permutation
// of the first N natural numbers having
// sum of absolute difference between
// element and indices as minimum
import java.util.*;

class GFG{

static void findPermutation(int N)
{

    // Initialize array arr[] from 1 to N
    int[] arr = new int[N];
    int temp;

    for(int i = 0; i < N; i++)
    {
        arr[i] = i + 1;
    }
    for(int i = 1; i < N; i += 2)
    {

        // Swap alternate positions
        temp = arr[i];
        arr[i] = arr[i - 1];
        arr[i - 1] = temp;
    }

    // Check N is greater than 1 and
    // N is odd
    if (N % 2 == 1 && N > 1)
    {

        // Swapping last two positions
        temp = arr[N - 1];
        arr[N - 1] = arr[N - 2];
        arr[N - 2] = temp;
    }

    // Print the permutation
    for(int i = 0; i < N; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 7;

    findPermutation(N);
}
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to generate the permutation
# of the first N natural numbers having
# sum of absolute difference between
# element and indices as minimum
def findPermutation(N):

    # Initialize array arr[] from 1 to N
    arr = [i + 1 for i in range(N)]

    # Swap alternate positions
    for i in range(1, N, 2):
        arr[i], arr[i-1] = arr[i-1], arr[i]

    # Check N is greater than 1 and
    # N is odd
    if N % 2 and N > 1:

        # Swapping last two positions
        arr[-1], arr[-2] = arr[-2], arr[-1]

    # Print the permutation
    for i in arr:
        print(i, end = " ")

# Driver Code
if __name__ == '__main__':

    N = 7
    findPermutation(N)
```

## C#

```
// C# program for the above approach

// Function to generate the permutation
// of the first N natural numbers having
// sum of absolute difference between
// element and indices as minimum
using System;
class GFG {

    static void findPermutation(int N)
    {

        // Initialize array arr[] from 1 to N
        int[] arr = new int[N];
        int temp;
        for (int i = 0; i < N; i++) {
            arr[i] = i + 1;
        }
        for (int i = 1; i < N; i += 2) {

            // Swap alternate positions
            temp = arr[i];
            arr[i] = arr[i - 1];
            arr[i - 1] = temp;
        }

        // Check N is greater than 1 and
        // N is odd
        if (N % 2 == 1 && N > 1) {

            // Swapping last two positions
            temp = arr[N - 1];
            arr[N - 1] = arr[N - 2];
            arr[N - 2] = temp;
        }

        // Print the permutation
        for (int i = 0; i < N; i++) {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int N = 7;
        findPermutation(N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to generate the permutation
// of the first N natural numbers having
// sum of absolute difference between
// element and indices as minimum
function findPermutation(N)
{
    var i;

    // Initialize array arr[] from 1 to N
    var arr = new Array(N);
    for(i = 0; i < N; i++)
    {
        arr[i] = i + 1;
    }

    for(i = 1; i < N; i += 2)
    {

        // Swap alternate positions
        var temp = arr[i];
        arr[i] = arr[i - 1];
        arr[i - 1] = temp;
    }

    // Check N is greater than 1 and
    // N is odd
    if (N % 2 == 1 && N > 1)
    {

        // Swapping last two positions
        var temp = arr[N - 1];
        arr[N - 1] = arr[N - 2];
        arr[N - 2] = temp;
    }

    // Print the permutation
    for(i = 0; i < N; i++)
    {
        document.write(arr[i] + " ");
    }
}

// Driver code
var N = 7;

findPermutation(N);

// This code is contributed by SURENDRA_GANGWAR

</script>
```

**Output:** 

```
2 1 4 3 6 7 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)