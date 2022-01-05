# 添加到数组 A 中 N-1 个元素的最小可能整数，使得数组 B 的元素出现在 A 中

> 原文:[https://www . geesforgeks . org/最小可能整数加到 n-1 个数组中的元素-a-这样数组中的元素-b-就出现在 a 中/](https://www.geeksforgeeks.org/smallest-possible-integer-to-be-added-to-n-1-elements-in-array-a-such-that-elements-of-array-b-are-present-in-a/)

给定两个长度为 **N** 的数组**A【】T1】和长度为 **N-1** 的**B【】T5 】,任务是找到除了一个元素之外添加到**A【】**每个元素的最小正整数 **X** ，使得数组**B【】**的所有元素都出现在数组**A【】**中。假设找到 **X** 总是可能的。****

**示例:**

> **输入:** A[] = {1，4，3，8}，B[] = {15，8，11}
> **输出:** 7
> **解释:**除了 3 之外，数组 A 的每个元素加 7 就得到数组 B 的所有元素
> 
> **输入:** A[] = {4，8}，B[] = {10}
> **输出:** 2
> **解释**:2 加 8 等于 10。

**进场:**思路是用[贪婪](https://www.geeksforgeeks.org/greedy-algorithms/)进场。

*   对数组 **A[]** 和 **B[]** 进行排序
*   观察可以看出， **X** 的值可以是**B[0]–A[0]**或**B[0]–A[1]**。
*   因此不考虑 **A[0]** 或 **A[1]** ，而将 **X** 添加到其余元素中。
*   通过遍历数组检查两个值是否有效，如果发现两个 **X** 值都有效，则选择**最小值**并打印。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest positive integer
// X such that X is added to every element of A
// except one element to give array B
void findVal(int A[], int B[], int N)
{
    // Stores the unique elements of array A
    unordered_set<int> s;

    for (int i = 0; i < N; i++) {
        // Insert A[i] into the set s
        s.insert(A[i]);
    }

    // Sort array A[]
    sort(A, A + N);

    // Sort array B[]
    sort(B, B + N - 1);

    // Assume X value as B[0] - A[1]
    int X = B[0] - A[1];

    // Check if X value assumed is negative or 0
    if (X <= 0)

        // Update the X value to B[0] - A[0]
        X = B[0] - A[0];

    else {

        for (int i = 0; i < N - 1; i++) {

            // If assumed value is wrong
            if (s.count(B[i] - X) == 0) {

                // Update X value
                X = B[0] - A[0];
                break;
            }
        }
    }

    cout << X << endl;
}

// Driver Code
int main()
{

    int A[] = { 1, 4, 3, 8 };
    int B[] = { 15, 8, 11 };
    int N = sizeof(A) / sizeof(A[0]);

    findVal(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

public class GFG
{

// Function to find the smallest positive integer
// X such that X is added to every element of A
// except one element to give array B
static void findVal(int []A, int []B, int N)
{
    // Stores the unique elements of array A
    HashSet<Integer> s = new HashSet<Integer>();

    for (int i = 0; i < N; i++) {
        // Insert A[i] into the set s
        s.add(A[i]);
    }

    // Sort array A[]
    Arrays.sort(A);

    // Sort array B[]
    Arrays.sort(B);

    // Assume X value as B[0] - A[1]
    int X = B[0] - A[1];

    // Check if X value assumed is negative or 0
    if (X <= 0)

        // Update the X value to B[0] - A[0]
        X = B[0] - A[0];

    else {

        for (int i = 0; i < N - 1; i++) {

            // If assumed value is wrong
            if (s.contains(B[i] - X) == false) {

                // Update X value
                X = B[0] - A[0];
                break;
            }
        }
    }

    System.out.println(X);
}

// Driver Code
public static void main(String args[])
{
    int []A = { 1, 4, 3, 8 };
    int []B = { 15, 8, 11 };
    int N = A.length;

    findVal(A, B, N);
}
}

// This code is contributed by Samim Hossain Mondal
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the smallest positive integer
# X such that X is added to every element of A
# except one element to give array B
def findVal(A, B, N):

    # Stores the unique elements of array A
    s = set()

    for i in range(N):
        # Insert A[i] into the set s
        s.add(A[i])

    # Sort array A[]
    A.sort()

    # Sort array B[]
    B.sort()

    # Assume X value as B[0] - A[1]
    X = B[0] - A[1]

    # Check if X value assumed is negative or 0
    if (X <= 0):

        # Update the X value to B[0] - A[0]
        X = B[0] - A[0]

    else:

        for i in range(N - 1):

            # If assumed value is wrong
            if (B[i] - X not in s):

                # Update X value
                X = B[0] - A[0]
                break

    print(X)

# Driver Code
if __name__ == '__main__':
    A = [1, 4, 3, 8]
    B = [15, 8, 11]
    N = len(A)

    findVal(A, B, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;
class GFG
{
// Function to find the smallest positive integer
// X such that X is added to every element of A
// except one element to give array B
static void findVal(int []A, int []B, int N)
{
    // Stores the unique elements of array A
    HashSet<int> s = new HashSet<int>();

    for (int i = 0; i < N; i++) {
        // Insert A[i] into the set s
        s.Add(A[i]);
    }

    // Sort array A[]
    Array.Sort(A);

    // Sort array B[]
    Array.Sort(B);

    // Assume X value as B[0] - A[1]
    int X = B[0] - A[1];

    // Check if X value assumed is negative or 0
    if (X <= 0)

        // Update the X value to B[0] - A[0]
        X = B[0] - A[0];

    else {

        for (int i = 0; i < N - 1; i++) {

            // If assumed value is wrong
            if (s.Contains(B[i] - X) == false) {

                // Update X value
                X = B[0] - A[0];
                break;
            }
        }
    }

    Console.Write(X);
}

// Driver Code
public static void Main()
{
    int []A = { 1, 4, 3, 8 };
    int []B = { 15, 8, 11 };
    int N = A.Length;

    findVal(A, B, N);
}
}
// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the smallest positive integer
        // X such that X is added to every element of A
        // except one element to give array B
        function findVal(A, B, N)
        {

            // Stores the unique elements of array A
            let s = new Set();

            for (let i = 0; i < N; i++)
            {

                // Insert A[i] into the set s
                s.add(A[i]);
            }

            // Sort array A[]
            A.sort(function (a, b) { return a - b });

            // Sort array B[]
            B.sort(function (a, b) { return a - b })

            // Assume X value as B[0] - A[1]
            let X = B[0] - A[1];

            // Check if X value assumed is negative or 0
            if (X <= 0)

                // Update the X value to B[0] - A[0]
                X = B[0] - A[0];

            else {

                for (let i = 0; i < N - 1; i++) {

                    // If assumed value is wrong
                    if (s.has(B[i] - X) == false) {

                        // Update X value
                        X = B[0] - A[0];
                        break;
                    }
                }
            }

            document.write(X);
        }

        // Driver Code
        let A = [1, 4, 3, 8];
        let B = [15, 8, 11];
        let N = A.length;

        findVal(A, B, N);

     // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
7
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*