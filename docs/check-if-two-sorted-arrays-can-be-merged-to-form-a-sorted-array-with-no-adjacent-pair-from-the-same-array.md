# 检查两个排序后的数组是否可以合并成一个排序后的数组，同一数组中没有相邻的对

> 原文:[https://www . geeksforgeeks . org/check-if-two-sorted-arrays-可以合并以形成一个排序后的数组，其中没有来自同一个数组的相邻对/](https://www.geeksforgeeks.org/check-if-two-sorted-arrays-can-be-merged-to-form-a-sorted-array-with-no-adjacent-pair-from-the-same-array/)

给定两个大小为 **N** 的[排序数组](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/) **A[]** 和 **B[]** ，任务是检查是否有可能将两个给定的排序数组合并到一个新的[排序数组](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)中，使得没有两个连续的元素来自同一个数组。

**示例:**

> **输入:** A[] = {3，5，8}，B[] = {2，4，6 }
> T3】输出:是
> 
> **说明:**合并数组= {B[0]，A[0]，B[1]，A[1]，B[2]，A[2]}
> 由于结果数组是排序数组，所以需要的输出是 Yes。
> 
> **输入:** A[] = {12，4，2，5，3}，B[] = {32，13，43，10，8}
> **输出:**否

**方法:**按照以下步骤解决问题:

*   初始化一个变量，说**标志=真**检查是否有可能通过合并给定的两个排序数组来形成一个新的[排序数组](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)，使得没有两个连续的元素来自同一个数组。
*   初始化一个变量，说 **prev** 检查合并数组的前一个元素是来自数组 **A[]** 还是数组 **B[]** 。如果 **prev == 1** ，则前一个元素来自数组 **A[]** ，如果 **prev == 0** ，则前一个元素来自数组 **B[]** 。
*   [使用变量 **i** 和 **j** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件:
    *   如果 **A[i] < B[j]和 prev！= 0** 然后增加 **i** 的值并将 **prev** 的值更新为 **0** 。
    *   如果 **B[j] < A[i[和 prev！= 1** 然后增加 **j** 的值，并将 **prev** 的值更新为 **1** 。
    *   如果 **A[i] == B[j]和 prev！= 1** 然后增加 **j** 的值，并将 **prev** 的值更新为 **1** 。
    *   如果 **A[i] == B[j]和 prev！= 0** 然后增加 **i** 的值，并将 **prev** 的值更新为 **0** 。
    *   如果以上条件都不满足，则更新**标志=假**。
*   最后，打印**标志**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to merge
// the two given arrays with given conditions
bool checkIfPossibleMerge(int A[], int B[], int N)
{
    // Stores index of
    // the array A[]
    int i = 0;

    // Stores index of
    // the array  B[]
    int j = 0;

    // Check if the previous element are from
    // the array A[] or from the array B[]
    int prev = -1;

    // Check if it is possible to merge the two
    // given sorted arrays with given conditions
    int flag = 1;

    // Traverse both the arrays
    while (i < N && j < N) {

        // If A[i] is less than B[j] and
        // previous element are not from A[]
        if (A[i] < B[j] && prev != 0) {

            // Update prev
            prev = 0;

            // Update i
            i++;
        }

        // If B[j] is less than A[i] and
        // previous element are not from B[]
        else if (B[j] < A[i] && prev != 1) {

            // Update prev
            prev = 1;

            // Update j
            j++;
        }

        // If A[i] equal to B[j]
        else if (A[i] == B[j]) {

            // If previous element
            // are not from B[]
            if (prev != 1) {

                // Update prev
                prev = 1;

                // Update j
                j++;
            }

            // If previous element is
            // not from A[]
            else {

                // Update prev
                prev = 0;

                // Update i
                i++;
            }
        }

        // If it is not possible to merge two
        // sorted arrays with given conditions
        else {

            // Update flag
            flag = 0;
            break;
        }
    }

    return flag;
}

// Driver Code
int main()
{
    int A[3] = { 3, 5, 8 };
    int B[3] = { 2, 4, 6 };
    int N = sizeof(A) / sizeof(A[0]);

    if (checkIfPossibleMerge(A, B, N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to check if it is possible to merge
// the two given arrays with given conditions
static boolean checkIfPossibleMerge(int[] A, int[] B,
                                    int N)
{

    // Stores index of
    // the array A[]
    int i = 0;

    // Stores index of
    // the array  B[]
    int j = 0;

    // Check if the previous element are from
    // the array A[] or from the array B[]
    int prev = -1;

    // Check if it is possible to merge the two
    // given sorted arrays with given conditions
    boolean flag = true;

    // Traverse both the arrays
    while (i < N && j < N)
    {

        // If A[i] is less than B[j] and
        // previous element are not from A[]
        if (A[i] < B[j] && prev != 0)
        {

            // Update prev
            prev = 0;

            // Update i
            i++;
        }

        // If B[j] is less than A[i] and
        // previous element are not from B[]
        else if (B[j] < A[i] && prev != 1)
        {

            // Update prev
            prev = 1;

            // Update j
            j++;
        }

        // If A[i] equal to B[j]
        else if (A[i] == B[j])
        {

            // If previous element
            // are not from B[]
            if (prev != 1)
            {

                // Update prev
                prev = 1;

                // Update j
                j++;
            }

            // If previous element is
            // not from A[]
            else
            {

                // Update prev
                prev = 0;

                // Update i
                i++;
            }
        }

        // If it is not possible to merge two
        // sorted arrays with given conditions
        else
        {

            // Update flag
            flag = false;
            break;
        }
    }
    return flag;
}

// Driver Code
public static void main(String[] args)
{
    int[] A = { 3, 5, 8 };
    int[] B = { 2, 4, 6 };
    int N = A.length;

    if (checkIfPossibleMerge(A, B, N))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if it is possible
# to merge the two given arrays with
# given conditions
def checkIfPossibleMerge(A, B, N):

    # Stores index of
    # the array A[]
    i = 0

    # Stores index of
    # the array  B[]
    j = 0

    # Check if the previous element
    # are from the array A[] or from
    # the array B[]
    prev = -1

    # Check if it is possible to merge
    # the two given sorted arrays with
    # given conditions
    flag = 1

    # Traverse both the arrays
    while (i < N and j < N):

        # If A[i] is less than B[j] and
        # previous element are not from A[]
        if (A[i] < B[j] and prev != 0):

            # Update prev
            prev = 0

            # Update i
            i += 1

        # If B[j] is less than A[i] and
        # previous element are not from B[]
        elif (B[j] < A[i] and prev != 1):

            # Update prev
            prev = 1

            # Update j
            j += 1

        # If A[i] equal to B[j]
        elif (A[i] == B[j]):

            # If previous element
            # are not from B[]
            if (prev != 1):

                # Update prev
                prev = 1

                # Update j
                j += 1

            # If previous element is
            # not from A[]
            else:

                # Update prev
                prev = 0

                # Update i
                i += 1

        # If it is not possible to merge two
        # sorted arrays with given conditions
        else:

            # Update flag
            flag = 0
            break

    return flag

# Driver Code
if __name__ == '__main__':

    A = [ 3, 5, 8 ]
    B = [ 2, 4, 6 ]
    N = len(A)

    if (checkIfPossibleMerge(A, B, N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if it is possible to merge
// the two given arrays with given conditions
static bool checkIfPossibleMerge(int[] A, int[] B,
                                 int N)
{

    // Stores index of
    // the array A[]
    int i = 0;

    // Stores index of
    // the array  B[]
    int j = 0;

    // Check if the previous element are
    // from the array A[] or from the
    // array B[]
    int prev = -1;

    // Check if it is possible to merge
    // the two given sorted arrays with
    // given conditions
    bool flag = true;

    // Traverse both the arrays
    while (i < N && j < N)
    {

        // If A[i] is less than B[j] and
        // previous element are not from A[]
        if (A[i] < B[j] && prev != 0)
        {

            // Update prev
            prev = 0;

            // Update i
            i++;
        }

        // If B[j] is less than A[i] and
        // previous element are not from B[]
        else if (B[j] < A[i] && prev != 1)
        {

            // Update prev
            prev = 1;

            // Update j
            j++;
        }

        // If A[i] equal to B[j]
        else if (A[i] == B[j])
        {

            // If previous element
            // are not from B[]
            if (prev != 1)
            {

                // Update prev
                prev = 1;

                // Update j
                j++;
            }

            // If previous element is
            // not from A[]
            else
            {

                // Update prev
                prev = 0;

                // Update i
                i++;
            }
        }

        // If it is not possible to merge two
        // sorted arrays with given conditions
        else
        {

            // Update flag
            flag = false;
            break;
        }
    }
    return flag;
}

// Driver Code
public static void Main()
{
    int[] A = { 3, 5, 8 };
    int[] B = { 2, 4, 6 };
    int N = A.Length;

    if (checkIfPossibleMerge(A, B, N))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if it is possible to merge
// the two given arrays with given conditions
function checkIfPossibleMerge(A, B, N)
{

    // Stores index of
    // the array A[]
    let i = 0;

    // Stores index of
    // the array  B[]
    let j = 0;

    // Check if the previous element are from
    // the array A[] or from the array B[]
    let prev = -1;

    // Check if it is possible to merge the two
    // given sorted arrays with given conditions
    let flag = true;

    // Traverse both the arrays
    while (i < N && j < N)
    {

        // If A[i] is less than B[j] and
        // previous element are not from A[]
        if (A[i] < B[j] && prev != 0)
        {

            // Update prev
            prev = 0;

            // Update i
            i++;
        }

        // If B[j] is less than A[i] and
        // previous element are not from B[]
        else if (B[j] < A[i] && prev != 1)
        {

            // Update prev
            prev = 1;

            // Update j
            j++;
        }

        // If A[i] equal to B[j]
        else if (A[i] == B[j])
        {

            // If previous element
            // are not from B[]
            if (prev != 1)
            {

                // Update prev
                prev = 1;

                // Update j
                j++;
            }

            // If previous element is
            // not from A[]
            else
            {

                // Update prev
                prev = 0;

                // Update i
                i++;
            }
        }

        // If it is not possible to merge two
        // sorted arrays with given conditions
        else
        {

            // Update flag
            flag = false;
            break;
        }
    }
    return flag;
}

    // Driver Code

    let A = [ 3, 5, 8 ];
    let B = [ 2, 4, 6 ];
    let N = A.length;

    if (checkIfPossibleMerge(A, B, N))
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }

// This code is contributed by splevel62.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)