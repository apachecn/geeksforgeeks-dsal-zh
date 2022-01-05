# 数组中每个无序对的成对和的异或

> 原文:[https://www . geesforgeks . org/每对无序数组对的异或运算/](https://www.geeksforgeeks.org/xor-of-pairwise-sum-of-every-unordered-pairs-in-an-array/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找到数组中每个可能的[无序对](https://en.wikipedia.org/wiki/Unordered_pair)的成对和的[异或](https://en.wikipedia.org/wiki/Exclusive_or)。无序对和定义如下–

```
XOR of pairwise sum  = (A[0] + A[1]) ^
    (A[0] + A[2]) ^ ...(A[0] + A[N]) ^
    (A[1] + A[2]) ^ ...(A[1] + A[N]) ^
    .......
    (A[N-1] + A[N])

Notice that after including A[0] and A[1] 
as pairs, then A[1] and A[0] are not included.
```

**例:**

> **输入:** arr[] = {1，2}
> **输出:** 3
> **说明:**
> 只有一个无序对。也就是(1，2)
> **输入:** arr[] = {1，2，3}
> **输出:** 2
> **解释:**
> 无序对的数字–
> {(1，2)、(1，3)、(2，3)}
> 无序对的异或运算–
> =>(1+2)^(1+3)^(2+3)

**天真方法:**想法是借助两个[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)找到每一个可能的无序对，并找到这些对的异或。
以下是上述方法的实施:

## C++

```
// C++ implementation to find XOR of
// pairwise sum of every unordered
// pairs in an array

#include <bits/stdc++.h>

using namespace std;

// Function to find XOR of pairwise
// sum of every unordered pairs
int xorOfSum(int a[], int n)
{
    int answer = 0;

    // Loop to choose every possible
    // pairs in the array
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++)
            answer ^= (a[i] + a[j]);
    }

    return answer;
}

// Driver Code
int main()
{
    int n = 3;
    int A[n] = { 1, 2, 3 };

    cout << xorOfSum(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find XOR of
// pairwise sum of every unordered
// pairs in an array
class GFG{

// Function to find XOR of pairwise
// sum of every unordered pairs
static int xorOfSum(int a[], int n)
{
    int answer = 0;

    // Loop to choose every possible
    // pairs in the array
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++)
            answer ^= (a[i] + a[j]);
    }

    return answer;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3;
    int A[] = { 1, 2, 3 };

    System.out.print(xorOfSum(A, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to find XOR of
# pairwise sum of every unordered
# pairs in an array

# Function to find XOR of pairwise
# sum of every unordered pairs
def xorOfSum(a, n):
    answer = 0

    # Loop to choose every possible
    # pairs in the array
    for i in range(n):
        for j in range(i + 1, n):
            answer ^= (a[i] + a[j])

    return answer

# Driver Code
if __name__ == '__main__':
    n = 3
    A=[1, 2, 3]

    print(xorOfSum(A, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find XOR of
// pairwise sum of every unordered
// pairs in an array
using System;
using System.Collections.Generic;

class GFG{

// Function to find XOR of pairwise
// sum of every unordered pairs
static int xorOfSum(int []a, int n)
{
    int answer = 0;

    // Loop to choose every possible
    // pairs in the array
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++)
            answer ^= (a[i] + a[j]);
    }

    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 3;
    int []A = { 1, 2, 3 };

    Console.Write(xorOfSum(A, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// JavaScript implementation to find XOR of
// pairwise sum of every unordered
// pairs in an array

// Function to find XOR of pairwise
// sum of every unordered pairs
function xorOfSum(a, n)
{
    let answer = 0;

    // Loop to choose every possible
    // pairs in the array
    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++)
            answer ^= (a[i] + a[j]);
    }

    return answer;
}

// Driver Code
    let n = 3;
    let A = [ 1, 2, 3 ];

    document.write(xorOfSum(A, n));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
2
```

**高效方法:**

*   为了获得我们在所有对和中看到的最终异或值的第 K <sup>位，它们的第 k <sup>位</sup>被置位或未被置位。如果甚至有许多对设置了第 K <sup>位</sup>位，那么对于第 K <sup>位</sup>位，它们的异或是零。</sup> 
*   为了找到设置了第 K<sup>位的对和的计数，我们注意到我们可以通过 2 <sup>(K+1)</sup> 来修改所有数组元素。这是因为 X 和 Y 属于输入数组，**和= X + Y** 。然后 X + Y 相加可以设置它们的 K <sup>第</sup>位，这意味着 Sum > = 2 <sup>K</sup> 。还可以观察到，它们可以有加法的遗留，这使得范围[2 <sup>(K+1)</sup> 、2 <sup>(K+1)</sup> + 2 <sup>K</sup> )中的数字的 K <sup>第</sup>位未置位。所以我们只关心所有数字的第 K <sup>位</sup>和第(K+1) <sup>位</sup>来检查第 K <sup>位</sup>位的异或。</sup> 
*   执行 mod 操作后，对于设置了 kth 位的 sum，其值将在范围–[ 2<sup>K</sup>、2<sup>(K+1)</sup>)U[2<sup>(K+1)</sup>+2<sup>K</sup>、最大值-Sum-Can-Take ]内。

*   要找到上述范围内的数字，制作另一个包含 arr[]的修改数组元素的数组 B，并对它们进行排序。那么 Sum 可以假设为 Sum = B <sub>i</sub> + B <sub>j</sub> 。最后用二分搜索法求 j 的最大界(C++内置[下界](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/))。修复 I，因为数组是排序的，所以找到满足给定条件的最后一个 j，并且索引范围内的所有数字都可以添加到计数中以检查 xor。

**辅助空间:** O(1)
下面是上述方法的实现:

## C++

```
// C++ implementation to find XOR of
// pairwise sum of every unordered
// pairs in an array

#include <bits/stdc++.h>

using namespace std;

// Function to find XOR of pairwise
// sum of every unordered pairs
int xorOfSum(int a[], int n)
{

    int i, j, k;

    // Sort the array
    sort(a, a + n);

    int ans = 0;

    // Array elements are not greater
    // than 1e7 so 27 bits are suffice
    for (k = 0; k < 27; ++k) {

        // Modded elements of array
        vector<int> b(n);

        // Loop to find the modded
        // elements of array
        for (i = 0; i < n; i++)
            b[i] = a[i] % (1 << (k + 1));

        // Sort the modded array
        sort(b.begin(), b.end());

        int cnt = 0;
        for (i = 0; i < n; i++) {
            // finding the bound for j
            // for given i using binary search
            int l = lower_bound(b.begin() +
                           i + 1, b.end(),
               (1 << k) - b[i]) - b.begin();
            int r = lower_bound(b.begin() +
                    i + 1, b.end(), (1 << (k + 1)) -
                          b[i]) - b.begin();

            // All the numbers in the range
            // of indices can be added to the
            // count to check the xor.
            cnt += r - l;

            l = lower_bound(b.begin() + i + 1,
                 b.end(), (1 << (k + 1)) +
                 (1 << k) - b[i]) - b.begin();
            cnt += n - l;
        }
        // Remainder of cnt * kth power
        // of 2 added to the xor value
        ans += (cnt % 2) * 1LL * (1 << k);
    }

    return ans;
}

// Driver Code
int main()
{
    int n = 3;
    int A[n] = { 1, 2, 3 };

    cout << xorOfSum(A, n);
    return 0;
}
```

**Output:** 

```
2
```

**业绩分析:**

*   **时间复杂度:** O(N * log(max(A))*log(N)
*   **辅助空间:** O(N)

最外面的循环运行 log(max(A))次，对于每个循环，我们创建并排序数组 b，数组 b 由 **N** 个元素组成，因此复杂性为**O(N * log(N)* log(max(A)))**