# 最多使用楼层(N / 2) + 2 次比较来检查数组中是否存在元素

> 原文:[https://www . geeksforgeeks . org/check-如果一个元素存在于一个数组中-最多使用-2-2-比较/](https://www.geeksforgeeks.org/check-if-an-element-is-present-in-an-array-using-at-most-floorn-2-2-comparisons/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和一个整数 **X** ，任务是[检查**A【】**](https://www.geeksforgeeks.org/linear-search/)中是否存在 **X** 且不超过**层(N/2) + 2** 的比较。
***注:**对于任何指标 **i** 、 **(i < N)** 或**(A【I】= = X)**均视为单独比较。*

**示例:**

> **输入:** A[] = {-3，5，11，3，100，2，88，22，7，900，23，4，1}，X = 88
> **输出:** Yes 8
> **说明:** X = 88 存在于给定数组中，A[] 通过 8 次比较检测到。
> 
> **输入:** A[]= {-3，5，11，3，100，2，88，22，7，900，23，4，1}，X = 6
> **输出:**否
> **说明:** X = 6 在给定数组中不存在，A[]。

**方法:**按照步骤解决问题:

*   初始化一个变量，称 **T** 为 **1** ，存储所有数组元素–**X**的[乘积，即**(A[I]–X)**](https://www.geeksforgeeks.org/program-for-product-of-array/)
*   初始化一个变量，将**比较**设为 **0** ，以存储所需的比较次数。
*   初始化指针， **i** 为 **0** 到[遍历数组。](https://www.geeksforgeeks.org/iterating-arrays-java/)
*   如果 [N 的值为奇数](https://www.geeksforgeeks.org/3-ways-check-number-odd-even-without-using-modulus-operator-set-2-can-merge-httpswww-geeksforgeeks-orgcheck-whether-given-number-even-odd/)，则将**比较**增加 1，因为检查了 N 的[奇偶性，并将 **T** 更新为**T *(A[0]–X)**和 **i** 到 **1** 。](https://www.geeksforgeeks.org/finding-the-parity-of-a-number-efficiently/)
*   因此**【I，N–1】**即**N–I**范围内的元素个数总是偶数。
*   [在**【I，N-1】**范围内遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**A[]**，并执行以下步骤:
    *   将 **T** 的值更新为**T *(A[I]–X)*(A[I+1]–X)**。
    *   将 **i** 更新为 **i + 2** 并将**比较增加 **1** ，因为条件 **i < N** 已选中。**
*   如果 **T** 的值为 **0** ，则将**比较**增加 **1** ，因为比较的是 **T** 的相等性。因此 **X** 存在于 **A[]** 中，打印**“是”**和**对比数量**。
*   否则，打印**结果为“否”**。
*   算法保证**比较次数≤楼层(N / 2) + 2** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether X
// is present in the array A[]
void findElement(int A[], int N, int X)
{
    // Initialise a pointer
    int i = 0;

    // Store the number
    // of comparisons
    int Comparisons = 0;

    // Variable to store product
    int T = 1;

    string Found = "No";

    // Check is N is odd
    Comparisons++;
    if (N % 2 == 1) {

        // Update i and T
        i = 1;
        T *= (A[0] - X);
    }

    // Traverse the array
    for (; i < N; i += 2) {

        // Check if i < N
        Comparisons += 1;

        // Update T
        T *= (A[i] - X);
        T *= (A[i + 1] - X);
    }

    // Check if T is equal to 0
    Comparisons += 1;
    if (T == 0) {
        cout << "Yes " << Comparisons;
    }
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    // Given Input
    int A[] = { -3, 5, 11, 3, 100, 2, 88,
                22, 7, 900, 23, 4, 1 };
    int N = sizeof(A) / sizeof(A[0]);
    int X = 1;

    // Function Call
    findElement(A, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to check whether X
    // is present in the array A[]
    static void findElement(int[] A, int N, int X)
    {

        // Initialise a pointer
        int i = 0;

        // Store the number
        // of comparisons
        int Comparisons = 0;

        // Variable to store product
        int T = 1;

        // Check is N is odd
        Comparisons++;
        if (N % 2 == 1) {

            // Update i and T
            i = 1;
            T *= (A[0] - X);
        }

        // Traverse the array
        for (; i < N; i += 2) {

            // Check if i < N
            Comparisons += 1;

            // Update T
            T *= (A[i] - X);
            T *= (A[i + 1] - X);
        }

        // Check if T is equal to 0
        Comparisons += 1;

        if (T == 0) {
            System.out.println("Yes " + Comparisons);
        }
        else {
            System.out.println("No");
        }
    }

    // Driver code
    public static void main(String[] args)
    { 
      // Given Input
        // Given Input
        int[] A = { -3, 5, 11,  3,  100, 2, 88,
                    22, 7, 900, 23, 4,   1 };
        int N = A.length;
        int X = 1;

        // Function Call
        findElement(A, N, X);
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check whether X
# is present in the array A[]
def findElement(A, N, X):

    # Initialise a pointer
    i = 0

    # Store the number
    # of comparisons
    Comparisons = 0

    # Variable to store product
    T = 1

    Found = "No"

    # Check is N is odd
    Comparisons += 1
    if (N % 2 == 1):

        # Update i and T
        i = 1
        T *= (A[0] - X)

    # Traverse the array
    while(i< N):

        # Check if i < N
        Comparisons += 1

        # Update T
        T *= (A[i] - X)
        T *= (A[i + 1] - X)
        i += 2

    # Check if T is equal to 0
    Comparisons += 1
    if (T == 0):
        print("Yes",Comparisons)
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = [-3, 5, 11, 3, 100, 2, 88, 22, 7, 900, 23, 4, 1]
    N = len(A)
    X = 1

    # Function Call
    findElement(A, N, X)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check whether X
// is present in the array A[]
static void findElement(int[] A, int N, int X)
{

    // Initialise a pointer
    int i = 0;

    // Store the number
    // of comparisons
    int Comparisons = 0;

    // Variable to store product
    int T = 1;

    // Check is N is odd
    Comparisons++;
    if (N % 2 == 1)
    {

        // Update i and T
        i = 1;
        T *= (A[0] - X);
    }

    // Traverse the array
    for(; i < N; i += 2)
    {

        // Check if i < N
        Comparisons += 1;

        // Update T
        T *= (A[i] - X);
        T *= (A[i + 1] - X);
    }

    // Check if T is equal to 0
    Comparions += 1;

    if (T == 0) 
    {
        Console.Write("Yes " + Comparisons);
    }
    else
    {
        Console.Write("No");
    }
}

// Driver Code
public static void Main()
{

    // Given Input
    int[] A = { -3, 5, 11, 3, 100, 2, 88,
                22, 7, 900, 23, 4, 1 };
    int N = A.Length;
    int X = 1;

    // Function Call
    findElement(A, N, X);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check whether X
// is present in the array A[]
function findElement(A, N, X)
{
    // Initialise a pointer
    var i = 0;

    // Store the number
    // of comparisons
    var Comparisons = 0;

    // Variable to store product
    var T = 1;

    var Found = "No";

    // Check is N is odd
    Comparisons += 1;
    if (N % 2 == 1) {

        // Update i and T
        i = 1;
        T *= (A[0] - X);
    }

    // Traverse the array
    for (; i < N; i += 2) {

        // Check if i < N
        Comparisons += 1;

        // Update T
        T *= (A[i] - X);
        T *= (A[i + 1] - X);
    }

    // Check if T is equal to 0
    Comparisons += 1;
    if (T == 0) {
        document.write("Yes " + Comparisons);
    }
    else {
        document.write("No");
    }
}

// Driver Code
    // Given Input
    var A = [-3, 5, 11, 3, 100, 2, 88,
                22, 7, 900, 23, 4, 1];
    var N = A.length;
    var X = 1;

    // Function Call
    findElement(A, N, X);

</script>
```

**Output:** 

```
Yes 8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)