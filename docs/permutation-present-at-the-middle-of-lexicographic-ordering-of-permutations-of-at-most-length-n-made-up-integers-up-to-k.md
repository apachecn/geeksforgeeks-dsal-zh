# 位于最多 N 个长度的排列的字典顺序中间的排列由 K 个整数组成

> 原文:[https://www . geeksforgeeks . org/排列-在字典中出现-排列-最多 n 个长度的排列-最多 k 个组成整数/](https://www.geeksforgeeks.org/permutation-present-at-the-middle-of-lexicographic-ordering-of-permutations-of-at-most-length-n-made-up-integers-up-to-k/)

给定两个正整数 **K** 和 **N** ，任务是找出最大长度 **N** 的所有排列中间的排列，由范围【1，K】的整数组成，按字典顺序排列。

**示例:**

> **输入:** K = 3，N = 2
> **输出:** 2 1
> **说明:**所有可能排列的字典顺序为:
> 
> 1.  {1}.
> 2.  {1, 1}
> 3.  {1, 2}
> 4.  {1, 3}
> 5.  {2}
> 6.  {2, 1}
> 7.  {2, 2}
> 8.  {2, 3}
> 9.  {3}
> 10.  {3, 1}
> 11.  {3, 2}
> 12.  {3, 3}
> 
> 因此，中间字典序最小的序列是(N/2) <sup>第</sup> (= 6 <sup>第</sup>序列，即{2，1}。
> 
> **输入:** K = 2，N = 4
> T3】输出:1 2 2 2 2

**天真方法:**解决给定问题的最简单方法是[生成长度为**【1，N】**的所有可能子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，由**【1，K】**的整数组成。将这些元素存储在数组中。生成所有子序列后，[对存储的子序列列表进行排序](https://www.geeksforgeeks.org/sorting-2d-vector-in-c-set-1-by-row-and-column/)并打印列表的中间元素。

***时间复杂度:**O(N<sup>K</sup>)*
***辅助空间:** O(N <sup>K</sup> )*

**高效法:**上述方法可以通过检查 **K** 的奇偶性 **K** 是**奇数**还是**偶数**来优化，然后相应地找到**中间的字典序最小序列**。按照以下步骤解决问题:

*   [如果 **K** 的值是**甚至**T5】，那么正好一半的序列以整数 **K/2** 或更少开始。因此，结果序列为 **K/2** 后接**(N–1)**出现 **K** 。](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)
*   [如果值 **K** 为**奇数**T5】，则认为 **B** 是包含 **(K + 1)/2** 的 **N** 次出现的序列。](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)
    *   对于一个序列 **X** ，让 **f(X)** 成为这样一个序列:将 **X** 中的**X<sub>I</sub>T7】替换为**(K+1 X<sub>I</sub>)**。**
    *   唯一的例外是 **B** 的前缀。
*   从顺序 **B** 开始，执行以下步骤**(N–1)/2**次:
    *   如果当前序列的最后一个元素是 **1** ，则将其移除。
    *   否则，将最后一个元素递减 **1** ，当序列包含的元素少于 **N** 时，在序列 **B** 的末尾插入 **K** 。
*   完成上述步骤后，打印数组 **B[]** 中获得的序列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that finds the middle the
// lexicographical smallest sequence
void lexiMiddleSmallest(int K, int N)
{
    // If K is even
    if (K % 2 == 0) {

        // First element is K/2
        cout << K / 2 << " ";

        // Remaining elements of the
        // sequence are all integer K
        for (int i = 0; i < N - 1; ++i) {
            cout << K << " ";
        }
        cout << "\n";
        exit(0);
    }

    // Stores the sequence when K
    // is odd
    vector<int> a(N, (K + 1) / 2);

    // Iterate over the range [0, N/2]
    for (int i = 0; i < N / 2; ++i) {

        // Check if the sequence ends
        // with in 1 or not
        if (a.back() == 1) {

            // Remove the sequence
            // ending in 1
            a.pop_back();
        }

        // If it doesn't end in 1
        else {

            // Decrement by 1
            --a.back();

            // Insert K to the sequence
            // till its size is N
            while ((int)a.size() < N) {
                a.push_back(K);
            }
        }
    }

    // Print the sequence stored
    // in the vector
    for (auto i : a) {
        cout << i << " ";
    }
    cout << "\n";
}

// Driver Code
int main()
{
    int K = 2, N = 4;
    lexiMiddleSmallest(K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function that finds the middle the
    // lexicographical smallest sequence
    static void lexiMiddleSmallest(int K, int N)
    {

        // If K is even
        if (K % 2 == 0) {

            // First element is K/2
            System.out.print(K / 2 + " ");

            // Remaining elements of the
            // sequence are all integer K
            for (int i = 0; i < N - 1; ++i) {
                System.out.print(K + " ");
            }
            System.out.println();
            return;
        }

        // Stores the sequence when K
        // is odd
        ArrayList<Integer> a = new ArrayList<Integer>();

        // Iterate over the range [0, N/2]
        for (int i = 0; i < N / 2; ++i) {

            // Check if the sequence ends
            // with in 1 or not
            if (a.get(a.size() - 1) == 1) {

                // Remove the sequence
                // ending in 1
                a.remove(a.size() - 1);
            }

            // If it doesn't end in 1
            else {

                // Decrement by 1
                int t = a.get(a.size() - 1) - 1;
                a.set(a.get(a.size() - 1), t);

                // Insert K to the sequence
                // till its size is N
                while (a.size() < N) {
                    a.add(K);
                }
            }
        }

        // Print the sequence stored
        // in the vector
        for (int i : a) {
            System.out.print(i + " ");
        }
        System.out.println();
    }

    // Driver Code
    public static void main(String[] args)
    {
        int K = 2, N = 4;
        lexiMiddleSmallest(K, N);
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the middle the
# lexicographical smallest sequence
def lexiMiddleSmallest(K, N):
    # If K is even
    if (K % 2 == 0):

        # First element is K/2
        print(K // 2,end=" ")

        # Remaining elements of the
        # sequence are all integer K
        for i in range(N - 1):
            print(K, end = " ")
        print()
        return

    # Stores the sequence when K
    # is odd
    a = [(K + 1) // 2]*(N)

    # Iterate over the range [0, N/2]
    for i in range(N//2):
        # Check if the sequence ends
        # with in 1 or not
        if (a[-1] == 1):

            # Remove the sequence
            # ending in 1
            del a[-1]

        # If it doesn't end in 1
        else:

            # Decrement by 1
            a[-1] -= 1

            # Insert K to the sequence
            # till its size is N
            while (len(a) < N):
                a.append(K)

    # Print sequence stored
    # in the vector
    for i in a:
        print(i, end = " ")
    print()

# Driver Code
if __name__ == '__main__':
    K, N = 2, 4
    lexiMiddleSmallest(K, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function that finds the middle the
    // lexicographical smallest sequence
    static void lexiMiddleSmallest(int K, int N)
    {
        // If K is even
        if (K % 2 == 0) {

            // First element is K/2
            Console.Write(K / 2 + " ");

            // Remaining elements of the
            // sequence are all integer K
            for (int i = 0; i < N - 1; ++i) {
                Console.Write(K + " ");
            }
            Console.WriteLine();
            return;
        }

        // Stores the sequence when K
        // is odd
        List<int> a = new List<int>();

        // Iterate over the range [0, N/2]
        for (int i = 0; i < N / 2; ++i) {

            // Check if the sequence ends
            // with in 1 or not
            if (a[a.Count - 1] == 1) {

                // Remove the sequence
                // ending in 1
                a.Remove(a.Count - 1);
            }

            // If it doesn't end in 1
            else {

                // Decrement by 1
                a[a.Count - 1] -= 1;

                // Insert K to the sequence
                // till its size is N
                while ((int)a.Count < N) {
                    a.Add(K);
                }
            }
        }

        // Print the sequence stored
        // in the vector
        foreach(int i in a) { Console.Write(i + " "); }
        Console.WriteLine();
    }

    // Driver Code
    public static void Main()
    {
        int K = 2, N = 4;
        lexiMiddleSmallest(K, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// javascript program for the above approach

    // Function that finds the middle the
    // lexicographical smallest sequence
    function lexiMiddleSmallest(K, N)
    {
        // If K is even
        if (K % 2 == 0) {

            // First element is K/2
            document.write(K / 2 + " ");

            // Remaining elements of the
            // sequence are all integer K
            for (let i = 0; i < N - 1; ++i) {
                document.write(K + " ");
            }
            document.write("<br/>");
            return;
        }

        // Stores the sequence when K
        // is odd
        let a = [];

        // Iterate over the range [0, N/2]
        for (let i = 0; i < N / 2; ++i) {

            // Check if the sequence ends
            // with in 1 or not
            if (a[a.length - 1] == 1) {

                // Remove the sequence
                // ending in 1
                a.pop(a.length - 1);
            }

            // If it doesn't end in 1
            else {

                // Decrement by 1
                a[a.length - 1] -= 1;

                // Insert K to the sequence
                // till its size is N
                while (a.length < N) {
                    a.push(K);
                }
            }
        }

        // Print the sequence stored
        // in the vector
        for(let i in a) { document.write(i + " "); }
        document.write("<br/>");
    }

// Driver Code

    let K = 2, N = 4;
    lexiMiddleSmallest(K, N);

</script>
```

**Output:** 

```
1 2 2 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)