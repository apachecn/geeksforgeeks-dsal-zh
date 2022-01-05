# 两个数组中任意两个元素乘积形成的数组中的第 k 个最小数

> 原文:[https://www . geeksforgeeks . org/kth-数组中的最小数字由两个数组中的任意两个元素的乘积形成/](https://www.geeksforgeeks.org/kth-smallest-number-in-array-formed-by-product-of-any-two-elements-from-two-arrays/)

给定两个排序的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**分别由 **N** 和 **M** 整数组成，任务是分别从数组**A【】**和**B【】**中找出所有可能对的乘积构成的数组中的 **K <sup>th</sup>** 最小数。

**示例:**

> **输入:** A[] = {1，2，3}，B[] = {-1，1}，K = 4
> **输出:** 1
> **说明:**数组 A[]和 B[]中任意两个数分别乘积形成的数组为 prod[] = {-3，-2，-1，1，2，3}。因此，prod[]数组中的第四个最小整数是 1。
> 
> **输入:** A[] = {-4，-2，0，3}，B[] = {1，10}，K = 7
> T3】输出: 3

**方法:**给定的问题可以借助[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在所有可能的产品价值上解决。这里讨论的方法与本文中讨论的方法非常相似。以下是要遵循的步骤:

*   创建[函数](https://www.geeksforgeeks.org/functions-in-c/) **检查(键)**，返回产品数组中小于键的元素个数是否大于 **K** 。这可以使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)来完成，类似于本文[中讨论的算法](https://www.geeksforgeeks.org/count-pairs-in-a-sorted-array-whose-product-is-less-than-k/)。
*   在范围**【INT _ MIN，INT _ MAX】**上执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)以找到最小的数 **ans** ，使得产品数组中小于 **ans** 的元素数至少为 **K** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define int long long

// Function to check if count of elements
// greater than req in product array are
// more than K or not
bool check(int req, vector<int> posA,
           vector<int> posB, vector<int> negA,
           vector<int> negB, int K)
{
    // Stores the count of numbers less
    // than or equal to req
    int cnt = 0;

    // Case with both elements of A[] and
    // B[] are negative
    int first = 0;
    int second = negB.size() - 1;

    // Count number of pairs formed from
    // array A[] and B[] with both elements
    // negative and there product <= req
    while (first < negA.size()) {
        while (second >= 0
               && negA[first]
                          * negB[second]
                      <= req)
            second--;

        // Update cnt
        cnt += negB.size() - second - 1;
        first++;
    }

    // Case with both elements of A[] and
    // B[] are positive
    first = 0;
    second = posB.size() - 1;

    // Count number of pairs formed from
    // array A[] and B[] with both elements
    // positive and there product <= req
    while (first < posA.size()) {
        while (second >= 0
               && posA[first]
                          * posB[second]
                      > req)
            second--;

        // Update cnt
        cnt += second + 1;
        first++;
    }

    // Case with elements of A[] and B[]
    // as positive and negative respectively
    first = posA.size() - 1;
    second = negB.size() - 1;

    // Count number of pairs formed from
    // +ve integers of A[] and -ve integer
    // of array B[] product <= req
    while (second >= 0) {
        while (first >= 0
               && posA[first]
                          * negB[second]
                      <= req)
            first--;

        // Update cnt
        cnt += posA.size() - first - 1;
        second--;
    }

    // Case with elements of A[] and B[]
    // as negative and positive respectively
    first = negA.size() - 1;
    second = posB.size() - 1;

    // Count number of pairs formed from
    // -ve and +ve integers from A[] and
    // B[] with product <= req
    for (; first >= 0; first--) {
        while (second >= 0
               && negA[first]
                          * posB[second]
                      <= req)
            second--;

        // Update cnt
        cnt += posB.size() - second - 1;
    }

    // Return Answer
    return (cnt >= K);
}

// Function to find the Kth smallest
// number in array formed by product of
// any two elements from A[] and B[]
int kthSmallestProduct(vector<int>& A,
                       vector<int>& B,
                       int K)
{
    vector<int> posA, negA, posB, negB;

    // Loop to iterate array A[]
    for (const auto& it : A) {
        if (it >= 0)
            posA.push_back(it);
        else
            negA.push_back(it);
    }

    // Loop to iterate array B[]
    for (const auto& it : B)
        if (it >= 0)
            posB.push_back(it);
        else
            negB.push_back(it);

    // Stores the lower and upper bounds
    // of the binary search
    int l = LLONG_MIN, r = LLONG_MAX;

    // Stores the final answer
    int ans;

    // Find the kth smallest integer
    // using binary search
    while (l <= r) {

        // Stores the mid
        int mid = (l + r) / 2;

        // If the number of elements
        // greater than mid in product
        // array are more than K
        if (check(mid, posA, posB,
                  negA, negB, K)) {
            ans = mid;
            r = mid - 1;
        }
        else {
            l = mid + 1;
        }
    }

    // Return answer
    return ans;
}

// Driver Code
int32_t main()
{
    vector<int> A = { -4, -2, 0, 3 };
    vector<int> B = { 1, 10 };
    int K = 7;

    cout << kthSmallestProduct(A, B, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if count of elements
// greater than req in product array are
// more than K or not
static boolean check(int req, Vector<Integer> posA,
           Vector<Integer> posB, Vector<Integer> negA,
           Vector<Integer> negB, int K)
{

    // Stores the count of numbers less
    // than or equal to req
    int cnt = 0;

    // Case with both elements of A[] and
    // B[] are negative
    int first = 0;
    int second = negB.size() - 1;

    // Count number of pairs formed from
    // array A[] and B[] with both elements
    // negative and there product <= req
    while (first < negA.size()) {
        while (second >= 0
               && negA.elementAt(first)
                          * negB.elementAt(second)
                      <= req)
            second--;

        // Update cnt
        cnt += negB.size() - second - 1;
        first++;
    }

    // Case with both elements of A[] and
    // B[] are positive
    first = 0;
    second = posB.size() - 1;

    // Count number of pairs formed from
    // array A[] and B[] with both elements
    // positive and there product <= req
    while (first < posA.size()) {
        while (second >= 0
               && posA.elementAt(first)
                          * posB.elementAt(second)
                      > req)
            second--;

        // Update cnt
        cnt += second + 1;
        first++;
    }

    // Case with elements of A[] and B[]
    // as positive and negative respectively
    first = posA.size() - 1;
    second = negB.size() - 1;

    // Count number of pairs formed from
    // +ve integers of A[] and -ve integer
    // of array B[] product <= req
    while (second >= 0) {
        while (first >= 0
               && posA.elementAt(first)
                          * negB.elementAt(second)
                      <= req)
            first--;

        // Update cnt
        cnt += posA.size() - first - 1;
        second--;
    }

    // Case with elements of A[] and B[]
    // as negative and positive respectively
    first = negA.size() - 1;
    second = posB.size() - 1;

    // Count number of pairs formed from
    // -ve and +ve integers from A[] and
    // B[] with product <= req
    for (; first >= 0; first--) {
        while (second >= 0
               && negA.elementAt(first)
                          * posB.elementAt(second)
                      <= req)
            second--;

        // Update cnt
        cnt += posB.size() - second - 1;
    }

    // Return Answer
    return (cnt >= K);
}

// Function to find the Kth smallest
// number in array formed by product of
// any two elements from A[] and B[]
static int kthSmallestProduct(int[] A,
                       int[] B,
                       int K)
{
    Vector<Integer> posA = new Vector<>();
    Vector<Integer> negA = new Vector<>();
    Vector<Integer> posB = new Vector<>();
    Vector<Integer> negB = new Vector<>();
    // Loop to iterate array A[]
    for (int  it : A) {
        if (it >= 0)
            posA.add(it);
        else
            negA.add(it);
    }

    // Loop to iterate array B[]
    for (int it : B)
        if (it >= 0)
            posB.add(it);
        else
            negB.add(it);

    // Stores the lower and upper bounds
    // of the binary search
    int l = Integer.MIN_VALUE, r = Integer.MAX_VALUE;

    // Stores the final answer
    int ans=0;

    // Find the kth smallest integer
    // using binary search
    while (l <= r) {

        // Stores the mid
        int mid = (l + r) / 2;

        // If the number of elements
        // greater than mid in product
        // array are more than K
        if (check(mid, posA, posB,
                  negA, negB, K)) {
            ans = mid;
            r = mid - 1;
        }
        else {
            l = mid + 1;
        }
    }

    // Return answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
   int[] A = { -4, -2, 0, 3 };
    int[] B = { 1, 10 };
    int K = 7;

    System.out.print(kthSmallestProduct(A, B, K));

}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# python program for the above approach
LLONG_MAX = 9223372036854775807
LLONG_MIN = -9223372036854775807

# Function to check if count of elements
# greater than req in product array are
# more than K or not
def check(req, posA, posB, negA, negB, K):

    # Stores the count of numbers less
    # than or equal to req
    cnt = 0

    # Case with both elements of A[] and
    # B[] are negative
    first = 0
    second = len(negB) - 1

    # Count number of pairs formed from
    # array A[] and B[] with both elements
    # negative and there product <= req
    while (first < len(negA)):
        while (second >= 0 and negA[first] * negB[second] <= req):
            second -= 1

        # Update cnt
        cnt += len(negB) - second - 1
        first += 1

    # Case with both elements of A[] and
    # B[] are positive
    first = 0
    second = len(posB) - 1

    # Count number of pairs formed from
    # array A[] and B[] with both elements
    # positive and there product <= req
    while (first < len(posA)):
        while (second >= 0 and posA[first] * posB[second] > req):
            second -= 1

        # Update cnt
        cnt += second + 1
        first += 1

    # Case with elements of A[] and B[]
    # as positive and negative respectively
    first = len(posA) - 1
    second = len(negB) - 1

    # Count number of pairs formed from
    # +ve integers of A[] and -ve integer
    # of array B[] product <= req
    while (second >= 0):
        while (first >= 0 and posA[first] * negB[second] <= req):
            first -= 1

        # Update cnt
        cnt += len(posA) - first - 1
        second -= 1

    # Case with elements of A[] and B[]
    # as negative and positive respectively
    first = len(negA) - 1
    second = len(posB) - 1

    # Count number of pairs formed from
    # -ve and +ve integers from A[] and
    # B[] with product <= req
    for first in range(first, -1, -1):
        while (second >= 0 and negA[first] * posB[second] <= req):
            second -= 1

        # Update cnt
        cnt += len(posB) - second - 1

    # Return Answer
    return (cnt >= K)

# Function to find the Kth smallest
# number in array formed by product of
# any two elements from A[] and B[]
def kthSmallestProduct(A, B, K):

    posA = []
    negA = []
    posB = []
    negB = []

    # Loop to iterate array A[]
    for it in A:
        if (it >= 0):
            posA.append(it)
        else:
            negA.append(it)

        # Loop to iterate array B[]
    for it in B:
        if (it >= 0):
            posB.append(it)
        else:
            negB.append(it)

        # Stores the lower and upper bounds
        # of the binary search
    l = LLONG_MIN
    r = LLONG_MAX

    # Stores the final answer
    ans = 0

    # Find the kth smallest integer
    # using binary search
    while (l <= r):

        # Stores the mid
        mid = (l + r) // 2

        # If the number of elements
        # greater than mid in product
        # array are more than K
        if (check(mid, posA, posB, negA, negB, K)):
            ans = mid
            r = mid - 1
        else:
            l = mid + 1

        # Return answer
    return ans

# Driver Code
if __name__ == "__main__":

    A = [-4, -2, 0, 3]
    B = [1, 10]
    K = 7

    print(kthSmallestProduct(A, B, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to check if count of elements
    // greater than req in product array are
    // more than K or not
    static bool check(int req, List<int> posA, List<int> posB, List<int> negA,
            List<int> negB, int K) {

        // Stores the count of numbers less
        // than or equal to req
        int cnt = 0;

        // Case with both elements of []A and
        // []B are negative
        int first = 0;
        int second = negB.Count - 1;

        // Count number of pairs formed from
        // array []A and []B with both elements
        // negative and there product <= req
        while (first < negA.Count) {
            while (second >= 0 && negA[first]
                          * negB[second] <= req)
                second--;

            // Update cnt
            cnt += negB.Count - second - 1;
            first++;
        }

        // Case with both elements of []A and
        // []B are positive
        first = 0;
        second = posB.Count - 1;

        // Count number of pairs formed from
        // array []A and []B with both elements
        // positive and there product <= req
        while (first < posA.Count) {
            while (second >= 0 && posA[first] * posB[second] > req)
                second--;

            // Update cnt
            cnt += second + 1;
            first++;
        }

        // Case with elements of []A and []B
        // as positive and negative respectively
        first = posA.Count - 1;
        second = negB.Count - 1;

        // Count number of pairs formed from
        // +ve integers of []A and -ve integer
        // of array []B product <= req
        while (second >= 0) {
            while (first >= 0 && posA[first] * negB[second] <= req)
                first--;

            // Update cnt
            cnt += posA.Count - first - 1;
            second--;
        }

        // Case with elements of []A and []B
        // as negative and positive respectively
        first = negA.Count - 1;
        second = posB.Count - 1;

        // Count number of pairs formed from
        // -ve and +ve integers from []A and
        // []B with product <= req
        for (; first >= 0; first--) {
            while (second >= 0 && negA[first]* posB[second]<= req)
                second--;

            // Update cnt
            cnt += posB.Count - second - 1;
        }

        // Return Answer
        return (cnt >= K);
    }

    // Function to find the Kth smallest
    // number in array formed by product of
    // any two elements from []A and []B
    static int kthSmallestProduct(int[] A, int[] B, int K) {
        List<int> posA = new List<int>();
        List<int> negA = new List<int>();
        List<int> posB = new List<int>();
        List<int> negB = new List<int>();
        // Loop to iterate array []A
        foreach (int it in A) {
            if (it >= 0)
                posA.Add(it);
            else
                negA.Add(it);
        }

        // Loop to iterate array []B
        foreach (int it in B)
            if (it >= 0)
                posB.Add(it);
            else
                negB.Add(it);

        // Stores the lower and upper bounds
        // of the binary search
        int l = int.MinValue, r = int.MaxValue;

        // Stores the readonly answer
        int ans = 0;

        // Find the kth smallest integer
        // using binary search
        while (l <= r) {

            // Stores the mid
            int mid = (l + r) / 2;

            // If the number of elements
            // greater than mid in product
            // array are more than K
            if (check(mid, posA, posB, negA, negB, K)) {
                ans = mid;
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }

        // Return answer
        return ans;
    }

    // Driver Code
    public static void Main(String[] args) {
        int[] A = { -4, -2, 0, 3 };
        int[] B = { 1, 10 };
        int K = 7;

        Console.Write(kthSmallestProduct(A, B, K));

    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if count of elements
// greater than req in product array are
// more than K or not
function check(req, posA, posB, negA, negB, K)
{

  // Stores the count of numbers less
  // than or equal to req
  let cnt = 0;

  // Case with both elements of A[] and
  // B[] are negative
  let first = 0;
  let second = negB.length - 1;

  // Count number of pairs formed from
  // array A[] and B[] with both elements
  // negative and there product <= req
  while (first < negA.length) {
    while (second >= 0 && negA[first] * negB[second] <= req) second--;

    // Update cnt
    cnt += negB.length - second - 1;
    first++;
  }

  // Case with both elements of A[] and
  // B[] are positive
  first = 0;
  second = posB.length - 1;

  // Count number of pairs formed from
  // array A[] and B[] with both elements
  // positive and there product <= req
  while (first < posA.length) {
    while (second >= 0 && posA[first] * posB[second] > req) second--;

    // Update cnt
    cnt += second + 1;
    first++;
  }

  // Case with elements of A[] and B[]
  // as positive and negative respectively
  first = posA.length - 1;
  second = negB.length - 1;

  // Count number of pairs formed from
  // +ve integers of A[] and -ve integer
  // of array B[] product <= req
  while (second >= 0) {
    while (first >= 0 && posA[first] * negB[second] <= req) first--;

    // Update cnt
    cnt += posA.length - first - 1;
    second--;
  }

  // Case with elements of A[] and B[]
  // as negative and positive respectively
  first = negA.length - 1;
  second = posB.length - 1;

  // Count number of pairs formed from
  // -ve and +ve integers from A[] and
  // B[] with product <= req
  for (; first >= 0; first--) {
    while (second >= 0 && negA[first] * posB[second] <= req) second--;

    // Update cnt
    cnt += posB.length - second - 1;
  }

  // Return Answer
  return cnt >= K;
}

// Function to find the Kth smallest
// number in array formed by product of
// any two elements from A[] and B[]
function kthSmallestProduct(A, B, K) {
  let posA = [],
    negA = [],
    posB = [],
    negB = [];

  // Loop to iterate array A[]
  for (it of A) {
    if (it >= 0) posA.push(it);
    else negA.push(it);
  }

  // Loop to iterate array B[]
  for (it of B)
    if (it >= 0) posB.push(it);
    else negB.push(it);

  // Stores the lower and upper bounds
  // of the binary search
  let l = Number.MIN_SAFE_INTEGER,
    r = Number.MAX_SAFE_INTEGER;

  // Stores the final answer
  let ans;

  // Find the kth smallest integer
  // using binary search
  while (l <= r)
  {

    // Stores the mid
    let mid = (l + r) / 2;

    // If the number of elements
    // greater than mid in product
    // array are more than K
    if (check(mid, posA, posB, negA, negB, K)) {
      ans = mid;
      r = mid - 1;
    } else {
      l = mid + 1;
    }
  }

  // Return answer
  return ans;
}

// Driver Code
let A = [-4, -2, 0, 3];
let B = [1, 10];
let K = 7;

document.write(kthSmallestProduct(A, B, K));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O((N+M)*log 2 <sup>64</sup> 或 O((N+M)* 64)*
*T8】辅助空间: O(N+M)*