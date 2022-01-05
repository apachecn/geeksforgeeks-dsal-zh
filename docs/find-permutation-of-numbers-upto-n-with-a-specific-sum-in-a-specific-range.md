# 在特定的范围内找到具有特定和的数的排列

> 原文:[https://www . geesforgeks . org/find-数字排列-up-n-with-specific-sum-in-specific-range/](https://www.geeksforgeeks.org/find-permutation-of-numbers-upto-n-with-a-specific-sum-in-a-specific-range/)

给定四个数字 **N** 、 **L** 、 **R** 和 **S** ，任务是找到第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)(基于 1 的索引)的排列，从索引 **L** 到 **R** 的和为 **S** 。如果有多个排列，那么打印其中任何一个。否则，打印 **-1** 。

**示例:**

> ***输入:** N = 6，L = 3，R = 5，S = 8*
> ***输出:** 3 4 5 2 1 6*
> ***说明:**输出排列在索引 L 处有 5，在索引 R 处有 1，从 L 到 R 的数字之和为 8(5+2+1)。*
> 
> ***输入:** N = 4，L = 2，R = 3，S = 2*
> ***输出:** -1*
> ***说明:**不存在从索引 L 到 R 的数之和为 S 的排列*

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，该方法基于这样的观察，即假设 **X** 个数字必须从第一个**N**T8】个自然数的排列中选择，因此使和为 **S** ，让 **X** 个数字的最小和最大和分别为 **minSum** 和 **maxSum** ，然后:

> *X = R–L+1*
> *minSum = X(X+1)/2*
> *maxSum = X(2 * N+1–X)/2*

因此，如果给定的和 **S** 位于范围**【明苏姆，maxSum】**内，则存在一种排列，使得从 **L** 到 **R** 的所有数字的和为 **S** 。否则，不存在任何这样的排列。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **可能(int x，int S，int N)** 并执行以下任务:
    *   将变量 **minSum** 初始化为 **x*(x + 1)/2** 并将 **maxSum** 初始化为**(x *(2 * N)–x+1)/2**。
    *   如果 **S** 小于**民数**或 **S** 大于 **maxSum** ，则返回 **false** 。否则，返回**真**。
*   初始化变量，说 **x** 为**(R–L+1)**。
*   如果函数 **返回的[值可能(x，S，N)](https://www.geeksforgeeks.org/c-function-argument-return-values/)** 返回**假，**则打印 **-1** 和[从函数](https://www.geeksforgeeks.org/return-statement-in-c-cpp-with-examples/)返回。
*   否则，[初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **v[]** 来存储给定段中出现的数字。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N，1】**，并执行以下任务:
    *   如果**S–I**大于或等于 **0** 且函数**可能(x–1，S–I，I–1)**返回**真**，则将 **S** 设置为**(S–I)**将 **x** 的值减少 **1** ，[将 **i** 的值推入矢量](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)
    *   **如果 **S** 等于 **0** ，则[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。**
*   **如果 **S** 不等于 **0** ，则打印 **-1** 并返回。**
*   **初始化一个向量，比如 **v1[]** 来存储给定段中不存在的数字。**
*   **使用变量 **i** 和[迭代范围**【1，N】**初始化向量迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)**和[使用 find()](https://www.geeksforgeeks.org/std-find-in-cpp/) 检查元素 **i** 是否存在于向量**v【】**中。如果不存在，则将其推入向量 **v1** 。****
*   ****将变量 **j** 和 **f** 初始化为 **0** 打印结果。****
*   ****使用变量 **i** 迭代范围**【1，L】**，打印**v1【j】**的值，将 **j** 的值增加 **1** 。****
*   ****使用变量 **i** 迭代范围**【L，R】**，打印**v【f】**的值，将 **f** 的值增加 **1** 。****
*   ****使用变量 **i** 迭代范围**【R+1，N】**，打印**v1【j】**的值，将 **j** 的值增加 **1** 。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if sum is possible
// with remaining numbers
bool possible(int x, int S, int N)
{

    // Stores the minimum sum possible with
    // x numbers
    int minSum = (x * (x + 1)) / 2;

    // Stores the maximum sum possible with
    // x numbers
    int maxSum = (x * ((2 * N) - x + 1)) / 2;

    // If S lies in the range
    // [minSum, maxSum]
    if (S < minSum || S > maxSum) {
        return false;
    }
    return true;
}

// Function to find the resultant
// permutation
void findPermutation(int N, int L,
                     int R, int S)
{

    // Stores the count of numbers
    // in the given segment
    int x = R - L + 1;

    // If the sum is not possible
    // with numbers in the segment
    if (!possible(x, S, N)) {

        // Output -1
        cout << -1;
        return;
    }
    else {

        // Stores the numbers present
        // within the given segment
        vector<int> v;

        // Iterate over the numbers from
        // 1 to N
        for (int i = N; i >= 1; --i) {

            // If (S-i) is a positive non-zero
            // sum and if it is possible to
            // obtain (S-i) remaining numbers
            if ((S - i) >= 0
                && possible(x - 1, S - i,
                            i - 1)) {

                // Update sum S
                S = S - i;

                // Update required numbers
                // in the segement
                x--;

                // Push i in vector v
                v.push_back(i);
            }

            // If sum has been obtained
            if (S == 0) {

                // Break from the loop
                break;
            }
        }

        // If sum is not obtained
        if (S != 0) {

            // Output -1
            cout << -1;
            return;
        }

        // Stores the numbers which are
        // not present in given segment
        vector<int> v1;

        // Loop to check the numbers not
        // present in the segment
        for (int i = 1; i <= N; ++i) {

            // Pointer to check if i is
            // present in vector v or not
            vector<int>::iterator it
                = find(v.begin(), v.end(), i);

            // If i is not present in v
            if (it == v.end()) {

                // Push i in vector v1
                v1.push_back(i);
            }
        }

        // Point to the first elements
        // of v1 and v respectively
        int j = 0, f = 0;

        // Print the required permutation
        for (int i = 1; i < L; ++i) {
            cout << v1[j] << " ";
            j++;
        }
        for (int i = L; i <= R; ++i) {
            cout << v[f] << " ";
            f++;
        }
        for (int i = R + 1; i <= N; ++i) {
            cout << v1[j] << " ";
            j++;
        }
    }

    return;
}

// Driver Code
int main()
{
    int N = 6, L = 3, R = 5, S = 8;
    findPermutation(N, L, R, S);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**import java.util.ArrayList;

// Java program for the above approach

class GFG{

// Function to check if sum is possible
// with remaining numbers
public static boolean possible(int x, int S, int N)
{

    // Stores the minimum sum possible with
    // x numbers
    int minSum = (x * (x + 1)) / 2;

    // Stores the maximum sum possible with
    // x numbers
    int maxSum = (x * ((2 * N) - x + 1)) / 2;

    // If S lies in the range
    // [minSum, maxSum]
    if (S < minSum || S > maxSum) {
        return false;
    }
    return true;
}

// Function to find the resultant
// permutation
public static void findPermutation(int N, int L,
                     int R, int S)
{

    // Stores the count of numbers
    // in the given segment
    int x = R - L + 1;

    // If the sum is not possible
    // with numbers in the segment
    if (!possible(x, S, N)) {

        // Output -1
        System.out.print(-1);
        return;
    }
    else {

        // Stores the numbers present
        // within the given segment
        ArrayList<Integer> v = new ArrayList<>();

        // Iterate over the numbers from
        // 1 to N
        for (int i = N; i >= 1; --i) {

            // If (S-i) is a positive non-zero
            // sum and if it is possible to
            // obtain (S-i) remaining numbers
            if ((S - i) >= 0
                && possible(x - 1, S - i,
                            i - 1)) {

                // Update sum S
                S = S - i;

                // Update required numbers
                // in the segement
                x--;

                // Push i in vector v
                v.add(i);
            }

            // If sum has been obtained
            if (S == 0) {

                // Break from the loop
                break;
            }
        }

        // If sum is not obtained
        if (S != 0) {

            // Output -1
            System.out.print(-1);
            return;
        }

        // Stores the numbers which are
        // not present in given segment
        ArrayList<Integer> v1 = new ArrayList<Integer>();

        // Loop to check the numbers not
        // present in the segment
        for (int i = 1; i <= N; ++i) {

            // Pointer to check if i is
            // present in vector v or not
            boolean it = v.contains(i);

            // If i is not present in v
            if (!it) {

                // Push i in vector v1
                v1.add(i);
            }
        }

        // Point to the first elements
        // of v1 and v respectively
        int j = 0, f = 0;

        // Print the required permutation
        for (int i = 1; i < L; ++i) {
            System.out.print(v1.get(j) + " ");
            j++;
        }
        for (int i = L; i <= R; ++i) {
            System.out.print(v.get(f) + " ");
            f++;
        }
        for (int i = R + 1; i <= N; ++i) {
            System.out.print(v1.get(j) + " ");
            j++;
        }
    }

    return;
}

// Driver Code
public static void main(String args[])
{
    int N = 6, L = 3, R = 5, S = 8;
    findPermutation(N, L, R, S);

}
}

// This code is contributed by saurabh_jaiswal.**
```

## ****蟒蛇 3****

```
**# python program for the above approach

#  Function to check if sum is possible
#  with remaining numbers
def possible(x,  S,  N):

        #  Stores the minimum sum possible with
        #  x numbers
    minSum = (x * (x + 1)) // 2

    # Stores the maximum sum possible with
    # x numbers
    maxSum = (x * ((2 * N) - x + 1)) // 2

    # If S lies in the range
    # [minSum, maxSum]
    if (S < minSum or S > maxSum):
        return False

    return True

#  Function to find the resultant
#  permutation
def findPermutation(N,  L, R,  S):

        # Stores the count of numbers
        # in the given segment
    x = R - L + 1

    # If the sum is not possible
    # with numbers in the segment
    if (not possible(x, S, N)):

                # Output -1
        print("-1")
        return

    else:

       # Stores the numbers present
       # within the given segment
        v = []

        # Iterate over the numbers from
        # 1 to N
        for i in range(N, 0, -1):

            # If (S-i) is a positive non-zero
            # sum and if it is possible to
            # obtain (S-i) remaining numbers
            if ((S - i) >= 0 and possible(x - 1, S - i, i - 1)):

                # Update sum S
                S = S - i

                # Update required numbers
                # in the segement
                x -= 1

                # Push i in vector v
                v.append(i)

                # If sum has been obtained
            if (S == 0):

                                # Break from the loop
                break

        # If sum is not obtained
        if (S != 0):

            # Output -1
            print(-1)
            return

        # Stores the numbers which are
        # not present in given segment
        v1 = []

        # Loop to check the numbers not
        # present in the segment
        for i in range(1, N+1):

            # Pointer to check if i is
            # present in vector v or not
            it = i in v

            # If i is not present in v
            if (not it):

                # Push i in vector v1
                v1.append(i)

        # Point to the first elements
        # of v1 and v respectively
        j = 0
        f = 0

        # Print the required permutation
        for i in range(1, L):
            print(v1[j], end = " ")
            j += 1

        for i in range(L, R + 1):
            print(v[f], end = " ")
            f += 1

        for i in range(R + 1, N + 1):
            print(v1[j], end = " ")
            j += 1

    return

# Driver Code
if __name__ == "__main__":
    N = 6
    L = 3
    R = 5
    S = 8
    findPermutation(N, L, R, S)

    # This code is contributed by rakeshsahni**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to check if sum is possible
    // with remaining numbers
    public static bool possible(int x, int S, int N)
    {

        // Stores the minimum sum possible with
        // x numbers
        int minSum = (x * (x + 1)) / 2;

        // Stores the maximum sum possible with
        // x numbers
        int maxSum = (x * ((2 * N) - x + 1)) / 2;

        // If S lies in the range
        // [minSum, maxSum]
        if (S < minSum || S > maxSum) {
            return false;
        }
        return true;
    }

    // Function to find the resultant
    // permutation
    public static void findPermutation(int N, int L, int R,
                                       int S)
    {

        // Stores the count of numbers
        // in the given segment
        int x = R - L + 1;

        // If the sum is not possible
        // with numbers in the segment
        if (!possible(x, S, N)) {

            // Output -1
            Console.WriteLine(-1);
            return;
        }
        else {

            // Stores the numbers present
            // within the given segment
            List<int> v = new List<int>();

            // Iterate over the numbers from
            // 1 to N
            for (int i = N; i >= 1; --i) {

                // If (S-i) is a positive non-zero
                // sum and if it is possible to
                // obtain (S-i) remaining numbers
                if ((S - i) >= 0
                    && possible(x - 1, S - i, i - 1)) {

                    // Update sum S
                    S = S - i;

                    // Update required numbers
                    // in the segement
                    x--;

                    // Push i in vector v
                    v.Add(i);
                }

                // If sum has been obtained
                if (S == 0) {

                    // Break from the loop
                    break;
                }
            }

            // If sum is not obtained
            if (S != 0) {

                // Output -1
                Console.WriteLine(-1);
                return;
            }

            // Stores the numbers which are
            // not present in given segment
            List<int> v1 = new List<int>();

            // Loop to check the numbers not
            // present in the segment
            for (int i = 1; i <= N; ++i) {

                // Pointer to check if i is
                // present in vector v or not
                bool it = v.Contains(i);

                // If i is not present in v
                if (!it) {

                    // Push i in vector v1
                    v1.Add(i);
                }
            }

            // Point to the first elements
            // of v1 and v respectively
            int j = 0, f = 0;

            // Print the required permutation
            for (int i = 1; i < L; ++i) {
                Console.Write(v1[j] + " ");
                j++;
            }
            for (int i = L; i <= R; ++i) {
                Console.Write(v[f] + " ");
                f++;
            }
            for (int i = R + 1; i <= N; ++i) {
                Console.Write(v1[j] + " ");
                j++;
            }
        }

        return;
    }

    // Driver Code
    public static void Main()
    {
        int N = 6, L = 3, R = 5, S = 8;
        findPermutation(N, L, R, S);
    }
}

// This code is contributed by ukasp.**
```

## ****java 描述语言****

```
**<script>
// Javascript program for the above approach

// Function to check if sum is possible
// with remaining numbers
function possible(x, S, N) {
  // Stores the minimum sum possible with
  // x numbers
  let minSum = (x * (x + 1)) / 2;

  // Stores the maximum sum possible with
  // x numbers
  let maxSum = (x * (2 * N - x + 1)) / 2;

  // If S lies in the range
  // [minSum, maxSum]
  if (S < minSum || S > maxSum) {
    return false;
  }
  return true;
}

// Function to find the resultant
// permutation
function findPermutation(N, L, R, S) {
  // Stores the count of numbers
  // in the given segment
  let x = R - L + 1;

  // If the sum is not possible
  // with numbers in the segment
  if (!possible(x, S, N)) {
    // Output -1
    document.write(-1);
    return;
  } else {
    // Stores the numbers present
    // within the given segment
    let v = [];

    // Iterate over the numbers from
    // 1 to N
    for (let i = N; i >= 1; --i) {
      // If (S-i) is a positive non-zero
      // sum and if it is possible to
      // obtain (S-i) remaining numbers
      if (S - i >= 0 && possible(x - 1, S - i, i - 1)) {
        // Update sum S
        S = S - i;

        // Update required numbers
        // in the segement
        x--;

        // Push i in vector v
        v.push(i);
      }

      // If sum has been obtained
      if (S == 0) {
        // Break from the loop
        break;
      }
    }

    // If sum is not obtained
    if (S != 0) {
      // Output -1
      document.write(-1);
      return;
    }

    // Stores the numbers which are
    // not present in given segment
    let v1 = [];

    // Loop to check the numbers not
    // present in the segment
    for (let i = 1; i <= N; ++i) {
      // Pointer to check if i is
      // present in vector v or not
      it = v.includes(i);

      // If i is not present in v
      if (!it) {
        // Push i in vector v1
        v1.push(i);
      }
    }

    // Point to the first elements
    // of v1 and v respectively
    let j = 0,
      f = 0;

    // Print the required permutation
    for (let i = 1; i < L; ++i) {
      document.write(v1[j] + " ");
      j++;
    }
    for (let i = L; i <= R; ++i) {
      document.write(v[f] + " ");
      f++;
    }
    for (let i = R + 1; i <= N; ++i) {
      document.write(v1[j] + " ");
      j++;
    }
  }

  return;
}

// Driver Code

let N = 6,
  L = 3,
  R = 5,
  S = 8;
findPermutation(N, L, R, S);

// This code is contributed by saurabh_jaiswal.
</script>**
```

******Output:** 

```
3 4 5 2 1 6
```**** 

*******时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*****