# 计算可消耗糖果的最大数量

> 原文:[https://www . geesforgeks . org/count-最大可消费糖果数量/](https://www.geeksforgeeks.org/count-maximum-number-of-consumable-candies/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和**B【】**，分别由表示每种糖果数量和最大消耗限额的 **N** 个整数和表示添加的未知糖果数量的整数 **M** 组成，任务是找出一个人在眼罩中可以消耗的最大糖果数量。

**示例:**

> **输入:** A[] = {4，5，2，3}，B[] = {8，13，6，4}，M = 5
> **输出:** 4
> **说明:**直接消耗第 4<sup>类型的全部 3 颗糖果，再消耗一颗可以是任意类型的糖果。因此，一个人总共只能安全食用 4 颗糖果。</sup>
> 
> **输入:** A[] = {2，4，1，9，6}，B[] = {8，7，3，12，7}，M = 0
> **输出:** 2
> **说明:**一个人可以直接消费所有的糖果，因为所有类型的糖果都在安全范围内。

**方法:**给定的问题可以基于以下观察来解决:

> *   If **a [i]+m ≤ b [i]** for each type of candy, it is safe to consume all available candy.
> *   Otherwise, all **0 ≤ I < N.**
> 
> 只能消耗最少**分钟(A[i] + M，B[i])**

按照以下步骤解决问题:

1.  初始化两个变量，比如**和**和**总计**，以存储可安全消费的最大糖果数和糖果总数
2.  初始化一个变量，比如 **allSafe = true** ，检查所有类型的糖果是否可以安全食用。
3.  [遍历范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**如果 **A[i] + M > B[i]** ，则设置 **allSafe = false** 并更新 **ans = min(ans，B[i])** 。否则，更新 **ans = min(ans，A[i])。**
4.  如果 **allSafe** 为真，则[打印数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) **A[]** 的总和。
5.  否则，在**和**中打印结果。

下面是上述方法的实现:

## C++

```
// C++ implementation
// of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// maximum consumable candies
int maximumCandy(int candies[],
                 int safety[],
                 int N, int M)
{

    // Store the count of total candies
    int total = 0;

    // Stores the count of maximum
    // consumable candies
    int ans = INT_MAX;

    // Checks if it is safe
    // to counsume all candies
    bool all_safe = true;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If A[i] + M is greater than B[i]
        if (candies[i] + M > safety[i]) {

            // Mark all_safe as false
            all_safe = false;

            // Update ans
            ans = min(ans, safety[i]);
        }
        else {

            // Update ans
            ans = min(ans, candies[i] + M);
        }

        // Increment total by A[i]
        total += candies[i];
    }

    // If all_safe is true
    if (all_safe)
        return total;

    // Otherwise,
    else
        return ans;
}

// Driver Code
int main()
{
    int A[] = { 2, 4, 1, 9, 6 };
    int B[] = { 8, 7, 3, 12, 7 };
    int M = 0;

    int N = sizeof(A) / sizeof(A[0]);

    // Function call to find
    // maximum consumable candies
    cout << maximumCandy(A, B, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implememtation
// of the above approach
public class GFG
{

  // Function to find the count of
  // maximum consumable candies
  static int maximumCandy(int []candies,
                          int []safety,
                          int N, int M)
  {

    // Store the count of total candies
    int total = 0;

    // Stores the count of maximum
    // consumable candies
    int ans = Integer.MAX_VALUE;

    // Checks if it is safe
    // to counsume all candies
    boolean all_safe = true;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

      // If A[i] + M is greater than B[i]
      if (candies[i] + M > safety[i])
      {

        // Mark all_safe as false
        all_safe = false;

        // Update ans
        ans = Math.min(ans, safety[i]);
      }
      else
      {

        // Update ans
        ans = Math.min(ans, candies[i] + M);
      }

      // Increment total by A[i]
      total += candies[i];
    }

    // If all_safe is true
    if (all_safe)
      return total;

    // Otherwise,
    else
      return ans;
  }

  // Driver Code
  public static void main (String[] args)
  {
    int A[] = { 4, 5, 2, 3 };
    int B[] = { 8, 13, 6, 4 };
    int M = 5;

    int N = A.length;

    // Function call to find
    // maximum consumable candies
    System.out.println(maximumCandy(A, B, N, M));

  }

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 implememtation
# of the above approach

# Function to find the count of
# maximum consumable candies
def maximumCandy(candies, safety, N, M):

    # Store the count of total candies
    total = 0

    # Stores the count of maximum
    # consumable candies
    ans = 10**8

    # Checks if it is safe
    # to counsume all candies
    all_safe = True

    # Traverse the array arr
    for i in range(N):

        # If A[i] + M is greater than B[i]
        if (candies[i] + M > safety[i]):

            # Mark all_safe as false
            all_safe = False

            # Update ans
            ans = min(ans, safety[i])
        else:

            # Update ans
            ans = min(ans, candies[i] + M)

        # Increment total by A[i]
        total += candies[i]

    # If all_safe is true
    if (all_safe):
        return total

    # Otherwise,
    else:
        return ans

# Driver Code
if __name__ == '__main__':
    A = [4, 5, 2, 3]
    B = [ 8, 13, 6, 4]
    M = 5

    N = len(A)

    # Function call to find
    # maximum consumable candies
    print (maximumCandy(A, B, N, M))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# implememtation
// of the above approach
using System;
class GFG {

    // Function to find the count of
    // maximum consumable candies
    static int maximumCandy(int[] candies, int[] safety, int N, int M)
    {

        // Store the count of total candies
        int total = 0;

        // Stores the count of maximum
        // consumable candies
        int ans = Int32.MaxValue;

        // Checks if it is safe
        // to counsume all candies
        bool all_safe = true;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // If A[i] + M is greater than B[i]
            if (candies[i] + M > safety[i]) {

                // Mark all_safe as false
                all_safe = false;

                // Update ans
                ans = Math.Min(ans, safety[i]);
            }
            else {

                // Update ans
                ans = Math.Min(ans, candies[i] + M);
            }

            // Increment total by A[i]
            total += candies[i];
        }

        // If all_safe is true
        if (all_safe)
            return total;

        // Otherwise,
        else
            return ans;
    }

  // Driver code
  static void Main()
  {
    int[] A = { 4, 5, 2, 3 };
    int[] B = { 8, 13, 6, 4 };
    int M = 5;

    int N = A.Length;

    // Function call to find
    // maximum consumable candies
    Console.WriteLine(maximumCandy(A, B, N, M));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// javascript program of the above approach

  // Function to find the count of
  // maximum consumable candies
  function maximumCandy(candies, safety,
                          N, M)
  {

    // Store the count of total candies
    let total = 0;

    // Stores the count of maximum
    // consumable candies
    let ans = Number.MAX_VALUE;

    // Checks if it is safe
    // to counsume all candies
    let all_safe = true;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++)
    {

      // If A[i] + M is greater than B[i]
      if (candies[i] + M > safety[i])
      {

        // Mark all_safe as false
        all_safe = false;

        // Update ans
        ans = Math.min(ans, safety[i]);
      }
      else
      {

        // Update ans
        ans = Math.min(ans, candies[i] + M);
      }

      // Increment total by A[i]
      total += candies[i];
    }

    // If all_safe is true
    if (all_safe)
      return total;

    // Otherwise,
    else
      return ans;
  }

    // Driver Code

    let A = [ 4, 5, 2, 3 ];
    let B = [ 8, 13, 6, 4 ];
    let M = 5;

    let N = A.length;

    // Function call to find
    // maximum consumable candies
    document.write(maximumCandy(A, B, N, M));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)