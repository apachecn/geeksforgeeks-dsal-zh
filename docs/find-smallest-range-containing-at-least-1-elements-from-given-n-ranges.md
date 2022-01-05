# 从给定的 N 个范围中找出包含至少 1 个元素的最小范围

> 原文:[https://www . geesforgeks . org/find-最小范围-包含至少 1 个元素-从给定的 n 个范围/](https://www.geeksforgeeks.org/find-smallest-range-containing-at-least-1-elements-from-given-n-ranges/)

给定形式为**【L，R】**的 **N** 范围，任务是找到具有最小整数个数的范围，使得所有给定的 **N** 范围中的至少一个点存在于该范围内。

**示例:**

> **输入:**范围[] = {{1，6}、{2，7}、{3，8}、{4，9}}
> **输出:**6 6
> T6】解释:所有给定的范围都包含 6 作为它们之间的整数。因此，[6，6]是具有 1 个整数的有效范围，这是最小可能值。其他有效范围是[4，4]和[5，5]。
> 
> **输入:**范围[] = {{1，4}，{4，5}，{7，9}，{9，12}}
> **输出:** 4 9

**方法:**这个问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)通过以下观察来解决:

*   假设 **L** 是所有给定范围内的最小端点。然后，可以观察到，所有给定的范围必须包含范围**【L，∩】**中的一个点。
*   同样，假设 **R** 是所有给定范围内的最大起点。然后，基于与上面类似的观察，所有范围还必须包含范围**[-∩，R]** 中的一个点。

因此，使用上述观察，所需的范围将是**【L，R】**。在 **L > R** 的情况下，答案可以是 **L** 和 **R** 之间的任意整数，因为它们都是有效范围。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum range such
// that alteast one point of all the
// given N ranges exist in the range
void minRequiredRange(
    vector<pair<int, int> > ranges,
    int N)
{

    // Stores the starting point of
    // the required range
    int L = INT_MAX;

    // Stores the ending point of the
    // required range
    int R = INT_MIN;

    // Loop to iterate over all the given
    // N ranges
    for (int i = 0; i < N; i++) {

        // Calculate the smallest end point
        // over all the given ranges
        L = min(L, ranges[i].second);

        // Calculate the largest starting point
        // over all the given ranges
        R = max(R, ranges[i].first);
    }

    // If starting point is greater that the
    // end point
    if (R < L) {

        // Print any integer between L and R
        cout << L << " " << L;
    }
    else {

        // Print Answer
        cout << L << " " << R;
    }
}

// Driver Code
int main()
{
    vector<pair<int, int> > ranges{
        { 1, 4 }, { 4, 5 }, { 7, 9 }, { 9, 12 }
    };

    minRequiredRange(ranges, ranges.size());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find minimum range such
    // that alteast one point of all the
    // given N ranges exist in the range
    public static void minRequiredRange(int[][] ranges, int N) {

        // Stores the starting point of
        // the required range
        int L = Integer.MAX_VALUE;

        // Stores the ending point of the
        // required range
        int R = Integer.MIN_VALUE;

        // Loop to iterate over all the given
        // N ranges
        for (int i = 0; i < N; i++) {

            // Calculate the smallest end point
            // over all the given ranges
            L = Math.min(L, ranges[i][1]);

            // Calculate the largest starting point
            // over all the given ranges
            R = Math.max(R, ranges[i][0]);
        }

        // If starting point is greater that the
        // end point
        if (R < L) {

            // Print any integer between L and R
            System.out.println(L + " " + L);
        } else {

            // Print Answer
            System.out.println(L + " " + R);
        }
    }

    // Driver Code
    public static void main(String args[]) {
        int[][] ranges = { { 1, 4 }, { 4, 5 }, { 7, 9 }, { 9, 12 } };

        minRequiredRange(ranges, ranges.length);
    }

}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find minimum range such
# that alteast one point of all the
# given N ranges exist in the range
def minRequiredRange(ranges, N):

    # Stores the starting point of
    # the required range
    L = 10 ** 9

    # Stores the ending point of the
    # required range
    R = 10 ** -9

    # Loop to iterate over all the given
    # N ranges
    for i in range(N):

        # Calculate the smallest end point
        # over all the given ranges
        L = min(L, ranges[i]["second"])

        # Calculate the largest starting point
        # over all the given ranges
        R = max(R, ranges[i]["first"])

    # If starting point is greater that the
    # end point
    if (R < L):

        # Print any integer between L and R
        print(f"{L} {L}")
    else:
        # Print Answer
        print(f"{L} {R}")

# Driver Code
ranges = [{"first": 1, "second": 4}, {"first": 4, "second": 5}, {
    "first": 7, "second": 9}, {"first": 9, "second": 12}
]

minRequiredRange(ranges, len(ranges))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find minimum range such
    // that alteast one point of all the
    // given N ranges exist in the range
    public static void minRequiredRange(int[, ] ranges,
                                        int N)
    {

        // Stores the starting point of
        // the required range
        int L = Int32.MaxValue;

        // Stores the ending point of the
        // required range
        int R = Int32.MinValue;

        // Loop to iterate over all the given
        // N ranges
        for (int i = 0; i < N; i++) {

            // Calculate the smallest end point
            // over all the given ranges
            L = Math.Min(L, ranges[i, 1]);

            // Calculate the largest starting point
            // over all the given ranges
            R = Math.Max(R, ranges[i, 0]);
        }

        // If starting point is greater that the
        // end point
        if (R < L) {

            // Print any integer between L and R
            Console.WriteLine(L + " " + L);
        }
        else {

            // Print Answer
            Console.WriteLine(L + " " + R);
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[, ] ranges
            = { { 1, 4 }, { 4, 5 }, { 7, 9 }, { 9, 12 } };

        minRequiredRange(ranges, ranges.GetLength(0));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to find minimum range such
       // that alteast one point of all the
       // given N ranges exist in the range
       function minRequiredRange(
           ranges,
           N) {

           // Stores the starting point of
           // the required range
           let L = Number.MAX_VALUE;

           // Stores the ending point of the
           // required range
           let R = Number.MIN_VALUE;

           // Loop to iterate over all the given
           // N ranges
           for (let i = 0; i < N; i++) {

               // Calculate the smallest end point
               // over all the given ranges
               L = Math.min(L, ranges[i].second);

               // Calculate the largest starting point
               // over all the given ranges
               R = Math.max(R, ranges[i].first);
           }

           // If starting point is greater that the
           // end point
           if (R < L) {

               // Print any integer between L and R
               document.write(L + " " + L);
           }
           else {

               // Print Answer
               document.write(L + " " + R);
           }
       }

       // Driver Code

       let ranges = [
           { first: 1, second: 4 }, { first: 4, second: 5 }, { first: 7, second: 9 }, { first: 9, second: 12 }
       ];

       minRequiredRange(ranges, ranges.length);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
4 9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)