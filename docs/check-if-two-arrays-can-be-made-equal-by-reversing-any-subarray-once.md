# 通过反转任一子阵列一次来检查两个阵列是否可以相等

> 原文:[https://www . geeksforgeeks . org/check-if-two-array-可通过一次反转任意子阵列使其相等/](https://www.geeksforgeeks.org/check-if-two-arrays-can-be-made-equal-by-reversing-any-subarray-once/)

给定两个大小相等的数组 **A[]** 和**B[]****N**，任务是通过只反转一次 **A** 的任意子数组来检查 **A[]** 是否可以等于 **B[]** 。

**示例:**

> **输入:** A[] = {1，3，2，4}
> B[] = {1，2，3，4}
> **输出:**是
> **说明:**
> 子阵{3，2}可以反转为{2，3}，这样 A 等于 B.
> 
> **输入:** A[] = {1，4，2，3}
> B[] = {1，2，3，4}
> **输出:**否
> **说明:**
> 不存在 A 的子数组，当反转时，A 等于 B

**天真方法:**检查**A【】**的所有子阵列，并在反转子阵列后比较两个阵列。
***时间复杂度:** O(N <sup>2</sup> )。*

**有效方法:**

*   首先，在 **A** 和 **B** 中找到不相等的子数组的开始和结束索引。
*   然后，通过反转所需的子阵列，我们可以检查 **A** 是否可以等于 **B** 。
*   起始索引是数组中的第一个索引 **A[i]！= B[i]** 并且结束索引是数组中的最后一个索引, **A[i]！= B[i]** 。

下面是上述方法的实现。

## C++

```
// C++ implementation to
// check whether two arrays
// can be made equal by
// reversing a sub-array
// only once
#include <bits/stdc++.h>
using namespace std;

// Function to check whether two arrays
// can be made equal by reversing
// a sub-array only once
void checkArray(int A[], int B[], int N)
{
    // Integer variable for
    // storing the required
    // starting and ending
    // indices in the array
    int start = 0;
    int end = N - 1;

    // Finding the smallest index
    // for which A[i] != B[i]
    // i.e the starting index
    // of the unequal sub-array
    for (int i = 0; i < N; i++) {
        if (A[i] != B[i]) {
            start = i;
            break;
        }
    }
    // Finding the largest index
    // for which A[i] != B[i]
    // i.e the ending index
    // of the unequal sub-array
    for (int i = N - 1; i >= 0; i--) {
        if (A[i] != B[i]) {
            end = i;
            break;
        }
    }

    // Reversing the sub-array
    // A[start], A[start+1] .. A[end]
    reverse(A + start, A + end + 1);

    // Checking whether on reversing
    // the sub-array A[start]...A[end]
    // makes the arrays equal

    for (int i = 0; i < N; i++) {
        if (A[i] != B[i]) {
            // If any element of the
            // two arrays is unequal
            // print No and return
            cout << "No" << endl;
            return;
        }
    }
    // Print Yes if arrays are
    // equal after reversing
    // the sub-array
    cout << "Yes" << endl;
}
// Driver code
int main()
{
    int A[] = { 1, 3, 2, 4 };
    int B[] = { 1, 2, 3, 4 };
    int N = sizeof(A) / sizeof(A[0]);
    checkArray(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// check whether two arrays
// can be made equal by
// reversing a sub-array
// only once
import java.util.*;
class GFG{

// Function to check whether two arrays
// can be made equal by reversing
// a sub-array only once
static void checkArray(int A[], int B[], int N)
{
    // Integer variable for
    // storing the required
    // starting and ending
    // indices in the array
    int start = 0;
    int end = N - 1;

    // Finding the smallest index
    // for which A[i] != B[i]
    // i.e the starting index
    // of the unequal sub-array
    for (int i = 0; i < N; i++)
    {
        if (A[i] != B[i])
        {
            start = i;
            break;
        }
    }
    // Finding the largest index
    // for which A[i] != B[i]
    // i.e the ending index
    // of the unequal sub-array
    for (int i = N - 1; i >= 0; i--)
    {
        if (A[i] != B[i])
        {
            end = i;
            break;
        }
    }

    // Reversing the sub-array
    // A[start], A[start+1] .. A[end]
    Collections.reverse(Arrays.asList(A));

    // Checking whether on reversing
    // the sub-array A[start]...A[end]
    // makes the arrays equal
    for (int i = 0; i < N; i++)
    {
        if (A[i] != B[i])
        {
            // If any element of the
            // two arrays is unequal
            // print No and return
            System.out.println("No");
            return;
        }
    }
    // Print Yes if arrays are
    // equal after reversing
    // the sub-array
   System.out.println("Yes");
}
// Driver code
public static void main(String[] args)
{
    int A[] = { 1, 3, 2, 4 };
    int B[] = { 1, 2, 3, 4 };
    int N = A.length;
    checkArray(A, B, N);
}
}

// This Code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 implementation to
# check whether two arrays
# can be made equal by
# reversing a sub-array
# only once

# Function to check whether two arrays
# can be made equal by reversing
# a sub-array only once
def checkArray(A, B, N):

    # Integer variable for
    # storing the required
    # starting and ending
    # indices in the array
    start = 0
    end = N - 1

    # Finding the smallest index
    # for which A[i] != B[i]
    # i.e the starting index
    # of the unequal sub-array
    for i in range(N):
        if (A[i] != B[i]):
            start = i
            break

    # Finding the largest index
    # for which A[i] != B[i]
    # i.e the ending index
    # of the unequal sub-array
    for i in range(N - 1, -1, -1):
        if (A[i] != B[i]):
            end = i
            break

    # Reversing the sub-array
    # A[start], A[start+1] .. A[end]
    A[start:end + 1] = reversed(A[start:end + 1])

    # Checking whether on reversing
    # the sub-array A[start]...A[end]
    # makes the arrays equal
    for i in range(N):
        if (A[i] != B[i]):

            # If any element of the
            # two arrays is unequal
            # print No and return
            print("No")
            return

    # Print Yes if arrays are
    # equal after reversing
    # the sub-array
    print("Yes")

# Driver code
if __name__ == '__main__':

    A = [ 1, 3, 2, 4 ]
    B = [ 1, 2, 3, 4 ]
    N = len(A)

    checkArray(A, B, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to
// check whether two arrays
// can be made equal by
// reversing a sub-array
// only once
using System;

class GFG{

// Function to check whether two arrays
// can be made equal by reversing
// a sub-array only once
static void checkArray(int []A, int []B, int N)
{

    // Integer variable for
    // storing the required
    // starting and ending
    // indices in the array
    int start = 0;
    int end = N - 1;

    // Finding the smallest index
    // for which A[i] != B[i]
    // i.e the starting index
    // of the unequal sub-array
    for(int i = 0; i < N; i++)
    {
        if (A[i] != B[i])
        {
            start = i;
            break;
        }
    }

    // Finding the largest index
    // for which A[i] != B[i]
    // i.e the ending index
    // of the unequal sub-array
    for(int i = N - 1; i >= 0; i--)
    {
        if (A[i] != B[i])
        {
            end = i;
            break;
        }
    }

    // Reversing the sub-array
    // A[start], A[start+1] .. A[end]
    Array.Reverse(A, start, end);

    // Checking whether on reversing
    // the sub-array A[start]...A[end]
    // makes the arrays equal
    for(int i = 0; i < N; i++)
    {
        if (A[i] != B[i])
        {

            // If any element of the
            // two arrays is unequal
            // print No and return
            Console.Write("No");
            return;
        }
    }

    // Print Yes if arrays are
    // equal after reversing
    // the sub-array
    Console.Write("Yes");
}

// Driver code
public static void Main(string[] args)
{
    int []A = { 1, 3, 2, 4 };
    int []B = { 1, 2, 3, 4 };
    int N = A.Length;
    checkArray(A, B, N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to
// check whether two arrays
// can be made equal by
// reversing a sub-array
// only once

// Function to check whether two arrays
// can be made equal by reversing
// a sub-array only once
function checkArray(A, B, N)
{
    // Integer variable for
    // storing the required
    // starting and ending
    // indices in the array
    var start = 0;
    var end = N - 1;

    // Finding the smallest index
    // for which A[i] != B[i]
    // i.e the starting index
    // of the unequal sub-array
    for (var i = 0; i < N; i++) {
        if (A[i] != B[i]) {
            start = i;
            break;
        }
    }
    // Finding the largest index
    // for which A[i] != B[i]
    // i.e the ending index
    // of the unequal sub-array
    for (var i = N - 1; i >= 0; i--) {
        if (A[i] != B[i]) {
            end = i;
            break;
        }
    }

    // Reversing the sub-array
    // A[start], A[start+1] .. A[end]
    var l = start;
    var r = end;
    var d = parseInt((r-l+2)/2);
      for(var i=0;i<d;i++)
      {
         var t = A[l+i];
         A[l+i] = A[r-i];
         A[r-i] = t;
      }

    // Checking whether on reversing
    // the sub-array A[start]...A[end]
    // makes the arrays equal

    for (var i = 0; i < N; i++) {
        if (A[i] != B[i]) {
            // If any element of the
            // two arrays is unequal
            // print No and return
            document.write( "No" );
            return;
        }
    }
    // Print Yes if arrays are
    // equal after reversing
    // the sub-array
    document.write( "Yes" );
}
// Driver code
var A = [1, 3, 2, 4];
var B = [1, 2, 3, 4];
var N = A.length;
checkArray(A, B, N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间** : O(1)*